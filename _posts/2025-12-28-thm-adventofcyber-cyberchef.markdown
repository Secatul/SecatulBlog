---
layout: post
title:  "THM: AdventOfCyber - Cyberchef"
date:   2025-12-28 13:02:02 -0300
categories: cybersecurity tryhackme
---

# URL
[Try this room](https://tryhackme.com/room/encoding-decoding-aoc2025-s1a4z7x0c3)

---

## Concept

- Encoding & Decoding
- Web Challenges
- Client-Side Logic
- Cryptography Basics (Base64, XOR, MD5, ROT)

---

## Method to Solve

This room is divided into multiple levels.
Each level introduces a different encoding or decoding mechanism that must be reversed to retrieve the correct password.

Levels **1 to 4** have one question each.
Levels **5 and 6** are both solved within **Level 5**.

---

## Level 1

**First clue:**
```
QWxsIGhhaWwgS2luZyBNYWxoYXJlIQ==
```

Decoded from Base64:
```
All hail King Malhare!
```

I replied using a Base64-encoded username:
```
Q290dG9uVGFpbA==  → CottonTail
```

The server responded with:
```
Lets go! All hail King Malhare!
```

Inspecting Developer Tools, inside the `level1` logic, I found a response header:

```
X-Magic-Question: What is the password for this level
```

Password (Base64):
```
SWFtc29mbHVmZnk= → Iamsofluffy
```

**Credentials**
```
Username: Q290dG9uVGFpbA==
Password: Iamsofluffy
```

**Q1 — Password**
```
Iamsofluffy
```

---

## Level 2

Username found in Debugger (`App.js`):

```
CarrotHelm
→ Q2Fycm90SGVsbQ==
```

Server hint:
```js
// Double from Base64
```

Password response:
```
SGVyZSBpcyB0aGUgcGFzc3dvcmQ6IFUxaFNkbUpIVWpWaU0xWXdZakpPYjFsWE5XNWFWMnd3U1ZFOVBRPT0=
```

Decoded twice:
```
Itoldyoutochangeit!
```

**Q2 — Password**
```
Itoldyoutochangeit
```

---

## Level 3

Username:
```
LongEars → TG9uZ0VhcnM=
```

Debugger comment:
```js
// Base64 --> XOR (recipeKey)
```

Key from header:
```
X-Recipe-Key: cyberchef
```

Decrypting reveals:
```
BugsBunny
```

**Q3 — Password**
```
BugsBunny
```

---

## Level 4

Username:
```
Lenny → TGVubnk=
```

Server returns MD5 hash:
```
b4c0be7d7e97ab74c13091b76825cf39
```

Cracked:
```
passw0rd1
```

**Q4 — Password**
```
passw0rd1
```

---

## Level 5

Request:
```
Carl, password please.
```

Response:
```
SGVyZSBpcyB0aGUgcGFzc3dvcmQ6IFpUTjRjREI1VDNWd05ETmxUMlV4TlE9PQ==
```

Decoded:
```
ZTN4cDB5T3VwNDNlT2UxNQ==
```

Using recipe ID:

| Recipe ID | Reverse Logic |
|---------|----------------|
| 1 | Base64 → Reverse → ROT13 |
| 2 | Base64 → Hex → Reverse |
| 3 | ROT13 → Base64 → XOR |
| 4 | ROT13 → Base64 → ROT47 |

Final password:
```
51rBr34chBl0ck3r
```

**Q5 — Password**
```
51rBr34chBl0ck3r
```

---

## Level 6 — Flag
```
THM{M3D13V4L_D3C0D3R_4D3P7}
```
