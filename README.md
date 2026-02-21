# Desi Arms — Internal Tools

Private internal toolset for Desi Arms staff. Hosted on GitHub Pages with password protection.

## 🔐 Default Access Code

```
desiarms2025
```

**Change this before deploying!** See "Changing the Password" below.

---

## 🚀 Deployment — GitHub Pages

### 1. Create a new GitHub repository

```bash
# In your terminal / command prompt:
cd path/to/this/folder

git init
git add .
git commit -m "Initial commit - internal tools"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/desi-arms-internal.git
git push -u origin main
```

> Replace `YOUR-USERNAME` with your GitHub username.

### 2. Enable GitHub Pages

1. Go to your repo on GitHub → **Settings** → **Pages**
2. Under **Source**, select **Deploy from a branch**
3. Set branch to `main` and folder to `/ (root)`
4. Click **Save**
5. Your site will be live at: `https://YOUR-USERNAME.github.io/desi-arms-internal/`

### 3. Test it

- Visit the URL above
- Enter the access code
- Verify the pricing page loads with editable prices

---

## 🔑 Changing the Password

The password is stored as a SHA-256 hash (not plaintext). To change it:

1. Open your browser's developer console (F12 → Console)
2. Run this command with your new password:

```javascript
crypto.subtle.digest('SHA-256', new TextEncoder().encode('YOUR_NEW_PASSWORD'))
  .then(b => Array.from(new Uint8Array(b)).map(x => x.toString(16).padStart(2,'0')).join(''))
  .then(console.log)
```

3. Copy the hash output
4. Replace the `PASS_HASH` value in **both** `index.html` and `pricing.html`
5. Commit and push

---

## 📁 File Structure

```
desi-arms-internal/
├── index.html      # Password gate + dashboard
├── pricing.html    # Price list (engraving + cerakote)
└── README.md       # This file
```

---

## 🛠 Features

### Laser Engraving Tab
- **Click-to-edit prices** — click any price, type new value, auto-saves to browser
- Prices persist in localStorage (per-browser, per-device)
- Reset All button to restore market-rate defaults
- Modified prices highlighted in gold

### Cerakote Tab
- Send It Cerakote provider pricing (01/06/2025)
- **Interactive markup slider** (0–100%) with quick presets
- Auto-calculated "Your Price" with profit shown
- Markup preference saved to browser

### Security
- SHA-256 hashed password (not stored in plaintext)
- "Remember this device" option (30-day localStorage token)
- Session-based auth (sessionStorage cleared on browser close)
- Pricing page redirects to login if not authenticated

---

## 🗺 Roadmap

- [ ] **Quote Builder** — select services, auto-total, generate printable quote
- [ ] **Customer Request Integration** — link incoming requests to quote builder
- [ ] **Customer-Facing Estimator** — self-service price configurator
- [ ] **NetSuite / POS Integration** — push quotes to work orders

---

## ✏️ Updating Prices

**Engraving:** Edit directly in the browser (click any price). Or edit `pricing.html` to change defaults.

**Cerakote:** Update the `data-cost` attributes in `pricing.html` when Send It updates their pricing. The markup slider applies on top automatically.

---

## ⚠️ Important Notes

- GitHub Pages sites are **publicly accessible** — the password gate is a deterrent, not enterprise security. Don't store truly sensitive data (SSNs, credit cards, etc.).
- Price edits are stored **per-browser** — if you edit prices on your laptop, they won't appear on your phone. This is by design (different staff can have different quoting discretion).
- The site works offline once loaded — no server or database needed.
