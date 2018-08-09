# UnSHc
UnSHc - How to decrypt SHc *.sh.x encrypted file ?

ARM VERSION (First Beta Release) 

It has only been tested on raspberry PI 3 with raspbian. It probably won't work on ARM binaries that you try to decrypt on other platforms.

# Please note

I will not decrypt any file for people.
Issues on GitHub are only to discuss about bug and/or improvement of the tool "UnSHc".

If you think you have found a bug, please provide me the encrypted file ***AND the unencrypted file corresponding***. Without these two files I can't reverse it and analyze it.
Add some information about the architecture where the encrypted file has been created (what linux distribution and version, what architecture x86 or x64, etc.).

***All others "file decryption issues" will be closed directly.***

# SHc review

SHc (SHell compiler) is a fabulous tool created and maintained by Francisco Javier Rosales Garcia (http://www.datsi.fi.upm.es/~frosal/).
This tool protect any shell script with encryption (ARC4).

```shell
wget -q http://www.datsi.fi.upm.es/~frosal/sources/shc-3.8.9.tgz
tar zxvf shc-3.8.9.tgz
cd shc-3.8.9
make
```

# How to use SHc ?

```shell
root@server:~/shc/shc-3.8.9# shc -h
shc Version 3.8.9, Generic Script Compiler
shc Copyright (c) 1994-2012 Francisco Rosales <frosal@fi.upm.es>
shc Usage: shc [-e date] [-m addr] [-i iopt] [-x cmnd] [-l lopt] [-rvDTCAh] -f script
-e %s Expiration date in dd/mm/yyyy format [none]
-m %s Message to display upon expiration [&quot;Please contact your provider&quot;]
-f %s File name of the script to compile
-i %s Inline option for the shell interpreter i.e: -e
-x %s eXec command, as a printf format i.e: exec('%s',@ARGV);
-l %s Last shell option i.e: --
-r Relax security. Make a redistributable binary
-v Verbose compilation
-D Switch ON debug exec calls [OFF]
-T Allow binary to be traceable [no]
-C Display license and exit
-A Display abstract and exit
-h Display help and exit
Environment variables used:
Name Default Usage
CC cc C compiler command
CFLAGS C compiler flags
Please consult the shc(1) man page.
```

Encrypted shell script are named "*.sh.x" by default.

UnSHc is a tool to reverse the encryption of any SHc encrypted *.sh.x script.

# How to use UnSHc ?

```shell
[root@server:~/unshc]$ ./unshc.sh -h
 _   _       _____ _   _
| | | |     /  ___| | | |
| | | |_ __ \ `--.| |_| | ___
| | | | '_ \ `--. \  _  |/ __|
| |_| | | | /\__/ / | | | (__
 \___/|_| |_\____/\_| |_/\___|

--- UnSHc - The shc decrypter.
--- Version: 0.6
------------------------------
UnSHc is used to decrypt script encrypted with SHc
Original idea from Luiz Octavio Duarte (LOD)
Updated and modernized by Yann CAM
- SHc   : [http://www.datsi.fi.upm.es/~frosal/]
- UnSHc : [https://www.asafety.fr/unshc-the-shc-decrypter/]
------------------------------

[*] Usage : ./unshc.sh [OPTIONS] <file.sh.x>
         -h | --help                          : print this help message
         -a OFFSET | --arc4 OFFSET            : specify the arc4() offset arbitrarily (without 0x prefix)
         -d DUMPFILE | --dumpfile DUMPFILE    : provide an object dump file (objdump -D script.sh.x > DUMPFILE)
         -s STRFILE | --stringfile STRFILE    : provide a string dump file (objdump -s script.sh.x > STRFILE)
         -o OUTFILE | --outputfile OUTFILE    : indicate the output file name

[*] e.g :
        ./unshc.sh script.sh.x
        ./unshc.sh script.sh.x -o script_decrypted.sh
        ./unshc.sh script.sh.x -a 400f9b
        ./unshc.sh script.sh.x -d /tmp/dumpfile -s /tmp/strfile
        ./unshc.sh script.sh.x -a 400f9b -d /tmp/dumpfile -s /tmp/strfile -o script_decrypted.sh
```

UnSHc can only decrypt SHc encrypted file on **X86/x64** architecture.

* Demonstration in video : 
    * https://www.youtube.com/watch?v=tmHVhMuG-Vg
* SHc (in french) : 
    * https://www.asafety.fr/prog-and-dev/bashshunix-shc-le-compilateur-et-protecteur-de-script-shell/
* UnSHc (in french) : 
    * https://www.asafety.fr/unshc-the-shc-decrypter/
    
# UnSHc-MIPS

Thanks to @fffonion, a dedicated version of UnSHc has been released targeting SHc encrypted file on MIPS arcitecture.
This **UnSHc-MIPS** version is available here : https://github.com/fffonion/UnSHc-MIPS

Thank you again for your work and contribution !
