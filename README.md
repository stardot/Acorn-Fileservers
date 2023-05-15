Notes on Level3 and FileStore source code and versions
======================================================

The goal of this project is to use the Acorn Fileserver Level3 1.06 source code, Level3 1.31 souce code and the FileStore 1.31 source code to recreate source code for all the different known binaries. This will help to identify precisely what changes were made between the version releases as no known documentation is available.

The source code for v1.06 is thought to be the original and creates a binary identical to an orginal 1.06 disk set albeit without the serial number. Assembling the source code appears to have originally been done on a BBC Micro with 256K Turbo co-processor and updated to assemble on an Archimedes under the 6502 Turbo Co-Processor emulator at some point - most likely at Acorn.

The FileStore 1.31 source code did not contain the MOS part of the ROM, only the Fileserver code. On examination it was clear this was a derivative work of the Level3 source code. 

The source code for the versions 0.90, 0.92, 1.01, 1.03, 1.04 have been recreated using the v1.06 source code and the individual binaries.

No changes were needed to the v1.06 souce code as it produced a binary identical to the original. It was found the binary for v1.07 was produced from the v1.06 source code but the dongle directive was set to present. This should not have resulted in a different version number and it is interesting that a binary without protection but with a valid serial number was "in the wild".

All the binaries to v1.07 are dated (C)1984 and this is probably left over from the Level2 code. There were several comments with dates in the source code which enabled recreation of an approximate time line and further understanding of the versions. Dates of the code versions have been estimated using the dates on source code comments.

The first version to update the copyright notice was v1.24 which used (C)1987. The availability of the source code from v1.31 enabled the creation of code for v1.24 which by now had support for AUN and pseudo directory symbols.

The source code for v1.31 had directories for L3, FileStore and Filesever. 
\L3 contained the Level3 source code and \FileStore the source code for the E01 FS ROM. The directory \Fileserver contained a set of files where work had been started to merge the two code bases for Level3 and FileStore, but was incomplete. 

The FileStore uses a 65C102 processor and the code had been optimised to make use of the extended instruction set, whereas the Level3 Fileserver was kept as 6502 instruction compatible. It made sense to complete this work and enable the creation of later Level3 Fiileserver versions based on FileStore changes and a single code base. However, it has been found the FileStore has implemented some changes to the filing structure which is causing backwards compatibility issues with existing filing systems. This may have been why the shared source was not finished, or was on the "to do" list.

The code will assemble on both BBC and RISC OS based machines. Due to limits on the number of files in a directory on the BBC, and to create a standard approach throughout the different code sets, the files used for the build process were moved to the root directory.

There are two discs for each version, one containing the source and the other has pre-assembled binaries for convenience.


Assembling the Fileserver Source Code
=====================================

The assembler sequence for the source code has been updated to assemble on either a BBC or RISC OS. No changes were required to the code, only the setting of directories and loading the 6502 Turbo Co-Processor emulator.

For later versions using the shared code base, a program asks which is required, Level3 or FileStore, and triggers the corresponding sequence. Due to space constraints, an 800K ADFS disc is provided for the RISC OS version.

On the BBC, ADFS and an Acorn Turbo (256K) 6502 Co Processor are needed to assemble the sources.


Using ADFS
==========

The disk organization on ADFS involves a single disk image containing the tools (TurMASM), build scripts, source code, and sufficient free space for the build process.

In the adfs/ directory there are the files 

v0.90-v1.31
   Level3-XXXsrc.adl - 640KB interleaved disk image with the source code
   Level3-XXXbin.adl - 640KB interleaved disk image with the binary code

v1.31-v1.40
   Fileserver-XXXsrc-BBC.adl  - 640KB interleaved disk image with the source
                                code for assembly on the BBC
   Fileserver-XXXsrc-RISC.adf - 800KB interleaved disk image with the source
                                code for assembly on RISC OS

The only difference between the BBC and RISC OS discs is the file "GO" and the RISC OS Turbo Emulator executable "65ARTHUT" have been removed.
   
Create a disk using the appropriate file or load into an emulator of your choice.

On an Archimedes/RISC PC execute the file $.GO.

It uses the turbo emulator 65ARTHURT so no changes to the assembler executables are required.

A BBC emulator will need to be running with an Acorn Turbo (256K) 6502 Co-Processor emulation. The b-em emulator supports this configuration. Pressing SHIFT-BREAK or *E.!BOOT will start the processs.

The resulting binary will be placed in the root directory, under the filename "FS". Pre-built executables are already included.

ROM images for the FileStore are created with the name FSRom.

The source code is in Acorn MASM format, and a copy of the "Turbo" version of MASM (called TurMASM) is included in the disk images in the library folder. MASM was released by Acornsoft as part of the "6502 Development Package" and many details how to use it are in the accompanying manual:
http://8bs.com/othrdnld/manuals/applications/6502-Development-Package.zip. 

Source for the assembler is available on GitHub:
https://github.com/stardot/AcornMASMv115


Assembler directives
====================

The assembler directive flag for the Winchester being present is &00. If set to another value the code assembly will fail as the definitions for PARAMS and NOPRMS are missing from the source. This directive may have been used in earlier versions of the code to produce L2 or L3 fileservers, however there is no directive to remove the banner in the code for "Winchester File Server" or Version 3 at the start of the source file UADE03. There appear to be significant differences to the code needed for Level2 to the source code for Level3 v0.90.


Software Protection
===================
Version numbers

1.01 23AES240100418

1.03 24AES240200625

1.04

1.06 24AES242001080

1.07 24AES243002000

1.24

1.31

The version numbers above replace the text  "Version string" found in line 30 of the source file UADE03. It is believed the file server binary "FS" had to be placed at the start of side 2 on the installation disc, and the install routine would apply this number when copying the binary. The installation disc was in the DFS format and original install disc images can be found with v1.06.


Dates
=====
With all binaries that use the date from the RTC dongle, the year is displayed incorrectly. These versions also do not display the seconds on the main screen. The versions assembled not to use the RTC dongle must have the date and time entered manually. There were large changes to the date handling in v1.24 and by v1.33 all the issues seem to have been resolved.

The versions without the dongle do display the seconds on the main screen. Only the patched version 0.92 corrects this problem and allows years after 1999 to be entered and displayed correctly.
