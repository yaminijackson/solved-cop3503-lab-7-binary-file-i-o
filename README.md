Download Link: https://assignmentchef.com/product/solved-cop3503-lab-7-binary-file-i-o
<br>
<h1>Overview</h1>

In this assignment, you are going to load a series of files containing data and then searching the loaded data for specific criteria (This sounds oddly familiar…). The files that you load will contain information about various hero characters, some of their attributes (i.e. strength, hit-points, etc.) as well as any items they may be carrying. The data that you load will also be in a <strong>binary format</strong>, which needs to be handled differently than <strong>text-based files</strong>.

<h1>Description</h1>

There are 2 main files that you will be loading in this assignment:

<ul>

 <li><em>shp </em></li>

 <li><em>shp </em></li>

</ul>

These files contain data about starships and some of the key information about them (their names, their maximum warp speed, etc). In binary files, you have to know the format or pattern of the data in order to read it, as you can’t open the file up in a text editor to see what’s in it. (Well, you CAN, but… it won’t be pretty.)

Starship Data

The output for a starship would look something like this:




The data stored for each ship is as follows:

<ul>

 <li>A string for the name of the vessel</li>

 <li>A string for the class of ship</li>

 <li>The length of the ship, stored as a <em>short</em></li>

 <li>The shield capacity, stored as an <em>integer</em></li>

 <li>The maximum warp speed of the ship, stored as a <em>float</em></li>

 <li>An inventory containing a variable number of weapons, each of which contain a <em>string</em>, <em>integer</em>, and <em>float</em>. If a ship doesn’t have any weapons, the file will still have to indicate a 0. Output-wise, you can just print out “<strong>Unarmed</strong>”</li>

</ul>

<h1>Reading binary data</h1>

Reading data in binary is all about copying <em>bytes</em> (1 byte := 2 nibbles := 8 bits) from a location in a file to a location in memory. When reading data you will <strong>always</strong> use the <em>read()</em> function, and when <strong>writing</strong> data you will always use the <em>write()</em> function. <strong>For this assignment</strong>, you will only need to <em>read()</em> data.

Strings are always an exceptional case. In the case of strings, you should read them in a 4 or 5 step process:

<ol>

 <li>Read the length of the string from the file. Unless you are dealing with fixed-length strings (in which case you know the length of the string from somewhere else), it will be there, promise. (If someone didn’t write this data out to a file, shame on them, they screwed up.)</li>

 <li>Dynamically allocate an array equal to the size of the string, plus 1 for the null terminator. If the length already includes the null terminator, <strong>do not</strong> add one to the count here — you’d be accounting for it twice, which is bad.</li>

 <li>Read the string into your newly created buffer.</li>

 <li>(<strong><u>OPTIONAL</u></strong>) Store your dynamic char * in something like a std::string, which manages its own internal memory. Then you don’t have to worry about it anymore.</li>

 <li>Delete the dynamically allocated array. If you did step 4, this should be immediately after you store it in the std::string (so you don’t forget to delete it later). If you are planning to use this variable later, be sure to delete it later on down the line.</li>

</ol>

Refer back to the Powerpoint slides about Binary File I/O for information on how to read and write binary files.

<h1>File format</h1>

The structure of the files is as follows:

<table width="623">

 <tbody>

  <tr>

   <td width="138">4 bytes</td>

   <td width="486">A <em>count</em> of how many ships are in the file</td>

  </tr>

  <tr>

   <td colspan="2" width="623"><strong>“Count” number of ships follow the first 4 bytes. Each ship has the following format: </strong></td>

  </tr>

  <tr>

   <td width="138">4 bytes</td>

   <td width="486">The <em>length</em> of the <em>name</em>, including the null terminator</td>

  </tr>

  <tr>

   <td width="138">“Length” bytes</td>

   <td width="486">The string data for the name, including the null terminator</td>

  </tr>

  <tr>

   <td width="138">4 bytes</td>

   <td width="486">The length of the ship’s <em>class</em>, including the null terminator</td>

  </tr>

  <tr>

   <td width="138">“Length” bytes</td>

   <td width="486">The string data for the class, including the null terminator</td>

  </tr>

  <tr>

   <td width="138">2 bytes</td>

   <td width="486">The ship’s length, in meters</td>

  </tr>

  <tr>

   <td width="138">4 bytes</td>

   <td width="486">The ship’s shield capacity, in terajoules</td>

  </tr>

  <tr>

   <td width="138">4 bytes</td>

   <td width="486">The warp speed of the ship</td>

  </tr>

  <tr>

   <td width="138">4 bytes</td>

   <td width="486">A count of the number of weapons equipped on the ship</td>

  </tr>

  <tr>

   <td colspan="2" width="623"><strong>“Count” number of weapons follow the previous 4 bytes. Each Item is as follows: </strong></td>

  </tr>

  <tr>

   <td width="138">4 bytes</td>

   <td width="486">The length of the weapon’s <em>name</em>, including the null terminator</td>

  </tr>

  <tr>

   <td width="138">“Length” bytes</td>

   <td width="486">The string <em>data</em> for the name of the item, including the null terminator</td>

  </tr>

  <tr>

   <td width="138">4 bytes</td>

   <td width="486">An integer for power rating of the weapon (on some fictional scale—higher is better)</td>

  </tr>

  <tr>

   <td width="138">4 bytes</td>

   <td width="486">A float for the power consumption of the weapon</td>

  </tr>

 </tbody>

</table>

<strong> </strong>




<strong>         </strong>

<h1>Searches</h1>

After you’ve loaded the data, you will perform a few operations on the stored data:

<ol>

 <li>Print all the ships</li>

 <li>Print the starship with the most powerful weapon</li>

 <li>Print the most powerful ship (highest combined power rating of all weapons)</li>

 <li>Print the weakest ship (out of ships that actually have weapons)</li>

 <li>Print the unarmed ships</li>

</ol>

<h1>Sample outputs</h1>




Left: First 2 ships from enemyships.shp — Right: Unarmed friendly vessels

<h1>Tips</h1>

<ol>

 <li>Choices you make at the start of a program can have a big impact on how the rest of the program gets developed. Think about how you want to store the information retrieved from the file, and how you could easily pass that data to various functions you might write.</li>

 <li>If you have a process for easily loading and accessing the data, the rest of the functionality should be a lot easier to write. Make sure the loading process is all taken care of before worrying about anything else.</li>

 <li>The code to load 1 file containing 1 piece of data (no matter how complex that data is) should not be much different than loading 100 files, each containing 100 elements. Start by thinking about just 1 element from the file first. Do the values you read match the values in the file? What about 2 entries, does everything add up? Etc…</li>

 <li>If you pass containers of data, make sure you pass them by REFERENCE, not by value. Don’t create copies of anything unless you specifically need a copy.</li>

 <li>Try reading one element at a time. Read the first 4 bytes, try printing it out to the screen. Is the number something reasonable, or something that seems incorrect, like -20? If that works, move on to the next piece of data in the file.</li>

</ol>