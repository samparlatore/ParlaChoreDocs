
## 🖼️ ParlaChore Static Assets

### 🎨 Theme Backgrounds

Used behind overlays and dashboard panels.

| Asset Type         | Suggested Size       | Format     | Notes                                      |
|--------------------|----------------------|------------|--------------------------------------------|
| Fullscreen BG      | 1920×1080 or larger  | JPG/PNG    | Use `background-size: cover`; keep lean    |
| Mobile BG (opt.)   | 1080×1920            | JPG/PNG    | Portrait crop for mobile optimization      |
| Placeholder BG     | 1280×720             | JPG        | Neutral gradient or blurred scene          |

---

### 🐠 ParlaPal Avatars

Used in list buttons, switching flows, and preview panels.

| Asset Type         | Suggested Size       | Format     | Notes                                      |
|--------------------|----------------------|------------|--------------------------------------------|
| Standard Avatar    | 256×256              | PNG        | Transparent background preferred           |
| Large Avatar       | 512×512              | PNG        | For preview panel or onboarding splash     |
| Placeholder Avatar | 128×128              | PNG        | Silhouette or shimmer animation            |

---

### 🧩 UI Icons & Decorative Elements

Used in buttons, badges, and overlays.

| Asset Type         | Suggested Size       | Format     | Notes                                      |
|--------------------|----------------------|------------|--------------------------------------------|
| Badge Icons        | 64×64                | PNG/SVG    | Transparent, theme-colored                 |
| Decorative Overlays| 300×300              | PNG        | Optional glow or blur effects              |

---


---


## 🧼 ParlaChore CSS Load Order

This structure ensures clean overrides, modular styling, and scalable theming.

### ✅ Load Order

```html
<link rel="stylesheet" href="/css/base.css">
<link rel="stylesheet" href="/css/themes.css">
<link rel="stylesheet" href="/css/components.css">
<link rel="stylesheet" href="/css/overrides.css">
```
---

## 📦 CSS File Purposes

| File            | Purpose                                                                 |
|-----------------|-------------------------------------------------------------------------|
| `core.css`      | Global defaults: `:root` variables, layout, typography, body styles     |
| `themes.css`    | Theme-specific overrides: `body[data-theme="..."]` variable definitions |
| `settings.css`  | Modular UI styles: `.avatar`, `.modal`, `.panel`, etc. using `var()`    |
| `overrides.css` | Last-resort tweaks: layout fixes, media queries, or user-specific hacks |

---
| Section                      | Suggested File     | Notes                                       |
|------------------------------|--------------------|---------------------------------------------|
| Global layout & typography   | `base.css`         | Body, main, attribution, alerts, forms      |
| Reusable UI components       | `base.css`         | Buttons, overlays, scroll-box               |
| Animated mascot styles       | `components.css`   | Mascot class and keyframes                  |
| Theme-specific patches       | `overrides.css`    | Only if needed for layout fixes             |
---

| Section                          | Suggested File     | Notes                                           |
|----------------------------------|--------------------|-------------------------------------------------|
| Layout, forms, modals, avatars   | `base.css`         | Core UI components used across all themes       |
| Mascot styles & animations       | `components.css`   | Timmy-specific positioning and hover effects     |
| Theme-specific patches           | `overrides.css`    | Only if needed for layout or media query tweaks |

---

| Section                          | Suggested File     | Notes                                           |
|----------------------------------|--------------------|-------------------------------------------------|
| Global layout & typography       | `base.css`         | Body, main, attribution, alerts, forms          |
| Reusable UI components           | `base.css`         | Buttons, overlays, modals, scroll-box           |
| ParlaPal dashboard & avatars     | `components.css`   | List panels, preview panels, avatars, badges    |
| Theme-specific patches           | `overrides.css`    | Reserved for layout fixes or media queries      |
---


## 👥 Author & Links
Created by [Sam Parlatore](https://linkedin.com/in/projectswithsam)  
GitHub: [github.com/samparlatore](https://github.com/samparlatore)

---
