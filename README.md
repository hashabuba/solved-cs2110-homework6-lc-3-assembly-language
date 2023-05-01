Download Link: https://assignmentchef.com/product/solved-cs2110-homework6-lc-3-assembly-language
<br>
The goal of this assembly assignment is to familiarize you with coding in the LC-3 assembly language. This will involve writing small programs, modifying memory, and converting from high-level code to assembly.

<a name="_Toc8328"></a>Part 1: DeMorgan’s Revenge (or.asm)

For this part, notice that the LC-3 assembly language directly accommodates AND and NOT operations with corresponding instructions but not an OR instruction.

Use your knowledge of DeMorgan’s Laws to compute A | B.

Open or.asm, and notice there are three labels. The labels A and B point to two .fill values to be OR’d.

Store the result of A | B in memory at the third label ANSWER.

<h2><a name="_Toc8329"></a>1.2         Part 2: Arrays – Summing Negative Numbers (sum negative.asm)</h2>

For this part, write a program which traverses an array and sums all of the negative numbers (there will also be positive numbers in the array).

Open sum negative.asm, and notice there are three labels. The labels ARRAY ADDR and ARRAY LEN point to the starting address and length of the array.

Before HALTing the program, be sure to store the result at the third label ANSWER.

<em>Note: </em>The sum will not necessarily be negative. For example, if there is overflow, you might end up with a positive number.

<h2><a name="_Toc8330"></a>1.3         Part 3: Arrays – Selection Sort (select.asm)</h2>

For this part, write a program which sorts an array in ascending order according to the selection sort algorithm.

Consider the following pseudocode:

<table width="586">

 <tbody>

  <tr>

   <td width="258">for i = 0 to ARRAY_LEN – 1:</td>

   <td width="328"># Iterate through every position in the array</td>

  </tr>

  <tr>

   <td width="258">min_idx = i</td>

   <td width="328"># Find the element that will move to position i</td>

  </tr>

 </tbody>

</table>

# Everything before index i is sorted, so we are # looking for the minimum value after index i

for j = i + 1 to ARRAY_LEN: if ARRAY_ADDR[j] &lt; ARRAY_ADDR[min_idx]:

min_idx = j

# Swap the value that belongs here with the current # value; these might be the same value!

# (and index i might be equal to index min_idx)

swap(ARRAY_ADDR[i], ARRAY_ADDR[min_idx])

Open select.asm, and notice that there are two labels. The labels ARRAY ADDR and ARRAY LEN correspond to the starting address and length of the array, respectively.

<em>Note: </em>This sort should be in-place, so when your program finishes, the location in memory that contained your original array should now contain the sorted array.

<h2><a name="_Toc8331"></a>1.4         Part 4: Strings – Comparing (strcmp.asm)</h2>

For this part, write a program which compares two null-terminated strings, or sequences of characters, according to the following specification:

<ul>

 <li>The function should store either 1, 0, or -1 at the label ANSWER according to whether the first string is greater than, equal to, or less than the second string</li>

 <li>Determine greater than, equal to, or less than by comparing their ASCII values</li>

</ul>

Consider the following examples:

strcmp(“dogcat”, catdog”) ==&gt; 1 strcmp(“whether”, “whither”) ==&gt; -1 strcmp(“”, “blank”) ==&gt; -1 strcmp(“same”, “same”) ==&gt; 0

Open strcmp.asm, and notice there are three labels. The labels ADDR STR 1 and ADDR STR 2 correspond to the starting addresses of the first and second strings to be compared.

The process is very simple: Iterate through both strings, comparing the character values at the same indices. When you find an inequality, or one of the two characters is a zero, stop the iteration and compute the result based on those two characters. If both characters are zero, the strings are equal. If one character is zero, that string comes first because it’s shorter. Otherwise, compare the differing characters, and the string with the smaller character value comes first.

Store the result at the third label ANSWER.

<em>Note: </em>Strings are zero-terminated sequences of 16-bit words. Consider the string “ASSEMBLY” starting at address x4000. The ASCII value for character ’A’ (x0041) is stored at x4000, the ASCII for character ’S’ (x0053) is stored at x4001, etc. Finally, the value 0 is stored at address x4008. You, of course, do not need to memorize or interpret the ASCII table to determine which value is smaller.

<h2><a name="_Toc8332"></a>1.5         Part 5: Linked List – Finding Extrema (max min.asm)</h2>

