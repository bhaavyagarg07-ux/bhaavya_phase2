# 5. Re:Draw

Her screen went black and a strange command window flickered to life, lines of text flashed across before everything went silent. Moments later, the system crashed. By sheer luck, we recovered a memory dump. Note: There are three stages to this challenge and you will find three flags. What we know: just before the crash, a black command window flickered across the screen, something in its output might still be visible if you dig through memory. She was drawing when it happened, and remnants of a painting program linger, which could reveal more if inspected in the right way. Finally, a mysterious archive hides deeper in memory, likely holding the last piece of her work. Hint: Learn up on volatility 2 and its various plugins and what they are used for.

## Solution:

First i downloaded the rar and extracted it, and got `MemoryDump_Lab1.raw` According to the hint I was supposed to use volatility 2 which i downloaded from github
### Part 1 - using cmd
From description we know, before the crash a black command window flashed which means command line
confirnmed it by running pslist got `cmd.exe` It mentioned that we can get command history using consoles command
<img width="1920" height="1200" alt="Screenshot 2025-12-06 183048" src="https://github.com/user-attachments/assets/4b8ecbc6-b840-43c5-82db-d2627537e215" />
Decoding in base 64 decoder got the first flag
### Part 2 - ms paint
The description also mentioned a paint program staying open and being used. We can verify this because mspaint.exe appears in the running processes right before the crash
i used `memdump`
<img width="1714" height="130" alt="Screenshot 2025-12-06 183602" src="https://github.com/user-attachments/assets/5f936cf8-5087-4a02-a3dc-cae68be882d1" />
I renamed the file with .data extension and opened it in GIMP as raw data
Changed offest and dimesnsions and got the next flag
<img width="1048" height="371" alt="Screenshot 2025-12-07 204301" src="https://github.com/user-attachments/assets/5d95c4de-9a1e-4c51-81fa-6725698e2667" />

![WhatsApp Image 2025-12-06 at 19 24 39_4f3b2a31](https://github.com/user-attachments/assets/0e8fea77-9d36-424c-8a7d-3765245aa408)
### Part 3 - using winRAR
<img width="1698" height="169" alt="Screenshot 2025-12-07 203335" src="https://github.com/user-attachments/assets/607a9d1f-8ce6-49d0-8213-eaaef978ad5f" />
I then dumped Important.rar file using 
` ./volatility_2.6_lin64_standalone -f MemoryDump_Lab1.raw --profile=Win7SP1x64 dumpfiles -Q 0x000000003eb0b770 -D ./output`
Then i unrar it it had a locked file flag3.png with a password
I looked into docs again and found `hashdump` which can give me hashes of various accounts
<img width="1669" height="214" alt="Screenshot 2025-12-06 184821" src="https://github.com/user-attachments/assets/9b23fefc-be20-41ce-8dbe-a51010a18dbd" />
<img width="500" height="500" alt="image" src="https://github.com/user-attachments/assets/ba5260c1-7ac6-444e-acc8-f5226412fb70" />


## Flag:

```
flag{th1s_1s_th3_1st_st4g3!!}
flag{G00d_BoY_good_girL}
flag{w3ll_3rd_stage_was_easy}
```
## Notes
- learned to use volitility 
- I didn’t realize that a simple memory dump could give access to the screen, clipboard, and other sensitive data, and that it’s so easy to analyze offline.
- We can see display of any process by simply dumping it and opening it as raw image data in a program such as `GIMP`


