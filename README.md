Download Link: https://assignmentchef.com/product/solved-ence361-week-3-accelerometer-buttons-and-display
<br>



<ol>

 <li><strong><em>Outcomes: </em></strong></li>

</ol>

<ul>

 <li>To learn how to read data from the Orbit BoosterPack’s accelerometer.</li>

 <li>To generate a program which responds reliably to manual button pushes.</li>

 <li>To generate a program which utilises SysTick timer interrupts.</li>

 <li>To continue development of useful C code functions for the fitness monitor project.</li>

</ul>

<ol start="3">

 <li><strong><em>Source files: </em></strong></li>

</ol>

You have been supplied with a number of source files for this laboratory.

All of the files can be found in a zip file on Learn:  <strong>Section 1 | Laboratory source code | Week-3 </strong>

<strong><em>Button support code </em></strong>

The button support module comprises the files:

<h1>buttons4.c, buttons4.h</h1>

<strong>butsTest4.c </strong>is a program which demonstrates how the button interface module can be used.

Care must be taken with manually controlled switches, since “switch bounce” can occur.  The philosophy behind the <strong>buttons4</strong> module and its design will be explained in detail in Lecture 10 (Week 4).  Until then, the following brief explanation should suffice:

All the buttons supported are polled regularly, using the <strong>updateButtons()</strong> function, to see if their state has altered.  Any change of state is stored in variables which are module globals.  The <strong>checkButton()</strong> function can be called at any time to see if a particular button, identified as  <strong>UP, DOWN, LEFT </strong>or  <strong>RIGHT</strong>, has been <strong>PUSHED</strong> or <strong>RELEASED</strong>.  The <strong>checkButton()</strong> function only returns the altered state once per action of the physical pushbutton, otherwise it returns <strong>NO_CHANGE</strong>.




<strong><em>Demonstration OLED display program </em></strong>

<strong>OLEDTest.c </strong> is an example program which demonstrates how to use the display on the Orbit BoosterPack.




<strong><em>Example accelerometer program </em></strong>

<strong>readAcc.c </strong>is an example program which reads data from the Orbit BoosterPack’s onboard accelerometer. A datasheet for the accelerometer (Analog Devices ADXL345) is available on Learn.




<ol start="4">

 <li><strong><em>Specification for Week 3: </em></strong></li>

</ol>




<h1>4.1 Set up a new project for the Week-3 Lab (call it “Week-3 Lab”)</h1>

While this is not strictly necessary, it will help to keep your work in sections.  Follow a similar procedure to that you used last week (see CCS Tutorial.pdf).  Unzip the source files from the zip file downloaded from Learn into your new project directory.  Then, move the OrbitOLED directory and its contents to your workspace directory, i.e. to  <strong>P:CoursesENCE361labs</strong>

This is so that you can include this code in your programs without duplicating it in every project.




Remember that you should only compile the .c files that are part of each program – use right click and “Exclude from Build” as required.




<h1>4.2 Compile, link and load OLEDTest.c</h1>

The build of this program needs access to the ustdlib module and to the OLED support module.

<strong>ustdlib.c</strong>:                     Right-click on the week3Lab project, <strong>Add Files</strong>

browse to <strong>C:tiTivaWare_C_Series-2.1.4.178utilsustdlib.c</strong>

<strong>                                        Open</strong>, then choose <strong>Link </strong>

<h1>                                        ustdlib.c will appear in the project with a link icon alongside. OrbitOLED:          File | New | Folder | Advanced &gt;&gt; | Link to alternate location</h1>

Browse to the OrbitOLED folder in your workspace, click <strong>Finish </strong>

<strong>                                                                        </strong>The OrbitOLED folder will appear in the project with a link icon alongside. Add   <strong>P:CoursesENCE361labs   </strong>(i.e., your workspace containing the OrbitOLED folder) to the compiler include paths,

<h1>                                                using Properties | ARM Compiler | Include Options  and  +</h1>




Remember: use “Exclude from Build” to only compile the .c files that are part of each program.




This very straightforward program puts 4 lines of characters on the display, with the third row updating the display of 0 to 255 at about 2 Hz.  It does not use the buttons.  It illustrates how to initialise and use the Orbit OLED display for text.

<h1>4.3 Compile and link butsTest4.c</h1>

NB: This file needs access to the OLED support module and to the ustdlib module. Remember to exclude OLEDTest.c from your build at this stage.

Confirm that each button push is detected by the program as a single “PUSH”, followed by a “RELS” (release). This may seem trivial, but it is not, because most simple switches “bounce”, as described in section 4 above.

<h1>4.4 Compile, link and load readAcc.c</h1>

NB: This file needs access to the OLED support module. You also need to exclude butsTest4.c from your build.

Run the program and watch the values on the OLED display update as you hold your Tiva board in different orientations. Confirm that the program behaves as the description in the file header states.

<strong>4.5</strong><strong> Prepare a new version, say ‘readAcc2.c’</strong>, which displays acceleration in m/s<sup>2</sup> on the Orbit display. <strong> </strong>Change the accelerometer’s settings to give the best possible sensitivity (m/s<sup>2</sup>/bit).

Hint: Consult the ADXL345 datasheet to find out how to change the accelerometer’s <em>resolution</em> and <em>range</em>.




<strong>4.6</strong><strong> Prepare a third version, say ‘readAcc3.c’</strong>, which causes the Tiva’s red and green LEDs to light up when the device is held approximately level in the <em>x</em> and <em>y</em> directions, respectively.

<strong>4.7</strong><strong> Prepare a fourth version, say ‘readAcc4.c’</strong>, which calculates the orientation (pitch and roll) of the Tiva board based on the acceleration vector. Display the pitch and roll as percentages, where 0% corresponds to a completely level orientation and 100% corresponds to a 90° rotation in the relevant direction. <strong> </strong>

<ol start="5">

 <li><strong><em>Guidance:</em></strong></li>

</ol>

<ul>

 <li>Before you start modifying a source file that has been provided to you, <strong>always</strong> use <em>SaveAs</em> to first copy it to a new file and a new name. Remember to exclude the original file from the next build.</li>

 <li>Prepare the new programs one step-at-a-time.</li>

 <li>Some code that you may link to requires the use of the “heap”. This requires that the heap size is increased from its default of 0 bytes.  Change this to (say) 512  via the Project Properties | ARM Linker | Basic Options window.  The stack size may need to be increased also in some cases, as your programs become more extensive.</li>

 <li>Make new code as modular as possible, using appropriately designed and named functions. This will pay off when you come to build a much bigger program to control the helicopter.  If an existing and already tested function does what you want, leave it alone.</li>

 <li>Test, test, and test once more. Make sure your tests cover the specification fully.  A lot of problems with software occur because the developer has not been thorough in testing their code.</li>

</ul>

—-:—-