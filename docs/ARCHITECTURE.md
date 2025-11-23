# 🧱 ParlaChore Architecture

This document provides a deeper look at the **system architecture, control flow, and resource organization** of ParlaChore.  
It complements the high-level overview in `README.md`.

---

## 📂 Project Structure

```
src/main/java/com/parlAquatics/parlaChore
├── ParlaChoreLauncher.java        # Spring Boot entry point
├── component
│   └── DatabaseConduit.java       # Database connection abstraction
├── controller                     # MVC controllers
│   ├── ChoreController.java
│   ├── DashboardController.java
│   ├── LandingController.java
│   └── SettingsController.java
├── dto                            # Data Transfer Objects
│   ├── AccountDTO.java
│   ├── AccountSettingsDTO.java
│   ├── ParlaPalSettingsDTO.java
│   └── RegistrationFormDTO.java
├── entity                         # JPA entities
│   ├── Account.java
│   ├── Chore.java
│   ├── ParlaPal.java
│   └── Reward.java
├── handlers                       # Authentication & error handling
│   ├── CustomAuthenticationFailureHandler.java
│   ├── CustomAuthenticationSuccessHandler.java
│   └── GlobalErrorHandler.java
├── repository                     # Spring Data repositories
│   ├── AccountRepository.java
│   ├── ChoreRepository.java
│   └── ParlaPalRepository.java
├── service                        # Business logic layer
│   ├── AccountService.java
│   ├── ChoreService.java
│   ├── ParlaPalService.java
│   └── ThemeAssetService.java
└── util                           # Utilities & configuration
├── SecurityConfig.java
├── WebConfig.java
└── deepUtil/
├── HtmlSanitizer.java
├── TokenUtils.java
├── LogUtils.java
└── DateTimeUtils.java
```

---

## 🌐 Controller Mappings

### ChoreController
- `POST /api/chores` → `create(Chore)`
- `GET /api/chores` → `getAll()`

### DashboardController
- `GET /dashboard` → `dashboardHome(Model, Account)`

### LandingController
- `GET /index` or `/` → `landing(Model, Authentication)`
- `GET /register` → `register(Model, Authentication)`
- `POST /account/register` → `handleRegister(RegistrationFormDTO, …)`
- `GET /login`, `/logout`, `/error`, `/privacy`, `/feedback`, `/price`, `/terms`, `/lost-password`
- `GET /partials/{page}` → `partial(String, Model, Authentication)`
- `GET /verify-email` → `verifyEmail(Model, Authentication)`
- `GET /account-administration` → `accountAdmin(Model, Authentication)`

### SettingsController
- `GET /settings` → `showSettings(Model, AccountDTO)`
- `POST /settings/api/account` → `updateAccountSettingsJson(AccountSettingsDTO, Account)`
- `GET /settings/api` → `getAccountSettings(Account)`
- `GET /settings/api/parlapals` → `getParlaPals(Account)`
- `POST /settings/api/parlapals` → `createParlaPal(ParlaPalSettingsDTO, Account)`
- `GET /settings/api/parlapal/{id}` → `getParlaPalSettings(Long, Account)`
- `POST /settings/api/parlapal/{id}` → `updateParlaPalSettings(Long, …)`
- `DELETE /settings/api/parlapal/{id}` → `deleteParlaPal(Long, Account)`
- `POST /settings/api/parlapal/{id}/validate-pin` → `validatePin(Long, Map, Account)`
- `POST /settings/api/parlapal/{id}/pin` → `updatePin(Long, Map, Account)`
- `GET /settings/api/theme-assets` → `getThemeAssets()`

---

## 🔄 Control Flow

1. **Initial Request**  
   - Browser requests a route → Spring Boot serves a **full HTML shell** (via Thymeleaf templates).  
   - Includes metadata, SEO tags, and placeholders.

2. **Overlay Swapper**  
   - User interaction triggers AJAX → backend responds with **lean partials** from `/partials/{page}`.  
   - Frontend swapper injects fragment and applies fade-in transitions.

3. **Debug & Logging**  
   - Lifecycle events logged via `LogUtils`.  
   - Debug flags toggle visibility for troubleshooting.

4. **Fallbacks**  
   - If JS fails, full shell still renders.  
   - Error handling uses mascot-driven illustrations.

---

## 🛠 Utilities

- **HtmlSanitizer** → Prevents XSS in user input.  
- **TokenUtils** → Generates and validates secure tokens.  
- **LogUtils** → Transparent lifecycle logging.  
- **DateTimeUtils** → Consistent time handling across services.  
- **SecurityConfig** → Role-based access control, hashed credentials.  
- **WebConfig** → MVC configuration, resource handlers.

---

## 🎨 Resources

- **Static Assets** → `/resources/static/css`, `/resources/static/js`, `/resources/static/images`  
- **Templates** → `/resources/templates` (Thymeleaf shells, partials, fragments)  
- **Themes** → `/resources/static/images/themes/{family}/` (avatars + backgrounds)  
- **Logs** → `/logs/` (developer-only, lifecycle events)  

---

## 📌 Notes

- **Lombok** is used to reduce boilerplate in DTOs and entities.  
- **Kotlin enums** (`ChoreType`, `RewardType`, `Role`) model domain concepts alongside Java classes.  
- **Spring Boot Test + Maven Surefire** provide unit/integration testing.  
- **Docker/Kubernetes readiness**: services are stateless, config externalized via `application.yml`.

---
## 👥 Author & Links
Created by [Sam Parlatore](https://linkedin.com/in/projectswithsam)  
GitHub: [github.com/samparlatore](https://github.com/samparlatore)

---
