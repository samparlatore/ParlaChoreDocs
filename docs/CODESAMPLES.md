# ParlaChore code samples

## 🚀 Basic Server Setup
⚠️ This repository is private, so cloning is restricted to authorized collaborators.
```shell
# clone the repo
git clone https://github.com/samparlatore/parlachore.git
cd parlachore

# install dependencies
npm install

# run dev server
npm run dev
```
---
## 🔐 SSL Server Setup
Deployment is streamlined with built‑in scripts that automatically generate PKCS12 keystores and provision secure endpoints for both web and microservices. The process checks for existing keystores to avoid duplication, then creates long‑lived RSA certificates with sensible defaults — meaning you get HTTPS out of the box without manual fiddling. This approach makes spinning up secure servers as simple as running a single script, ensuring encrypted connections and production‑ready trust with minimal effort

```shell
#!/bin/bash
KEYSTORE_PATH="keystore/keystore.p12"

if [ -f "$KEYSTORE_PATH" ]; then
  echo "✅ Keystore already exists at $KEYSTORE_PATH. Skipping generation."
else
  echo "🔐 Generating keystore at $KEYSTORE_PATH..."
  keytool -genkeypair \
    -alias parlachore \
    -keyalg RSA \
    -keysize 2048 \
    -storetype PKCS12 \
    -keystore "$KEYSTORE_PATH" \
         ...
    -dname "CN=localhost, OU=ParlaChore, O=ParlAquatics, L=Western Springs, ST=IL, C=US" \
    -validity 3650
fi
```
---
## 📈 Monitoring & Metrics
I would like to extend the stack with lightweight health checks and metrics endpoints, making it easy to plug into Prometheus or Grafana dashboards. This would provide real‑time visibility into system performance, error rates, and uptime — ensuring that deployments aren’t just secure and themed, but also observable and production‑ready.

