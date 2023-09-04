# PES_ASIC_Class
Name: Srinidhi B S        SRN: PES1UG20EC201 
## Day1 
### Instruction Set Architecture
<details>
  
  <summary>Theory</summary>
  
+ ISA defines the interface between a computer's hardware and its software, specifically how the processor and its components interact with the software instructions that drive the execution of tasks. It encompasses a set of instructions, addressing modes, data types, registers, memory organization, and the mechanisms for executing and managing instructions. 
+ RISC V refers to Reduced Instruction Set Computing - Five Architecture. It is an open-source Instruction Set Architecture (ISA) that has gained significant attention and adoption in the world of computer architecture and semiconductor design.
</details>

### Integer Number Representation
<details>
  <summary>Theory</summary>
  
+ Unsigned numbers:- also known as non-negative numbers, are numerical values that represent magnitudes without indicating direction or sign.(Range: [0, (2^n)-1 ])  
+ Signed numbers are numerical values that can represent both positive and negative magnitudes, along with zero.(Range : Positive : [0 , 2^(n-1)-1] Negative : [-1 to 2^(n-1)])
  
 <img width="536" alt="Signmemalloc" src="https://github.com/Srini-web/pes_asic_class/assets/77874288/86000e0f-e3bc-4ae3-8c54-ce5f41b5a932">
 </details>
Dropdown
<details>
<summary>Run sum1ton.c</summary>
  
+ Run sum1ton.c
```
gcc sum1ton.c
./a.out
```
<img width="365" alt="Run1" src="https://github.com/Srini-web/pes_asic_class/assets/77874288/6610f24b-18f5-4e77-b069-364047e482ab">

</details>
<details>
<summary>GCC compile modes and disassemble instruction comparison</summary>
  
+ GCC compile modes and disassemble instruction comparison
  + Error encountered : stdio not recognised
