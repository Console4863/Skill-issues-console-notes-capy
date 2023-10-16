#hacking #forensics 
# NAME

_xxd_ - make a hexdump or do the reverse.

# SYNOPSIS

**xxd** -h[elp]  
**xxd** [options] [infile [outfile]]  
**xxd** -r[evert] [options] [infile [outfile]]

# DESCRIPTION

_xxd_ creates a hex dump of a given file or standard input. It can also convert a hex dump back to its original binary form. Like **uuencode**(1) and **uudecode**(1) it allows the transmission of binary data in a ‘mail-safe’ ASCII representation, but has the advantage of decoding to standard output. Moreover, it can be used to perform binary file patching.

# OPTIONS

If no _infile_ is given, standard input is read. If _infile_ is specified as a `**-**’ character, then input is taken from standard input. If no _outfile_ is given (or a `**-**’ character is in its place), results are sent to standard output.

Note that a "lazy" parser is used which does not check for more than the first option letter, unless the option is followed by a parameter. Spaces between a single option letter and its parameter are optional. Parameters to options can be specified in decimal, hexadecimal or octal notation. Thus **-c8**, **-c 8**, **-c 010** and **-cols 8** are all equivalent.

Tag

Description

_-a_ | _-autoskip_

 

toggle autoskip: A single ’*’ replaces nul-lines. Default off.

_-b_ | _-bits_

 

Switch to bits (binary digits) dump, rather than hexdump. This option writes octets as eight digits "1"s and "0"s instead of a normal hexadecimal dump. Each line is preceded by a line number in hexadecimal and followed by an ascii (or ebcdic) representation. The command line switches -r, -p, -i do not work with this mode.

_-c cols_ | _-cols cols_

 

format <_cols_> octets per line. Default 16 (-i: 12, -ps: 30, -b: 6). Max 256.

_-E_ | _-EBCDIC_

 

Change the character encoding in the righthand column from ASCII to EBCDIC. This does not change the hexadecimal representation. The option is meaningless in combinations with -r, -p or -i.

_-g bytes_ | _-groupsize bytes_

 

separate the output of every <_bytes_> bytes (two hex characters or eight bit-digits each) by a whitespace. Specify _-g 0_ to suppress grouping. <_Bytes_> defaults to _2_ in normal mode and _1_ in bits mode. Grouping does not apply to postscript or include style.

_-h_ | _-help_

 

print a summary of available commands and exit. No hex dumping is performed.

_-i_ | _-include_

 

output in C include file style. A complete static array definition is written (named after the input file), unless xxd reads from stdin.

_-l len_ | _-len len_

 

stop after writing <_len_> octets.

_-p_ | _-ps_ | _-postscript_ | _-plain_

 

output in postscript continuous hexdump style. Also known as plain hexdump style.

_-r_ | _-revert_

 

reverse operation: convert (or patch) hexdump into binary. If not writing to stdout, xxd writes into its output file without truncating it. Use the combination _-r -p_ to read plain hexadecimal dumps without line number information and without a particular column layout. Additional Whitespace and line-breaks are allowed anywhere.

_-seek offset_

 

When used after _-r_: revert with <_offset_> added to file positions found in hexdump.

_-s [+][-]seek_

 

start at <_seek_> bytes abs. (or rel.) infile offset. _+_ indicates that the seek is relative to the current stdin file position (meaningless when not reading from stdin). _-_ indicates that the seek should be that many characters from the end of the input (or if combined with _+_: before the current stdin file position). Without -s option, xxd starts at the current file position.

_-u_

use upper case hex letters. Default is lower case.

_-v_ | _-version_

 

show version string.

# CAVEATS

_xxd -r_ has some builtin magic while evaluating line number information. If the output file is seekable, then the linenumbers at the start of each hexdump line may be out of order, lines may be missing, or overlapping. In these cases xxd will lseek(2) to the next position. If the output file is not seekable, only gaps are allowed, which will be filled by null-bytes.

_xxd -r_ never generates parse errors. Garbage is silently skipped.

When editing hexdumps, please note that _xxd -r_ skips everything on the input line after reading enough columns of hexadecimal data (see option -c). This also means, that changes to the printable ascii (or ebcdic) columns are always ignored. Reverting a plain (or postscript) style hexdump with xxd -r -p does not depend on the correct number of columns. Here anything that looks like a pair of hex-digits is interpreted.

Note the difference between  
_% xxd -i file_  
and  
_% xxd -i < file_

_xxd -s +seek_ may be different from _xxd -s seek_, as lseek(2) is used to "rewind" input. A ’+’ makes a difference if the input source is stdin, and if stdin’s file position is not at the start of the file by the time xxd is started and given its input. The following examples may help to clarify (or further confuse!)...

