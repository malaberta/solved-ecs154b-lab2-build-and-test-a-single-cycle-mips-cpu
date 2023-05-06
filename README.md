Download Link: https://assignmentchef.com/product/solved-ecs154b-lab2-build-and-test-a-single-cycle-mips-cpu
<br>
<h1></h1>

<ul>

 <li>Build and test a single cycle MIPS CPU that implements a subset of the MIPS instruction set.</li>

 <li>Design a combinational logic control unit.</li>

</ul>

<h1>Description</h1>

In this lab, you will use Logisim to build a single cycle CPU to understand the MIPS control and datapath signals. To test your CPU, you will run an assembly language program given to you, and simulate the operations in Logisim. You will be given several functional blocks to help you out. You must implement the control signals as combinational logic.

<h1>Details</h1>

You will be given an empty project to start your lab, which includes an implementation of an ALU and a Register File. In creating your CPU, you are allowed to use all of the features and modules available in Logisim. The project is available in the Assignment section of the course’s SmartSite page. Simply download the .zip file containing <strong>Lab 2 Given.circ</strong>. The blocks are described below:

<h2>ALU</h2>

<ul>

 <li><strong>A</strong>, <strong>B</strong>: The 32 bit data inputs to the ALU.</li>

 <li><strong>ALUResult</strong>: The 32 bit result of the ALU operation.</li>

 <li><strong>Overflow</strong>: Not used in this lab.</li>

 <li><strong>Shamt</strong>: 5 bit shift amount. Not used in this lab. Connect a constant zero to this input.</li>

 <li><strong>Zero</strong>: A flag bit that is set when the ALU result equals zero (all bits are low).</li>

 <li><strong>ALUCtl</strong>: The 4 bit control input, as described in the following table:</li>

</ul>

<table width="357">

 <tbody>

  <tr>

   <td width="80">Instruction</td>

   <td width="69">ALUCtl3</td>

   <td width="69">ALUCtl2</td>

   <td width="69">ALUCtl1</td>

   <td width="69">ALUCtl0</td>

  </tr>

  <tr>

   <td width="80">OR</td>

   <td width="69">0</td>

   <td width="69">0</td>

   <td width="69">0</td>

   <td width="69">0</td>

  </tr>

  <tr>

   <td width="80">SLTU</td>

   <td width="69">0</td>

   <td width="69">0</td>

   <td width="69">0</td>

   <td width="69">1</td>

  </tr>

  <tr>

   <td width="80">SLT</td>

   <td width="69">0</td>

   <td width="69">0</td>

   <td width="69">1</td>

   <td width="69">0</td>

  </tr>

  <tr>

   <td width="80">ADD</td>

   <td width="69">0</td>

   <td width="69">0</td>

   <td width="69">1</td>

   <td width="69">1</td>

  </tr>

  <tr>

   <td width="80">SUB</td>

   <td width="69">0</td>

   <td width="69">1</td>

   <td width="69">0</td>

   <td width="69">0</td>

  </tr>

  <tr>

   <td width="80">XOR</td>

   <td width="69">0</td>

   <td width="69">1</td>

   <td width="69">0</td>

   <td width="69">1</td>

  </tr>

  <tr>

   <td width="80">AND</td>

   <td width="69">0</td>

   <td width="69">1</td>

   <td width="69">1</td>

   <td width="69">0</td>

  </tr>

 </tbody>

</table>

More instruction types to be supported will be added in Lab 3, thus the extra ALUCtl signal.

<h2>Register File</h2>

<ul>

 <li><strong>Clock</strong>: The main clock signal.</li>

 <li><strong>RdAddr1</strong>, <strong>RdAddr2</strong>: The 5 bit register addresses to read. MIPS has 32 registers in its register file.</li>

 <li><strong>RdData1</strong>, <strong>RdData2</strong>: The 32 bit data values from the read registers.</li>

 <li><strong>WrAddr</strong>: The 5 bit register address to write.</li>

 <li><strong>WrReg</strong>: A control signal that causes the register file to be written to when high. If <strong>WrReg </strong>is low, no register values will change.</li>

 <li><strong>WrData</strong>: The 32 bit value to store in the register specified by <strong>WrAddr</strong>, if <strong>WrReg </strong>is set.</li>

</ul>

You will need to add additional logic blocks to your diagram: a PC, an instruction memory, a data memory, and combinational logic circuits to decode the current instruction word and enable the respective datapaths.

<h2>PC</h2>

<ul>

 <li>Use a 32 bit Register as your PC.</li>

 <li><strong>Please note that MIPS is a byte addressable architecture, and therefore PC is incremented by 4, not 1.</strong></li>

</ul>

<h2>Instruction Memory – ROM</h2>

<ul>

 <li>Use an 8 bit address, 32 bit data ROM from the memory library as your instruction memory, to which you can load your hex code.</li>

 <li>A sample test program will be included. To load the instructions into your ROM, right-click the ROM and select <em>Edit Contents… </em>In the Hex Editor that pops up, click <em>Open </em>and select <strong>lst</strong>, which is provided with the assignment files.</li>

 <li>The corresponding MIPS instructions are in <strong>mps</strong>.</li>

 <li>You can assemble your own test programs using Sean Davis’ ASIDE program, available at <a href="http://csiflabs.cs.ucdavis.edu/~ssdavis/50/">http:</a></li>

</ul>

