# 1. GDB Baby step 1

Can you figure out what is in the eax register at the end of the main function? Put your answer in the picoCTF flag format: picoCTF{n} where n is the contents of the eax register in the decimal number base. If the answer was 0x11 your flag would be picoCTF{17}.

## Solution:

i opened the file in gdb online debugger but it didn't work hence i downloaded it in my wsl and ran the file. i checked function info then disassemble the main function using disassemble command with main as the argument in the hint it was given eax and then used print to get the desired decimal number.

```
gdb ./debugger0_a
```
```
(gdb) info functions
Non-debugging symbols:
0x0000000000001000 _init
0x0000000000001030 __ cxa_finalize@plt
0x0000000000001040 _start
0x0000000000001070 deregister_tm_clones
0x00000000000010a0 register_tm_clones
0x00000000000010e0 do_global_dtors_aux
0x0000000000001120 frame_dummy
Ox0000000000001129 main
0x0000000000001140 libc_csu_init
0x00000000000011b0 __ libc_csu_fini
Ox00000000000011b8 _fini
(gdb) disassemble main
Dump of assembler code for function main:
0x0000000000001129 <+0>: endbr64
Ox000000000000112d <+4>: push %rbp

Ox000000000000112e <+5>: mov %rsp,%rbp

Ox0000000000001131 <+8>: mov %edi,-0x4(%rbp)

0x0000000000001134 <+11>: mov %rsi,-0x10(%rbp)

0x0000000000001138 <+15>: mov $0x86342, %eax

0x000000000000113d <+20>: pop %rbp

0x000000000000113e <+21>: ret

End of assembler dump.
(gdb) print eax
No symbol table is loaded. Use the "file" command.
(gdb) print 0x86342
$1 = 549698
(gdb)
```


## Flag:

```
picoCTF{549698}
```

## Concepts learnt:

- learned how a gdb debugger works and its commands like info function disassemblle

## Notes:

- when i used online debugger it said invalid but worked well with wsl. 

