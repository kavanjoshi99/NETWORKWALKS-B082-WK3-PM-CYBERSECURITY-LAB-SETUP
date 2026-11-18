Here is an **“awesome” style GitHub README** for John the Ripper, focused on dictionary attacks and other attack modes. It is structured for clarity, quick reference, and practical use—perfect for a dedicated repository or a reference page.

---

# 🔓 John the Ripper Attack Guide

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![John the Ripper](https://img.shields.io/badge/John%20the%20Ripper-Jumbo-blueviolet)](https://github.com/openwall/john)
[![License: GPL v2](https://img.shields.io/badge/License-GPL%20v2-blue.svg)](https://www.gnu.org/licenses/old-licenses/gpl-2.0.en.html)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](https://github.com/openwall/john/blob/bleeding-jumbo/CONTRIBUTING.md)

> A curated, practical guide to **John the Ripper (JtR)** — the legendary open‑source password cracker.  
> This README focuses on **dictionary (wordlist) attacks**, **rule‑based mangling**, and **other powerful attack modes** such as single crack, incremental, mask, PRINCE, and external.  
> **Use only on systems you own or have explicit permission to test.** ⚠️

---

## 📖 Table of Contents

- [What is John the Ripper?](#-what-is-john-the-ripper)
- [Attack Modes at a Glance](#-attack-modes-at-a-glance)
- [Dictionary (Wordlist) Attack](#-dictionary-wordlist-attack)
- [Rule‑Based Mangling (Level Up Your Wordlist)](#-rule-based-mangling-level-up-your-wordlist)
- [Single Crack Mode](#-single-crack-mode)
- [Incremental Mode (Brute‑Force)](#-incremental-mode-brute-force)
- [Mask Attack (Pattern‑Based)](#-mask-attack-pattern-based)
- [PRINCE Mode (Word Combinations)](#-prince-mode-word-combinations)
- [Hybrid Attacks](#-hybrid-attacks)
- [External Mode](#-external-mode)
- [Extracting Hashes (\*2john Helpers)](#-extracting-hashes-2john-helpers)
- [Essential Commands Cheat Sheet](#-essential-commands-cheat-sheet)
- [Session Management & Performance](#-session-management--performance)
- [Resources & Further Reading](#-resources--further-reading)
- [Legal & Ethical Notice](#-legal--ethical-notice)

---

## 🧠 What is John the Ripper?

**John the Ripper (JtR)** is a fast, versatile password cracker used to recover weak or stolen passwords. It supports **hundreds of hash and cipher formats** (MD5, bcrypt, SHA*, NTLM, ZIP, Office, PDF, and many more) and runs on Linux, macOS, Windows, and even some FPGAs.

The **“Jumbo”** version is the community‑enhanced build with the widest format support and all modern attack modes. Most penetration testing distributions (Kali, Parrot) ship with Jumbo by default.

**Basic syntax:**

```bash
john [options] <hashfile>
```

---

## ⚔️ Attack Modes at a Glance

| Mode | Flag | Best For |
|------|------|----------|
| **Wordlist (Dictionary)** | `--wordlist=FILE` | Common passwords, leaked wordlists |
| **Wordlist + Rules** | `--wordlist=FILE --rules` | Mutated words (years, leet, symbols) |
| **Single Crack** | `--single` | Using username/gecos info to guess passwords |
| **Incremental** | `--incremental` | Exhaustive brute‑force with smart charset guessing |
| **Mask** | `--mask=MASK` | Known patterns (e.g., `?u?l?l?l?d?d?d?d`) |
| **PRINCE** | `--prince=FILE` | Combining words into passphrases |
| **Hybrid** | `--wordlist=FILE --mask=MASK` | Wordlist + pattern (e.g., base word + year) |
| **External** | `--external=MODE` | Custom C‑like cracking logic |

John can also **auto‑select** modes: by default it tries **single**, then **wordlist**, then **incremental**.

---

## 📖 Dictionary (Wordlist) Attack

The **most common and efficient** attack. Supply a text file with one candidate password per line.

```bash
john --wordlist=/usr/share/wordlists/rockyou.txt hashes.txt
```

**Specify the hash format** when auto‑detection is uncertain:

```bash
john --format=raw-md5 --wordlist=rockyou.txt md5_hashes.txt
john --format=nt --wordlist=rockyou.txt ntlm_hashes.txt
```

**List all supported formats:**

```bash
john --list=formats
```

Popular formats include `raw-md5`, `raw-sha256`, `sha512crypt`, `bcrypt`, `nt` (NTLM), `zip`, `office`, `pdf`.

---

## 🧬 Rule‑Based Mangling (Level Up Your Wordlist)

Rules transform each wordlist entry **on‑the‑fly** without modifying the file.  
This is where John’s power truly shines.

### Using built‑in rule sets

```bash
john --wordlist=rockyou.txt --rules hashes.txt
```

### Using a custom rule section from `john.conf`

```bash
john --wordlist=wordlist.txt --rules=Custom hash.txt
```

Example `Custom` rule (in `john.conf`):

```ini
[List.Rules:Custom]
# Append four digits (years)
$[0-9]$[0-9]$[0-9]$[0-9]
# Capitalise first letter
c
# Leet speak substitutions
sa@se3si1so0
# Append a symbol
$[!@#$%^&*]
```

**Common rule commands:**

| Command | Effect |
|---------|--------|
| `c` | Capitalise first letter |
| `u` | Uppercase all |
| `l` | Lowercase all |
| `sa@` | Replace `a` with `@` |
| `$1` | Append character `1` |
| `^1` | Prepend character `1` |
| `{` / `}` | Rotate left / right |
| `d` | Duplicate word |

Rules can dramatically expand a small wordlist into millions of candidates.

---

## 👤 Single Crack Mode

Uses **login/username information** (gecos, home directory) and mutates it with rules.  
Very fast and often effective on real system hashes.

```bash
john --single hashes.txt
john --single --format=raw-md5 hash.txt
```

This is usually the **first mode John tries automatically** when no mode is specified.

---

## 🔢 Incremental Mode (Brute‑Force)

Tries **every possible character combination** within a defined charset, but uses statistical models to try likely passwords first.

```bash
john --incremental hashes.txt
john --incremental=Alnum hashes.txt   # alphanumeric only
```

This mode is **exhaustive** and can run indefinitely; use it when other methods fail or for short passwords.

---

## 🎭 Mask Attack (Pattern‑Based)

When you **know the password policy or pattern**, mask mode is far more efficient than brute‑force.

```bash
john --mask='?u?l?l?l?d?d?d?d' hashes.txt
```

**Mask placeholders:**

| Placeholder | Meaning |
|-------------|---------|
| `?l` | lowercase letter |
| `?u` | uppercase letter |
| `?d` | digit |
| `?s` | symbol |
| `?a` | all printable |
| `?w` | word from wordlist (for hybrid) |

Example: `?u?l?l?l?d?d?d?d` matches passwords like `Pass1234`.

---

## 👑 PRINCE Mode (Word Combinations)

PRINCE combines words from a wordlist to form **multi‑word passwords** (passphrases, concatenations).

```bash
john --prince=words.txt hashes.txt
```

It works like wordlist mode but also **joins words together** in a clever order, generating longer candidates.

You can combine PRINCE with rules or mask:

```bash
john --prince=words.txt --rules hashes.txt
john --prince=words.txt --mask='?w?d?d' hashes.txt
```

---

## 🔀 Hybrid Attacks

Combine **wordlist + mask** (or wordlist + rules + mask) to cover patterns that pure wordlists miss.

```bash
john --wordlist=words.txt --mask='?w?d?d?d?d' hashes.txt
```

This tries each word from the list followed by four digits (e.g., `summer2024`).

---

## 🧩 External Mode

Write **custom cracking logic** in a C‑like language inside `john.conf`.  
External modes can filter candidates, implement unique mangling rules, or drive entire attacks.

```bash
john --external=MyMode hashes.txt
```

External modes are defined in the `[List.External:MyMode]` section of `john.conf`.

---

## 🔧 Extracting Hashes (`*2john` Helpers)

John cannot crack a file directly—you must first **extract the hash** into a text file.

| Source | Helper | Example |
|--------|--------|---------|
| Linux `/etc/shadow` | `unshadow` | `unshadow passwd shadow > unshadowed.txt` |
| ZIP archive | `zip2john` | `zip2john secret.zip > zip.hash` |
| PDF document | `pdf2john` | `pdf2john file.pdf > pdf.hash` |
| Office document | `office2john` | `office2john doc.docx > office.hash` |
| SSH private key | `ssh2john` | `ssh2john id_rsa > ssh.hash` |

After extraction, run John on the hash file:

```bash
john --wordlist=rockyou.txt zip.hash
```



---

## 🧾 Essential Commands Cheat Sheet

| Command | Description |
|---------|-------------|
| `john hashes.txt` | Auto‑select mode and crack |
| `john --wordlist=rockyou.txt hashes.txt` | Dictionary attack |
| `john --wordlist=rockyou.txt --rules hashes.txt` | Dictionary + mangling rules |
| `john --single hashes.txt` | Single crack mode |
| `john --incremental hashes.txt` | Brute‑force |
| `john --mask='?u?l?l?l?d?d?d?d' hashes.txt` | Mask attack |
| `john --prince=words.txt hashes.txt` | PRINCE mode |
| `john --list=formats` | List supported hash formats |
| `john --show hashes.txt` | Display cracked passwords |
| `john --restore` | Resume an interrupted session |
| `unshadow passwd shadow > unshadowed.txt` | Merge Linux passwd/shadow |
| `zip2john file.zip > zip.hash` | Extract ZIP hash |



---

## ⚙️ Session Management & Performance

- **Sessions** are saved in `$JOHN/john.rec` (default `.john/` directory). Resume with `--restore`.
- **Cracked passwords** are stored in `$JOHN/john.pot`. Use `--show` to retrieve them.
- **Parallelise across CPU cores** with `--fork=N`.
- **Name a session** for easy recovery: `--session=mycrack`.
- **Adjust max length** with `--max-len=N` (default often 13; PRINCE mode may support up to 24).

```bash
john --wordlist=rockyou.txt --fork=4 --session=attack1 hashes.txt
```

---

## 📚 Resources & Further Reading

- **[Openwall John the Ripper (Jumbo) – Official Repository](https://github.com/openwall/john)** – source code, documentation, and issue tracker.
- **[John the Ripper Documentation (Openwall Wiki)](https://openwall.info/wiki/john)** – hash formats, options, examples.
- **[n0kovo/awesome-password-cracking](https://github.com/n0kovo/awesome-password-cracking)** – curated list of tools, wordlists, and resources.
- **[lunaaarrr/John-The-Ripper---Cheatsheet-](https://github.com/lunaaarrr/John-The-Ripper---Cheatsheet-)** – community cheat sheet for CTFs and pentesting.
- **[SploitHQ/John-the-Ripper](https://github.com/SploitHQ/John-the-Ripper)** – beginner‑friendly guide with examples.
- **Wordlists:** `rockyou.txt` (Kali: `/usr/share/wordlists/rockyou.txt`), SecLists, and custom generated lists.

---

## ⚖️ Legal & Ethical Notice

> **John the Ripper is a security auditing tool.**  
> Only use it on **systems, hashes, or files you own**, or for which you have **explicit written authorisation** from the owner.  
> Unauthorised password cracking is illegal in most jurisdictions and violates ethical security practices.  
> The authors and contributors of this README assume **no liability** for misuse.

---

**Happy (authorised) cracking!** 🚀  
*Stay ethical, stay curious.*