Solution
```
export PATH="/home/vboxuser/riscv_toolchain/riscv64-unknown-elf-gcc-8.3.0-2019.08.0-x86_64-linux-ubuntu14/bin:$PATH"
```
```
riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c
#in a new terminal window
riscv64-unknown-elf-objdump -d sum1ton.o
```
![o1bincom](https://github.com/Srini-web/pes_asic_class/assets/77874288/bce74458-6d4f-4562-a552-9222c9fadcf6)

```
riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c
#in a new terminal window
riscv64-unknown-elf-objdump -d sum1ton.o
```
![ofastbincom](https://github.com/Srini-web/pes_asic_class/assets/77874288/05d2aea1-4903-48f3-a6e5-da8d410779fb)
</details>
<details>
<summary> Spike simulation </summary>
  
+ Spike simulation
  
![s1](https://github.com/Srini-web/pes_asic_class/assets/77874288/1afad98b-d71c-4b11-91d6-991c862e1ebb)

</details>
<details>
<summary>Finding the maximum and minimum values of a long long unsigned and signed integer</summary>
  
+ Finding the maximum and minimum values of a long long unsigned integer
    + Also finding out what happens when the value assigned is beyond the datatype range
      
  <img width="560" alt="s2" src="https://github.com/Srini-web/pes_asic_class/assets/77874288/7629b726-9c9d-4d56-a838-88b213468e66">

</details>


## Day 2
### Application Binary Interface
<details>
  
  <summary>Theory</summary>
  
+ An Application Binary Interface (ABI) is a set of rules and conventions that dictate how binary code interacts with and communicates with other binary code, typically at the level of machine code or compiled code. In simpler terms, it defines the interface between two software components or systems that are written in different programming languages, compiled by different compilers, or running on different hardware architectures.
+ The ABI is crucial for enabling interoperability between different software components, such as different libraries, object files, or even entire programs. It allows components compiled independently and potentially on different platforms to work seamlessly together by adhering to a common set of rules for communication and data representation.
+ RISC V architecture being currently used uses Little Endian memory allocation
   + In little-endian representation, you store the least significant byte (LSB) at the lowest memory address and the most significant byte (MSB) at the highest memory address.
+ Given the 5 bits which are allocated, 2^5 or 32 bits are used for memory allocation.
+ An ABI table is refered to where every register is mapped to a particular variable/function.
<img width="430" alt="ABITable" src="https://github.com/Srini-web/pes_asic_class/assets/77874288/4ca9c3cb-6253-43cd-8bac-a66090687d17">
</details>

### Running C program using ABI Function calls
<details>
  
  <summary>Theory</summary>
  
+ In this program, a base(caller) c program calls a function written in assembly-level language. While they are both manipulated using ABI, the function call suceeds.
 <img width="407" alt="ABIFLOW" src="https://github.com/Srini-web/pes_asic_class/assets/77874288/e046f952-d4b3-4239-8379-415eba3ae42e">
 
+ CPU Functioning
  
<img width="502" alt="insert" src="https://github.com/Srini-web/pes_asic_class/assets/77874288/d9da06e4-242c-449e-9b4b-a80acc6c48a9">
</details>
 
Dropdown
<details>
<summary>Create cnt1t9.c and load.S</summary>
  
+ create files
```
leafpad cnt1t9.c
leafpad load.S
```
</details>

<details>
<summary>Run and simulate using spike</summary>
  
+ Run c program file and function in assembly language
```
riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o cnt1t9.o cnt1t9.c load.S
spike pk cnt1t9.o
```

<img width="531" alt="s1" src="https://github.com/Srini-web/pes_asic_class/assets/77874288/b91d2dab-0d0d-44ae-92c2-8090aa048adb">


</details>

<details>
<summary>Run disassembly</summary>  

```
riscv64-unknown-elf-objdump -d cnt1tn.o|less
```
<img width="448" alt="s2" src="https://github.com/Srini-web/pes_asic_class/assets/77874288/d1bb18cf-9b3f-4737-8b19-a02d27870b5f">

</details>

<details>
<summary>RISCV CPU verification using iverilog</summary>
  
+ verification of CPU using verilog
   + using vim command
```
vim picorv32.v
```
![s3](https://github.com/Srini-web/pes_asic_class/assets/77874288/f49b626b-b6ef-469e-91a2-718d3a98919c)


  + using less command
```
less picorv32.v
```

![s4](https://github.com/Srini-web/pes_asic_class/assets/77874288/d37d6754-fb5f-4d3c-9632-0974ec25e38e)
  
 + running iverilog and testbench
```
vim picorv32.v
vim testbench.v
vim rv32im.sh
chmod 777 rv32im.sh
./rv32im.sh
```

<img width="439" alt="vimrins5" src="https://github.com/Srini-web/pes_asic_class/assets/77874288/0b39bfc9-8065-4ab2-9858-229919b3147e">

  + genrating hexadecimal (HEX file)
```
vim firmare.hex
```
  <img width="467" alt="s6" src="https://github.com/Srini-web/pes_asic_class/assets/77874288/ce2201f4-40a5-4b8b-9722-39d723b60d82">
  
</details>

## Day 3

### Introduction to Verilog RTL Design and Synthesis
<details>
<summary> Theory </summary>

 - **Simulator**
   - It is a tool used for simulating the design. It looks for the changes in the input signals to evaluate the outputs.
   - If there is no change in the inputs, the simulator doesn't evaluate the outputs.
   - RTL is checked for adherence to the spec by simulating the design.
   - The tool used here is **iverilog**.

- **iVerilog**
  -  It is an open-source Verilog simulator used for testing and simulating digital circuit designs described in the Verilog hardware description language (HDL).
  -  Both the design and the testbench are fed to the simulator and it produces a vcd (value change dump) file.
  -  In order to view the vcd file, we use the GTKwave where we can see the waveforms.
    
   <img width="526" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/37b643b5-e41e-425d-85f0-a55d7e190571">

- **Design**
  - It is the actual verilog code or set of verilog codes that the intended functionality to meet the required specifications.
  - Verilog is used to describe the behavior and structure of digital circuits at different levels of abstraction, from high-level system descriptions down to low-level gate-level representations. 

- **Testbench**
  - A testbench is a specialized Verilog module or program used to verify the functionality and behavior of another Verilog module, circuit, or design. Testbenches are essential for testing and simulating digital designs before they are synthesized or manufactured as physical chips.
  - It is a setup to apply a stimulus to the design to check its functionality.

    <img width="526" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/72e6ffe4-abba-41f1-b79f-240f125b410b">

 + **Synthesizer**
  - It is a tool used for converting RTL design code to netlist.
  - Here, the synthesizer used is **Yosys**.

+ **Yosys**
  - It is an open-source framework for Verilog RTL synthesis and formal verification.
  - Yosys provides a collection of tools and algorithms that enable designers to transform high-level RTL (Register Transfer Level) descriptions of digital circuits into optimized gate-level representations suitable for physical implementation on hardware.

 <img width="561" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/5f879aaa-ec65-4362-9f91-f39999069732">

   - Design and .lib files are fed to the synthesizer to get a netlist file.
   - **Netlist** is the representation of the design in the form of standard cells in the .lib
     
+ Commands used to perform different operations:
  - `read_verilog` to read the design
  - `read_liberty` to read the .lib file
  - `write_verilog` to write out the netlist file
 
+ To verify the synthesis

<img width="566" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/fd73f6b8-f594-4e4f-bb1a-b600fb4475f8">

   - Netlist along with the testbench is fed to the iverilog simulator.
   - The vcd file generated is fed to the gtkwave simulator.
   - The output on the simulator must be the same as the output observed during RTL simulation.
   - The same RTL testbench can be used as the primary inputs and primary outputs remain same between the RTL design and synthesised netlist.

 + **Logic Synthesis**
  - Logic synthesis is a process in digital design that transforms a high-level hardware description of a digital circuit, typically in a hardware description language (HDL) like Verilog or VHDL, into a lower-level representation composed of logic gates and flip-flops.
  - The goal of logic synthesis is to optimize the design for various criteria such as performance, area, power consumption, and timing.

 + **.lib**
   - It is a collection of logical modules like And, Or, Not etc.
   - It has different flavors of same gate like 2 input AND gate, 3 input AND gate etc with different performace speed.
  
+ **Why different flavors  of gate?**
  - In order to make a circuit faster, the clock frequency should be high.
  - For that, the time period of the clock should be as low as possible.
  
<img width="400" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/bc2242db-49e8-4c19-a06e-8f8e82f55729">

+ In a sequential circuit, clock period depends on:
  - Clock to Q of flip-flop A.
  - Propagation delay of combinational circuit.
  - Setup time of flip-flop B.

<img width="400" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/112de4cd-6e0c-46ec-ad94-0cb6540af7e1">

+ **Why need fast and slow cells?**
  - To ensure that there are no HOLD issues at flip-flop B, we require slow cells.
  - For a smaller propagation time, we need faster cells.
  - The collection forms the .lib

+ **Faster Cells vs Slower Cells**
  - Load in digital circuit is of Capacitence.
  - Faster the charging or dicharging of capacitance, lesser is the cell delay.
  - However, for a quick charge/ discharge of capacitor, we need transistors capable of sourcing more current i.e, we need **wide transistors**.
  - Wider transistors have lesser delay but consume more area and power.
  - Narrow transistors have more delay but consume less area and performance.
  - Faster cells come with a cost of area and power.
 
+ **Selection of the Cells**
  - We have to guide the Synthesizer to choose the flavour of cells that is optimum for implementation of logic circuit.
  - More use of faster cells leads to bad circuit in terms of power and area and also hold time violations.
  - More use of slower cells leads to sluggish circuits amd may not meet the performance needs.
  - Hence the guidance is offered to the synthesiser in the form of **constraints**. 

 - **Setup**
   - Contains sky130RTLDesignAndSynthesisWorkshop folder which contains
    - my_lib: contains all the library files
    - lib: contains sky130 standard cell library used for our synthesis
    - verilog_model: contains all the standard cell verilog modules of the standard cells contained in the .lib
    - verilog_files: contains all the verilog source files and testbench files that are required for labs

</details>



<details>
<summary> iVerilog GTKwave </summary>	

```
cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files
ls
```
![s1verilogfiles](https://github.com/Srini-web/pes_asic_class/assets/77874288/6c2f3048-5342-438f-956f-4cdee3604e6e)

```
iverilog good_mux.v tb_good_mux.v
./a.out
gtkwave tb_good_mux.vcd
```

![s2goodmuxrun](https://github.com/Srini-web/pes_asic_class/assets/77874288/cd3c3ce0-54f1-4268-81cc-aaaab905d885)

![s3gtk1](https://github.com/Srini-web/pes_asic_class/assets/77874288/22c308a1-cfaf-4edc-aefe-b2ba2219f28d)

```
gvim tb_good_mux.v -o good_mux.v
```
![s3gtk2](https://github.com/Srini-web/pes_asic_class/assets/77874288/90449417-dc0c-4edb-a842-cfd87de0d78c)

</details>

<details>
<summary> Yosys good_mux  </summary>	

+ To invoke yosys
```
cd
cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files
yosys
```
![s4yosys](https://github.com/Srini-web/pes_asic_class/assets/77874288/2dabd406-6263-4bcd-94b0-8412e8dba545)

+ To read the library, design and synthesize a module named "good_mux.v"
  ```
  read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
  read_verilog good_mux.v
  synth -top good_mux
  ```
  
![s5yosysdesread](https://github.com/Srini-web/pes_asic_class/assets/77874288/93b46c6b-85a4-4ae4-a13f-41227c4c8c23)

![s6yosyssynth](https://github.com/Srini-web/pes_asic_class/assets/77874288/4a405886-992a-4b2f-8c4c-8340f36983bb)

   
 + Generate the netlist
   ```
   abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
   ```

 ![s7yosysnetlist](https://github.com/Srini-web/pes_asic_class/assets/77874288/85d7298a-d438-4dd0-b2b9-fefa7676ef18)


+ To see the logic realized
  ```
  show
  ```
  
![s8yosysshow](https://github.com/Srini-web/pes_asic_class/assets/77874288/04abfbfd-c6f4-4520-9f97-234264db7a6d)


+ To write the netlist
  ```
  write_verilog good_mux_netlist.v
  !gvim good_mux_netlist.v
  ```
  ![s9yosyswrnl](https://github.com/Srini-web/pes_asic_class/assets/77874288/832a9261-1c64-4d35-a176-6c89f91861ae)

  + To view a simplified code
    ```
    write_verilog -noattr good_mux_netlist.v     
    !gvim good_mux_netlist.v
    ```
     ![s10yosysnlsimp](https://github.com/Srini-web/pes_asic_class/assets/77874288/3aa56285-4512-4e8b-a7ec-bd5431c5f779)


</details>
