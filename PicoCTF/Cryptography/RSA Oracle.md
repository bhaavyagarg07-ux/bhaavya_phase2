# 1. RSA Oracle

Can you abuse the oracle?
An attacker was able to intercept communications between a bank and a fintech company. They managed to get the message (ciphertext) and the password that was used to encrypt the message.
After some intensive reconassainance they found out that the bank has an oracle that was used to encrypt the password and can be found here nc titan.picoctf.net 60921. Decrypt the password and use it to decrypt the message. The oracle can decrypt anything except the password.

## Solution:
```python
#!/usr/bin/env python3
from pwn import remote

HOST = 'titan.picoctf.net'
PORT = 51864

# The m^e value you gave in the prompt (as an integer)
M_E = 2575135950983117315234568522857995277662113128076071837763492069763989760018604733813265929772245292223046288098298720343542517375538185662305577375746934

def main():
    conn = remote(HOST, PORT)
    try:
        # receive initial messages up to 'decrypt.'
        resp = conn.recvuntil(b'decrypt.')
        print(resp.decode(errors='ignore'))

        # choose to encrypt (send 'E')
        conn.send(b'E\n')

        # read until it asks for keysize
        resp = conn.recvuntil(b'keysize):')
        print(resp.decode(errors='ignore'))

        # We want to encrypt the number 2
        conn.send(b'\x02\n')

        # read until it prints 'ciphertext (m ^ e mod n)'
        conn.recvuntil(b'ciphertext (m ^ e mod n)')
        # next line should be the ciphertext (an integer)
        c_line = conn.recvline().strip()
        print("Received ciphertext line:", c_line.decode(errors='ignore'))

        # parse ciphertext as integer
        c_int = int(c_line)

        # multiply by the known m^e to get (2^e * m^e) = (2*m)^e
        combined = c_int * M_E

        # Now choose to decrypt
        resp = conn.recvuntil(b'decrypt.')
        print(resp.decode(errors='ignore'))
        conn.send(b'D\n')

        # read until prompt for decrypt value
        resp = conn.recvuntil(b'decrypt:')
        print(resp.decode(errors='ignore'))

        # send the combined ciphertext as decimal (the service expects a number)
        conn.send(str(combined).encode() + b'\n')

        # read until it prints 'hex (c ^ d mod n):'
        resp = conn.recvuntil(b'hex (c ^ d mod n):')
        print(resp.decode(errors='ignore'))

        # next line is the hex plaintext (c ^ d mod n)
        hexline = conn.recvline().strip().decode(errors='ignore')
        print("Received hex:", hexline)

        # sanitize hex string: remove leading '0x' if present, whitespace
        if hexline.startswith('0x') or hexline.startswith('0X'):
            hexline = hexline[2:]
        hexline = ''.join(hexline.split())

        # convert hex to int, then divide by 2 (because decrypted is 2*m)
        plaintext_int = int(hexline, 16)
        half = plaintext_int // 2

        # convert back to hex string (without 0x), ensure even length
        hex_half = format(half, 'x')
        if len(hex_half) % 2 == 1:
            hex_half = '0' + hex_half

        # bytes and ascii
        byte_array = bytes.fromhex(hex_half)
        try:
            decoded = byte_array.decode('ascii')
        except UnicodeDecodeError:
            decoded = byte_array.decode('ascii', errors='replace')

        print("\n--- RESULT ---")
        print("Plaintext (int):", half)
        print("Plaintext (hex):", hex_half)
        print("Plaintext (ASCII):")
        print(decoded)

    finally:
        conn.close()
```
<img width="1822" height="679" alt="image" src="https://github.com/user-attachments/assets/5b5feb51-f5ea-45de-8ae9-40b1b108df80" />
<img width="288" height="151" alt="image" src="https://github.com/user-attachments/assets/24354eef-844d-4f8e-895c-7d8aee6b60b9" />


<img width="1080" height="140" alt="image" src="https://github.com/user-attachments/assets/f77f7646-2e3e-4717-82dc-17f9056663ff" />




## Flag:

```
picoCTF{su((3ss_(r@ck1ng_r3@_24bcbc66}
```
## Notes
used plaintext attack



