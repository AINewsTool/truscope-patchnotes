# 🧩 TruScope Patch Notes

---

## **Version 1.3.5**
📅 *Released: January 4, 2026*

### 🌐 Website Updates
* Migrated **truscope.app** from a static GitHub Pages site to a **Next.js** app hosted on **Firebase App Hosting**.
* Refactored authentication for improved security, reliability, and error handling.
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


