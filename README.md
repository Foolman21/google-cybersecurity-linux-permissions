# 🐧 Linux File Permissions & Access Control

> **Project Context:** Google Cybersecurity Professional Certificate

<div align="center">

  ![Google](https://img.shields.io/badge/Google-Cybersecurity-4285F4?style=for-the-badge&logo=google&logoColor=white)
  ![Linux](https://img.shields.io/badge/Linux-Bash-FCC624?style=for-the-badge&logo=linux&logoColor=black)
  ![Permissions](https://img.shields.io/badge/Access-Control-00BFFF?style=for-the-badge&logo=securityscorecard&logoColor=white)
  ![Shell](https://img.shields.io/badge/Shell-Scripting-4EAA25?style=for-the-badge&logo=gnu-bash&logoColor=white)

</div>

---

## 📄 Project Overview

**Scenario:** As a security professional working with a research team, I was tasked with auditing and updating file permissions within the `projects` directory. The existing permissions did not reflect the appropriate level of authorization required by the organization. 

Checking and updating these permissions was essential to maintain the security of the system. This repository documents the **technical analysis** and **remediation** performed to ensure that only authorized users have access to sensitive research data.

---

## 🔍 Technical Implementation

Detailed breakdown of the auditing process and the specific authorization changes implemented in the Linux environment.

### 1. 📋 System Audit & Inspection

* **Task:** Identify existing permissions and locate hidden files within the project environment.
* **🛠️ Analysis:** Used the `ls` command with the `-la` option to display a detailed listing of all files, including hidden ones.
* **🔑 Key Findings:** The directory contains one directory named `drafts`, one hidden file named `.project_x.txt`, and five other project files.
* **⚠️ Risk Identified:** The initial audit showed that certain files allowed "others" to have write access, which violated internal security policies.

### 2. 🔐 Deconstructing the Permission String

The 10-character string represents the permissions set on each file or directory. Understanding this structure is vital for precise access control.

| Character Position | Represents | Description |
| :--- | :--- | :--- |
| **1st** | **File Type** | `d` for directory, hyphen `-` for regular file. |
| **2nd - 4th** | **User** | Read (`r`), write (`w`), and execute (`x`) for the owner. |
| **5th - 7th** | **Group** | Read (`r`), write (`w`), and execute (`x`) for the group. |
| **8th - 10th** | **Others** | Permissions for all other users apart from the user and group. |

### 3. 🛠️ Permission Hardening Tasks

I used the `chmod` command to modify permissions to match the organization's requirements and enforce the Principle of Least Privilege.

| Target | Security Requirement | Linux Command |
| :--- | :--- | :--- |
| **Standard Files** | Remove write access for "others" from `project_k.txt`. | `chmod o-w project_k.txt` |
| **Hidden Files** | Remove user/group write access and add group read access to `.project_x.txt`. | `chmod u-w,g=r .project_x.txt` |
| **Directories** | Restrict the `drafts` directory so only the `researcher2` user has execute permissions. | `chmod g-x drafts` |

---

## 🛡️ Security Principles Applied

The following core security practices were applied to the file system:

* **🔎 Audit & Identification:** Conducted a baseline audit using `ls -la` to check the current directory state against the required security posture.
* **🛡️ Least Privilege:** Removed unnecessary write and execute permissions from groups and others to minimize the attack surface.
* **📁 Archive Integrity:** Specifically secured archived hidden files by removing write permissions, preventing accidental or malicious modification.

---

## 🚀 Key Takeaways

* **🛡️ Hidden File Visibility:** Using the `-a` flag is critical, as hidden files (starting with a period) often contain sensitive configurations or archived data that are easily overlooked.
* **🔑 Granular Control:** The `chmod` command allows for precise control by targeting specific owner types (user, group, or others), which is essential for collaborative environments.
* **📏 Policy Alignment:** Regular auditing of permission strings ensures that actual system access matches organizational authorization policies, maintaining compliance.

---

<div align="center">
  <sub><i>Disclaimer: This is a fictional case study completed for educational purposes as part of the Google Cybersecurity Certificate.</i></sub>
</div>
