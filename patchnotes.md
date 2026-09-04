# 🧩 TruScope Patch Notes

---

## **Version 2.1.2**
📅 *Released: August 16, 2026*

🌐 *Website onboarding page deployed: August 19, 2026*

### 👋 New-User Onboarding
* **Automatic Welcome Guide:** Fresh installations now open the TruScope welcome page in a new tab.
* **Update-Safe Behavior:** The guide opens only after a first-time installation, so extension updates do not interrupt returning users.
* **60-Second Setup:** The new website guide explains how to pin TruScope, open a supported news or opinion article, and run a first analysis.
* **Clear Result Preview:** New users can preview the signal score, exact supporting passages, and article-direction result before getting started.

---

## **Version 2.1.1**
📅 *Released: August 15, 2026*

### 🧭 Navigation Improvements
* **Clearer Contact Link:** The extension's Contact navigation item now includes an external-link icon and tooltip so users know it opens the website in a new tab.

---

## **Version 2.1.0**
📅 *Released: August 14, 2026*

### 🧠 Direction Analysis v3
* **More Accurate Framing Detection:** Expanded the language and stance patterns used to identify left, right, mixed, or unclear article direction.
* **Headline, Summary & Body Context:** Direction analysis now considers article summaries alongside headlines and body text.
* **Better Evidence Weighting:** Model confidence now influences the strength of directional evidence, while nearby sentences can supply context for references such as “this policy.”
* **Improved Quote Attribution:** Quoted or attributed opinions are separated from the publication's own voice and receive reduced weight.
* **More Nuanced Results:** Updated thresholds improve mixed-direction detection and reduce unsupported directional labels.

### 📰 Extraction & Packaging Fixes
* **Cleaner Article Text:** Expanded removal of Mother Jones newsletter and promotional lead-ins from extracted articles.
* **Manifest Packaging Fix:** Renamed the bundled model-package manifest so Chrome no longer mistakes it for an extension manifest.
* **Clean Production Builds:** Production builds now remove stale generated files before creating a new package.

---

## **Version 2.0.0**
📅 *Extension released: August 8, 2026*

🌐 *Website redesign deployed: August 19, 2026*

### 🧠 Private, On-Device Analysis
* **Local AI Models:** Article analysis now runs entirely on the user's device with bundled, quantized ONNX models; normal analysis no longer sends article text to a TruScope analysis server.
* **New Bias Signal Score:** Results now report a 0–100 signal for loaded wording and sensational presentation instead of presenting the score as factual accuracy or publisher trust.
* **Article Direction:** Added left, right, mixed, and unclear direction results based on the framing of the individual article.
* **Reviewable Evidence:** Biased wording, sensational presentation, and direction results include the exact passages that influenced them.
* **Independent Publisher Context:** Verified, attributed publisher information is shown separately and never changes the article-level result.

### 📰 Extraction & Page Detection
* **Stronger Article Extraction:** Added Readability and JSON-LD extraction with safeguards for malformed or oversized page data, better metadata capture, and improved handling of preview-only pages.
* **News-Page Gate:** TruScope now checks article schema, metadata, URL shape, and body structure before analysis and rejects homepages, search engines, social platforms, and other unsupported pages more reliably.
* **Analyze Anyway:** Short or uncertain articles can still be analyzed after an explicit confirmation.
* **Smarter Article Prompts:** Optional on-page prompts identify likely articles, support single-page-app navigation, and can open TruScope directly into analysis.
* **Improved Highlighting:** Evidence highlighting is more reliable across split page elements and punctuation differences.

### 🗂️ Local History & Research Exports
* **Recent Activity:** The latest completed analysis is available from the extension home screen.
* **Local Analysis Archive:** TruScope stores up to 100 complete analysis records on the user's device, including article text, evidence, extraction diagnostics, model versions, thresholds, and methodology.
* **JSON & CSV Downloads:** The local archive can be exported in validated JSON or spreadsheet-safe CSV formats and cleared at any time.

### 💬 Feedback & Guest Access
* **Continue as Guest:** Users can analyze articles locally without creating or signing into an account.
* **Optional Feedback Restored:** Account users and guests can mark a result helpful or unhelpful and add an optional comment.
* **Explicit Data Disclosure:** TruScope shows exactly what will be uploaded before feedback is submitted; selecting a rating alone sends nothing.
* **Private Guest Authentication:** A guest receives an anonymous Firebase identity only when submitting feedback.
* **Safer Submissions:** Feedback now includes strict validation, duplicate protection, retry safety, and per-user and per-network rate limits. Raw IP addresses and account email are not stored with feedback.

