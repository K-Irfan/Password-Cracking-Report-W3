# PENETRATION TESTING REPORT
## Cryptographic Hash Extraction & Password Cracking
**W3-PM-FINAL | CYBERSECURITY | NETWORKWALKS**

| Field | Detail |
| :--- | :--- |
| **Pentester Name (Cybersecurity Professional)** | Irfan K |
| **Program / Batch** | Networkwalks Cybersecurity Internship — Batch B084 |
| **Date** | 20 November 2026 |
| **Modules Completed** | **W3-PM1:** Password Cracking with JTR (John the Ripper & Johnny)<br>**W3-PM2:** Password Cracking with Networkwalks Tools |
| **Target Files** | `My Locked PDF1.pdf` (`W3-PM1`) & `Locked PDF2.pdf` (`W3-PM2`) |
| **Previous Reports** | [Week 1: Cybersecurity Lab Setup](https://github.com/K-Irfan/Cybersecurity-Lab-Setup)<br>[Week 2: Footprinting & Network Scanning Report](https://github.com/K-Irfan/NetworkWalks-W2-Pentesting-Report) |

---

## 1. Executive Summary
This report documents the technical methodology, cryptographic hash extraction workflows, and password auditing results completed during **Week 3 (Password Cracking & Credential Security)** of the Networkwalks Cybersecurity Internship (Batch B084).

Using both local offline auditing tools (**John the Ripper 1.9.0-jumbo-1** and the **Johnny 2.2** graphical interface) and browser-based dictionary attack utilities (**Networkwalks Hash Calculator** and **Networkwalks Password Cracker**), encrypted PDF documents were analyzed to extract their `$pdf$` cryptographic hashes and evaluate their resistance against dictionary-based password recovery. These exercises demonstrate how weak, dictionary-common passwords compromise document encryption within seconds and outline defensive controls to mitigate credential cracking.

---

## 2. W3-PM1: Password Cracking with John the Ripper (JTR) & Johnny
**John the Ripper (`1.9.0-jumbo-1 OMP`)** and its graphical frontend **Johnny (`v2.2`)** were configured on Windows to extract and crack the document-open password protecting `My Locked PDF1.pdf`.

### Summary of Technical Workflow & Findings
| Step | Action / Tool | Technical Details & Findings |
| :--- | :--- | :--- |
| **1. Environment Setup** | John the Ripper `1.9.0-jumbo-1` & Johnny `v2.2` | Installed Johnny GUI and linked it to `john.exe` (`OMP 64-bit x86_64 AVX2`) inside the `john-1.9.0-jumbo-1-win64/run/` directory. |
| **2. Hash Extraction** | OnlineHashCrack (`pdf2john` engine) | Uploaded `My Locked PDF1.pdf` to extract the raw PDF encryption hash (`$pdf$4*4*128*-1060*1*16*55d1a5c1...`) and saved it cleanly to `hash1.txt`. |
| **3. Dictionary Attack** | Johnny GUI (`Start new attack`) | Loaded `hash1.txt` into Johnny (`format=PDF`) and executed a wordlist attack, recovering the plaintext password (`password1`) in seconds. |
| **4. Verification** | PDF Viewer | Opened `My Locked PDF1.pdf` using the recovered password (`password1`) and captured the embedded 1st Flag verification screen. |

### Evidence Screenshots (`W3-PM1`)

#### 1. Configuring John the Ripper (`john.exe`) in Johnny Settings
![John the Ripper Executable Setup](./Outputs/Password%20cracking%20with%20JTR/John%20the%20ripper%20exe.png)

#### 2. Dictionary Attack Execution & Cracked Password in Johnny
![Locked PDF Password Cracking](./Outputs/Password%20cracking%20with%20JTR/Locked%20PDF%20password%20cracking.png)

#### 3. Password Prompt Verification on Target PDF
![PDF Password Prompt](./Outputs/Password%20cracking%20with%20JTR/Password.png)

#### 4. Unlocked Target Document (1st Flag Captured)
![PDF Unlocked Flag](./Outputs/Password%20cracking%20with%20JTR/PDF%20unlocked.png)

---

## 3. W3-PM2: Password Cracking with Networkwalks Tools
Client-side browser utilities developed by **Networkwalks Academy** (`Hash Calculator` and `Password Cracker`) were used to locally parse an encrypted PDF file, extract its `$pdf$` hash without uploading the document to external servers, and execute a browser-based dictionary attack.

### Summary of Technical Workflow & Findings
| Step | Tool / URL | Technical Details & Findings |
| :--- | :--- | :--- |
| **1. Client-Side Hash Extraction** | [Networkwalks Hash Calculator](https://networkwalks.com/hash-calculator/) | Parsed `Locked PDF2.pdf` locally in the browser (`PDF` tab) to extract its `pdf2john` / `hashcat`-compatible `$pdf$4*4*128*...` hash string. |
| **2. Dictionary Attack Execution** | [Networkwalks Password Cracker](https://networkwalks.com/password-cracker/) | Pasted the extracted `$pdf$` hash into the Dictionary Attack Lab and ran it against the built-in 100-password wordlist (`9 pw/s`), successfully identifying a matching password. |
| **3. Document Unlock Verification** | PDF Viewer | Entered the recovered password into the locked PDF prompt to verify full document decryption. |

### Evidence Screenshots (`W3-PM2`)

#### 1. Extracting the `$pdf$` Hash with Networkwalks Hash Calculator
![Hash File with Hash Calculator](./Outputs/Password%20cracking%20with%20Networkwalks%20Tools/Hash%20file%20with%20Hash%20Calculator.png)

#### 2. Dictionary Attack Execution in Networkwalks Password Cracker
![Password Cracking with Attack Lab](./Outputs/Password%20cracking%20with%20Networkwalks%20Tools/Password%20cracking%20with%20Attack%20Lab.png)

#### 3. Entering the Cracked Password into the Locked PDF
![PDF Password Verification](./Outputs/Password%20cracking%20with%20Networkwalks%20Tools/Password.png)

#### 4. Unlocked PDF Confirmation
![PDF Unlocked Confirmation](./Outputs/Password%20cracking%20with%20Networkwalks%20Tools/PDF%20unlocked.png)

---

## 4. Defensive Remediation & Password Hardening Recommendations
To protect encrypted documents, archives, and authentication systems against offline hash extraction and dictionary attacks:

1. **Enforce High-Entropy Passphrases (14+ Characters):** Avoid single dictionary words or predictable substitutions (e.g., `password1`). Use randomly generated passwords or 4+ word diceware passphrases combining uppercase, lowercase, digits, and symbols.
2. **Use Strong Encryption Standards (AES-256):** When encrypting sensitive PDFs or archives, enforce **AES-256** encryption (PDF 2.0 / Acrobat X+) rather than legacy RC4 or 128-bit encryption, which allows vastly higher hash-guessing speeds per second on modern hardware.
3. **Eliminate Password Reuse & Implement MFA:** Never reuse document passwords across corporate accounts or portals, and enforce Multi-Factor Authentication (MFA) on all identity providers so compromised credentials cannot be used independently.

---

## Author

* **Irfan K**
* Cybersecurity Intern @ NetworkWalks Academy
