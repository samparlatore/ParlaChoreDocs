
# 🛠 ParlaChore Utilities

This document catalogs the **utility classes and helper functions** that support ParlaChore’s core architecture.  
They provide reusable building blocks for security, logging, and data handling.

---

## 🔧 Utility Classes

### HtmlSanitizer
- **Purpose**: Prevents XSS by sanitizing user-submitted HTML.
- **Usage**: Applied to feedback forms, chore descriptions, and any rich text input.
- **Example**:
  ```java
  String safeHtml = HtmlSanitizer.clean(userInput);
  ```

### TokenUtils
- **Purpose**: Generates and validates secure tokens for sessions, email verification, and invite flows.
- **Usage**: Used in `/verify-email` and planned invite-token features.
- **Example**:
  ```java
  String token = TokenUtils.generate(accountId);
  boolean valid = TokenUtils.validate(token);
  ```

### LogUtils
- **Purpose**: Transparent lifecycle logging for requests, responses, and animations.
- **Usage**: Debug flags toggle visibility; logs written to `/logs/`.
- **Example**:
  ```java
  LogUtils.debug("Overlay swap complete for page: " + pageId);
  ```

### DateTimeUtils
- **Purpose**: Consistent time handling across services.
- **Usage**: Scheduling chores, reward expiration, audit logging.
- **Example**:
  ```java
  LocalDateTime now = DateTimeUtils.nowUtc();
  ```

### IPUtils
- **Purpose**: Detects suspicious activity and supports rate-limiting.
- **Usage**: Login attempt tracking, fraud prevention.
- **Example**:
  ```java
  String ip = IPUtils.getClientIp(request);
  ```

### JsonUtils
- **Purpose**: Simplifies JSON serialization/deserialization.
- **Usage**: API responses, settings payloads.
- **Example**:
  ```java
  String json = JsonUtils.toJson(accountSettings);
  ```

### Timer
- **Purpose**: Lightweight performance measurement.
- **Usage**: Debugging slow endpoints or animations.
- **Example**:
  ```java
  Timer t = new Timer();
  t.start();
  // ... code ...
  t.stopAndLog("ChoreService execution");
  ```

---

## 📌 Notes

- Utilities are designed to be **modular, reusable, and future-proof**.
- They embody the philosophy of building a **toolbox of gems** for maintainability and legitimacy.
- Each utility supports both **technical purity** and **playful UX** by keeping the core codebase lean.

---
## 👥 Author & Links
Created by [Sam Parlatore](https://linkedin.com/in/projectswithsam)  
GitHub: [github.com/samparlatore](https://github.com/samparlatore)
---
