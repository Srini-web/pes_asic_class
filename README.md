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
+ Given the 5 bits that are allocated, 2^5 or 32 bits are used for memory allocation.
+ An ABI table is referred to where every register is mapped to a particular variable/function.
<img width="430" alt="ABITable" src="https://github.com/Srini-web/pes_asic_class/assets/77874288/4ca9c3cb-6253-43cd-8bac-a66090687d17">
</details>

### Running C program using ABI Function calls
<details>
  
  <summary>Theory</summary>
  
+ In this program, a base(caller) c program calls a function written in assembly-level language. While they are both manipulated using ABI, the function call succeeds.
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

## Day 4
### Timing libs, hierarchical vs flat synthesis and efficient flop coding styles

<details>
<summary> Theory </summary>	
  
+ libraries in yosys
  + The first line in the file `library ("sky130_fd_sc_hd__tt_025C_1v80") ` :
    
    - tt: indicates variations due to process and here it indicates **Typical Process**.
    - 025C: indicates the variations due to temperatures where the silicon will be used.
    - 1v80: indicates the variations due to the voltage levels where the silicon will be incorporated.
      
 **Hierarchical Synthesis**
  Hierarchical synthesis is an approach in digital design and logic synthesis where complex designs are broken down into smaller, more manageable modules or sub-circuits, and each module is synthesized individually. These synthesized modules are then integrated back into the overall design hierarchy. This approach helps manage the complexity of large designs and allows designers to work on different parts of the design independently. 

 **Flattened Synthesis**
  Flattened synthesis is the opposite of hierarchical synthesis. Instead of maintaining the hierarchical structure of the design during synthesis, flattened synthesis combines all modules and sub-modules into a single, flat representation. This means that the entire design is synthesized as a single unit, without preserving the modular organization present in the original high-level description.

**Why do we need a Flop?**

+ A flip-flop (often abbreviated as "flop") is a fundamental building block in digital circuit design.
+ It's a type of sequential logic element that stores binary information (0 or 1) and can change its output based on clock signals and input values.
+ In a combinational circuit, the output changes after the propagation delay of the circuit once inputs are changed.
+ During the propagation of data, if there are different paths with different propagation delays, then a glitch might occur.
+ There will be multiple glitches for multiple combinational circuits.
+ Hence, we need flops to store the data from the combinational circuits.
+ When a flop is used, the output of combinational circuit is stored in it and it is propagated only at the posedge or negedge of the clock so that the next combinational circuit gets a glitch free input thereby stabilising the output.
+ We use control pins like **set** and **reset** to initialise the flops.
+ They can be synchronous and asynchronous.

</details>  
<details>
  <summary> Introduction to Timing Dot Libs </summary>	
  
