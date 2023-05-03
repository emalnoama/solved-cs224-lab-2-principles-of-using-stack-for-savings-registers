Download Link: https://assignmentchef.com/product/solved-cs224-lab-2-principles-of-using-stack-for-savings-registers
<br>
. Understanding preliminary principles of using stack for saving s registers, passing arguments to and receiving results from subprograms, and dynamic storage allocation. 2. Code generation for branch, jump, load address and load word.You are obliged to read this document word by word and are responsible for the mistakes you make by not following the rules. Your programs should be reasonably documented and must have a neat syntax in terms of variable names and spacing. In all labs if it is not specified assume that inputs are always correct.

<strong>Summary </strong>

<strong>Part 1</strong> Preliminary Report/Preliminary Design Report: Learning principles of writing subprograms. Involves converting octal number to decimal. Generating object code for beq, bne, j, la, lw instructions.

<strong>Part 2</strong>  (: Learning principles of writing subprograms. Involves dynamic storage allocation for arrays, getting the elements of an integer array from user, sorting numbers, finding the min, max and mode values, and providing a user interface.

<ol>

 <li>Please bring and drop your hardcopy (printed copy) of the preliminary work into the box(es) provided in the lab by 10:40 on Wednesday.</li>

</ol>

Please <strong>upload your programs of Part 1 (PRELIMINARY WORK)</strong> to the Unilica by 10:40 on Wednesday. Use filename <strong>StudentID_FirstName_LastName_SecNo_PRELIM_LabNo.txt</strong> <u>Upload only the programs. Only a NOTEPAD FILE (txt file) is accepted. </u>Your paper submission for preliminary work must match MOSS submission. <u>Any format other than txt gets 0 points.</u>



<ol>

 <li>To get credit for preliminary work you have to submit its hard copy and upload its txt version to unilica. <strong>No late submission will be accepted</strong>.</li>

</ol>




<strong>DUE DATE PART 2-5: (different for each section) YOUR LAB DAY</strong>

You have to demonstrate your lab work to the TA for grade by <strong>12:15</strong> in the morning lab and by <strong>17:15</strong> in the afternoon lab. Your TAs may give further instructions on this. If you wait idly and show your work last minute, 20 points may be taken off from your grade.

At the conclusion of the demo for getting your grade, you will <strong>upload your entire program work</strong> to the Unilica Assignment, for similarity testing by MOSS. See Part 6 below for details.

<strong>Part 1. Preliminary Work / Preliminary Design Report</strong>

You have to provide a neat presentation prepared by <u>Word or a word processor with similar output quality such as Latex as you were asked in Lab 1</u>. At the top of the paper on left provide the following information and staple all papers. In this part provide the program listings with proper identification (please make sure that this info is there for proper grading of your work, otherwise some points will be taken off).

CS224

Section No.: Enter your section no. here

Lab No.

Your Full Name/Bilkent ID




<ol>

 <li><strong>1</strong>Write MIPS assembly language programs as described below.</li>

</ol>




<ol>

 <li><strong>a</strong>. <strong>convertToDec</strong>: Write a subprogram, called convertToDec, that receives the beginning address of an asciiz string that contains a number in base 8 in the form of a string, for example, like “20”, and returns its decimal (20<sub>8</sub>= 16<sub>10</sub>) equivalent in register $v0. It assumes that the number passed is a legal octal number. Be sure that the program works for longer octal numbers as well.</li>

</ol>




A sketch of this convertToDec is as follows.

main:

…

la   $a0, octalNo

jal   convertToDec

# result comes in $v0

…

# stop execution here by syscall

convertToDec:

…

jr   $ra

.data

octalNo:   .asciiz “20”




<ol>

 <li><strong>b</strong>.  <strong>interactWithUser</strong>: Write a subprogram, called interactWithUser, that asks the user enter an octal number in the form of a string, makes sure that it is a proper octal number if not it generates an error message and ensures that a proper input is received. It passes this address to the subprogram defined above convertToDec, gets the result from it, prints it, and returns the decimal value back to the caller, i.e. the main program. How to read a string: See MIPS system calls on the web to understand how to read a string or use MARS help menu.</li>

</ol>




Use the $s registers during the implementation of the above subprograms. Using $s registers means that you have to save them to stack and restore them back from stack.  Make sure that you also save/restore any other register that need to be saved.




<ol start="2">

 <li><strong>2</strong>. <strong> </strong>Generating machine instructions(<strong>Each instruction: 2 points</strong>) Give the object code in hexadecimal for the following branch (be, bne), jump (j) and load instructions. Note that the meaning of the code segment is insignificant.</li>

</ol>

… # some other instructions

again:            add  $t0, $t1, $t2

add  $t0, $t0, $t3

add  $t0, $t0, $t4

add  $t0, $t0, $t5

<strong>beq    $t0, $t6, next</strong>

<strong>bne  $t0, $t6, again</strong>

add  $t0, $t0, $t5

next:             <strong>j               again</strong>

<strong>la      $t0, array2</strong>

<strong>lw     $t1, array2</strong>

…

.data

array1:          .space   100

array2:          .word    10, 20, 30




Assume that the label <strong>again</strong> is located at memory location 00 40 00 A0<sub>16</sub> and the array <strong>array1</strong> starts at memory location 10 01 00 00<sub>16</sub>. If you think that you do not have enough information to generate the code explain. See slide number 117 in the new Chap 6 slides of the textbook for the MIPS memory map (available at our unilica web site, Documents folder).




<strong>Part 2. <u>Lab Work</u>: Writing MIPS assembly language programs(70 points)</strong>

In this part when needed you have to follow the conventions of professional MIPS programmers and use stack.




<ol>

 <li><strong>1</strong>. <strong>(10 points)</strong> <strong>readArray</strong>: Write a subprogram, called readArray, that asks the user the size of an integer array and gets the values of array members from the user in a loop. It returns the beginning address of the array in $v0, and array size in terms of number of integers in $v1.</li>

</ol>

<strong>Hint</strong>.

li $a0, 20 #allocate enough space for 5 integers

li $v0, 9 #syscall 9 (sbrk)

syscall

# beginning address of the allocated space is returned in $v0







<ol start="2">

 <li><strong>2</strong>. <strong>bubbleSort</strong>: Write a subprogram, called bubbleSort, that sorts an integer array in decreasing/descending order using the bubble sort algorithm and using the <strong>absolute values of the numbers stored</strong>. (When -5, 1, 4, 2 is sorted after sorting the array contains -5, 4, 2, 1.) The subprogram receives the beginning address of the array in $a0, and the array size in $a1. The array size can be 0 or more.</li>

</ol>




<ol start="3">

 <li><strong>3</strong><strong>)</strong> <strong>thirdMinThirdMax</strong>: Write a subprogram, called thirdMinThirdMax, that returns the third minimum and third maximum numbers of an integer array. For example, for the array {13, 5, 1, 3, 8, 7} 3th minimum is 5, and 3th maximum is 7. You may assume that the array has at least 3 elements. The input array may or may not be sorted. Use $a registers for passing parameters and use $v0 and $v1 to return the thirdMin and thirdMax values.</li>

</ol>




<ol start="4">

 <li><strong>4</strong>. <strong>(10 points)</strong> <strong>mode</strong>: Write a subprogram, called mode, to return the mode (the most frequently appearing) value of a sorted array. If there are more than one candidate it returns the minimum of them. It receives array address and array size in $a0 and $a1 registers, respectively.</li>

 <li><strong>5</strong>. <strong>)</strong> <strong>print</strong>: Write a subprogram, called print, to print the content of the array. Use $a registers for passing parameters and don’t forget that array size can be 0.</li>

 <li><strong>6</strong>. <strong>monitor</strong>: Write a monitor program that provides a user interface to use the above subprograms in an interactive manner. The main program, the one that contains __start, provides a simple user interface that will use the above subprograms in the way that you imagine. A simple interface is enough if you like you may make it fancy.</li>

</ol>