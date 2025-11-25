## 📖 ParlaChore Partial Swapper – Developer Notes

### 🔎 What we built to handle the front end
- **Overlay swapper (`loadPage`)**
    - Fetches a partial HTML fragment (`/partials/*.html`).
    - Parses it, extracts `.overlay-content`, and swaps it into the current DOM with a fade‑in effect.
    - Updates `<title>` and `<meta description>` so SEO and browser context stay correct.
    - Decides which partial to load based on `<meta name="page">` set by the backend.

- **User state handling**
    - Backend success handler returns JSON `{ "userState": N }` and sets a cookie.
    - Frontend updates `<meta name="userState">` and calls `refreshNav()`.
    - Nav ribbon is rebuilt dynamically from `/api/nav` config, showing only items allowed for the current state (1=anonymous, 2=logged‑in, 3=admin).

- **Scoped form listeners**
    - We attach listeners only when a partial is loaded.
    - For login/register flows, we use a **one‑shot handler**: it intercepts the form, submits via `csrfFetch`, consumes JSON, updates state, then removes itself.
    - This avoids duplicate handlers and removes the need for explicit `destroy*` functions.

- **Error partial**
    - If `<meta name="page" content="error">` is set, the swapper loads `/partials/error.html`.
    - That partial uses Thymeleaf `th:switch` to show Timmy’s fun error states (404 lost, 500 guilty, 403 trespass, 401 login, etc.).
    - Provides trace info and a feedback link for debugging.

---

### 🧪 Lifecycle summary
1. **Page scaffold loads** → `initParlaChore()` runs.
2. **Nav config fetched** → `buildNavRibbon()` draws nav based on `userState`.
3. **Page flag read** → `loadPage("/partials/${page}.html")`.
4. **Partial swapped in** → overlay content replaced, fade‑in applied.
5. **Init hook runs** → e.g. `initLoginPartial()` attaches one‑shot listener.
6. **Form submitted** → handler intercepts, calls backend, consumes JSON.
7. **State updated** → `<meta name="userState">` set, `refreshNav()` redraws nav.
8. **Next partial loaded** → e.g. settings or welcome page.
9. **Error case** → if `page=error`, load Timmy error partial instead.

---