For this part, write a program that traverses a singly-linked list of nodes and finds both the maximum and minimum elements, where each node is comprised of a next address that points to the next node and an integer data. Consider the following pseudocode:

node = HEAD_ADDR

<table width="642">

 <tbody>

  <tr>

   <td width="216">if node == NULL:</td>

   <td width="425"># For an empty list, set some invalid values:</td>

  </tr>

  <tr>

   <td width="216">max = MIN_INT</td>

   <td width="425">#                – The smallest possible number for max</td>

  </tr>

  <tr>

   <td width="216">min = MAX_INT</td>

   <td width="425">#                 – The largest possible number for min</td>

  </tr>

  <tr>

   <td width="216">else:</td>

   <td width="425"># For a non-empty list, initialize with the head node’s data:</td>

  </tr>

  <tr>

   <td width="216">max = mem[node + 1] min = mem[node + 1]</td>

   <td width="425">#                 Remember: mem[node + 1] is the node’s integer data</td>

  </tr>

  <tr>

   <td width="216">node = mem[node]</td>

   <td width="425">#               Remember: mem[node] is the node’s next address</td>

  </tr>

  <tr>

   <td width="216">while node != 0:</td>

   <td width="425"># For all remaining nodes in the list:</td>

  </tr>

  <tr>

   <td width="216">if mem[node + 1] &gt; max: max = mem[node + 1]</td>

   <td width="425">#          Check for a new max</td>

  </tr>

  <tr>

   <td width="216">if mem[node + 1] &lt; min: min = mem[node + 1]</td>

   <td width="425">#           Check for a new min</td>

  </tr>

  <tr>

   <td width="216">node = mem[node]</td>

   <td width="425"># How do we get the address of the next node?</td>

  </tr>

 </tbody>

</table>

Once again, each node of this list is comprised of two consecutive 16-bit values in memory: The address of the next node and the data being stored.

Consider an example list with a HEAD ADDR, or starting node, at address x4000.

Address | Contents | Comments

———+———-+————–

<table width="216">

 <tbody>

  <tr>

   <td width="77">x4000 |</td>

   <td width="139">x4004 | Node 1: next</td>

  </tr>

  <tr>

   <td width="77">x4001 |</td>

   <td width="139">x0035 | Node 1: data</td>

  </tr>

  <tr>

   <td width="77">x4002 |</td>

   <td width="139">x345A | …</td>

  </tr>

  <tr>

   <td width="77">x4003 |</td>

   <td width="139">x7441 | …</td>

  </tr>

  <tr>

   <td width="77">x4004 |</td>

   <td width="139">x4008 | Node 2: next</td>

  </tr>

  <tr>

   <td width="77">x4005 |</td>

   <td width="139">x0101 | Node 2: data</td>

  </tr>

  <tr>

   <td width="77">x4006 |</td>

   <td width="139">x0000 | Node 4: next</td>

  </tr>

  <tr>

   <td width="77">x4007 |</td>

   <td width="139">x9040 | Node 4: data</td>

  </tr>

  <tr>

   <td width="77">x4008 |</td>

   <td width="139">x4006 | Node 3: next</td>

  </tr>

  <tr>

   <td width="77">x4009 |</td>

   <td width="139">x7000 | Node 3: data</td>

  </tr>

 </tbody>

</table>

Observe that Node 1 points to Node 2 (at address x4004). Node 2 points to Node 3 (at address x4008). Node 3 points to Node 4 (at address x4006). Finally, Node 4 points to address x0000 (i.e. NULL), signaling the end of the list!

Our autograder will, in general, store nodes near x4000, so please avoid writing any instructions or storing any data near there.

<em>Note: </em><strong>The grader will only test lists with nonnegative integer data! (i.e. </strong>0x0000 ··· 0x7FFF<strong>) </strong>Store max at ANSWER MAX and min at ANSWER MIN.

<h1><a name="_Toc8333"></a>2           Deliverables</h1>

Please upload the following files to the assignment on Gradescope:

<ol>

 <li>asm</li>

 <li>sum negative.asm</li>

 <li>asm</li>

 <li>asm</li>

 <li>max min.asm</li>

</ol>

<strong>Be sure to check your score to see if you submitted the right files, as well as your email frequently until the due date of the assignment for any potential updates.</strong>

<h1><a name="_Toc8334"></a>3           LC-3 Assembly Programming Requirements</h1>

<h2><a name="_Toc8335"></a>3.1         Overview</h2>

