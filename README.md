# PES_ASIC_Class
Name: Srinidhi B S        SRN: PES1UG20EC201
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





