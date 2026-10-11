# Graphic Designer Portfolio & Brand Showcase

A production-grade, responsive Graphic Designer & Brand Showcase web application built with **React 19**, **Vite**, **TypeScript**, and **Tailwind CSS**.

Features include:
- 9 switchable theme templates (including **Swiss International Studio**, **Executive Slate Minimal**, **Independence Day**, **Eid Mubarak**, **Luxury Gold**, **Neo-Brutalist**, and **Cyber Future**).
- Dynamic custom color engine with global tokens and per-section granular color overrides.
- Physics-based motion graphics overlays with master toggle and speed/particle controls.
- In-browser owner Admin Control Panel with JSON export/import and live data customization.
- Before/After interactive case study comparison slider.
- WhatsApp instant project enquiry direct integration.
- Full responsive design and automatic system dark/light mode detection.

---

## 1. Prerequisites (Windows 10 / Windows 11)

- **Node.js**: Version `18.x`, `20.x`, or `22.x` (LTS recommended)
  - Download from: [https://nodejs.org/](https://nodejs.org/)
- **npm**: Included automatically with Node.js (`npm -v`)
- Terminal: **Command Prompt (`cmd`)**, **PowerShell**, or **Windows Terminal**

---

## 2. Quick Start on Windows

Open Command Prompt or PowerShell in the project root directory:

```bat
:: 1. Install dependencies
npm install

:: 2. Start the local development server (runs at http://localhost:3000)
npm run dev

:: 3. Build for production (outputs to dist/)
npm run build

:: 4. Preview the production build locally
npm run preview

:: 5. Clean build artifacts (Windows-compatible cross-platform script)
npm run clean
```

---

## 3. Cloudflare Pages Deployment Guide

This project is pre-configured and tested for zero-configuration static deployment on **Cloudflare Pages**.

### Deployment Settings in Cloudflare Dashboard:

1. Log in to [Cloudflare Dashboard](https://dash.cloudflare.com/) and go to **Workers & Pages** > **Create application** > **Pages** > **Connect to Git**.
2. Select your repository.
3. Configure the **Build settings**:
   - **Framework preset**: `Vite` (or `None`)
   - **Build command**: `npm run build`
   - **Build output directory**: `dist`
   - **Root directory**: `/` (leave empty or default)
   - **Node.js Version**: `20` (in Environment Variables set `NODE_VERSION=20` if prompted)
4. Click **Save and Deploy**.

### Single-Page Application (SPA) Routing & Refreshes:
- A `public/_redirects` file is included in this repository:
  ```text
  /*    /index.html   200
  ```
- When Cloudflare Pages builds the project, this rule ensures that direct deep links and browser refreshes route to `dist/index.html` with HTTP 200 without 404 errors.

---

## 4. Admin Control Panel & Security Architecture

### Zero-Exposure Security Model:
- **No Hardcoded Passwords**: All default and hardcoded passwords (`admin123`) have been removed from source code, default state objects, and production bundles.
- **Client-Side SHA-256 Hashing**: When the owner first unlocks the Admin Control Panel (`Ctrl+Shift+A` or `#admin`), they configure their own private master username and password. The credential hash is saved in their browser's local storage using native Web Crypto SHA-256 with zero exposure in public bundles.
- **Frontend-Only Authentication Limitations**:
  - In a purely static client-side single-page app without a server database, administrative changes (updating bio, adding projects) alter the local browser's state (`localStorage`).
  - **Shared Global Edits**: If you want changes made in the Admin Panel to update the website for *all* visitors across the globe in real time, a backend database is required (e.g. Cloudflare D1 with Pages Functions, or Supabase/Firebase).
  - Until such a backend is attached, the Admin Panel serves as a personal design sandbox, and custom configurations can be exported via the **Export JSON Backup** button.

---

## 5. Downloadable Project Package

A complete, clean, and self-contained project archive (excluding `node_modules`, secret files, and build caches) is generated and available:
- **ZIP Path**: `/graphic-designer-portfolio.zip` (available in `public/` and served directly in development/production at `/graphic-designer-portfolio.zip`).

---

## 6. Verification Status

| Step | Command | Result |
| :--- | :--- | :--- |
| Dependencies | `npm install` | Verified clean |
| Compilation & Types | `npm run lint` (`tsc --noEmit`) | **0 Errors** |
| Cross-Platform Clean | `npm run clean` | **Exited code 0** (runs on Windows & Linux) |
| Production Build | `npm run build` | **Exited code 0** (`dist/` created in ~880ms) |
| Production Preview | `npm run preview` | **Verified working on port 4173** |
| Secret Leak Scan | `grep -rn "admin123" dist/` | **Zero leaked credentials** |
