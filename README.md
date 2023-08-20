# PES_ASIC_Class
Name: Srinidhi B S        SRN: PES1UG20EC201 (VMSBS in the output stands for VM Srinidhi B S)
## Day1 
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
<summary>Finding the maximum and minimum values of a long long unsigned integer</summary>
  
+ Finding the maximum and minimum values of a long long unsigned integer
    + Also finding out what happens when the value assigned is beyond the datatype range
      
  <img width="559" alt="usnmaxf" src="https://github.com/Srini-web/pes_asic_class/assets/77874288/cea84d41-2cfa-49e8-a999-ad6530e8dcd4">
</details>





## Day 2
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
  
+ Run c program file and function in assemly language
```
riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o cnt1t9.o cnt1t9.c load.S
spike pk cnt1tn.o
```
<img width="571" alt="D2run2" src="https://github.com/Srini-web/pes_asic_class/assets/77874288/09798d44-3a40-42da-a274-99496613d647">


</details>

<details>
<summary>Run disassembly</summary>  

```
riscv64-unknown-elf-objdump -d cnt1tn.o|less
```
![D2disassembly](https://github.com/Srini-web/pes_asic_class/assets/77874288/4c7b2ddb-2880-4551-ae06-a0ee8eb13592)

</details>

<details>
<summary>RISCV CPU verification using iverilog</summary>
  
+ verification of CPU using verilog
   + using vim command
```
vim picorv32.v
```
![D2cpuss2](https://github.com/Srini-web/pes_asic_class/assets/77874288/90b92f7e-b750-4197-8904-1d2052794604)

  + using less command
```
less picorv32.v
```
![D2cpuss](https://github.com/Srini-web/pes_asic_class/assets/77874288/0dae9f41-ebc0-4ab3-9bf1-d99eafc3568d)


</details>


