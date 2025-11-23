# 🔐 ParlaChore Security

This document outlines the **account security model, authentication flow, and planned enhancements** for ParlaChore.  
It complements the architectural overview in `ARCHITECTURE.md`.

---

## 🛡️ Current Security Practices

### Authentication & Authorization
- **Spring Security** configured via `SecurityConfig.java`.
- **Role-based access control**:
    - `PARENT` and `CHILD` roles defined in `Role.kt`.
    - Controllers enforce role checks for sensitive endpoints.
- **Hashed Credentials**:
    - Passwords stored using industry-standard hashing algorithms.
    - Login attempts tracked via `LoginAttemptService`.

### Account Lifecycle
- **Registration**:
    - `RegistrationFormDTO` validates input.
    - Email verification required (`/verify-email` endpoint).
- **Login/Logout**:
    - Custom handlers (`CustomAuthenticationSuccessHandler`, `CustomAuthenticationFailureHandler`) manage session flow.
- **Error Handling**:
    - `GlobalErrorHandler` ensures consistent responses without leaking sensitive details.

### Input & Data Protection
- **HtmlSanitizer** prevents XSS in user-submitted content.
- **TokenUtils** generates secure tokens for session and verification flows.
- **IPUtils** supports rate-limiting and suspicious activity detection.

---

## 🔒 Planned Enhancements

### Account Security
- **Invite Tokens**:
    - Parents can invite other parents to join ParlaChore via secure, expiring tokens.
- **Parent Sign-Off**:
    - Child accounts require parental approval before activation.
- **Audit Logging**:
    - Detailed logs of account changes and security events.

### Authentication Improvements
- **Multi-Factor Authentication (MFA)**:
    - Optional MFA for parent accounts.
- **PIN Validation**:
    - `validatePin` and `updatePin` endpoints already scaffolded in `SettingsController`.
    - Planned expansion for stronger secondary authentication.

### Infrastructure
- **Externalized Config**:
    - Sensitive keys and secrets stored outside codebase (`application.yml`).
- **Container Security**:
    - Docker/Kubernetes deployments hardened with health checks and secret management.

---

## 📌 Notes

- Security is treated as a **first-class concern** in ParlaChore’s design.
- Current implementation balances usability with strong defaults.
- Planned features aim to support **family safety**, **role clarity**, and **scalable enterprise practices**.

---
## 👥 Author & Links
Created by [Sam Parlatore](https://linkedin.com/in/projectswithsam)  
GitHub: [github.com/samparlatore](https://github.com/samparlatore)
---