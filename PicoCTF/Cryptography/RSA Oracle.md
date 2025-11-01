# 1. RSA Oracle

Can you abuse the oracle?
An attacker was able to intercept communications between a bank and a fintech company. They managed to get the message (ciphertext) and the password that was used to encrypt the message.
After some intensive reconassainance they found out that the bank has an oracle that was used to encrypt the password and can be found here nc titan.picoctf.net 60921. Decrypt the password and use it to decrypt the message. The oracle can decrypt anything except the password.

## Solution:
```python
from pwn import *

HOST = 'titan.picoctf.net'
PORT = 60921

# connect
io = remote(HOST, PORT)

# receive initial text until the word 'decrypt.' appears
data = io.recvuntil(b'decrypt.')
print(data.decode(errors='replace'))

# send choice 'E' (encrypt) and newline
io.sendline(b'E')

# receive until it asks for keysize
data = io.recvuntil(b'keysize):')
print(data.decode(errors='replace'))

# send the keysize (2) as a line
io.sendline(b'2')

# read until the 'ciphertext (m ^ e mod n)' prompt, then read the ciphertext line
io.recvuntil(b'ciphertext (m ^ e mod n)')
cipherline = io.recvline().strip()
print(b'ciphertext line:', cipherline)

try:
    ciphertext = int(cipherline.decode())
except Exception as e:
    print("Failed to parse ciphertext as int:", e)
    raise

# ---- IMPORTANT: verify the big multiplier below is exactly what you intend ----
MULTIPLIER = int(
    "2575135950983117315234568522857995277662113128076071837763492069763989760018604733813265929772245292223046288098298720343542517375538185662305577375746934"
)
# ------------------------------------------------------------------------------

# compute result (whatever arithmetic you need here)
result = ciphertext * MULTIPLIER

# show what we will send (optional)
print("Computed result (decimal):", result)
```

<img width="1891" height="426" alt="image" src="https://github.com/user-attachments/assets/88fa4469-6777-4732-a412-da8e6909ac09" />




## Flag:

```

```
## Notes
couldnt solve further



