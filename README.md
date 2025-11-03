# 🛡️ Academy Portal Vulnerability Reports

This repository contains a collection of vulnerability assessments conducted on the **Academy Portal** system.  
Each report provides a detailed breakdown of identified security flaws, including reproduction steps, technical evidence, and recommended mitigations.

---

## 📋 Overview

The vulnerabilities documented here primarily fall under the **OWASP Top 10** categories — focusing on **Broken Access Control**, **Insecure Direct Object References (IDOR)**, and **Session Management** issues.  
Each report aims to improve system resilience and raise awareness about secure backend authorization practices.

---

## 🧾 Vulnerability Summaries

### 1. Broken Access Control — User Data Exposure via Unrestricted API Access
**Classification:** Insecure Direct Object Reference (IDOR) / Missing Server-Side Authorization  
**Summary:**  
An ordinary student account could modify API calls and retrieve sensitive user data (names, emails, phone numbers, IDs, roles) belonging to all registered users.  
This was caused by missing backend authorization checks on API endpoints.  
**Impact:** Major data exposure of personally identifiable information (PII).  

---

### 2. Broken Access Control — Exam Page Reload after Submission
**Classification:** IDOR / Missing State Validation after Exam Submission  
**Summary:**  
After submitting an exam, navigating directly to the exam URL reloaded the exam interface even though it had been submitted.  
Although resubmission was blocked, the system failed to enforce backend state validation on completed exams.  
**Impact:** Unauthorized access to completed exam resources.  

---

### 3. Broken Access Control — Unauthorized Access to Lecture Slides (PDF Download)
**Classification:** IDOR / Missing Server-Side Authorization  
**Summary:**  
Lecture slides embedded as images were backed by an unprotected PDF file URL.  
By inspecting the network requests, the direct PDF URL could be retrieved and downloaded, bypassing frontend restrictions.  
**Impact:** Unauthorized access to internal course materials.  

---

### 4. Broken Access Control — Restricted Resources Accessible During Exams
**Classification:** IDOR / Missing Server-Side Authorization  
**Summary:**  
Certain course materials remained accessible during exam sessions when accessed via saved URLs.  
Additionally, modifying URL identifiers exposed other course documents not intended for the user’s class.  
**Impact:** Circumvention of exam-time content restrictions and unauthorized resource access.  

---

### 5. Broken Authentication & Session Management — Cookie Replay and Session Hijacking
**Classification:** Cookie Replay / Incomplete Session Invalidation  
**Summary:**  
By replacing browser cookies with another student’s active session tokens, an attacker could access that student’s exam results.  
The vulnerability persisted even after the victim logged out, indicating improper session termination handling.  
**Impact:** Full account impersonation risk and unauthorized access to confidential exam results.  

---

### 6. Directory Listing — Unauthorized directory listing
**Classification:** Information Disclosure / Sensitive Data Exposure
**Summary:**  
Directory listing allows attackers to view the contents of web directories that should not be publicly accessible.  
This can reveal sensitive files (e.g., API's configuration files, backups, source code, credentials) and lead to further exploitation.  
**Impact:** Unauthorized directory listing can disclose sensitive files and metadata (including operating system type and version),  
enabling attackers to fingerprint the environment and launch targeted exploits, privilege escalation, or full system compromise.  

## 🧩 Common Root Causes
- Missing server-side authorization checks on API endpoints.  
- Reliance on frontend-only access restrictions.  
- Lack of proper session invalidation upon logout.  
- Inadequate state validation for exam and resource access.
- Misconfiguring the web application

---

## 🔐 Recommendations
- Implement **server-side authorization middleware** to validate user roles and permissions for every endpoint.  
- Enforce **token/session invalidation** on logout or credential changes.  
- Protect **static resource URLs** using signed URLs or backend proxy access.  
- Perform **regular security audits** following the [OWASP ASVS](https://owasp.org/ASVS/) framework.  

---

## 📚 References
- [OWASP Top 10: 2021 – A01: Broken Access Control](https://owasp.org/Top10/A01_2021-Broken_Access_Control/)  
- [OWASP ASVS](https://owasp.org/ASVS/)  
- [OWASP Session Management Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Session_Management_Cheat_Sheet.html)  

---

## 🧑‍💻 Author
**Ali Alawami, Bakr Alrayes, Abdulmajeed Alghamdi**  
Security Researcher | Application Security Enthusiast  

---

## ⚠️ Responsible Disclosure
All findings were responsibly disclosed to the system owners before public publication of these reports.
