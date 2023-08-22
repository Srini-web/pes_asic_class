# PES_ASIC_Class
Name: Srinidhi B S        SRN: PES1UG20EC201 (VMSBS in the output stands for VM Srinidhi B S)
## Day1 
### Instruction Set Architecture
+ ISA defines the interface between a computer's hardware and its software, specifically how the processor and its components interact with the software instructions that drive the execution of tasks. It encompasses a set of instructions, addressing modes, data types, registers, memory organization, and the mechanisms for executing and managing instructions
+ RISC V refers to Reduced Instruction Set Computing - Five Architecture. It is an open-source Instruction Set Architecture (ISA) that has gained significant attention and adoption in the world of computer architecture and semiconductor design.
### Integer Number Representation
+ Unsigned numbers:- also known as non-negative numbers, are numerical values that represent magnitudes without indicating direction or sign.(Range: [0, (2^n)-1 ])
+ Signed numbers are numerical values that can represent both positive and negative magnitudes, along with zero.(Range : Positive : [0 , 2^(n-1)-1] Negative : [-1 to 2^(n-1)])
  
 <img width="536" alt="Signmemalloc" src="https://github.com/Srini-web/pes_asic_class/assets/77874288/86000e0f-e3bc-4ae3-8c54-ce5f41b5a932">
 
Dropdown
<details>
<summary>Run sum1ton.c</summary>
  
+ Run sum1ton.c
```
gcc sum1ton.c
./a.out
```
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
  
  ![d1t3](https://github.com/Srini-web/pes_asic_class/assets/77874288/5a63c4d9-0086-48fb-aa95-d71c1c783e08)
</details>
<details>
<summary>Finding the maximum and minimum values of a long long unsigned and signed integer</summary>
  
+ Finding the maximum and minimum values of a long long unsigned integer
    + Also finding out what happens when the value assigned is beyond the datatype range
      
  <img width="559" alt="usnmaxf" src="https://github.com/Srini-web/pes_asic_class/assets/77874288/cea84d41-2cfa-49e8-a999-ad6530e8dcd4">
</details>





## Day 2
### Application Binary Interface
+ An Application Binary Interface (ABI) is a set of rules and conventions that dictate how binary code interacts with and communicates with other binary code, typically at the level of machine code or compiled code. In simpler terms, it defines the interface between two software components or systems that are written in different programming languages, compiled by different compilers, or running on different hardware architectures.
+ The ABI is crucial for enabling interoperability between different software components, such as different libraries, object files, or even entire programs. It allows components compiled independently and potentially on different platforms to work seamlessly together by adhering to a common set of rules for communication and data representation.
+ RISC V architecture being currently used uses Little Endian memory allocation
   + In little-endian representation, you store the least significant byte (LSB) at the lowest memory address and the most significant byte (MSB) at the highest memory address.
+ Given the 5 bits which are allocated, 2^5 or 32 bits are used for memory allocation.
+ An ABI table is refered to where every register is mapped to a particular variable/function.
<img width="430" alt="ABITable" src="https://github.com/Srini-web/pes_asic_class/assets/77874288/4ca9c3cb-6253-43cd-8bac-a66090687d17">

### Running C program using ABI Function calls
+ In this program, a base(caller) c program calls a function written in assembly-level language. While they are both manipulated using ABI, the function call suceeds.
 <img width="407" alt="ABIFLOW" src="https://github.com/Srini-web/pes_asic_class/assets/77874288/e046f952-d4b3-4239-8379-415eba3ae42e">
 
+ CPU Functioning
  
<img width="502" alt="insert" src="https://github.com/Srini-web/pes_asic_class/assets/77874288/d9da06e4-242c-449e-9b4b-a80acc6c48a9">

 
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


