# 🎨 ParlaChore Themes

Our UI ships with a fully modular theming engine: over 40 CSS variables define backgrounds, layout, and mascot styling, all scoped per theme. Each theme overrides only what it needs, while unused styles are automatically purged via PostCSS for lean, lightning‑fast delivery. This approach ensures expressive customization without sacrificing performance — whether you’re swapping palettes, adjusting radii, or giving mascots their own glow, every detail is declarative, reusable, and optimized.


ParlaChore supports multiple **theme families** to make the app playful, customizable, and emotionally resonant.  
Each theme includes background images, mascot avatars, and a suggested color palette.

---

## 🌊 Undersea
- **Backgrounds**: `/images/themes/undersea/backgrounds/undersea-bg1.png` … `undersea-bg4.png`
- **Avatars**: coralGoby.png, mandrinGoby.png, redEye.png, timmy.png
- **Palette**: Aqua, teal, coral, seafoam

## ✈️ Airport
- **Backgrounds**: `/images/themes/airPort/backgrounds/airPort-bg1.png`
- **Avatars**: luggage, sky mascots
- **Palette**: Sky blue, tarmac gray, luggage tan

## 🌌 Outer Space
- **Backgrounds**: outerSpace-bg1.png … outerSpace-bg6.png
- **Avatars**: cosmic mascots
- **Palette**: Midnight blue, starlight white, cosmic purple

## 🏗 Build Site
- **Backgrounds**: buildSite-bg1.png
- **Avatars**: construction mascots
- **Palette**: Safety yellow, concrete gray, orange stripe

## 🏇 Race Track
- **Backgrounds**: raceTrack-bg1.png … raceTrack-bg4.png
- **Avatars**: racing mascots
- **Palette**: Asphalt black, racing red, checkered white

## 🐉 Dragon Cliffs
- **Backgrounds**: dragonCliffs-bg1.png
- **Avatars**: dragon mascots
- **Palette**: Charcoal, ember red, smoky violet

## 🧚 Fairy Forest
- **Backgrounds**: fairyForest-bg1.png
- **Avatars**: fairy mascots
- **Palette**: Lavender, moss green, sparkle pink

## 🐱 Cat’s Den
- **Backgrounds**: catsDen-bg1.png
- **Avatars**: cat mascots
- **Palette**: Cream, tabby orange, cozy gray

## 🐶 Dog Pen
- **Backgrounds**: dogPen-bg1.png
- **Avatars**: dog mascots
- **Palette**: Biscuit beige, leash red, kennel blue

## 🐴 Stables
- **Backgrounds**: stable-bg1.png
- **Avatars**: horse mascots
- **Palette**: Saddle brown, hay gold, forest green

---

## 📌 Notes
- Themes are stored under `/resources/static/images/themes/{family}/`.
- Each theme includes **avatars** (mascots) and **backgrounds** for immersive UX.
- Mascot-driven error handling ties into themes for playful recovery.



---

### ⚙️ Core Frameworks & Libraries
- **PostCSS** → The engine that transforms the CSS. It parses styles into an abstract syntax tree, applies plugins, and outputs optimized CSS.
- **PostCSS Plugins** → Modular add‑ons that do the heavy lifting:
    - `postcss-preset-env` → Allows modern CSS features safely by transpiling them for older browsers.
    - `autoprefixer` → Automatically adds vendor prefixes for cross‑browser compatibility.
    - `cssnano` → Minifies and optimizes CSS for production builds.
    - Utility packs like `postcss-utilities` or `rucksack` can add mixins, shortcuts, and helpers.
- **postcss-loader** → The Webpack bridge that runs PostCSS on the styles during bundling.
- **Webpack** → The bundler that ties everything together, ensuring CSS variables and theme overrides are compiled, purged, and shipped efficiently.

---

### 🖌️ How these technologies benefit the Theme Loader
- **CSS Variables (`--bg-color`, `--accent-color`)** → Declarative theming, scoped per theme.
- **PostCSS Purge** → Removes unused CSS, keeping payloads lean.
- **Webpack + postcss-loader** → Ensures themes are processed at build time, so `themes.css` stays modular but compiles down to fast, production‑ready assets.
- **Plugins like cssnano** → Guarantee that even with 40+ theme variables, the final CSS is compact and performant.

---


---
## 👥 Author & Links
Created by [Sam Parlatore](https://linkedin.com/in/projectswithsam)  
GitHub: [github.com/samparlatore](https://github.com/samparlatore)
---