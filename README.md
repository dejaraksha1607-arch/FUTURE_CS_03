# FUTURE_CS_03

# API Security Assessment Report — JSONPlaceholder

> **Internship Project | BE.CSE (Cyber Security)**
> Prepared by: **Dejasini**

---

## 📋 Overview

This repository contains a comprehensive **API Security Assessment Report** conducted on the [JSONPlaceholder](https://jsonplaceholder.typicode.com) public REST API as part of a Cyber Security internship. The assessment follows the **OWASP API Security Top 10 (2023)** framework and was performed using **Postman** as the primary testing tool.

The goal is to identify, analyze, and document common API vulnerabilities — and propose real-world remediation strategies.

---

## 📂 Repository Contents

| File | Description |
|------|-------------|
| `API_Security_Report_Dejasini.docx` | Full professional report (Word format) |
| `README.md` | This file |

---

## 🎯 Target API

| Property | Details |
|----------|---------|
| **API Name** | JSONPlaceholder |
| **Type** | Public Fake REST API |
| **Base URL** | `https://jsonplaceholder.typicode.com` |
| **Authentication** | None |
| **Data Format** | JSON |

---

## 🔍 Endpoints Tested

- `/users` — User profile data including PII
- `/posts` — Blog post entries
- `/comments` — User comments on posts
- `/users/{id}` — Individual user records
- `/posts/{id}` — Individual post records (read/write)

---

## 🚨 Vulnerabilities Found

| # | Vulnerability | OWASP Category | Risk Level |
|---|--------------|----------------|------------|
| 1 | Lack of Authentication | API1:2023 | 🔴 Critical |
| 2 | Broken Authorization | API5:2023 | 🟠 High |
| 3 | Excessive Data Exposure | API3:2023 | 🟠 High |
| 4 | No Rate Limiting | API4:2023 | 🟡 Medium |
| 5 | Weak Input Validation | API8:2023 | 🟡 Medium |

---

## 🛠️ Methodology

The assessment was conducted using a **black-box testing approach**, simulating an external attacker with no prior internal knowledge.

**Phases:**
1. Reconnaissance — Identifying accessible endpoints
2. Endpoint Enumeration — Testing all major API routes
3. Authentication Testing — Verifying access controls
4. Authorization Testing — Attempting cross-user access
5. Data Exposure Analysis — Examining response payloads
6. Rate Limit Testing — Sending repeated automated requests
7. Input Validation Testing — Submitting malformed payloads

**Tools Used:**
- [Postman](https://www.postman.com/) — HTTP request testing
- Browser Developer Tools — Header and response inspection
- Manual analysis — Response review and risk evaluation

---

## 📌 Key Findings Summary

### 🔴 Lack of Authentication
All endpoints are fully accessible without any credentials. A single unauthenticated `GET /users` request returns full PII including names, emails, phone numbers, and geolocation data.

### 🟠 Broken Authorization
Any user can perform `DELETE`, `PUT`, or `PATCH` operations on records belonging to other users. No ownership checks or role validation exists.

### 🟠 Excessive Data Exposure
API responses return full objects including unnecessary sensitive fields. The `/users` endpoint exposes geolocation coordinates, company data, and personal contact information in every response.

### 🟡 No Rate Limiting
Hundreds of consecutive requests can be sent with no throttling, blocking, or HTTP 429 responses — enabling DoS attacks and automated data scraping.

### 🟡 Weak Input Validation
The API accepts malformed input including oversized strings, wrong data types, and HTML/script payloads — returning HTTP 201 Created without any rejection.

---

## ✅ Recommendations

- **Implement JWT / OAuth 2.0** authentication on all endpoints
- **Enforce Role-Based Access Control (RBAC)** to prevent unauthorized resource modification
- **Apply field filtering** — return only necessary data fields per request
- **Implement rate limiting** — enforce per-IP/per-user quotas with HTTP 429 responses
- **Validate all inputs** — use strict JSON schema validation and sanitize string inputs

---

## 📚 References

- [OWASP API Security Top 10 (2023)](https://owasp.org/API-Security/)
- [JSONPlaceholder API](https://jsonplaceholder.typicode.com)
- [Postman Documentation](https://www.postman.com/docs)
- [RFC 7519 — JSON Web Token (JWT)](https://datatracker.ietf.org/doc/html/rfc7519)
- [GDPR — EU Data Protection Regulation](https://gdpr-info.eu)

---

## 👩‍💻 Author

**Dejasini**
BE.CSE — Cyber Security Specialization
Internship Security Assessment Project

---

## ⚠️ Disclaimer

This assessment was conducted solely for **educational and internship purposes**. JSONPlaceholder is an intentionally open public testing API and does not represent a production system. All testing was performed ethically with no intent to exploit or harm any system.

---

*Report Classification: Confidential — Internship Use Only*
