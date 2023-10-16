Link: https://infosecwriteups.com/beginners-ctf-guide-finding-hidden-data-in-images-e3be9e34ae0d


## File

The file command is used to determine the file type of a file. There may be times when you are given a file that does not have an extension or the incorrect extension has been applied to add confusion and misdirection.

We’ll cover 2 examples of the file command.

**Example 1:**  
You are given a file named [rubiks.jpg](https://github.com/mkmety/Medium-Steg-Image/blob/master/rubiks.jpg).  
Running the file command reveals the following information.

mrkmety@kali:~$ **file rubiks.jpg  
**rubiks.jpg: PNG image data, 609 x 640, 8-bit/color RGBA, non-interlaced

The file command shows that this is a PNG file and not a JPG.

**Example 2:**  
You are given a file named [solitaire.exe](https://github.com/mkmety/Medium-Steg-Image/blob/master/solitaire.exe).  
Running the file command reveals the following:

mrkmety@kali:~$ **file solitaire.exe  
**solitaire.exe: PNG image data, 640 x 449, 8-bit/color RGBA, non-interlaced

The file command show this is a PNG file and not an executable file. Changing the extension to .png will allow you to further interact with the file.

## Exiftool

Exiftool allows you to read and write meta information in files. Flags may be hidden in the meta information and can easily be read by running exiftool.

You may need to install exiftool on your system. Run the following command to install exiftool.

mrkmety@kali:~ $ ==**sudo apt install libimage-exiftool-perl -y**==

**Example 1:  
**You are provided an image named [ocean.jpg](https://github.com/mkmety/Medium-Steg-Image/blob/master/ocean.jpg).  
Running the exiftool command reveals the following information.

mrkmety@kali:~ $ **exiftool ocean.jpg**  
ExifTool Version Number         : 11.16  
File Name                       : ocean.jpg  
Directory                       : .  
File Size                       : 42 kB  
File Modification Date/Time     : 2020:07:05 14:56:03-05:00  
File Access Date/Time           : 2020:07:05 14:56:03-05:00  
File Inode Change Date/Time     : 2020:07:05 14:56:03-05:00  
File Permissions                : rw-r--r--  
File Type                       : JPEG  
File Type Extension             : jpg  
MIME Type                       : image/jpeg  
JFIF Version                    : 1.01  
Resolution Unit                 : inches  
X Resolution                    : 72  
Y Resolution                    : 72  
Profile CMM Type                : Little CMS  
Profile Version                 : 2.1.0  
Profile Class                   : Display Device Profile  
Color Space Data                : RGB  
Profile Connection Space        : XYZ  
Profile Date Time               : 2012:01:25 03:41:57  
Profile File Signature          : acsp  
Primary Platform                : Apple Computer Inc.  
CMM Flags                       : Not Embedded, Independent  
Device Manufacturer             :  
Device Model                    :  
Device Attributes               : Reflective, Glossy, Positive, Color  
Rendering Intent                : Perceptual  
Connection Space Illuminant     : 0.9642 1 0.82491  
Profile Creator                 : Little CMS  
Profile ID                      : 0  
Profile Description             : c2  
Profile Copyright               : IX  
Media White Point               : 0.9642 1 0.82491  
Media Black Point               : 0.01205 0.0125 0.01031  
Red Matrix Column               : 0.43607 0.22249 0.01392  
Green Matrix Column             : 0.38515 0.71687 0.09708  
Blue Matrix Column              : 0.14307 0.06061 0.7141  
Red Tone Reproduction Curve     : (Binary data 64 bytes, use -b option to extract)  
Green Tone Reproduction Curve   : (Binary data 64 bytes, use -b option to extract)  
Blue Tone Reproduction Curve    : (Binary data 64 bytes, use -b option to extract)  
**Comment                         : THIS IS THE HIDDEN FLAG**  
Image Width                     : 640  
Image Height                    : 425  
Encoding Process                : Progressive DCT, Huffman coding  
Bits Per Sample                 : 8  
Color Components                : 3  
Y Cb Cr Sub Sampling            : YCbCr4:2:0 (2 2)  
Image Size                      : 640x425  
Megapixels                      : 0.272

Hidden in the meta-information is a field named ‘Comment’. The value is where the flag can be hidden.

Additional meta-information within files may be useful depending on the challenge.

## xxd

xxd allows you to take a file and dump it in a hexadecimal (hex) format.

Flags may be hidden in the image and can only be revealed by dumping the hex and looking for a specific pattern. Typically, each CTF has its flag format such as ‘HTB{_flag_}’.

**Example 1:  
**You are provided an image named [computer.jpg](https://github.com/mkmety/Medium-Steg-Image/blob/master/computer.jpg).  
Run the following command to dump the file in hex format.

mrkmety@kali:~ $ **xxd computer.jpg  
**00000000: ffd8 ffe0 0010 4a46 4946 0001 0101 0048  ......JFIF.....H  
00000010: 0048 0000 ffe2 021c 4943 435f 5052 4f46  .H......ICC_PROF  
00000020: 494c 4500 0101 0000 020c 6c63 6d73 0210  ILE.......lcms..  
00000030: 0000 6d6e 7472 5247 4220 5859 5a20 07dc  ..mntrRGB XYZ ..  
00000040: 0001 0019 0003 0029 0039 6163 7370 4150  .......).9acspAP  
00000050: 504c 0000 0000 0000 0000 0000 0000 0000  PL..............  
00000060: 0000 0000 0000 0000 0000 0000 f6d6 0001  ................  
00000070: 0000 0000 d32d 6c63 6d73 0000 0000 0000  .....-lcms......  
00000080: 0000 0000 0000 0000 0000 0000 0000 0000  ................  
00000090: 0000 0000 0000 0000 0000 0000 0000 0000  ................  
...  
0008fc30: 8a65 aec6 47fb 1170 cfa1 5c17 ecf5 eab1  .e..G..p..\.....  
0008fc40: eb31 e87f 56d8 4acb 467b 6bec 39ef 67d2  .1..V.J.F{k.9.g.  
0008fc50: 2170 7c56 eb76 67b8 f92e e2f4 8fbc fd0e  !p|V.vg.........  
0008fc60: 7f65 d33c 1945 af53 8efe 3ecc c77c 1707  .e.<.E.S..>..|..  
0008fc70: de5d e5c1 7671 e950 b8bf dab9 ee64 63b8  .]..vq.P.....dc.  
0008fc80: 92a4 6173 cf67 3cf3 eab3 eb16 cb65 7d9c  ..as.g<......e}.  
0008fc90: 0acf 1c3c ed93 064c 6ca8 c76f 1dec eeb6  ...<...Ll..o....  
0008fca0: 542d d084 2ee6 7d5f 9db3 b63e d1ff d954  T-....}_...>...**T**  
0008fcb0: 4849 5320 4953 2041 2048 4944 4445 4e20  **HIS IS A HIDDEN**  
0008fcc0: 464c 4147                                **FLAG**

The output shows “THIS IS A HIDDEN FLAG” at the end of the file. Most challenges won’t be this straight forward or easy. You may have to grep for a pattern, decode data, or look for anything that stands out and can be used to find the flag.

## Strings

The strings command will print out strings that are at least 4 characters long from a file. A flag may be embedded in a file and this command will allow a quick view of the strings within the file.

**Example 1:  
**You are provided an image named [computer.jpg](https://github.com/mkmety/Medium-Steg-Image/blob/master/computer.jpg).  
Run the following command to view the strings in the file.

mrkmety@kali:~ $ **strings computer.jpg  
**JFIF  
ICC_PROFILE  
lcms  
mntrRGB XYZ  
9acspAPPL  
-lcms  
desc  
^cprt  
wtpt  
bkpt  
...  
DlDH  
[gkB  
42_#  
lf{/  
<dXEIl  
"DB?  
.       q|  
+d!m  
!p|V  
**THIS IS A HIDDEN FLAG**

The string “THIS IS A HIDDEN FLAG” is displayed at the end of the file. Flags may be embedded anywhere in the file. You may need to manipulate the output of strings to look for specific details.

> Tip 1: Pipe the strings command to grep to locate specific patterns.
> 
> Tip2: Use the -n flag on the strings command to search for strings that are at least n characters in length. Look at “man strings” for more details.

## Binwalk

Binwalk is a tool that allows you to search binary images for embedded files and executable code. We can use binwalk to search images for embedded files such as flags or files that may contain clues to the flag.

You may need to download binwalk on your system. Run the following command to install binwalk.

mrkmety@kali:~ $ **sudo apt install binwalk -y**

**Example 1:  
**You are provided an image named [dog.jpg](https://github.com/mkmety/Medium-Steg-Image/blob/master/dog.jpg).  
Run the following command to see if Binwalk finds any embedded files.

mrkmety@kali:~ $ **binwalk dog.jpg  
**DECIMAL       HEXADECIMAL     DESCRIPTION  
-------------------------------------------------------------------  
0             0x0             JPEG image data, JFIF standard 1.01  
88221         0x1589D         Zip archive ... name: hidden_text.txt  
88384         0x15940         End of Zip archive, footer length: 22

Binwalk detects a zip file embedded within dog.jpg. The file within the zip file is named hidden_text.txt.

You can extract hidden files by running the following command.

mrkmety@kali:~ $ **binwalk -e dog.jpg**DECIMAL  HEXADECIMAL  DESCRIPTION  
-------------------------------------------------------------------  
0           0x0             JPEG image data, JFIF standard 1.01  
88221       0x1589D         Zip archive data, ... hidden_text.txt  
88384       0x15940         End of Zip archive, footer length: 22

A directory named ‘_dog.jpg.extracted’ has been created with the file automatically unzipped.

mrkmety@kali:~ $ **cd _dog.jpg.extracted/**  
mrkmety@kali:~/_dog.jpg.extracted $ **ls -l**  
total 8  
-rw-r--r-- 1 pi pi 185 Jul  5 19:50 1589D.zip  
-rw-r--r-- 1 pi pi  21 Jul  5 15:39 hidden_text.txt  
mrkmety@kali:~/_dog.jpg.extracted $  
mrkmety@kali~/_dog.jpg.extracted $ **cat hidden_text.txt**  
THIS IS A HIDDEN FLAG

Running the cat command on the embedded text file reveals “THIS IS A HIDDEN FLAG.”