+ To view the contents in the .lib
```
gvim ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
```
![s1dotappl](https://github.com/Srini-web/pes_asic_class/assets/77874288/0e37b704-3c54-454a-a108-1ca563283200)

 
+ It also displays the units of various parameters and cells.

![s2dotlibclass](https://github.com/Srini-web/pes_asic_class/assets/77874288/6632c33b-1786-46c2-b07c-7bb83bf1245d)

+ It gives the features of the cells
  + To enable line number `:se nu`
  ![s3serno](https://github.com/Srini-web/pes_asic_class/assets/77874288/d32b885a-93c7-4a26-b3da-3f6ce1d41d1b)

+ To view any instance `:/instance`
  + Since there are 5 inputs, for all the 32 possible combinations, it gives the delay, power, and all the other parameters for each cell.
  + The below image shows the power consumption and area comparison.
  
![s4 1comp](https://github.com/Srini-web/pes_asic_class/assets/77874288/24fa7730-0bfa-4331-8039-794669ab1add)

</details>

<details>
<summary> Hierarchical Synthesis Flat Synthesis </summary>	
  
+ The file we used in this lab is multiple_modules.v
  
  ```
  cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files
  gvim multiple_modules.v
  ```

![s5file](https://github.com/Srini-web/pes_asic_class/assets/77874288/136819b9-5e96-4d19-a9d2-22192abfcb97)


+  `multiple_modules` instantiates `sub_module1` and `sub_module2`

```
Launch yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog multiple_modules.v
synth -top multiple_modules
```

![s6yosys](https://github.com/Srini-web/pes_asic_class/assets/77874288/fd46db6d-9f8b-45ed-a96c-925ac82bd2eb)

+  Netlist generation
  
  ```
  abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
  show multiple_modules
  ```

![s7moduleload](https://github.com/Srini-web/pes_asic_class/assets/77874288/c3386884-ef18-42c9-9a3a-1c997219a64b)

```
write_verilog -noattr multiple_modules_hier.v
!gvim multiple_modules_hier.v
```


![s8submoduleload](https://github.com/Srini-web/pes_asic_class/assets/77874288/ed9c6d8b-7100-4a14-84d2-94d0eca10618)

![s9submoddiag](https://github.com/Srini-web/pes_asic_class/assets/77874288/01d74903-1338-4066-90b1-ac8fe6719ce9)


+  Flattened Synthesis
  ```
  yosys
  read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
  synth -top multiple_modules
  abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
  flatten
  show
  ```
  
![s10flatteneddiag](https://github.com/Srini-web/pes_asic_class/assets/77874288/db029588-9994-4a2e-bd1f-04981bfb4365)

```
write_verilog -noattr multiple_modules_flat.v`
!gvim multiple_modules_flat.v
```
  ![s11befflat](https://github.com/Srini-web/pes_asic_class/assets/77874288/9736cae1-c6f6-4276-be9d-ee05f375ecd8)
  ![s12afflat](https://github.com/Srini-web/pes_asic_class/assets/77874288/ebf2d734-130c-443f-97bd-9e0d928a413a)

</details>


<details>
<summary> D Flip-flop review </summary>	

+ D Flip-Flop with Asynchronous Reset
  + When the reset is high, the output of the flip-flop is forced to 0, irrespective of the clock signal.
  + Else, on the positive edge of the clock, the stored value is updated at the output.
 ```
  gvim dff_asyncres_syncres.v
 ```
   ![s13dasres](https://github.com/Srini-web/pes_asic_class/assets/77874288/2a2bc0c9-abd8-4f59-90a9-9c4b8932787c)


+ D Flip_Flop with Asynchronous Set
  + When the set is high, the output of the flip-flop is forced to 1, irrespective of the clock signal.
  + Else, on positive edge of the clock, the stored value is updated at the output.

```
gvim dff_async_set.v
```

![s14dasset](https://github.com/Srini-web/pes_asic_class/assets/77874288/2a77a30a-2e9f-4d59-a779-ccc5fed5731e)


+ D Flip-Flop with Synchronous Reset
  + When the reset is high on the positive edge of the clock, the output of the flip-flop is forced to 0.
  + Else, on the positive edge of the clock, the stored value is updated at the output.

```
gvim dff_syncres.v
```

![s15dsres](https://github.com/Srini-web/pes_asic_class/assets/77874288/40a5b9ca-8390-4bc7-a4c0-9770ea65492c)

+ D Flip-Flop with Asynchronous Reset and Synchronous Reset
  + When the asynchronous reset is high, the output is forced to 0.
  + When the synchronous reset is high at the positive edge of the clock, the output is forced to 0.
  + Else, on the positive edge of the clock, the stored value is updated at the output.
  + Here, it is a combination of both synchronous and asynchronous reset DFF.

```
gvim dff_asyncres_syncres.v
```

![s16dsynasynrst](https://github.com/Srini-web/pes_asic_class/assets/77874288/0b1dd71b-a36a-431c-92c1-c45a0c040017)


</details>

<details>
<summary> Lab Flop Synthesis and Simulations </summary>	

+ D Flip-Flop with Asynchronous Reset
  + Simulation
    ```
    cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files
    iverilog dff_asyncres.v tb_dff_asyncres.v
    ./a.out
    gtkwave tb_dff_asyncres.vcd
    ```
  

   ![s16simul](https://github.com/Srini-web/pes_asic_class/assets/77874288/361b062d-4000-45da-8250-f9ae73d24efa)



  + Synthesis
    ```
    cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files
    yosys
    read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
    read_verilog dff_asyncres.v
    synth -top dff_asyncres
    dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
    abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
    show
    ```
   
    <img width="925" alt="s17synth" src="https://github.com/Srini-web/pes_asic_class/assets/77874288/d92920ea-1c72-4be8-bd7b-a26ac75f75a6">

 + D Flip_Flop with Asynchronous Set
   + Simulation
     ```
     cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files
     iverilog dff_async_set.v tb_dff_async_set.v
     ./a.out
     gtkwave tb_dff_async_set.vcd
     ```

![s18simul2](https://github.com/Srini-web/pes_asic_class/assets/77874288/cddf0a2b-252d-41b0-bf4e-f15b1deba4d1)

  + Synthesis
```
cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog dff_async_set.v`
synth -top dff_async_set
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```
<img width="922" alt="s19synth2" src="https://github.com/Srini-web/pes_asic_class/assets/77874288/89d2d27c-18b4-45c2-9052-a12f5ed70148">


+ D Flip-Flop with Synchronous Reset
  + Simulation
  ```  
  cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files
  iverilog dff_syncres.v tb_dff_syncres.v
  ./a.out
  gtkwave tb_dff_syncres.vcd
   ``` 

  ![s20simul3](https://github.com/Srini-web/pes_asic_class/assets/77874288/649d05d6-34be-4d10-93c1-34ad70b6f9aa)

 
  + Synthesis
  ```
  cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files
  yosys
  read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
  read_verilog dff_syncres.v
  synth -top dff_syncres
  dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
  abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
  show
  ```

<img width="925" alt="s21synth3" src="https://github.com/Srini-web/pes_asic_class/assets/77874288/f5ba1e8f-6dc2-4f68-bf61-23db96e779dc">

</details>

<details>
<summary> Interesting Optimisations </summary>	

```
gvim mult_2.v
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog mult_2.v
synth -top mul2
```

![s22nosynth](https://github.com/Srini-web/pes_asic_class/assets/77874288/e0d2d63c-b1f2-42be-b64c-756de22f037f)

```
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```


![s23diag](https://github.com/Srini-web/pes_asic_class/assets/77874288/960b508e-dcde-4377-8522-dee1556cbbbe)

```
write_verilog -noattr mul2_netlist.v
!gvim mul2_netlist.v
```
  <img width="436" alt="s24c1" src="https://github.com/Srini-web/pes_asic_class/assets/77874288/0643321d-a40a-44ca-a68e-ae9a6f9fa553">


```
gvim mult_8.v
```
<img width="443" alt="s25c2" src="https://github.com/Srini-web/pes_asic_class/assets/77874288/e5db84ea-d62e-4ef4-b550-4ede689e8a3a">

``` 
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib  
read_verilog mult_8.v
synth -top mult8
```
<img width="202" alt="s26op2" src="https://github.com/Srini-web/pes_asic_class/assets/77874288/6838fdc6-9a89-4e45-ac8a-25e49a5c2b47">

```
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```

<img width="305" alt="s27diag2" src="https://github.com/Srini-web/pes_asic_class/assets/77874288/4ca57c53-c118-4f7a-ae0f-198f2db9a27a">


```
write_verilog -noattr mult8_netlist.v
!gvim mult8_netlist.v
```
<img width="377" alt="s28c3" src="https://github.com/Srini-web/pes_asic_class/assets/77874288/c160860c-702e-4230-9d21-dab61dd1f815">

</details>


## Day 5
###  Combinational and sequential optimizations
#### Theory
<details>
<summary> Theory : Combinational Optimisation </summary>
	
+ Combinational logic refers to logic circuits where the outputs depend only on the current inputs and not on any previous states.
+ Combinational optimization is a field of study in computer science and operations research that focuses on finding the best possible solution from a finite set of options for problems that involve discrete variables and have no inherent notion of time.
+ Optimising the combinational logic circuit is squeezing the logic to get the most optimized digital design so that the circuit finally is area and power efficient.
+ Techniques for Optimisations:
  - **Constant propagation** is an optimization technique used in compiler design and digital circuit synthesis to improve the efficiency of code and circuit implementations by replacing variables or expressions with their constant values where applicable.
  - **Boolean logic optimization**, also known as logic minimization or Boolean function simplification, is a process in digital design that aims to simplify Boolean expressions or logic circuits by reducing the number of terms, literals, and gates required to implement a given logical function.

</details>

<details>
<summary> Theory : Sequential Logic Optimisations </summary>	

+ Sequential logic optimizations involve improving the efficiency, performance, and resource utilization of digital circuits that include memory elements like flip-flops and latches.
+ Optimizing sequential logic is crucial in ensuring that digital circuits meet timing requirements, consume minimal power, and occupy the least possible area while maintaining correct functionality.
+ Optimisation methods:
  - **Sequential constant propagation**, also known as constant propagation across sequential elements, is an optimization technique used in digital design to identify and propagate constant values through sequential logic elements like flip-flops and registers. This technique aims to replace variable values with their known constant values at various stages of the logic circuit, optimizing the design for better performance and resource utilization.
  - **State optimization**, also known as state minimization or state reduction, is an optimization technique used in digital design to reduce the number of states in finite state machines (FSMs) while preserving the original functionality.
  - **Sequential logic cloning**, also known as retiming-based cloning or register cloning, is a technique used in digital design to improve the performance of a circuit by duplicating or cloning existing registers (flip-flops) and introducing additional pipeline stages. This technique aims to balance the critical paths within a circuit and reduce its overall clock period, leading to improved timing performance and better overall efficiency.
  - **Retiming** is an optimization technique used in digital design to improve the performance of a circuit by repositioning registers (flip-flops) along its paths to balance the timing and reduce the critical path delay. The primary goal of retiming is to achieve a shorter clock period without changing the functionality of the circuit.
 
</details>

#### Combinational Logic Optimisation 
<details>
<summary> opt_check </summary>	
	
```
gvim opt_check.v
```
![s1code](https://github.com/Srini-web/pes_asic_class/assets/77874288/cc3d71c8-ddf6-4e1c-9b3b-0032f6678524)

```
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog opt_check.v
synth -top opt_check
opt_clean -purge
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```

 ![s2op](https://github.com/Srini-web/pes_asic_class/assets/77874288/0d255928-5568-4b56-b2fb-517b32fbf13f)


</details>

<details>
<summary> opt_check2 </summary>	
	
```
gvim opt_check2.v`
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog opt_check2.v
synth -top opt_check2
opt_clean -purge
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```
 
![s3op2](https://github.com/Srini-web/pes_asic_class/assets/77874288/707a8cc8-9ace-492e-813b-a8c43bba8aa6)

</details>

<details>
<summary> opt_check3 </summary>	
	
```
gvim opt_check3.v
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog opt_check3.v
synth -top opt_check3
opt_clean -purge
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```

![s4op3](https://github.com/Srini-web/pes_asic_class/assets/77874288/badbf03d-d8c4-4a5f-8818-2cf6adb9201d)

</details>

<details>
<summary> opt_check4 </summary>
	
```
gvim opt_check4.v
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog opt_check4.v
synth -top opt_check4
opt_clean -purge
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```

![s5op4](https://github.com/Srini-web/pes_asic_class/assets/77874288/156fcc50-30f2-4f85-8477-e6bac76c186d)

</details>

<details>
<summary> multiple_module_opt </summary>
	
```
gvim multiple_module_opt.v
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog multiple_module_opt.v
synth -top multiple_module_opt
opt_clean -purge
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```
![s6op5](https://github.com/Srini-web/pes_asic_class/assets/77874288/63b9746a-0a10-47dd-87e2-3ec01be1f213)

<img width="301" alt="s6 2op5" src="https://github.com/Srini-web/pes_asic_class/assets/77874288/7a84ba38-e617-4ddf-b41f-c5a868c90b27">

</details>

#### Sequential Logic Optimisations

<details>
<summary> dff_const1 </summary>	

+ Simulation
```
gvim dff_const1.v
iverilog dff_const1.v tb_dff_const1.v
/a.out
gtkwave tb_dff_const1.vcd
```

![s7dff1](https://github.com/Srini-web/pes_asic_class/assets/77874288/4687bc6d-1b7a-494f-b549-f96758c5bd8f)

+ Synthesis

```
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog dff_const1.v
synth -top dff_const1
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```

![s8op1](https://github.com/Srini-web/pes_asic_class/assets/77874288/9e85d0ec-162e-4f8d-8b99-531acc5eaab5)

</details>

<details>
<summary> dff_const2 </summary>	
+ Simulation
  
```  
gvim dff_const2.v
iverilog dff_const2.v tb_dff_const2.v
/a.out
gtkwave tb_dff_const2.vcd
```


![s9dff2](https://github.com/Srini-web/pes_asic_class/assets/77874288/2a337dc0-243a-45f6-a966-c51845153a96)

 + Synthesis
 
```
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog dff_const2.v
synth -top dff_const2
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```

![s10op2](https://github.com/Srini-web/pes_asic_class/assets/77874288/99326cd3-3e8e-4f7e-8634-2fad94d0c575)

</details>

<details>
<summary> dff_const3 </summary>
+ Simulation

```
gvim dff_const3.v
iverilog dff_const3.v tb_dff_const3.v
/a.out
gtkwave tb_dff_const3.vcd
```

![s11dff3](https://github.com/Srini-web/pes_asic_class/assets/77874288/6d02cd6a-d6d0-4f75-abfc-a8093ef5b6f7)

+ Synthesis

```
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog dff_const3.v
synth -top dff_const3
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```


![s12op3](https://github.com/Srini-web/pes_asic_class/assets/77874288/fe820bb0-4e11-43c8-99d8-b5e464994eb2)

</details>

<details>
<summary> dff_const4 </summary>	

+ Simulation

 ``` 
gvim dff_const4.v
iverilog dff_const4.v tb_dff_const4.v
/a.out
gtkwave tb_dff_const4.vcd
```
![s13dff4](https://github.com/Srini-web/pes_asic_class/assets/77874288/879957c2-92a5-4fc0-b350-3d708fcb0b41)

+ Synthesis

```
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog dff_const4.v
synth -top dff_const4
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```

![s13op4](https://github.com/Srini-web/pes_asic_class/assets/77874288/45eb59d6-df92-4b5f-876e-9432d7d069fc)

</details>

<details>
<summary> dff_const5 </summary>	

+ Simulation
```
gvim dff_const5.v
iverilog dff_const4.v tb_dff_const4.v
/a.out
gtkwave tb_dff_const5.vcd
```

![s15dff5](https://github.com/Srini-web/pes_asic_class/assets/77874288/71e9d404-de5d-4a8a-b6ba-e29ea5c8e2d7)

+ Synthesis

```
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog dff_const4.v
synth -top dff_const4
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```
![s16op5](https://github.com/Srini-web/pes_asic_class/assets/77874288/88c9441c-0ab2-4893-ba91-0cf4f889c70f)


</details>

#### Counter Logic Optimisations
<details>
<summary> counter_opt </summary>

 ```
gvim counter_opt.v
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog counter_opt.v
synth -top counter_opt
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```

![s17ctr1](https://github.com/Srini-web/pes_asic_class/assets/77874288/c845b435-a9ff-4c6b-b778-f8ee410d540f)

</details>

<details>
<summary> counter_opt2 </summary>	

```
gvim counter_opt2.v
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog counter_opt2.v
synth -top counter_opt2
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```

<img width="923" alt="s18ctr2" src="https://github.com/Srini-web/pes_asic_class/assets/77874288/1a444ed6-80d1-4534-bdaf-30bc0390b607">

</details>
