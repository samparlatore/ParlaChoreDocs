![ParlaChore](images/logo.png)

## About ParlaChore
ParlaChore is a family chore and relationship app designed to turn everyday routines into joyful, collaborative experiences. It’s more than a task list — it’s a way for households to share responsibility, celebrate progress, and build small moments of connection that add up to something bigger.

Built with love by Sam and the ParlaPals — a whimsical crew of animated helpers — ParlaChore believes that chores can be playful, and that relationships deserve care. Kids learn intuitive UI conventions, parents stay in control, and families discover that teamwork can sparkle.

Whether you’re navigating the chaos of daily life or trying to reconnect with the people you love, ParlaChore offers gentle nudges, clear roles, and a little magic to make it easier. By turning chores into shared goals, it helps sculpt youngsters into confident, responsible people — and gives families a way to celebrate the everyday wins together.

---
| [📑 Table of contents](/docs/TOC.md)  | [🖼️ Business Plan](/docs/BUSINESSPLAN.md) | [📈 Marketing](/docs/MARKETING.md)   |
|:--------------------------------------|:-------------------------|:-----------------------------|   
| [🧩Code Samples](/docs/CODESAMPLES.md)         | [🌐ParlaChore Intro Screens](/docs/INTROSCREENS.md)      | [🔗YML binding](/docs/YMLBINDING.md) |
| [🐠ParlaChore vs. SPA](/docs/PARLACHORESPA.md) | [🐉ParlaChore content swapping](/docs/CONTENTSWAPPER.md) | [🔐 Security](/docs/SECURITY.md)     |
---


## ❓ Why ParlaChore?

- **Clean, intuitive UI** — Helps younger children learn standard computer/app conventions while keeping older kids frustration‑free with a streamlined flow.
- **Focus on family, not finance** — Rewards are tracked with *ParlaBucks*, a fun, symbolic system. Parents decide how those translate into real‑world recognition (screen time, outings, allowance).
- **Playful engagement** — Mascot‑driven themes, helpful tips, and a constructive feedback system turns chores into shared experiences rather than dull tasks.
- **Technical rigor** — Built with scalable backend architecture, secure account flows, and deployment readiness on AWS/Kubernetes.
- **Portfolio clarity** — Documentation demonstrates system design, security awareness, and DevOps practices alongside creative UX.

---

### Simple, Clean, Intuitive UI
- Designed to help **younger children** learn typical computer and app conventions in a safe, approachable way.
- A streamlined interface keeps **older children** focused — no clutter, no unnecessary steps.
- The goal: make it easy to log in, mark chores complete, and see rewards without frustration.

### Reward System: ParlaBucks
- ParlaChore uses a **virtual reward system** called *ParlaBucks*.
- ParlaBucks are **not real currency** — they’re a fun, symbolic way for kids to track progress and anticipate rewards.
- Parents decide how ParlaBucks translate into real‑world recognition, whether that’s extra screen time, a family outing, or even allowance.
- This keeps the app focused on **motivation and accountability**, while leaving financial decisions entirely up to families.

---
# ⚙️ Tech Stack & Control Flow

## Tech Stack Overview
- **Backend**
    - Spring Boot controllers expose RESTful endpoints for both **full-page shells** (SEO-friendly) and **AJAX partials** (dynamic overlays).
    - Layered architecture: DTOs, entities, repositories, and services with Lombok for reduced boilerplate.
    - Transparent debug logging and lifecycle checklists for collaborative troubleshooting.
- **Frontend**
    - Overlay swapper architecture with fade-in transitions for playful, emotionally resonant UX.
    - Progressive enhancement ensures crawlability even if JavaScript fails.
    - Utility classes and maintainable JS/CSS patterns keep the codebase future-proof.
- **SEO & Accessibility**
    - Controller mappings ensure crawlers see complete shells.
    - Semantic HTML and ARIA roles for inclusive design.
    - Declarative UI structure supports both human readability and machine parsing.

## 🔄 Request → Response → Swapper → Animation Lifecycle

| Step              | Trigger/Event                  | Backend Response                  | Frontend Action                          | Outcome                          |
|-------------------|--------------------------------|-----------------------------------|------------------------------------------|----------------------------------|
| **1. Initial Load** | Browser requests route         | Full HTML shell (SEO tags, metadata, placeholders) | Render shell, preload assets              | Crawlable, complete page         |
| **2. User Action**  | Click / navigation / overlay   | AJAX request sent to `/partials/` | Overlay swapper listens and intercepts    | Request lifecycle begins         |
| **3. Partial Fetch**| AJAX request received          | Lean fragment (no scaffolding)    | Swapper replaces target overlay           | Content updated dynamically      |
| **4. Transition**   | Fragment injected              | —                                 | Fade-in animation applied                 | Playful, emotionally resonant UX |
| **5. Debug Log**    | Lifecycle events (req/res/render/anim) | Transparent logs written to `/logs/` | Debug flags toggle visibility             | Collaborative troubleshooting    |
| **6. Fallbacks**    | JS disabled or error           | Full shell served                 | Browser displays complete page            | Resilient, SEO-friendly recovery |

---

## 🧱 Architecture & Design

### Domain Modeling
- `Account` entity with secure hashed credentials and verification flow.
- `User` entity with `PARENT` and `CHILD` roles (via `Role` enum).
- Planned: `Chore`, `ChoreTemplate`, `ChoreInstance`, `WeeklySchedule`.

