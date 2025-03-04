# Report write up for GDSC Pack and Ship

## Introduction

In this challenge, we had to bypass a password check in a packed binary to extract the flag.

## Getting started 

### Getting the string data
First ran the command `string` to get the all the string in the file 
so that if password is not encrypted we can get that 
```shell
strings release
```

there is the output that [I got](stringdata.txt) but I did not find the password so i can assumed that it's encrypted.
but got a very good lead for future use that the given binary is packed using `UPX`

```txt
This file is packed with the UPX executable packer http://upx.sf.net
```
### First attempt  Buffer overflow

A buffer overflow occurs when a program writes more data into a buffer than it can hold, leading to memory corruption. This can sometimes be exploited to overwrite function return addresses, change program execution flow, or even achieve arbitrary code execution.
We can check the binary if it is vulnerable to buffer overflow by providing large `password`

``` bash
python3 -c 'print("A" * 100)' | ./release
```
but it did not worked it seams the input function is not vulnerable to buffer or there are other measure to prevent that.

### Second attempt Decompilation of a Binary
Decompilation is the process of converting a compiled binary (machine code) back into a higher-level representation, usually resembling the original source code. This is useful for reverse engineering, security analysis, and debugging.

I tried to decompile the binary by using **`Radare2`**

```shell
r2 -aa release # to open the binary in r2
```

