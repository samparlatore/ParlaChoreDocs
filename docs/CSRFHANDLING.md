# 🔒 CSRF Protection Made Simple

---

Modern browsers and Spring Security enforce CSRF tokens to prevent malicious sites from tricking users into sending unwanted requests. Instead of manually wiring tokens into every AJAX call, this utility wrapper centralizes the logic: it reads the CSRF token and header name injected by Thymeleaf, and automatically attaches them to any state‑changing request (POST, PUT, DELETE, PATCH). Safe methods like GET remain untouched, so your overlay swapper and nav builder stay lightweight while your data‑changing endpoints remain secure. This keeps your dev workflow smooth and your app protected without extra boilerplate.

---


### ✅ Utility wrapper for CSRF‑aware fetch
```js
// parlaChore.js
function getCsrfToken() {
  return document.querySelector('meta[name="_csrf"]').getAttribute('content');
}

function getCsrfHeader() {
  return document.querySelector('meta[name="_csrf_header"]').getAttribute('content');
}

/**
 * Wrapper around fetch that automatically attaches CSRF headers
 * for unsafe methods (POST, PUT, DELETE, PATCH).
 */
async function csrfFetch(url, options = {}) {
  const method = (options.method || 'GET').toUpperCase();
  const headers = options.headers || {};

  // Only attach CSRF for state-changing requests
  if (['POST', 'PUT', 'DELETE', 'PATCH'].includes(method)) {
    headers[getCsrfHeader()] = getCsrfToken();
  }

  return fetch(url, {
    ...options,
    method,
    headers,
    credentials: 'same-origin' // keep cookies/session
  });
}
```

---

### ✅ Using it in your script
```js
document.addEventListener('DOMContentLoaded', async () => {
  if (!window.parlaChoreLoaded) {
    window.parlaChoreLoaded = true;
    const DEBUG = true;
    try {
      // Fetch nav config (GET → no CSRF needed, wrapper handles it anyway)
      const navItems = await csrfFetch('/api/nav', {
        method: 'GET'
      }).then(res => res.json());

      if (DEBUG) console.debug("Nav items:", navItems);

      // Example POST with CSRF auto-attached
      await csrfFetch('/api/tasks', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ name: 'Do the dishes' })
      });
    } catch (err) {
      console.error("Error loading nav:", err);
    }
  }
});
```

---

### 🧪 Sanity check
- **GET requests** → wrapper doesn’t add CSRF, just passes through.
- **POST/PUT/DELETE/PATCH** → wrapper automatically adds the correct header and token from your Thymeleaf‑injected `<meta>` tags.
- **Credentials** → always set to `same-origin` so cookies/session are preserved.

---
