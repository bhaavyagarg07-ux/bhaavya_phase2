# 3. RAR of the Abyss
Two philosophers peer into the networked abyss and swap a secret. Use the secret to decrypt the Abyss’ RAwR and pull your flag from the void.

## Solution
First opened ```abyss.pcap``` file in wireshark. Then scrolled through them and some of them had conversations in them then I found the password in a TCP packet's string  ```b3y0ndG00dand3vil```.
<img width="1815" height="964" alt="Screenshot 2025-12-04 212226" src="https://github.com/user-attachments/assets/6da41930-a9f8-4e27-9b4b-97d58cb5e7a2" />
Found a ```TCP``` packet having some ```RA R ASCII``` text.
<img width="1889" height="518" alt="Screenshot 2025-12-04 211744" src="https://github.com/user-attachments/assets/3f301d84-e05a-420a-920c-cbefff12ea5f" />
Followed that TCP stream and converted the format from ```ASCII``` to ```Raw``` and then saved it as a zipped file.
Then unzipped the zipped file using password- ```b3y0ndG00dand3vil``` using ```WINRAR``` application tool and got the flag.
<img width="1103" height="443" alt="Screenshot 2025-12-04 212057" src="https://github.com/user-attachments/assets/2b125a5f-b345-40c6-aa8a-62fe89023f3d" />

## Flag:
```
nite{thus_sp0k3_th3_n3tw0rk_f0r3ns1cs_4n4lyst}
```
## Notes
- Learned how to analyse ```.pcap``` files using ```WIRESHARK``` tool.