### Config-Driven Setup
- `application.yml` for environment-specific settings.
- Externalized Kafka, DB, and service wiring.

### Secure Account Flow
- Email verification, hashed passwords, role-based access.
- Planned: Invite tokens, parent sign-off, and audit logging.

---

## 🧪 Testing & DevOps
- **Spring Boot Test** — Unit and integration testing.
- **Maven + Surefire Plugin** — Build and test automation.
- **Docker-Ready** — Modular services designed for containerization.
- **Kubernetes-Ready** — Stateless services, external config, and health endpoints planned.

---

## 🎨 Theme Families (Condensed)
ParlaChore supports multiple theme families for playful customization:
- **Classic** (default) — muted blues and grays.
- **Undersea** — aqua, teal, coral.
- **Outer Space** — midnight blue, cosmic purple.
- **Airport, Build Site, Race Track, Stables, Fairy Forest, Dragon Cliffs, Cat’s Den, Dog Pen** — each with unique palettes and mascot-driven backgrounds.

Themes are stored under `/resources/static/images/themes/` with avatars and backgrounds organized by family.

---

## 🏆 Skills Demonstrated

ParlaChore showcases a blend of **technical engineering** and **creative UX design**.  
Key skills highlighted through this project include:

### Backend & Architecture
- **Spring Boot / MVC** — Designed layered architecture with controllers, services, repositories, DTOs, and entities.
- **RESTful API Design** — Exposed endpoints for both full-page shells and AJAX partials.
- **Domain Modeling** — Structured entities (`Account`, `Chore`, `ParlaPal`, `Reward`) with role-based access via enums.

### Security & Reliability
- **Authentication & Authorization** — Role-based access control (`PARENT`, `CHILD`), hashed credentials, email verification.
- **Input Sanitization** — Prevented XSS with `HtmlSanitizer` and secure token flows with `TokenUtils`.
- **Error Handling** — Global error controller and mascot-driven recovery for safe, user-friendly fallback.

### Frontend & UX
- **Progressive Enhancement** — Overlay swapper with fade-in transitions, ensuring crawlability and accessibility.
- **Playful UX Design** — Mascot-driven illustrations, theme families, and emotionally resonant onboarding.
- **Accessibility** — Semantic HTML, ARIA roles, and declarative UI structure.

### DevOps & Deployment
- **AWS Hosting** — Domain served via Route 53, assets via S3 + CloudFront, monitoring with CloudWatch.
- **Containerization** — Docker-ready services, Kubernetes (EKS) readiness with externalized config and health endpoints.
- **CI/CD** — Maven builds, Surefire testing, GitHub Actions/Jenkins pipeline integration.

### Utilities & Tooling
- **Reusable Utility Classes** — `HtmlSanitizer`, `TokenUtils`, `LogUtils`, `DateTimeUtils`, `JsonUtils`.
- **Debugging & Transparency** — Lifecycle logging, debug flags, and developer handoff checklists.
- **Performance Measurement** — Lightweight `Timer` utility for profiling and optimization.

### Creative & Collaborative
- **Theme Families** — Customizable backgrounds and mascots for immersive, family-friendly UX.
- **Documentation** — High-level overview in `README.md` with deeper technical docs (`ARCHITECTURE.md`, `SECURITY.md`, `DEPLOYMENT.md`, `UTILS.md`, `THEMES.md`).
- **Collaboration** — Transparent logging and lifecycle checklists designed for team handoffs.

---
For detailed documentation, see:
- [Architecture](docs/ARCHITECTURE.md)
- [Security](docs/SECURITY.md)
- [Deployment](docs/DEPLOYMENT.md)
- [Themes](docs/THEMES.md)
- [Utilities](docs/UTILS.md)
- [Code Samples](docs/CODESAMPLES.md)
- [YAML Binding](docs/YAMLBINDING.md)
- [Business Plan](docs/BUSINESSPLAN.md)
- [Marketing](docs/MARKETING.md)
- [Roadmap](docs/ROADMAP.md)

---

## 👋 About Me
![ParlaChore](images/samHeadSmall.png)

Hi, I’m **Sam Parlatore** — a versatile backend engineer, systems architect, and creative educator.  
I founded **ParlAquatics LLC** and am now channeling that experience into **ParlaChore**, a family-focused chore and relationship app.

### What I Bring
- **Technical Depth**: Skilled in frontend/backend debugging, progressive enhancement, accessibility, and maintainable JS/CSS patterns.
- **Architectural Clarity**: Experienced in RESTful API design, layered Spring Boot architecture, and pragmatic utility libraries.
- **Creative UX**: Passionate about playful, mascot-driven design that balances technical purity with emotional resonance.
- **Collaborative Mindset**: Transparent logging, lifecycle checklists, and iterative refactoring for team-friendly development.

### Connect With Me
- LinkedIn: [linkedin.com/in/projectswithsam](https://linkedin.com/in/projectswithsam)
- GitHub: [github.com/samparlatore](https://github.com/samparlatore)

---

## 📌 Portfolio Note

This repository is designed to demonstrate **system design, security awareness, deployment readiness, and creative UX thinking**.  
While the codebase remains private, the documentation reflects production-ready practices and résumé-level skills.

---
## 👥 Author & Links
Created by [Sam Parlatore](https://linkedin.com/in/projectswithsam)  
GitHub: [github.com/samparlatore](https://github.com/samparlatore)
---
