## 🧩 What is an SPA?
**SPA = Single‑Page Application.**  
It’s a web app architecture where:
- The browser loads one HTML “shell” page once.
- Navigation and content changes happen entirely via JavaScript.
- Instead of full page reloads, the app fetches data (usually JSON or fragments) and dynamically updates the DOM.
- Frameworks like React, Angular, Vue are common SPA engines.

---

## 🔎 How ParlaChore's swapper is *similar* to an SPA
- **Partial swapping:** ParlaChore loads fragments (`/partials/*.html`) and replaces `.overlay-content` instead of reloading the whole page. That’s SPA‑like behavior.
- **Dynamic nav:** The page rebuilds the nav ribbon based on `userState` and config JSON — just like an SPA would conditionally render components.
- **AJAX login/register:** ParlaChore intercepts form submissions, sends them via `fetch`, consumes JSON, and updates the DOM without a full reload. That’s classic SPA flow.
- **Error handling:** it swaps in an error partial instead of letting the browser show a raw error page — again, SPA‑style routing.

---

## 🔎 How ParlaChore is *different* from a full SPA
- **Server‑rendered fragments:** Instead of a JS framework rendering components, Thymeleaf‑rendered HTML partials are fetched. That means the server still does the secure templating.
- **No client‑side router:** SPAs usually have a router (e.g. `/settings` → component). ParlaChore uses `loadPage()` with URLs to partials, but not a full routing system.
- **SEO friendliness:** Because the backend still renders HTML with `<title>` and `<meta description>`, search engines can index it more easily than a pure JS SPA.
- **Lightweight:** The page does not have a big framework runtime. It’s just vanilla JS + fetch + DOM swap. That makes it simpler, but also less feature‑rich than React/Vue.
- **Lifecycle management:** In SPAs, components mount/unmount automatically. In this swapper, attaching/detaching listeners is donr manually when partials load/unload.

---

## 🎯 Think of it like this
- **SPA:** Browser loads one skeleton, JS framework renders everything, server only provides JSON.
- **ParlaChore swapper:** Browser loads one scaffold, server provides HTML partials, JS swaps them in and manages state.

It’s a **hybrid**: SPA‑like user experience (no full reloads, dynamic nav, smooth transitions) but with server‑rendered fragments instead of client‑side components.

---

##### 👉 A “mini SPA framework” with vanilla JS and Thymeleaf. It’s lighter, easier to debug, and still gives the smooth overlay transitions we all want.

---


| 🎯              |            SPA             |                   ParlaChore                    |
|:--------------|:--------------------------:|:-----------------------------------------------:|
| Behavior      |    Full screen updates     |              .overlay-content swap              |
| Data Handling |  JSON API for UI and Data  |        Mix of JSON API and server render        |
| LifeCycle     | Attach persistant handlers | Attach one-shot handlers or persistant handlers |


---

🧩 How to read it
- Behavior:
  - <font color="darkred">SPA</font> → full screen updates driven by a client‑side router.
  - <font color="blue">ParlaChore</font> → swaps only .overlay-content fragments.
- Data Handling:
  - <font color="darkred">SPA</font> → server sends JSON, client renders UI.
  - <font color="blue">ParlaChore</font> → mix of JSON (for nav/state) and server‑rendered Thymeleaf partials.
- Lifecycle:
  - <font color="darkred">SPA</font> → persistent event handlers attached once.
  - <font color="blue">ParlaChore</font> → one‑shot handlers that self‑remove after firing (login/register), or scoped attach/detach for multi‑submit forms.

---
