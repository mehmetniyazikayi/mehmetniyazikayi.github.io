# Personal Website — Mehmet Niyazi Kayi

This repository hosts my personal website, built with [Jekyll](https://jekyllrb.com) and the dark **Midnight** theme.

Visit the live site:  
👉 [https://mehmetniyazikayi.github.io](https://mehmetniyazikayi.github.io)

---

### About the Site

The site presents my work and interests in:

- Quantum Computing (QAOA, QPE, VQE, QML)
- High-Performance Computing (HPC)
- Quantum Algorithms and Research Applications

---

### Tech Stack

- **Theme:** [`jekyll-theme-midnight`](https://github.com/pages-themes/midnight)
- **Hosted on:** [GitHub Pages](https://pages.github.com)
- **Written in:** Markdown & HTML
- **Analytics:** Google Analytics 4 (GA4)

---

### Setting Up Google Analytics

This site is configured to use Google Analytics 4 for tracking visitor statistics.

#### How to Enable:

1. **Create a Google Analytics 4 Property:**
   - Go to [Google Analytics](https://analytics.google.com/)
   - Create a new GA4 property for your website
   - Copy your Measurement ID (format: `G-XXXXXXXXXX`)

2. **Update the Configuration:**
   - Open `_config.yml`
   - Replace `G-XXXXXXXXXX` with your actual Measurement ID:
     ```yaml
     google_analytics: G-YOUR-ACTUAL-ID
     ```

3. **Deploy:**
   - Commit and push your changes
   - GitHub Pages will rebuild your site automatically
   - Analytics will start tracking once deployed (only in production)

#### Technical Details:

- The Google Analytics tracking code is located in `_includes/google-analytics.html`
- It's included via `_includes/head.html` 
- Tracking only activates in production environment (not during local development)
- Uses the latest GA4 gtag.js implementation

---

© 2025 Mehmet Niyazi Kayi

