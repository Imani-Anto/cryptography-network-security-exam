# Risk Assessment Report

## 1. Assets, Vulnerabilities, and Consequences
1. **Asset: Student Records Database/Server**
   - **Vulnerability:** Weak staff passwords and guest network access allowed to the server.
   - **Consequence:** Unauthorized access, data breaches, and illegal manipulation of student grades/records.
2. **Asset: File Transfers Between Campuses**
   - **Vulnerability:** Unencrypted file transfer protocols (e.g., FTP, HTTP).
   - **Consequence:** Interception of sensitive data via Man-in-the-Middle (MitM) eavesdropping.
3. **Asset: Network Availability and Infrastructure**
   - **Vulnerability:** Outdated software and unmonitored external traffic attempts.
   - **Consequence:** System exploitation, malware infection, or Denial-of-Service (DoS) attacks.

## 2. Risk Ranking Matrix
| Risk ID | Risk Description | Likelihood | Impact | Overall Rank | Justification |
|---------|------------------|------------|--------|--------------|---------------|
| **R1**  | Unencrypted transfer eavesdropping | High | High | **1 (Highest)** | Active file transfers occur frequently over unencrypted channels, exposing raw data continuously. |
| **R2**  | Guest network access to records | High | Medium | **2** | Guest access presents an easy local vector for unauthorized users to probe and access internal resources. |
| **R3**  | Outdated software exploitation | Medium | High | **3** | Requires specific external exploit payloads, but poses severe system-wide compromise risks. |

## 3. Recommended Controls
- **Control for R1 (Encryption):** Implement end-to-end transport layer security (TLS/SFTP) and symmetric payload encryption (AES-256 / Fernet).
- **Control for R2 (Traffic Filtering):** Implement subnet segmentation and `iptables` firewall rules to drop guest subnet access to the record server.
- **Control for R3 (Patching & ACLs):** Update server software binaries to patched releases and restrict external inbound IP connectivity.