### ⚙️ Preferences & Reliability
* **Synced Preferences:** Signed-in users can sync appearance, highlighting, notifications, one-click detection, and smart-prompt settings while article text and results remain local.
* **System Theme Support:** Appearance can follow the operating system or be set explicitly to light or dark mode, with migration from the previous dark-mode setting.
* **Analysis Controls:** Added one-click analysis, cancellation for in-progress analysis, clearer timeouts and errors, and cleanup that prevents signed-out sessions from restoring stale data.
* **Improved Interfaces:** Redesigned the Home, Results, Settings, Donate, loading, authentication, and guest screens and fixed numerous visual and state-handling issues.

### 🔐 Security & Infrastructure
* **Hardened Boundaries:** Restricted website-to-extension authentication to trusted TruScope origins, validated synced settings and privileged messages, and escaped page-controlled result content.
* **Firebase Protection:** Tightened Firestore rules, CORS, API-key restrictions, secret handling, and error responses; enabled deletion protection and point-in-time recovery.
* **Service Cleanup:** Retired the remote scraper, orchestrator, model-hosting, classifier-uploader, and deployed quota services after analysis moved on-device.
* **Expanded Test Coverage:** Added automated coverage for extraction, page classification, tokenization, local models, direction analysis, exports, messaging security, feedback, Firestore rules, and full extension smoke flows.

### 🌐 Website Redesign
* **New Product Experience:** Rebuilt the home page around the 2.0 product with a visual product tour, real extension screenshots, evidence demonstrations, privacy explanation, methodology principles, FAQs, and clearer installation actions.
* **On-Device Privacy Messaging:** Updated website copy to explain that normal article analysis stays on the device and that account sync is limited to preferences.
* **Responsive Navigation & Footer:** Added a redesigned desktop/mobile navigation system, signed-in account controls, product links, support links, and direct access to release notes.
* **Updated Authentication:** Redesigned login, signup, password recovery, reset, and change-password screens with consistent validation, clearer errors, and a shared extension-session handoff.
* **Contact & Community Support:** Redesigned the contact form and replaced the upgrade-focused page with a community-support page centered on keeping TruScope free and independent.
* **Rewritten Legal Pages:** Updated the Privacy Policy and Terms of Service for local analysis, guest mode, preference sync, local exports, optional feedback, and current service providers.
* **Brand & Search Presentation:** Added new light/dark brand assets, updated site metadata and favicon, and introduced a dedicated social-sharing image.

---

## **Version 1.3.6**
📅 *Released: January 10, 2026*

### 🔐 Authentication & Security
* **Firebase App Check:** Implemented App Check using reCAPTCHA v3 to secure backend resources.
  * Added automatic **Localhost Debugging** support (bypasses reCAPTCHA locally).
  * Configured to work seamlessly in both dev (using debug token) and production (using reCAPTCHA).
* **Backend Auth Fix:** Updated `firebase-admin` initialization to support dual-environment credentials.

### 🔌 Extension Integration
* **Bi-Directional Logout:**
  * **Website to Extension:** The website now broadcasts the "Logout" signal to **both** the Production and Testing versions of the Chrome Extension simultaneously when you log out.
  * **Extension to Website:** Added a listener on the `Navbar` to detect logout requests coming *from* the extension, ensuring that logging out via the extension also logs you out of the website.
* **Console Cleanup:** Removed verbose "Extension not found" logs and other debug messages from Login, Signup, and Navbar components to keep the console clean.
* **Tighter Extension Access:** Removed the localhost URL from the production extension's externally connectable website list.

### 🌐 Website Updates
* **Contact Form Delivery:** Added a backend contact-form route using Resend so website messages can be delivered reliably.
* **Release Messaging:** Updated the website's release popup and footer for version 1.3.6.

### 🧩 Extension Metadata
* Updated the extension to version 1.3.6 and revised its store description to better explain Trust Scores and bias highlighting.

---

## **Version 1.3.5**
📅 *Released: January 4, 2026*

