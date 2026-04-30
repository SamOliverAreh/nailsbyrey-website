# 💅 Nails by Rey — Business Website

> A fully responsive small business website built for **Vive Reytchel (Nails by Rey)**, a professional nail technician based in Kajang Utama, Selangor. Built with pure HTML, CSS, and vanilla JavaScript — no frameworks, no dependencies, no build tools.

🔗 **Live Site:** [nailsbyrey.com](https://nailsbyrey.com)
🔗 **GitHub Pages Mirror:** [samoliverareh.github.io/Nails-by-Rey](https://samoliverareh.github.io/Nails-by-Rey)

-----

## 📌 Project Overview

This project was built as a complete real-world business platform for a home-based nail tech small business. It covers the full customer journey — from discovering services and viewing the gallery, to booking an appointment and receiving a WhatsApp confirmation — and includes a fully featured admin dashboard for day-to-day business management backed by Google Sheets as a live database.

It demonstrates practical full-stack thinking applied with front-end technologies: UI/UX design, business logic, data management, analytics, and customer communication flows — all in a two-file deployment (`index.html` + `admin.html`).

-----

## ✨ Features

### 🌸 Customer-Facing (`index.html`)

- **Hero Landing Page** — branded intro with scroll-reveal animations and call-to-action buttons
- **Social Links Strip** — direct links to WhatsApp, TikTok, Threads, and Google Maps location
- **Filterable Gallery** — nail art portfolio filtered by style (3D Arts, Cat Eye, French Tips, Gel, Ombré, Others) — images served from ImgBB cloud storage and synced via Google Sheets
- **Pricing Library** — full service menu with descriptions and pricing (Gel Removal, Manicure, Manicure + Gel, Extensions, Nail Art add-ons)
- **Smart Booking Form** — multi-select service dropdown, date picker, intelligent time slot system that:
  - Blocks past dates and times
  - Greys out slots within ±2 hours of any active (pending/confirmed) booking on the same day
  - Weekday slots (Mon–Fri): evening only (8:00 PM – 9:00 PM)
  - Weekend slots (Sat–Sun): full day (11:00 AM – 6:00 PM)
- **Booking Confirmation** — personalised success message with auto-opened WhatsApp notification to Rey for every new submission
- **Scroll Reveal Animations** — elements animate in as user scrolls down the page
- **Mobile Responsive** — hamburger nav, stacked layouts, touch-friendly on all screen sizes

### 🔐 Admin Dashboard (`admin.html`)

Accessible at `/admin` — hidden from public navigation, password-protected on load, and secured at the network level via Cloudflare Access.

#### Overview Stats Strip

Real-time counts of Total, Pending, Confirmed, Completed, Cancelled bookings and total Revenue (with thousands separator, e.g. RM 1,250).

#### Dashboard Tab (Analytics)

- **Revenue Trend** — line/bar chart switchable between Daily, Weekly, Monthly, Yearly views
- **Weekday vs Weekend Performance** — pie chart of revenue split, with per-side breakdown of:
  - Revenue (RM)
  - Booking count
  - Estimated hours spent (smart calculation: overlapping 2-hr slots are merged, not double-counted)
  - Average revenue per hour worked
- **Top Services** — horizontal bar chart of most completed services ranked by frequency
- **Customer Retention** — stacked bar chart (Active vs Cancelled) switchable between Daily / Weekly / Monthly / Yearly, with overall retention rate %

#### Bookings Tab

- Searchable by name, phone, service, ID, or notes
- Filterable by status (All / Cancelled / Completed / Confirmed / Pending — A–Z order)
- Sortable by every column (click to sort ascending ▲, click again for descending ▼) — Date column defaults to latest first, Final Price defaults to highest first
- Actions per row: **Edit**, **Delete**, **Confirm**, **Complete** (prompts for final price), **Cancel**, **Notify** (opens pre-filled WhatsApp message to customer)
- Manual booking entry via **➕ Add Booking** button
- **📥 Export CSV** — full bookings data export with UTF-8 BOM for Excel compatibility

#### Customers Tab

- Auto-aggregated from completed bookings — grouped by phone number (no-phone customers included via name-based fallback key)
- Shows: Name, Phone, Visit count, All services ever received, Total spent (RM)
- Searchable by name, phone, or service
- Sortable by every column
- Row count indicator showing unique customer count
- **📥 Export CSV** — customers summary export
- 15 rows per page with pagination matching Bookings tab

#### Gallery Tab

- Drag & drop or browse to upload photos
- Each photo tagged by style category (matches public gallery tabs)
- Uploads to **ImgBB** cloud storage — cross-device synced via Google Sheets Gallery tab
- Delete individual photos or clear all
- Photos appear instantly on the public gallery

-----

## 🛠️ Tech Stack

|Layer         |Technology                                                                 |
|--------------|---------------------------------------------------------------------------|
|Structure     |HTML5 (two-file architecture)                                              |
|Styling       |CSS3 (custom properties, flexbox, grid, animations, media queries)         |
|Logic         |Vanilla JavaScript ES6+ (async/await, IntersectionObserver, fetch API)     |
|Charts        |Chart.js 4.4.1 (via cdnjs CDN)                                             |
|Fonts         |Google Fonts — Cormorant Garamond + DM Sans                                |
|Database      |Google Sheets (Bookings tab + Gallery tab)                                 |
|Backend       |Google Apps Script (Web App — REST-style POST/GET handler)                 |
|Image Hosting |ImgBB API (free tier, permanent URLs)                                      |
|Deployment    |GitHub Pages                                                               |
|Custom Domain |`nailsbyrey.com` via Porkbun registrar                                     |
|DNS & Security|Cloudflare (DNS proxy, DDoS protection, SSL/TLS)                           |
|Admin Security|Cloudflare Access (Zero Trust — admin URL protected by email OTP)          |
|Notifications |WhatsApp `wa.me` deep links (customer booking alerts + admin confirmations)|

**No frameworks. No build tools. No npm. No server.** Fully portable — works by opening the HTML file in any browser.

-----

## 🗄️ Database Architecture

The project uses **Google Sheets as a lightweight relational database** with two tabs:

### Bookings Sheet

|Column      |Type  |Notes                                             |
|------------|------|--------------------------------------------------|
|id          |String|Sequential: BK001, BK002… generated by Apps Script|
|fname       |String|Customer first name                               |
|lname       |String|Customer last name                                |
|phone       |String|With country code e.g. +60123456789               |
|service     |String|Comma-separated selected services                 |
|date        |Date  |YYYY-MM-DD format                                 |
|time        |String|24hr or 12hr format                               |
|notes       |String|Inspiration notes from customer                   |
|status      |String|pending / confirmed / completed / cancelled       |
|finalservice|String|Confirmed service after completion                |
|finalprice  |Number|Final charged amount (RM)                         |

### Gallery Sheet

|Column|Type  |Notes                             |
|------|------|----------------------------------|
|id    |String|Timestamp-based unique ID         |
|label |String|Photo title                       |
|tag   |String|Category slug (gel, cat-eye, etc.)|
|url   |String|Permanent ImgBB URL               |

-----

## 🔧 Google Apps Script

The Apps Script Web App (`NailsByRey_AppsScript.gs`) handles all write operations as a REST-style POST endpoint:

|Operation           |`type` value        |Description                                           |
|--------------------|--------------------|------------------------------------------------------|
|Add booking         |`addBooking`        |Appends new row to Bookings sheet                     |
|Update booking      |`updateBooking`     |Rewrites full row by ID                               |
|Update status only  |`updateStatus`      |Writes only status + finalprice cells                 |
|Delete booking      |`deleteBooking`     |Deletes row by ID                                     |
|Add gallery photo   |`addGallery`        |Appends to Gallery sheet                              |
|Delete gallery photo|`deleteGallery`     |Deletes gallery row by ID                             |
|Clear gallery       |`clearGallery`      |Deletes all gallery data rows                         |
|Get next ID         |GET `?action=nextId`|Returns next sequential BK### ID                      |
|Setup sheets        |`setupSheets()`     |One-time: creates correct headers, removes old columns|

-----

## 🌐 Custom Domain & Security Setup

### Domain — Porkbun

The domain `nailsbyrey.com` is registered via [Porkbun](https://porkbun.com). DNS is managed through Cloudflare (nameservers pointed from Porkbun → Cloudflare).

### Cloudflare — DNS, SSL & DDoS Protection

All traffic routes through Cloudflare’s proxy:

- **SSL/TLS** — Full (strict) mode, auto HTTPS redirect
- **DDoS protection** — automatic via Cloudflare’s free tier
- **DNS records** — CNAME pointing `nailsbyrey.com` → `samoliverareh.github.io`
- GitHub Pages custom domain configured in repo Settings → Pages

### Cloudflare Access — Admin URL Protection

The admin dashboard at `nailsbyrey.com/admin` is protected by **Cloudflare Access (Zero Trust)**:

- Access policy requires email OTP verification before the page loads
- Only whitelisted email addresses can pass through
- Even if the password inside the page were known, the URL is blocked at the network level without a valid session token
- Free tier supports up to 50 users

This means the admin URL has **two independent layers of security**:

1. Cloudflare Access (network-level, email OTP)
1. In-page password gate (`Eden1008!` — change before sharing)

-----

## 📐 Architecture Highlights

- **Two-file deployment** — `index.html` (public) and `admin.html` (admin) are completely separate with no shared state or cross-links in the public UI
- **Google Sheets as database** — reads via Sheets API v4 (GET, public API key), writes via Apps Script Web App (POST, JSON body, `mode: no-cors`)
- **Smart time slot blocking** — booking form computes blocked windows client-side from live sheet data loaded at page start, without any server round-trip
- **Hours calculation logic** — for analytics, overlapping 2-hour booking windows on the same day are merged (e.g. 11:00 AM + 1:30 PM + 3:00 PM = 5.5 hours, not 6 hours)
- **Customer aggregation** — customer history is computed on-the-fly from bookings using phone number as the primary key (name-based fallback for no-phone records), equivalent to SQL `GROUP BY phone`
- **Sequential IDs** — booking IDs (BK001, BK016…) generated server-side via Apps Script to avoid race conditions from concurrent submissions
- **ImgBB + Sheets gallery sync** — photos uploaded from admin are stored in ImgBB (permanent CDN URLs) and registered in the Gallery sheet, making them available across all devices and browsers instantly

-----

## 🚀 Getting Started

No setup needed for the public site. Just open `index.html` in any browser.

```bash
git clone https://github.com/SamOliverAreh/Nails-by-Rey.git
cd Nails-by-Rey
open index.html
```

For the full stack (Google Sheets + Apps Script):

1. Create a Google Sheet with `Bookings` and `Gallery` tabs
1. Run `setupSheets()` in Apps Script to set correct headers
1. Deploy Apps Script as a Web App (Execute as: Me, Access: Anyone)
1. Update `APPS_SCRIPT_URL`, `SPREADSHEET_ID`, and `API_KEY` in both HTML files
1. Set your `IMGBB_API_KEY` in `admin.html`
1. Set your `ADMIN_PASSWORD` in `admin.html`

-----

## 📁 Project Structure

```
Nails-by-Rey/
│
├── index.html                  # Public-facing website (customer-facing)
├── admin.html                  # Admin dashboard (password + Cloudflare protected)
├── NailsByRey_AppsScript.gs    # Google Apps Script backend
└── README.md                   # This file
```

-----

## 🔮 Future Improvements

- [ ] Calendar view with visual slot blocking for confirmed bookings
- [ ] Automated WhatsApp reminders 24 hours before appointment (via Twilio or WhatsApp Business API)
- [ ] Customer loyalty tracking — flag returning customers with visit milestones
- [ ] Revenue forecasting based on booking pipeline (pending + confirmed)
- [ ] Gallery lightbox — full-screen image viewer on the public gallery
- [ ] Multi-language support (English / Bahasa Malaysia)
- [ ] Progressive Web App (PWA) — installable on home screen for customers

-----

## 👨‍💻 Author

**SamOliverAreh**
Husband · Data Analyst · Data Scientist · Developer
🔗 [github.com/SamOliverAreh](https://github.com/SamOliverAreh)

-----

*Built with love for Vive Reytchel — Nails by Rey 💅*
*Kajang Utama, Selangor · [nailsbyrey.com](https://nailsbyrey.com)*