Rewind stdin before reading; needed because the ‘cat’ has already read to the end of stdin.  
_% sh -c "cat > plain_copy; xxd -s 0 > hex_copy" < file_

Hexdump from file position 0x480 (=1024+128) onwards. The ‘+’ sign means "relative to the current position", thus the ‘128’ adds to the 1k where dd left off.  
_% sh -c "dd of=plain_snippet bs=1k count=1; xxd -s +128 > hex_snippet" < file_

Hexdump from file position 0x100 ( = 1024-768) on.  
_% sh -c "dd of=plain_snippet bs=1k count=1; xxd -s +-768 > hex_snippet" < file_

However, this is a rare situation and the use of ‘+’ is rarely needed. The author prefers to monitor the effect of xxd with strace(1) or truss(1), whenever -s is used.

# EXAMPLES

Print everything but the first three lines (hex 0x30 bytes) of **file**.  
_% xxd -s 0x30 file_

Print 3 lines (hex 0x30 bytes) from the end of **file**.  
_% xxd -s -0x30 file_

Print 120 bytes as continuous hexdump with 40 octets per line.  
_% xxd -l 120 -ps -c 20 xxd.1_  
2e54482058584420312022417567757374203139  
39362220224d616e75616c207061676520666f72  
20787864220a2e5c220a2e5c222032317374204d  
617920313939360a2e5c22204d616e2070616765  
20617574686f723a0a2e5c2220202020546f6e79  
204e7567656e74203c746f6e79407363746e7567

Hexdump the first 120 bytes of this man page with 12 octets per line.  
_% xxd -l 120 -c 12 xxd.1_  
0000000: 2e54 4820 5858 4420 3120 2241 .TH XXD 1 "A  
000000c: 7567 7573 7420 3139 3936 2220 ugust 1996"  
0000018: 224d 616e 7561 6c20 7061 6765 "Manual page  
0000024: 2066 6f72 2078 7864 220a 2e5c for xxd"..\  
0000030: 220a 2e5c 2220 3231 7374 204d "..\" 21st M  
000003c: 6179 2031 3939 360a 2e5c 2220 ay 1996..\"  
0000048: 4d61 6e20 7061 6765 2061 7574 Man page aut  
0000054: 686f 723a 0a2e 5c22 2020 2020 hor:..\"  
0000060: 546f 6e79 204e 7567 656e 7420 Tony Nugent  
000006c: 3c74 6f6e 7940 7363 746e 7567 <tony@sctnug

Display just the date from the file xxd.1  
_% xxd -s 0x36 -l 13 -c 13 xxd.1_  
0000036: 3231 7374 204d 6179 2031 3939 36 21st May 1996

Copy **input_file** to **output_file** and prepend 100 bytes of value 0x00.  
_% xxd input_file | xxd -r -s 100 > output_file_

Patch the date in the file xxd.1  
_% echo "0000037: 3574 68" | xxd -r - xxd.1_  
_% xxd -s 0x36 -l 13 -c 13 xxd.1_  
0000036: 3235 7468 204d 6179 2031 3939 36 25th May 1996

Create a 65537 byte file with all bytes 0x00, except for the last one which is ’A’ (hex 0x41).  
_% echo "010000: 41" | xxd -r > file_

Hexdump this file with autoskip.  
_% xxd -a -c 12 file_  
0000000: 0000 0000 0000 0000 0000 0000 ............  
*  
000fffc: 0000 0000 40 ....A

Create a 1 byte file containing a single ’A’ character. The number after ’-r -s’ adds to the linenumbers found in the file; in effect, the leading bytes are suppressed.  
_% echo "010000: 41" | xxd -r -s -0x10000 > file_

Use xxd as a filter within an editor such as **vim(1)** to hexdump a region marked between ‘a’ and ‘z’.  
_:’a,’z!xxd_

Use xxd as a filter within an editor such as **vim(1)** to recover a binary hexdump marked between ‘a’ and ‘z’.  
_:’a,’z!xxd -r_

Use xxd as a filter within an editor such as **vim(1)** to recover one line of a hexdump. Move the cursor over the line and type:  
_!!xxd -r_

Read single characters from a serial line  
_% xxd -c1 < /dev/term/b &_  
_% stty < /dev/term/b -echo -opost -isig -icanon min 1_  
_% echo -n foo > /dev/term/b_

# RETURN VALUES

The following error values are returned:

Tag

Description

0

no errors encountered.

-1

operation not supported ( _xxd -r -i_ still impossible).

1

error while parsing options.

2

problems with input file.

3

problems with output file.

4,5

desired seek position is unreachable.