---
## 🧩 Overlay Swapper (Frontend)
The Overlay Swapper is a lightweight JavaScript utility that dynamically replaces sections of the DOM with backend‑rendered Thymeleaf fragments. By handling navigation and updates through partial swaps instead of full page reloads, it maintains data obfuscation while delivering a seamless, app‑like user experience. Smooth fade‑in transitions and debug logging ensure both visual polish and developer transparency during content updates.
```jshelllanguage
    logDebug("newContent found:", !!newContent, newContent);
    logDebug("content found in current DOM:", !!content, content);

    if (newContent && content) {
        logDebug("Swapping content...");
        content.classList.remove("fade-in");
        content.innerHTML = newContent.innerHTML;
        requestAnimationFrame(() => {
                content.classList.add("fade-in");
        logDebug("Fade-in reapplied.");
        });
    } else {
        logDebug("Swap skipped: newContent or content missing.");
    }
```
---
## 🌐 Controller Endpoint (Backend)
The Spring controllers provide the backend half of the swapper architecture, serving partial Thymeleaf templates and configuration data for injection into the frontend. The **_NavController_** exposes navigation metadata via a REST endpoint, while the **_PartialController_** securely delivers page fragments for AJAX requests. Together, they enforce allowed‑page rules, populate login forms when needed, and hydrate user state before returning the fragment — ensuring that every partial swap is both secure and context‑aware.
```java
 // --- serves the nav config ---
@RequestMapping("/api/nav")
public class NavController {
    private final ParlaChoreConfigDTO config;

    public NavController(ParlaChoreConfigDTO config) {
        this.config = config;
    }

    @GetMapping
    public Map<String, ParlaChoreConfigDTO.NavItemDTO> getNav() {
        return config.getNavConfig();
    }
}

// --- partials for AJAX swapper ---
@Controller
public class PartialController {
    private final ParlaChoreConfigDTO config;

    public PartialController(ParlaChoreConfigDTO config) {
        this.config = config;
    }

    @GetMapping("/partials/{page}")
    public String partial(@PathVariable String page, Model model, Authentication authentication) {
        if (!config.getAllowedPartialPages().contains(page)) {
            throw new ResponseStatusException(HttpStatus.NOT_FOUND,
                    "Resource " + page + " not configured in allowed pages.");
        }
        if (page.equals("login") && !model.containsAttribute("loginForm")) {
            model.addAttribute("loginForm", AccountSettingsDTO.from(new Account()));
        }
        getSetAndReturnUserState(model, authentication);
        return "partials/" + page;
    }
}
```
---
## 🎨 Theme Loader
The theming system is powered by PostCSS and Webpack, with plugins like autoprefixer, cssnano, and postcss‑preset‑env ensuring modern CSS features, automatic vendor prefixing, and production‑grade optimization. Unused styles are purged at build time for maximum performance.
```yaml
/* Themes.css */
/* Root defaults */
:root {
    --theme-name: "default";
      /* Backgrounds */
    --bg-color: #f0f0f0;
    --bg-image: url('/images/themes/default/backgrounds/default-bg1.png');
    --panel-bg: rgba(248,248,248, .7);
    --modal-bg: rgba(214,214,214, 0.7);
    
      /* Layout */
    --panel-radius: 12px;
    --panel-padding: 2rem;
    --panel-max-width: 720px;
    
      /* Mascot */
    --title-mascot-size: 32px;
    --avatar-mascot-size: 128px;
    --mascot-glow: 0 0 12px var(--accent-color-light);
    --mascot-border: 2px solid var(--accent-color);
}  
```
```yaml
/* Theme: Undersea */
body[data-theme="undersea"] {
    --theme-name: "Undersea";
    --bg-image: url('/images/themes/undersea/backgrounds/undersea-bg1.png');
    --avatar-bg: #b2f0d6;
    --avatar-border: #4db3ff;
    --overlay-blur: blur(10px);
    --accent-color: #4db3ff;
    --accent-color-light: #9ed6ff;
    --overlay-bg: rgba(255, 255, 255, 0.6);
}
```
---
## 🪵 Logging
Logback and SLF4J are used to ensure a configurable, lightweight, dependable logging infrastructure, with this configuration streaming logs to the console and rotating daily log files for structured long‑term analysis.
### 📜 Logback Configuration
```xml
<configuration>
    <!-- Console output for quick debugging -->
    <appender name="STDOUT" class="ch.qos.logback.core.ConsoleAppender">
        <encoder>
            <pattern>%d{yyyy-MM-dd HH:mm:ss.SSS} %-5level [%thread] %logger{36} - %msg%n</pattern>
        </encoder>
    </appender>

    <!-- File output with rotation -->
    <appender name="FILE" class="ch.qos.logback.core.rolling.RollingFileAppender">
        <file>logs/app.log</file>
        <append>true</append>
        <encoder>
            <pattern>%d{yyyy-MM-dd HH:mm:ss.SSS} %-5level [%thread] %logger{36} - %msg%n</pattern>
        </encoder>

        <!-- Rotate daily, keep 30 days of history -->
        <rollingPolicy class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">
            <fileNamePattern>logs/app.%d{yyyy-MM-dd}.log</fileNamePattern>
            <maxHistory>30</maxHistory>
        </rollingPolicy>
    </appender>

    <!-- Root logger -->
    <root level="info">
        <appender-ref ref="STDOUT"/>
        <appender-ref ref="FILE"/>
    </root>
</configuration>
```
### 🗒️ Core Logging Configurations
```yaml
logging:
  level:
    root: DEBUG
    com.parlAquatics.parlaChore: DEBUG

```
## 🛡️ Debug Flags
A centralized set of debug flags provides fine‑grained control over application behavior during development. Each flag toggles a specific aspect of the system — from verbose logging to visual overlays and transition effects — allowing developers to isolate issues without touching production code. This modular approach ensures that debugging remains transparent, configurable, and safe
```jshelllanguage
// config/debug.js
export const DEBUG = {
    logging: true,
    transparentOverlay: true,
    showTransitions: false,
};
```
---
## ⚙️ Dynamic Configuration
The application is driven by a flexible configuration layer that centralizes control over key behaviors. Options range from seeding test users to defining which partial pages are allowed for AJAX swaps, ensuring both developer convenience and runtime safety. Navigation is declaratively managed through visibility rules, where each item specifies its audience — anonymous visitors, logged‑in users, or administrators — all without hard‑coding logic into the frontend or backend. This approach keeps the system adaptable, secure, and easy to extend.
### 🛠️ Application configuration 
```yaml
parlachore:
  seed-test-users: true
  allowed-partial-pages:
    - login
    - price
       ...
    - feedback
    - error
  nav-config: ## Visibility: 1=anonymous 2=logged-in 3=admin 0=not on nav
    items:
      nav1:
        name: Home
        url: /index
        visibility: [1,2,3] #everyone
      nav2:
        name: Login
        url: /login
        visibility: [1] #only anonymous
      nav3:
        name: Register
        url: /register
        visibility: [0] #not on nav - linked from login page
```
### 🌱 Spring & Hibernate Configuration
The application leverages Spring Boot’s declarative configuration to streamline startup and persistence. Core options disable verbose startup logs, define a PostgreSQL datasource, and wire Hibernate through the standard driver. Server settings are centralized, including SSL keystore paths for secure deployments, ensuring that both local development and production environments can be provisioned consistently. This approach keeps infrastructure details transparent, maintainable, and ready for extension.

