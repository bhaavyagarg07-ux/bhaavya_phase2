# Nutrela Chunks
One of my favorite foods is soya chunks. But as I was enjoying some Nutrela today, I noticed a few chunks weren’t quite right. Seems like something’s off with their structure. Could you help me fix these broken chunks so I can enjoy my meal again?


## solution
I opened corrupted PNG File in the hex editor and then checked for correct PNG hexdump and realised that hexdump for the given PNG file was wrong. Corrected it by editing ```png to PNG``` , ```ihdr to IHDR``` , ```idat to IDAT``` by replacing with correct hexdump.
<img width="1755" height="1019" alt="image" src="https://github.com/user-attachments/assets/b0d9dddd-8ba0-4039-b7a5-74233730639b" />
<img width="1677" height="948" alt="image" src="https://github.com/user-attachments/assets/b1a84ccc-c86e-4918-b000-51b7943f06d6" />
<img width="1000" height="1000" alt="jdcniwrjijwhigr" src="https://github.com/user-attachments/assets/8828b8e5-ab60-4049-9dc9-88de63ffee79" />

## FLag:
```
nite{n0w_y0u_kn0w_ab0ut_PNG_chunk5}
```
## Notes
learned more about hexdump and how to correct it