<ol>

 <li>Your code must assemble with <strong>NO WARNINGS OR ERRORS</strong>. To assemble your program, open the file with Complx. It will complain if there are any issues. <strong>If the code in this file does not assemble, you WILL get a zero for that file.</strong></li>

 <li><strong>Comment your code! </strong>This is especially important in assembly, because it’s much harder to interpret what is happening later, and you’ll be glad you left yourself notes on what certain instructions are contributing to the code. Comment things like what registers are being used for and what less intuitive lines</li>

</ol>

of code are actually doing. To comment code in LC-3 assembly just type a semicolon (;), and the rest of that line will be a comment.

<ol start="3">

 <li>Avoid stating the obvious in your comments; it doesn’t help in understanding what the code is doing. Try to write high-level pseudo-code instead!</li>

</ol>

<strong>Good Comment</strong>

<table width="404">

 <tbody>

  <tr>

   <td width="167">ADD R3, R3, -1</td>

   <td width="237">; counter–</td>

  </tr>

  <tr>

   <td width="167">BRp LOOP<strong>Bad Comment</strong></td>

   <td width="237">; if counter == 0 don’t loop again</td>

  </tr>

  <tr>

   <td width="167">ADD R3, R3, -1</td>

   <td width="237">; Decrement R3</td>

  </tr>

  <tr>

   <td width="167">BRp LOOP</td>

   <td width="237">; Branch to LOOP if positive</td>

  </tr>

 </tbody>

</table>

<ol start="4">

 <li><strong>DO NOT assume that ANYTHING in the LC-3 is already zero. </strong>Treat the machine as if your program was loaded into a machine with random values stored in the memory and register file.</li>

 <li>Following from 3. You can randomize the memory and load your program by doing File – Randomize and Load.</li>

 <li>Do not add any comments beginning with @plugin or change any comments of this kind.</li>

 <li><strong>Test your assembly. </strong>Don’t just assume it works and turn it in.</li>

</ol>

<h1><a name="_Toc8336"></a>4           Hints</h1>

<h2><a name="_Toc8337"></a>4.1         Pseudo-Ops</h2>

Pseudo-Ops are directions for the assembler that aren’t actually instructions in the ISA.

<ol>

 <li>.orig: Tells the assembler to put this block of code at the desired address.</li>

</ol>

Example: .orig x3000 will put the block of code at address x3000.

<ol start="2">

 <li>.stringz “something”: Will put a string of characters in memory followed by NULL (which is a single ASCII character with the value 0).</li>

</ol>

Example: .stringz “sanjay” will put the ASCII code for the letter ‘s’ in the first memory location, the code for ‘a’ in the second memory location, and so on until putting ‘y’ in the next-to-last position and NULL (which again, has the ASCII code 0) in the last memory location as the terminator.

<ol start="3">

 <li>.blkw n: A pseudo-op that will allocate the next n locations of memory for a specified label.</li>

 <li>.fill value: A pseudo-op that will put the value in that memory location.</li>

 <li>.end: A psuedo-op that denotes the end of an address block. Matches with an .orig.</li>

</ol>

<h2><a name="_Toc8338"></a>4.2         Traps</h2>

Traps are subroutines built into the LC-3 to help simplify instructions. Some helpful TRAPS include:

<ol>

 <li>HALT: HALT is an alias for a TRAP that will stop the LC-3 from running</li>

 <li>OUT: OUT is an alias for a TRAP that will take whatever character is in R0 and print it to the console</li>

 <li>PUTS: PUTS is an alias for a TRAP that will print a string of characters with the starting address saved in R0 until it reaches a NULL (0) character</li>

 <li>GETC: GETC is another TRAP alias that will take in a character input and store it in R0</li>

</ol>

Being an alias for a TRAP instruction means that the assembler will convert them to TRAP instructions at assembly time. For example, if you write HALT in your code, the assembler will convert it to the instruction, TRAP x25 for you.

<h2><a name="_Toc8339"></a>4.3         Example</h2>

The following small example will demonstrate the use of these Traps and pseudo-ops:

.orig x3000                                              ; Where the code will begin

LEA R0, HW                                                     ; Loads the address of the string into R0

PUTS                                                                  ; Print the string whose address is in R0

HALT                                                             ; Stops the program from executing

HW .stringz “Hello. 
”                                ; Stores the word ’Hello’ in memory with ’H’ be located at

; address x3003, ’e’ will be located at address x3004, etc

.end                                                                ; Denotes the end of the address block