<a href="http://csiflabs.cs.ucdavis.edu/~ssdavis/50/">//csiflabs.cs.ucdavis.edu/</a><a href="http://csiflabs.cs.ucdavis.edu/~ssdavis/50/">~</a><a href="http://csiflabs.cs.ucdavis.edu/~ssdavis/50/">ssdavis/50/</a><a href="http://csiflabs.cs.ucdavis.edu/~ssdavis/50/">.</a> After compiling, you will need to edit the .lst file that corresponds to your code to match the input that Logisim expects.

<ul>

 <li>The MIPS architecture is byte addressable, so the PC is incremented by 4 to reach the next instruction. For example the first instruction will be at 0x00000000, the second at 0x00000004, the third at 0x00000008, and so on.</li>

</ul>

<h2>Data Memory – RAM</h2>

<ul>

 <li>Use an 8 bit address, 32 bit data RAM from the memory library as your data memory. The separate load and store ports option is easier to use but you can use the other two options if you’d like.</li>

 <li><strong>A</strong>: the 8 bit address of the word you want to access.</li>

 <li><strong>D</strong>, left side: the 32 bit word to be written or stored at the address specified by A.</li>

 <li><strong>str</strong>: When high, the value on the left D is stored at address A. • <strong>sel</strong>: When 0, the chip is disabled. Set to high or leave floating.</li>

 <li><strong>ˆ</strong>: the main clock signal.</li>

 <li><strong>ld</strong>: When high, the value on the memory at address A is placed on the right D.</li>

 <li><strong>clr</strong>: When high, sets all of the values in the RAM to 0. Either set low or leave floating.</li>

 <li><strong>D</strong>, right side: the 32 bit word to be read or loaded from the address specified by A.</li>

</ul>

<h1>Instructions to Implement</h1>

Your CPU must execute the following instructions:

AND, ANDI, ADD, ADDI, OR, ORI, SUB, SLT, SLTU*, XOR, LW, SW, BEQ, J, JAL, JR

<strong>Note that the instructions for SLTU are incorrect in the given MIPS PDF. </strong>See the section below.

<h1>MIPS Architecture</h1>

A PDF was included in the archive to help you with the lab. Note that the instructions for SLTU are incorrect. It should read:

If rs <em>&lt; </em>rt with an unsigned comparison, put 1 into rd. Otherwise put 0 into rd.

For this lab, you must use only combinational logic to implement the control signals. Do not use a MUX with constant inputs to generate your control signals.

<h2>JAL and JR</h2>

The book does not explain too much about these instructions or give any designs on how to implement them, so it will be up to you to figure out what you need to do.

<ul>

 <li>JAL (jump and link) is just like J, except it stores the contents of PC + 4 in register 31.</li>

 <li>Use: jal offset</li>

 <li>Effect: $31 = PC + 4. PC = PC + 4[31..28], Inst[25..0], 00</li>

 <li>Encoding: 0000 11ii iiii iiii iiii iiii iiii iiii, where the i’s are the bits encoding the immediate value.</li>

 <li>JR (jump, register) sets the PC to the value contained in register s.</li>

 <li>Use: jr $s</li>

 <li>Effect: PC = $s</li>

 <li>Encoding: 0000 00ss sss0 0000 0000 0000 0000 1000, where s is the address of the register.</li>

</ul>

The following probes are included to help you debug your lab.

<table width="557">

 <tbody>

  <tr>

   <td width="86">Label Name</td>

   <td width="121">Radix</td>

   <td width="350">Description</td>

  </tr>

  <tr>

   <td width="86"><strong>PC</strong></td>

   <td width="121">Unsigned Decimal</td>

   <td width="350">The current value of the PC.</td>

  </tr>

  <tr>

   <td width="86"><strong>WrReg</strong></td>

   <td width="121">Binary</td>

   <td width="350">1 if writing to the register file, 0 otherwise.</td>

  </tr>

  <tr>

   <td width="86"><strong>WrAddr</strong></td>

   <td width="121">Unsigned Decimal</td>

   <td width="350">The address of the register that is going to be written to.</td>

  </tr>

  <tr>

   <td width="86"><strong>WrData</strong></td>

   <td width="121">Signed Decimal</td>

   <td width="350">The value that is going to be written to the register.</td>

  </tr>

  <tr>

   <td width="86"><strong>MemWr</strong></td>

   <td width="121">Binary</td>

   <td width="350">1 if writing to memory, 0 otherwise.</td>

  </tr>

  <tr>

   <td width="86"><strong>MemData</strong></td>

   <td width="121">Signed Decimal</td>

   <td width="350">The data to be written to memory.</td>

  </tr>

  <tr>

   <td width="86"><strong>Branch</strong></td>

   <td width="121">Binary</td>

   <td width="350">1 if taking a branch, 0 otherwise.</td>

  </tr>

  <tr>

   <td width="86"><strong>Jump</strong></td>

   <td width="121">Binary</td>

   <td width="350">1 if executing the jump instruction, 0 otherwise.</td>

  </tr>

  <tr>

   <td width="86"><strong>Jal</strong></td>

   <td width="121">Binary</td>

   <td width="350">1 if executing the jump and link instruction, 0 otherwise.</td>

  </tr>

  <tr>

   <td width="86"><strong>Jr</strong></td>

   <td width="121">Binary</td>

   <td width="350">1 if executing the jump register instruction, 0 otherwise.</td>

  </tr>

 </tbody>

</table>