### 🌐 Website Updates
* Migrated **truscope.app** from a static GitHub Pages site to a **Next.js** app hosted on **Firebase App Hosting**.
* Refactored authentication for improved security, reliability, and error handling.
* Added a Firebase Admin custom-token route and improved the login-tab lifecycle used to transfer authenticated website sessions into the extension.
* Applied global styling updates for a cleaner, more consistent UI.

### 🆕 Extension Features
* **Hybrid Scraping (Anti-Blocking):**
  Added client-side article extraction using **@mozilla/readability**, enabling analysis on sites that block server-side scrapers (e.g., Reuters, Axios). Text is extracted directly from the browser tab and sent to the backend, bypassing Cloud Run IP blocks.
* **On-Page Bias Highlighting:**
  Biased sentences are now highlighted directly within the article after analysis.
* **Bias Categories (Color-Coded):**
  🟡 Political Bias · 🔴 Hate Speech · 🟠 Clickbait · 🟣 Emotional Language · 🟢 Conspiracy Theory
* **Interactive Tooltips:**
  Hover over highlights to see the detected bias type.
* **Highlight Toggle:**
  Added a **“Highlight Biases”** setting to instantly enable or disable highlights without reloading.

### 🎨 UI / UX Improvements
* Added a new **Preferences** section in Settings.
* Standardized spacing across **Account**, **Preferences**, and **Legal** tabs.
* Restored default cursor behavior on highlighted text for smoother reading.

### 🔧 Technical & Cleanup
* Added **mark.js** for reliable text highlighting.
* Added **@mozilla/readability** for accurate article parsing.
* Removed redundant root-level `package.json` and `package-lock.json` files.
* Removed development `console.log` statements from background scripts.

---

## **Version 1.3.0**
📅 *Released: December 25, 2025*

### 🆕 New Features
- **Real-time Quota Sync:** The extension now fetches the user's latest quota immediately upon login or opening the popup, ensuring the display is always accurate.
- **Read-Only Quota Endpoint:** Added a new backend function (`getQuota`) to securely check usage limits without consuming detection credits.

### 🐛 Bug Fixes
- **Quota Rollback Logic:** Fixed a critical bug where users gained an extra credit if an error occurred before analysis started. Now, credits are only refunded if they were actually consumed.
- **"No Quota Object" Error:** Resolved the console error `[Quota] No quota object passed` by adding proper checks in the storage listener.
- **Scraper 401 Errors:** Fixed scraping failures on certain sites by adding a proper `User-Agent` header to backend requests.
- **Backend 500 Errors:** Resolved NLTK dependency issues (`punkt_tab`) by updating Dockerfiles to Python 3.10 and fixing the download script.

### 🎨 UI/UX Improvements
- **Fixed Navigation Bar:** The navigation bar is now permanently anchored to the bottom of the screen, ensuring it's always accessible regardless of page length.
- **Hidden Scrollbars:** Removed the buggy/unsightly scrollbars from the popup window while keeping the content scrollable.
- **Content Padding:** Added padding to the bottom of the main view so content isn't hidden behind the fixed navigation bar.

### 🔒 Security & Infrastructure
- **Secret Management:** Moved all API keys and service URLs out of the codebase and into `.env` files.
- **Project Cleanup:** Renamed `ai-scraper` to `scraper` and removed unused files/text from the project structure.
- **Documentation:** Updated `README.md` with a complete setup and deployment guide.

### 🚀 Performance & Accuracy
- **New Scraping Engine:** Replaced `newspaper3k` with **Trafilatura**. This upgrade significantly improves text extraction speed and accuracy, ensuring that only the main article content is captured while effectively stripping out ads, menus, and other "fluff."
- **Production Server:** Switched from the default Flask development server to **Gunicorn**. This allows the scraper to handle multiple concurrent requests more efficiently and improves overall service stability.

### 🛠️ Backend Improvements
- **Health Check Endpoint:** Added a `/` health check route to the scraper service for better monitoring and deployment verification.
- **Dependency Cleanup:** Removed unused dependencies related to the old scraping library, resulting in a cleaner and more lightweight build.

---

## **Version 1.2.6**
📅 *Released: October 5, 2025*

### 🆕 New Features
- Added ability to analyze articles from **unverified** and **opinion** sources.

### 🐞 Bug Fixes
- Quota check bug.
- Infinite loading issue.
- Results screen flicker.
