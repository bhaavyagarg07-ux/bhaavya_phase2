# 1. Challenge name

Can you get sense of this code file and write the function that will decode the given encrypted file content.
Find the encrypted file here flag_info and code file might be good to analyze and get the flag.

## Solution:
in this we had to make a program with reverses the operation and gets us the flag

```python
def generator(g, x, p):
    return pow(g, x, p)

def is_prime(p):
    if p < 2:
        return False
    for i in range(2, int(p ** 0.5) + 1):
        if p % i == 0:
            return False
    return True

def dynamic_xor_decrypt(cipher_text, text_key):
    plain_text = ""
    key_length = len(text_key)
    for i, char in enumerate(cipher_text):
        key_char = text_key[i % key_length]
        decrypted_char = chr(ord(char) ^ ord(key_char))
        plain_text += decrypted_char
    # Encryption reversed plaintext before XOR — so we reverse again here
    return plain_text[::-1]

def decrypt(cipher, shared_key, text_key):
    xor_text = ""
    for num in cipher:
        if num == 0:
            xor_text += "\x00"
        else:
            xor_text += chr(int(num / (shared_key * 311)))
    return dynamic_xor_decrypt(xor_text, text_key)

# --- Example values from your encryption ---
p = 97
g = 31
a = 88
b = 26
cipher = [97965, 185045, 740180, 946995, 1012305, 21770, 827260, 751065,
           718410, 457170, 0, 903455, 228585, 54425, 740180, 0, 239470,
           936110, 10885, 674870, 261240, 293895, 65310, 65310, 185045,
           65310, 283010, 555135, 348320, 533365, 283010, 76195, 130620,
           185045]

# --- Recompute shared key ---
u = generator(g, a, p)
v = generator(g, b, p)
key = generator(v, a, p)
b_key = generator(u, b, p)

if key != b_key:
    print("Invalid key")
else:
    shared_key = key
    plaintext = decrypt(cipher, shared_key, "trudeau")
    print("Decrypted plaintext:", repr(plaintext))

```

## Flag:

```
picoCTF{custom_d2cr0pt6d_019c831c}
```

## Notes

- still learning python so took help to write the code understood the concept


- Include the resources you've referred to with links. [example hyperlink](https://google.com)