```yaml
spring:
  main:
    log-startup-info: false
  datasource:
    url:  jdbc:postgresql://postgre.local:5432/parlaChoredb
    driver-class-name: org.postgresql.Driver
    username: sammalammadblamma

server:
  port: 8080
  ssl:
    enabled: false
    key-store: keystore/keystore.p12
    key-store-type: PKCS12
    key-store-alias: parlachore
```


## 🧭 Kotlin Enums
Because Kotlin kicks ass at modeling roles cleanly, the application defines its core permissions as an . Each role — , , , and  — encapsulates its own intent, from account administration to encouragement and tracking. Helper methods (, , etc.) make role checks expressive and type‑safe, eliminating magic strings and keeping business logic readable. This approach ensures that responsibilities are enforced declaratively while keeping the codebase elegant and maintainable.

```java
package com.parlAquatics.parlaChore.kotlin

enum class Role {
    ADMIN,      // AccountAdmin
    APPROVER,   // Can assign and approve chores
    DOER,       // Can be assigned chores
    SUPPORTER;  // Optional — for encouragement, tracking, or emotional presence

    fun isAdmin(): Boolean = this == ADMIN
    fun canApprove(): Boolean = this == APPROVER
    fun canDo(): Boolean = this == DOER
    fun isSupporter(): Boolean = this == SUPPORTER
}
```


# 📦 Lombok & Jackson for DTO Management & Serialization
The configuration layer uses Lombok to eliminate boilerplate and Jackson to handle JSON serialization, keeping DTOs concise, expressive, and production‑ready. Lombok annotations (, , etc.) generate constructors, getters, setters, and equality logic automatically, while Jackson annotations (, ) ensure clean, predictable JSON output. Together, they provide a declarative, maintainable approach to managing configuration objects — reducing manual code and improving readability without sacrificing flexibility.

```java
@Data
@NoArgsConstructor
@AllArgsConstructor
@Builder(toBuilder = true)
@EqualsAndHashCode
@ToString
@JsonInclude(JsonInclude.Include.NON_NULL)
@Component
@ConfigurationProperties(prefix = "parlachore")
public class ParlaChoreConfigDTO implements Serializable {

    @Serial
    private static final long serialVersionUID = 1L;

    /** Allowed partial pages for AJAX swapper */
    @JsonProperty("allowed-partial-pages")
    private List<String> allowedPartialPages;

    /** Map of nav items keyed by identifier */
    @JsonProperty("nav-config")
    private Map<String, NavItemDTO> navConfig;

    @Data
    @NoArgsConstructor
    @AllArgsConstructor
    @Builder(toBuilder = true)
    @EqualsAndHashCode
    @ToString
    @JsonInclude(JsonInclude.Include.NON_NULL)
    public static class NavItemDTO implements Serializable {
        @Serial
        private static final long serialVersionUID = 1L;

        private String name;
        private String url;
        private List<Integer> visibility;

        public boolean isVisibleFor(int state) {
            return visibility != null && visibility.contains(state);
        }
    }
}
```
---



---
## 👥 Author & Links
Created by [Sam Parlatore](https://linkedin.com/in/projectswithsam)  
GitHub: [github.com/samparlatore](https://github.com/samparlatore)
---
