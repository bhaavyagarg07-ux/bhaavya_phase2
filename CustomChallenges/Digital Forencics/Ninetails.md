# 4. NineTails

Description: Looks like I got a little too clever and hid the flag as a password in Firefox, tucked away like one of NineTails’ many tails. Recover the "logins" and the "key4" and let it guide you to the flag. Hint: I named my Ninetails "j4gjesg4", quite a peculiar name isn't it?

## Solution:

- Extracted the rar and got a ad1 file
- opened in a program called `FTK imager`
- I looked for password in firefox folder
- So I went in appdata and local, there I found firefox under mozilla folder but there was no sign of passwords or anything useful under username `j4gjesg4`
- I searched and found they are actually stored in roaming, so I went there and got the db and json file
- A tool called `firepwd` i used
- It ccracked and showed me the output

## Flag:

```
GCTF{m0zarella_f1ref0x_p4ssw0rd}
```

## Concepts learnt:

- Learnt how passwords are unsecurily stored in browsers
