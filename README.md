# PENETRATION TESTING REPORT
## Cryptographic Hash Extraction & Password Cracking
**W3-PM-FINAL | CYBERSECURITY | NETWORKWALKS**

| Field | Detail |
| :--- | :--- |
| **Pentester Name (Cybersecurity Professional)** | Irfan K |
| **Program / Batch** | Networkwalks Cybersecurity Internship[cite: 31] |
| **Date** | 20 November 2026 |
| **Modules Completed** | **W3-PM1:** Password Cracking with JTR (John the Ripper & Johnny)[cite: 32, 55]<br>**W3-PM2:** Password Cracking with Networkwalks Tools[cite: 47, 55] |
| **Target Files** | `My Locked PDF1.pdf` (`W3-PM1`) & `Locked PDF2.pdf` (`W3-PM2`) |
| **Previous Reports** | [Week 1: Cybersecurity Lab Setup](https://github.com/K-Irfan/Cybersecurity-Lab-Setup)<br>[Week 2: Footprinting & Network Scanning Report](https://github.com/K-Irfan) |

---

## 1. Executive Summary
This report documents the technical methodology, cryptographic hash extraction workflows, and password auditing results completed during **Week 3 (Password Cracking & Credential Security)** of the Networkwalks Cybersecurity Internship[cite: 31, 32, 55].

Using both local offline auditing tools (**John the Ripper 1.9.0-jumbo-1** and the **Johnny 2.2** graphical interface)[cite: 33, 35] and browser-based dictionary attack utilities (**Networkwalks Hash Calculator** and **Networkwalks Password Cracker**), encrypted PDF documents were analyzed to extract their `$pdf$` cryptographic hashes and evaluate their resistance against dictionary-based password recovery[cite: 32, 47, 49]. These exercises demonstrate how weak, dictionary-common passwords compromise document encryption within seconds and outline defensive controls to mitigate credential cracking.

---

## 2. W3-PM1: Password Cracking with John the Ripper (JTR) & Johnny
**John the Ripper (`1.9.0-jumbo-1 OMP`)**[cite: 35] and its graphical frontend **Johnny (`v2.2`)**[cite: 33] were configured on Windows to extract and crack the document-open password protecting `My Locked PDF1.pdf`[cite: 32, 33, 36].

### Summary of Technical Workflow & Findings
| Step | Action / Tool | Technical Details & Findings |
| :--- | :--- | :--- |
| **1. Environment Setup** | John the Ripper `1.9.0-jumbo-1` & Johnny `v2.2`[cite: 33] | Installed Johnny GUI and linked it to `john.exe` (`OMP 64-bit x86_64 AVX2`) inside the `john-1.9.0-jumbo-1-win64/run/` directory[cite: 34, 35]. |
| **2. Hash Extraction** | OnlineHashCrack (`pdf2john` engine)[cite: 36] | Uploaded `My Locked PDF1.pdf` to extract the raw PDF encryption hash (`$pdf$4*4*128*-1060*1*16*55d1a5c1...`)[cite: 36, 37] and saved it cleanly to `hash1.txt`[cite: 39]. |
| **3. Dictionary Attack** | Johnny GUI (`Start new attack`)[cite: 41] | Loaded `hash1.txt` into Johnny (`format=PDF`)[cite: 41] and executed a wordlist attack, recovering the plaintext password (`password1`) in seconds[cite: 42]. |
| **4. Verification** | Adobe Acrobat Reader[cite: 43] | Opened `My Locked PDF1.pdf` using the recovered password (`password1`) and captured the embedded 1st Flag verification screen[cite: 43, 44]. |

### Evidence Screenshots (`W3-PM1`)

#### 1. Configuring John the Ripper (`john.exe`) in Johnny Settings[cite: 35]
![John the Ripper Executable Setup](./Outputs/Password%20cracking%20with%20JTR/John%20the%20ripper%20exe.png)[cite: 70]

#### 2. Dictionary Attack Execution & Cracked Password in Johnny[cite: 41, 42]
![Locked PDF Password Cracking](./Outputs/Password%20cracking%20with%20JTR/Locked%20PDF%20password%20cracking.png)[cite: 70]

#### 3. Password Prompt Verification on Target PDF[cite: 43]
![PDF Password Prompt](./Outputs/Password%20cracking%20with%20JTR/Password.png)[cite: 70]

#### 4. Unlocked Target Document (1st Flag Captured)[cite: 44]
![PDF Unlocked Flag](./Outputs/Password%20cracking%20with%20JTR/PDF%20unlocked.png)[cite: 70]

---

## 3. W3-PM2: Password Cracking with Networkwalks Tools
Client-side browser utilities developed by **Networkwalks Academy** (`Hash Calculator` and `Password Cracker`) were used to locally parse an encrypted PDF file, extract its `$pdf$` hash without uploading the document to external servers, and execute a browser-based dictionary attack[cite: 47, 48, 49, 50].

### Summary of Technical Workflow & Findings
| Step | Tool / URL | Technical Details & Findings |
| :--- | :--- | :--- |
| **1. Client-Side Hash Extraction** | [Networkwalks Hash Calculator](https://networkwalks.com/hash-calculator/)[cite: 48] | Parsed `Locked PDF2.pdf` locally in the browser (`PDF` tab) to extract its `pdf2john` / `hashcat`-compatible `$pdf$4*4*128*...` hash string[cite: 49]. |
| **2. Dictionary Attack Execution** | [Networkwalks Password Cracker](https://networkwalks.com/password-cracker/)[cite: 49] | Pasted the extracted `$pdf$` hash into the Dictionary Attack Lab and ran it against the built-in 100-password wordlist (`9 pw/s`), successfully identifying a matching password[cite: 50, 51]. |
| **3. Document Unlock Verification** | PDF Viewer[cite: 51] | Entered the recovered password into the locked PDF prompt to verify full document decryption[cite: 51, 52]. |

### Evidence Screenshots (`W3-PM2`)

#### 1. Extracting the `$pdf$` Hash with Networkwalks Hash Calculator[cite: 49]
![Hash File with Hash Calculator](./Outputs/Password%20cracking%20with%20Networkwalks%20Tools/Hash%20file%20with%20Hash%20Calculator.png)[cite: 70]

#### 2. Dictionary Attack Execution in Networkwalks Password Cracker[cite: 50, 51]
![Password Cracking with Attack Lab](./Outputs/Password%20cracking%20with%20Networkwalks%20Tools/Password%20cracking%20with%20Attack%20Lab.png)[cite: 70]

#### 3. Entering the Cracked Password into the Locked PDF[cite: 51]
![PDF Password Verification](./Outputs/Password%20cracking%20with%20Networkwalks%20Tools/Password.png)[cite: 70]

#### 4. Unlocked PDF Confirmation[cite: 52]
![PDF Unlocked Confirmation](./Outputs/Password%20cracking%20with%20Networkwalks%20Tools/PDF%20unlocked.png)[cite: 70]

---

## 4. Defensive Remediation & Password Hardening Recommendations
To protect encrypted documents, archives, and authentication systems against offline hash extraction and dictionary attacks:

1. **Enforce High-Entropy Passphrases (14+ Characters):** Avoid single dictionary words or predictable substitutions (e.g., `password1`)[cite: 42, 51]. Use randomly generated passwords or 4+ word diceware passphrases combining uppercase, lowercase, digits, and symbols.
2. **Use Strong Encryption Standards (AES-256):** When encrypting sensitive PDFs or archives, enforce **AES-256** encryption (PDF 2.0 / Acrobat X+) rather than legacy RC4 or 128-bit encryption, which allows vastly higher hash-guessing speeds per second on modern hardware.
3. **Eliminate Password Reuse & Implement MFA:** Never reuse document passwords across corporate accounts or portals, and enforce Multi-Factor Authentication (MFA) on all identity providers so compromised credentials cannot be used independently.
