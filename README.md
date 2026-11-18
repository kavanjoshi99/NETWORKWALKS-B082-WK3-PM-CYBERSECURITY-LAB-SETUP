# 🔐 JOHN THE RIPPER & PASSWORD CRACKING TOOLKIT

\<h1 align="center">⚡ PASSWORD CRACKING & DICTIONARY ATTACKS ⚡\</h1>

\<p align="center">   \<img src="[https://img.shields.io/badge/Cybersecurity-Password%20Auditing-red?style=for-the-badge&logo=kalilinux&logoColor=white](https://img.shields.io/badge/Cybersecurity-Password%20Auditing-red?style=for-the-badge\&logo=kalilinux\&logoColor=white)"/>   \<img src="[https://img.shields.io/badge/Tool-John%20The%20Ripper-black?style=for-the-badge](https://img.shields.io/badge/Tool-John%20The%20Ripper-black?style=for-the-badge)"/>   \<img src="[https://img.shields.io/badge/Platform-Kali%20Linux-blue?style=for-the-badge&logo=linux](https://img.shields.io/badge/Platform-Kali%20Linux-blue?style=for-the-badge\&logo=linux)"/>   \<img src="[https://img.shields.io/badge/Focus-Dictionary%20Attacks-purple?style=for-the-badge](https://img.shields.io/badge/Focus-Dictionary%20Attacks-purple?style=for-the-badge)"/> \</p>

\<p align="center">   \<b>Master Password Security | Hash Auditing | Dictionary Attacks | Wordlist Analysis\</b> \</p>

---

## 🧠 ABOUT THE PROJECT

Welcome to the **Password Cracking & Dictionary Attack Toolkit**!

This repository demonstrates practical password security auditing techniques using **John the Ripper** and other dictionary-based password testing methods.

The project explores how weak passwords can be identified through hash analysis, wordlist testing, and password auditing techniques in controlled cybersecurity lab environments.

## 🎯 PROJECT OBJECTIVES

- Understand password hashing and authentication security.
- Learn how John the Ripper works.
- Perform dictionary-based password auditing.
- Understand wordlists and custom password dictionaries.
- Explore different password attack techniques.
- Identify weak passwords and improve password policies.
- Develop practical penetration testing skills.

## 🛠️ TOOLS & TECHNOLOGIES

| Tool                | Purpose                                    |
| ------------------- | ------------------------------------------ |
| 🔥 John the Ripper  | Password hash auditing                     |
| 🐉 Kali Linux       | Security testing environment               |
| 📚 RockYou Wordlist | Dictionary-based password testing          |
| ⚡ Hashcat           | Password hash auditing using CPU/GPU       |
| 🔎 Hash-Identifier  | Hash type identification                   |
| 📝 Crunch           | Custom wordlist generation                 |
| 🧪 Hydra            | Authorized authentication security testing |

## ⚙️ INSTALLATION

### 1. Update Kali Linux

```bash
sudo apt update && sudo apt upgrade -y
```

### 2. Install John the Ripper

```bash
sudo apt install john -y
```

### 3. Install Additional Tools

```bash
sudo apt install hashcat crunch hydra wordlists -y
```

### 4. Verify Installation

```bash
john --version
```

```bash
hashcat --version
```

## 🔑 JOHN THE RIPPER COMMANDS

### 1. Display Help

```bash
john --help
```

### 2. Identify Supported Formats

```bash
john --list=formats
```

### 3. Dictionary Attack

```bash
john --wordlist=/usr/share/wordlists/rockyou.txt hashes.txt
```

### 4. Show Recovered Passwords

```bash
john --show hashes.txt
```

### 5. Show Session Status

```bash
john --status
```

### 6. Incremental Mode

```bash
john --incremental hashes.txt
```

## 📚 WORDLIST MANAGEMENT

Wordlists contain collections of potential passwords used during password security audits.

### Extract RockYou Wordlist

```bash
sudo gzip -dk /usr/share/wordlists/rockyou.txt.gz
```

### View Wordlist Contents

```bash
head /usr/share/wordlists/rockyou.txt
```

### Count Password Entries

```bash
wc -l /usr/share/wordlists/rockyou.txt
```

### Generate a Custom Wordlist

```bash
crunch 4 8 abc123 -o custom_wordlist.txt
```

## ⚡ OTHER PASSWORD AUDITING TECHNIQUES

| Technique          | Description                                          |
| ------------------ | ---------------------------------------------------- |
| Dictionary Attack  | Tests passwords from a wordlist                      |
| Brute Force Attack | Tests possible character combinations                |
| Rule-Based Attack  | Modifies dictionary words using predefined rules     |
| Hybrid Attack      | Combines dictionary words with additional characters |
| Rainbow Table      | Uses precomputed hash lookup tables                  |
| Mask Attack        | Tests passwords matching a specified pattern         |

## 🧪 PRACTICAL LAB WORKFLOW

```text
       PASSWORD SECURITY AUDIT
                  |
                  ▼
          Identify Hash Type
                  |
                  ▼
          Prepare Hash File
                  |
                  ▼
          Select Wordlist
                  |
                  ▼
          Run John the Ripper
                  |
                  ▼
          Analyze Results
                  |
                  ▼
          Document Findings
                  |
                  ▼
          Recommend Strong Passwords
```

## 📂 PROJECT STRUCTURE

```text
Password-Cracking-Toolkit/
│
├── README.md
│
├── Wordlists/
│   ├── rockyou.txt
│   └── custom_wordlist.txt
│
├── Hashes/
│   └── sample_hashes.txt
│
├── Commands/
│   └── john_commands.txt
│
├── Screenshots/
│   └── john_execution.png
│
└── Reports/
    └── password_audit_report.pdf
```

## 🛡️ PASSWORD SECURITY RECOMMENDATIONS

- Use long and unique passwords.
- Avoid common dictionary words.
- Enable Multi-Factor Authentication (MFA).
- Use a trusted password manager.
- Implement secure password hashing algorithms such as Argon2id.
- Use appropriate password salts.
- Monitor authentication failures.
- Regularly conduct authorized password audits.

## 📸 PROJECT SCREENSHOTS

Add your practical screenshots here:

```markdown
![John the Ripper](Screenshots/john_execution.png)
![Dictionary Attack](Screenshots/dictionary_attack.png)
![Password Audit](Screenshots/password_audit.png)
```

## ⚖️ DISCLAIMER

This repository is intended strictly for **educational purposes, cybersecurity training, and authorized password security auditing**.

Only test password hashes and authentication systems that you own or have explicit permission to assess.

Unauthorized password cracking or access to accounts and systems is prohibited.

---

## 👨‍💻 AUTHOR

**Kavan Joshi**

🎓 Bachelor's in Information Technology
🎓 Master's in Cyber Security

**Areas of Interest:**

- Ethical Hacking
- Penetration Testing
- Vulnerability Assessment
- Password Security
- Linux & Kali Linux
- Cybersecurity Research

\<p align="center">
&#x20; \<b>⚡ LEARN • EXPLORE • SECURE • REPEAT ⚡\</b>
\</p>

\<p align="center">
&#x20; ⭐ If you find this repository useful, consider giving it a star!
\</p>
