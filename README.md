![Create new chip](https://github.com/JuliProg/TC58TEG6DCJTA00/workflows/Create%20new%20chip/badge.svg?event=repository_dispatch)
![ChipUpdate](https://github.com/JuliProg/TC58TEG6DCJTA00/workflows/ChipUpdate/badge.svg)
# Join the development of the project ([list of tasks](https://github.com/users/JuliProg/projects/1))


# TC58TEG6DCJTA00
Implementation of the TC58TEG6DCJTA00 chip for the JuliProg programmer

Dependency injection, DI based on MEF framework is used to connect the chip to the programmer.

<section class = "listing">

# Chip parameters
```c#


        //--------------------Vendor Specific Pin configuration---------------------------

        //  VSP1(38pin) - Vcc    
        //  VSP2(35pin) - NC
        //  VSP3(20pin) - NC

        ChipAssembly()
        {
            myChip.devManuf = "TOSHIBA";
            myChip.name = "TC58TEG6DCJTA00";
            myChip.chipID = "98DE849372";               // device ID

            myChip.width = Organization.x8;           // chip width
            myChip.bytesPP = 16384;                   // page size in bytes
            myChip.spareBytesPP = 1280;               // size Spare Area in bytes
            myChip.pagesPB = 256;                     // the number of pages per block
            myChip.bloksPLUN = 2092;                  // number of blocks in CE
            myChip.LUNs = 1;                          // the amount of CE in the chip
            myChip.colAdrCycles = 2;                  // cycles for column addressing
            myChip.rowAdrCycles = 3;                  // cycles for row addressing 
            myChip.vcc = Vcc.v3_3;                    // supply voltage
            (myChip as ChipPrototype_v1).EccBits = 1; // required Ecc bits for each 512 bytes

```
# Chip operations
```c#


            //------- Add chip operations   https://github.com/JuliProg/Wiki#command-set---------------------------------------------------

            myChip.Operations("Reset_FFh").
                   Operations("Erase_60h_D0h").
                   Operations("Read_00h_30h").
                   Operations("PageProgram_80h_10h");

```
# Chip registers (optional)
```c#


            //------- Add chip registers (optional)----------------------------------------------------

            myChip.registers.Add(                   // https://github.com/JuliProg/Wiki/wiki/StatusRegister
                "Status Register").
                Size(1).
                Operations("ReadStatus_70h").
                Interpretation("SR_Interpreted").   
                UseAsStatusRegister();



            myChip.registers.Add(                  // https://github.com/JuliProg/Wiki/wiki/ID-Register
                "Id Register").
                Size(5).
                Operations("ReadId_90h");               
                //Interpretation(ID_interpreting);          

```
# Interpretation of ID-register values ​​(optional)
```c#


        public string ID_interpreting(Register register)   
        
```
</section>
















footer
