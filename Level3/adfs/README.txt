Introduction
============

This repository contains the original source code for the Acorn Level3 
Fileserver v1.06.

The structure of the repository is as follows:

fs106src,ddc
             - a sparc fs zip file of the original files. Changing the file 
               extension to .zip will allow opening using a zip archive tool
               on Windows/Linux    

L3srcIndex_v106.txt
             - an index file for the v1.06 source code files.


adfs/        - disk images for assembling on the Archimedes/RISC OS including
               RISC PCs and another for the BBC with an Acorn Turbo Processor.
         
src/         - cleaned up source files. UNIX line endings (orginals were &D) and 
               no control characters
             - FSASM - assembler sequence file
             - Loader - a basic program to combine the individual binaries and
               create the final file server binary "FS"
         
         
         
Assembling the Fileserver Source Code
=============================

The source code as found had it's assembler sequence file updated to assemble
on an Archimedes/RISC OS. A version has been provided for both the Archimedes
and BBC. No changes were required to the code, only the setting of directories
and loading the 6502 Turbo Co-Processor emulator.

On the BBC, ADFS and an Acorn Turbo (256K) 6502 Co Processor are needed to 
assemble the sources.



Using ADFS:
===========

The disk organization on ADFS involves a single disk image containing the tools
(TurMASM), build scripts, source code, and sufficient free space for the build 
process.

In the adfs/ directory are the following versions:
   
   L3_106Src-640k_ARC.adl - this is a 640KB interleaved disk image with the 
   files for the Archimedes/RISC PC computers.
   
   L3_106Src-640k_BBC.adl - this is a 640KB interleaved disk image with the 
   files for the BBC computer.
   
Create a disk using the appropriate file or load into an emulator of your 
choice.

On an Archimedes/RISC PC execute the file $.GO.

It uses the turbo emulator 65ARTHURT so no changes to the assembler 
executables are required.

A BBC emulator will need to be running with an Acorn Turbo (256K) 6502 
Co-Processor emulation. Pressing SHIFT-BREAK or *E.!BOOT will start the


The resulting binary will be placed in the root directory, under the 
filename "FS". Pre-built executables are already included.


The source code is in Acorn MASM format, and a copy of the "Turbo"
version of MASM (called TurMASM) is included in the disk images in the
library folder.
         
        
Dating
======         
The source code compiles the binary as (C) Acorn 1984 as defined in the
source file UADE03. The readme file with the sources is dated 23/11/1987.
In the sources themselves, the most recent comment with a date is 
5/6/86 in file Uade14 by LH (probably Laurence Hardwick).

The Assembly sequence file contains "By Jes 3/9/84, Updated by Glenn 8/5/85"

65ARTHURT - the 6502 256K Tube emulation has the version 0.91/13 (23 Nov 1987).

TURMASM - the turbo version of the Macro Assembler is v0.77 and dated (C)1983.

CB appears to be HIBASIC although the version is unclear. It is (C)1984.


Acknowledgements:
=================
           
Many thanks to Alan Williams for discovering these sources and making them 
available to the Acorn community.

Mark Usher. March 2021
