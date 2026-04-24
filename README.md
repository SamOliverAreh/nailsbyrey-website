# 💅 Nails by Rey — Business Website

> A fully responsive small business website built for **Vive Reytchel (Nails by Rey)**, a professional nail technician based in Kajang, Selangor. Built with pure HTML, CSS, and vanilla JavaScript — no frameworks, no dependencies.

🔗 **Live Demo:** [samoliverareh.github.io/Nails-by-Rey.com](https://samoliverareh.github.io/Nnails-by-Rey.com)

---

## 📌 Project Overview

This project was built as a real-world business website for a nail tech small business. It covers the full customer journey — from discovering services and viewing the gallery, to booking an appointment and receiving a confirmation — as well as an admin dashboard for business management.

It demonstrates practical full-stack thinking applied with front-end technologies: UI/UX design, business logic, data management, and customer communication flows — all in a single-file deployment.

---

## ✨ Features

### Customer-Facing
- **Hero Landing Page** — branded intro with call-to-action
- **Social Links Strip** — direct links to WhatsApp, Instagram, TikTok, and Threads
- **Filterable Gallery** — nail art portfolio filtered by style (Gel, Acrylic, Nail Art, French, Ombré)
- **Pricing Library** — full service menu with descriptions, durations, and pricing
- **Discount / Offers Section** — publicly displayed promo codes with conditions
- **Booking Form** — full appointment request with service selection, date/time picker, discount code input, and inspiration notes
- **Booking Confirmation** — personalised confirmation message with WhatsApp quick-link

### Admin Dashboard
- **Live Stats** — total bookings, confirmed count, pending count, estimated revenue
- **Bookings Management** — searchable table with Confirm / Cancel / WhatsApp Notify actions
- **Customer History** — auto-aggregated customer records with visit count and total spend
- **Discount Manager** — add and remove promo codes dynamically; reflects instantly on the public page

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| Structure | HTML5 |
| Styling | CSS3 (custom properties, flexbox, grid, animations) |
| Logic | Vanilla JavaScript (ES6+) |
| Fonts | Google Fonts — Cormorant Garamond + DM Sans |
| Deployment | GitHub Pages |
| Notifications | WhatsApp API (`wa.me` deep links) |

**No frameworks. No build tools. No dependencies.** Single-file architecture — fully portable and deployable anywhere.

---

## 📐 Architecture Highlights

- **Component-based JS** — gallery, pricing, bookings, customers and discounts each managed by dedicated render functions
- **In-memory data store** — bookings and customer records managed in a structured JS array, mimicking a lightweight database
- **Dynamic customer aggregation** — customer history table is computed on the fly from booking data (visit count, last service, total spend) — similar logic to SQL GROUP BY
- **Responsive design** — mobile-first CSS grid layout adapts across all screen sizes
- **WhatsApp notification flow** — admin can trigger a pre-filled WhatsApp message to any customer with one click, using the `wa.me` API with URL-encoded message templates

---

## 📊 Relevance to Data & Analytics Work

While this is a front-end project, it reflects core data thinking:

- Designed a **booking data schema** (customer, service, date, status, discount code)
- Built **aggregation logic** to derive customer lifetime value and visit frequency from raw booking records
- Implemented **filter and search** on tabular data — equivalent to `WHERE` and `LIKE` in SQL
- Modelled **discount redemption tracking** as a separate data layer linked to booking records

---

## 🚀 Getting Started

No setup needed. Just open `index.html` in any browser.

```bash
git clone https://github.com/SamOliverAreh/nailsbyrey-website.git
cd nailsbyrey-website
open index.html
```

---

## 📁 Project Structure

```
nailsbyrey-website/
│
├── index.html        # Entire application (HTML + CSS + JS)
└── README.md         # This file
```

---

## 🔮 Future Improvements

- [ ] Backend integration (Node.js / Supabase) for persistent bookings database
- [ ] Real email notifications via EmailJS or SendGrid
- [ ] Calendar view with slot blocking for confirmed bookings
- [ ] Admin authentication (password-protected dashboard)
- [ ] Gallery image upload support
- [ ] Analytics dashboard (bookings by service, revenue trends, customer retention)

---

## 👨‍💻 Author

**SamOliverAreh**
Husband . Data Analyst . Data Scientist . Developer
🔗 [github.com/SamOliverAreh](https://github.com/SamOliverAreh)

---

*Built with love for Vive Reytchel — Nails by Rey 💅*
