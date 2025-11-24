## 🔗 Configuration Binding Overview

Spring Boot automatically binds `application.yml` keys under the `parlachore` prefix into the `ParlaChoreConfigDTO` bean. Hyphenated YAML keys map to camelCase Java fields.

### YAML → DTO Mapping

| YAML Key                        | Java Field                  | Type                        | Notes                                                                 |
|---------------------------------|-----------------------------|-----------------------------|-----------------------------------------------------------------------|
| `parlachore.allowed-partial-pages` | `allowedPartialPages`        | `List<String>`              | List of allowed partial templates for AJAX swapper.                   |
| `parlachore.nav-config.items`      | `navConfig`                  | `Map<String, NavItemDTO>`   | Map of navigation items keyed by identifier (`nav1`, `nav2`, …).      |
| `parlachore.nav-config.items.navX.name` | `NavItemDTO.name`          | `String`                    | Display name for the nav item.                                        |
| `parlachore.nav-config.items.navX.url`  | `NavItemDTO.url`           | `String`                    | URL path for the nav item.                                            |
| `parlachore.nav-config.items.navX.visibility` | `NavItemDTO.visibility` | `List<Integer>`             | Visibility codes (e.g. `1=anonymous`, `2=logged-in`, `3=admin`).      |


### Example

```yaml
parlachore:
  allowed-partial-pages:
    - login
    - logout
    - price
  nav-config:
    items:
      nav1:
        name: Home
        url: /index
        visibility: [1,2,3]
      nav2:
        name: Login
        url: /login
        visibility: [1]
```

Binds into:

```java
config.getAllowedPartialPages(); // ["login","logout","price"]

config.getNavConfig().get("nav1").getName(); // "Home"
config.getNavConfig().get("nav1").getUrl();  // "/index"
config.getNavConfig().get("nav1").getVisibility(); // [1,2,3]
```

---

### Why this matters
- **Hyphenated YAML keys** (`allowed-partial-pages`) are automatically converted to camelCase (`allowedPartialPages`) by Spring Boot’s relaxed binding rules.
- **One DTO** (`ParlaChoreConfigDTO`) cleanly holds both navigation and partials config.
- **Controllers** can inject the same bean and use whichever part they need.

---


---
## 👥 Author & Links
Created by [Sam Parlatore](https://linkedin.com/in/projectswithsam)  
GitHub: [github.com/samparlatore](https://github.com/samparlatore)
---
