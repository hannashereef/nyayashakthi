<div align="center">

<h1>🛡️ NyayaShakti</h1>
<h3>Women's Safety Platform — Your Safety Is Non-Negotiable. Your Power Is Real.</h3>

[![Live Demo](https://img.shields.io/badge/Live%20Demo-nyayashakthi.onrender.com-C8102E?style=for-the-badge&logo=render)](https://nyayashakthi.onrender.com)
[![Python](https://img.shields.io/badge/Python-3.11-3776AB?style=for-the-badge&logo=python)](https://python.org)
[![Django](https://img.shields.io/badge/Django-5.0.6-092E20?style=for-the-badge&logo=django)](https://djangoproject.com)
[![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)](LICENSE)

</div>

---

## 📖 Project Description

**NyayaShakti** (Sanskrit: *Power of Justice*) is a full-stack web application designed to give women immediate, accessible safety tools — no account, no login, no personal data stored. Built for use in emergency situations, the platform works entirely in the browser and is optimized for mobile devices.

The app provides one-press SOS alerting with live GPS, an interactive map of nearby police stations, hospitals and support centres, and a fully anonymous support chat that vanishes on refresh — all without any database.

> Built as part of a student project focusing on women's safety technology in Kerala, India.

---

## 🧰 Tech Stack

| Layer | Technology |
|---|---|
| **Backend** | Python 3.11, Django 5.0.6 |
| **Frontend** | Django Templates, Vanilla CSS3, Vanilla JavaScript (ES6+) |
| **Map** | Leaflet.js 1.9.4 + OpenStreetMap |
| **Static Files** | WhiteNoise 6.7.0 |
| **Server** | Gunicorn 22.0.0 |
| **Hosting** | Render (Free Plan) |
| **Fonts** | Google Fonts — Cormorant Garamond + DM Sans |
| **Database** | ❌ None — fully stateless architecture |

---

## ✨ Features

### 1. 🚨 Emergency SOS Alert
One press of the SOS button captures the user's live GPS coordinates and generates an instant alert with a Google Maps link, timestamp, and accuracy reading. The alert can be shared via WhatsApp or the native Web Share API to predefined emergency contacts. The button pulses continuously so it's always visible in a panic.

### 2. 📍 Nearby Help Centers Map
An interactive OpenStreetMap (via Leaflet.js) that auto-detects the user's device location and re-centres to show the nearest police stations, hospitals, and women's support centres. Users can filter by type, tap any marker to see contact details and get directions, or click the sidebar list to fly to that location on the map.

### 3. 💬 Anonymous Support Chat
A real-time support chat with a volunteer simulation engine. No account required, no messages stored anywhere — everything lives only in the browser's DOM and disappears the moment the tab is closed. The backend uses keyword-aware routing to provide contextually relevant responses (abuse → helpline referral, police → FIR guidance, danger → SOS redirect).

### 4. 📱 Mobile-First Responsive Design
Designed from the ground up for smartphones. Features large touch-target buttons, a sticky navigation bar with hamburger drawer on mobile, a pulsing SOS button always visible in the nav, and a CSS design system built on custom properties for consistent theming across all screen sizes.

### 5. ☎️ One-Tap Emergency Helplines
Six national emergency numbers (112, 1091, 100, 108, 1098, 181) displayed on the homepage and SOS page as tappable `tel:` links — functional even in airplane mode if the carrier allows it.

---

## 🖥️ Screenshots

> **Add 3+ screenshots here.** Place images in a `docs/screenshots/` folder and reference them below.

| Homepage | SOS Page | Help Map |
|---|---|---|
| ![Homepage](docs/screenshots/homepage.png) | ![SOS](docs/screenshots/sos.png) | ![Map](docs/screenshots/map.png) |

| Support Chat | Mobile View |
|---|---|
| ![Chat](docs/screenshots/chat.png) | ![Mobile](docs/screenshots/mobile.png) |

---

## 🎬 Demo Video

> 📹 [Watch Demo on YouTube / Google Drive](#) ← *Replace with your actual link*

The demo covers:
- Triggering the SOS alert with live location
- Browsing help centres on the map
- Using the anonymous support chat
- Mobile responsive layout

---

## 🏗️ Architecture Diagram

```
┌─────────────────────────────────────────────────────────┐
│                        BROWSER                          │
│                                                         │
│  ┌─────────┐  ┌─────────┐  ┌──────────┐  ┌─────────┐  │
│  │  Home   │  │   SOS   │  │   Map    │  │  Chat   │  │
│  │  Page   │  │  Page   │  │  Page    │  │  Page   │  │
│  └────┬────┘  └────┬────┘  └────┬─────┘  └────┬────┘  │
│       │            │            │              │        │
│       └────────────┴────────────┴──────────────┘        │
│                         │                               │
│              JavaScript (ES6+)                          │
│         Geolocation API │ Leaflet.js │ Fetch API        │
└─────────────────────────┼───────────────────────────────┘
                          │ HTTP/HTTPS
┌─────────────────────────▼───────────────────────────────┐
│                   DJANGO (WSGI / Gunicorn)               │
│                                                         │
│  config/urls.py  ──►  nyayashakthi/urls.py              │
│                              │                          │
│                    nyayashakthi/views.py                 │
│                    ┌─────────┴──────────┐               │
│                    │   Page Views       │               │
│                    │   index()          │               │
│                    │   sos_view()       │               │
│                    │   map_view()       │               │
│                    │   chat_view()      │               │
│                    ├────────────────────┤               │
│                    │   API Endpoints    │               │
│                    │   /api/sos-alert/  │               │
│                    │   /api/help-centers│               │
│                    │   /api/chat-response               │
│                    └─────────┬──────────┘               │
│                              │                          │
│              Static Data (no DB)                        │
│         EMERGENCY_CONTACTS │ HELP_CENTERS               │
│                                                         │
│  Templates ◄── WhiteNoise (static files)                │
└─────────────────────────────────────────────────────────┘
                          │
┌─────────────────────────▼───────────────────────────────┐
│                    RENDER.COM                           │
│              Free Plan · HTTPS · Auto-deploy            │
└─────────────────────────────────────────────────────────┘
```

---

## 📁 Project Structure

```
nyayashakthi/
├── config/
│   ├── __init__.py
│   ├── settings.py          # Django settings — WhiteNoise, env vars, Render config
│   ├── urls.py              # Root URL dispatcher
│   └── wsgi.py              # WSGI entry point for Gunicorn
│
├── nyayashakthi/            # Main Django app
│   ├── __init__.py
│   ├── views.py             # All page views + 3 REST API endpoints
│   ├── urls.py              # App URL patterns
│   ├── static/              # CSS, JS, images
│   └── templates/
│       └── nyayashakthi/
│           ├── base.html    # Shared layout — sticky nav, toast, footer
│           ├── index.html   # Homepage
│           ├── sos.html     # Emergency SOS page
│           ├── map.html     # Help centres map (Leaflet + OpenStreetMap)
│           └── chat.html    # Anonymous support chat
│
├── docs/                    # Architecture diagrams, screenshots
├── manage.py
├── requirements.txt
├── runtime.txt              # python-3.11.0
├── render.yaml              # Render deployment config
├── .gitignore
├── LICENSE
└── README.md
```

---

## ⚙️ Installation

### Prerequisites
- Python 3.11+
- pip
- Git

### Clone the repository
```bash
git clone https://github.com/YOUR_USERNAME/nyayashakthi.git
cd nyayashakthi
```

### Install dependencies
```bash
pip install -r requirements.txt
```

### Run the development server
```bash
python manage.py runserver
```

### Open in browser
```
http://localhost:8000
```

> ✅ No migrations needed — there is no database.

---

## 🚀 Deployment (Render — Free Plan)

### 1. Push to GitHub
```bash
git init
git add .
git commit -m "Initial commit"
git remote add origin https://github.com/YOUR_USERNAME/nyayashakthi.git
git push -u origin main
```

### 2. Create a Render Web Service
- Go to [render.com](https://render.com) → New → Web Service
- Connect your GitHub repository
- Set the following:

| Field | Value |
|---|---|
| Runtime | Python 3 |
| Build Command | `pip install -r requirements.txt && python manage.py collectstatic --noinput` |
| Start Command | `gunicorn config.wsgi:application --bind 0.0.0.0:$PORT` |
| Instance Type | Free |

### 3. Set Environment Variables
| Key | Value |
|---|---|
| `DJANGO_SECRET_KEY` | Generate a random 60-char string |
| `DEBUG` | `False` |

```bash
# Generate a secret key locally:
python -c "import secrets; print(secrets.token_urlsafe(60))"
```

### 4. Deploy
Click **"Create Web Service"** — Render builds and deploys automatically. Live in ~2 minutes.

---

## 🔌 API Documentation

### `POST /api/sos-alert/`
Receives GPS coordinates, returns a formatted emergency alert payload.

**Request:**
```json
{
  "lat": 9.654591,
  "lng": 76.827902,
  "accuracy": 12
}
```

**Response:**
```json
{
  "success": true,
  "timestamp": "28 Feb 2026, 10:45 AM IST",
  "maps_link": "https://www.google.com/maps?q=9.654591,76.827902",
  "whatsapp_link": "https://wa.me/?text=🚨 EMERGENCY SOS...",
  "sms_text": "🚨 EMERGENCY SOS – NyayaShakti\nTime: ...\nLocation: ...",
  "contacts": [{ "name": "National Emergency", "phone": "112" }]
}
```

---

### `GET /api/help-centers/`
Returns all predefined help centres. Optional `type` filter.

**Query Parameters:**

| Param | Values |
|---|---|
| `type` | `police` \| `hospital` \| `support` |

**Example:** `GET /api/help-centers/?type=police`

**Response:**
```json
{
  "centers": [
    {
      "id": 1,
      "name": "Tripunithura Police Station",
      "type": "police",
      "lat": 9.9450,
      "lng": 76.3390,
      "phone": "0484-2781520",
      "address": "Mini Bypass Road, Tripunithura, Ernakulam",
      "hours": "24/7"
    }
  ],
  "total": 3
}
```

---

### `POST /api/chat-response/`
Returns a context-aware support response. Stateless — nothing stored.

**Request:**
```json
{ "message": "I feel unsafe at home" }
```

**Response:**
```json
{
  "success": true,
  "response": "What you're describing is not okay and you deserve support. The Women Helpline (1091) can connect you with counsellors 24/7.",
  "timestamp": "10:47 PM"
}
```

**Keyword routing logic:**

| Keywords | Response Type |
|---|---|
| help, danger, unsafe, scared, fear | Direct to SOS + 112 |
| abuse, hit, hurt, violence, beat | Women Helpline 1091 referral |
| police, report, fir, complaint | FIR guidance + map redirect |
| thank, ok, okay, good | Positive affirmation |
| *(no match)* | Random from 9 supportive responses |

---

## 🔒 Privacy & Security

- **No database** — zero persistent storage of any kind
- **Anonymous chat** — messages exist only in browser memory (JavaScript DOM)
- **No login required** — instant access, no accounts
- **CSRF protected** — all POST endpoints use Django CSRF tokens
- **HTTPS enforced** — via Render's edge network in production
- **No PII collected** — the app never asks for name, email, or phone number

---

## 📞 Emergency Helplines (India)

| Service | Number | Hours |
|---|---|---|
| National Emergency | 112 | 24/7 |
| Women Helpline | 1091 | 24/7 |
| Police | 100 | 24/7 |
| Ambulance | 108 | 24/7 |
| Child Helpline | 1098 | 24/7 |
| Domestic Violence | 181 | 24/7 |

---

## 👥 Team Members

| Name | Role |
|---|---|
| *(Your Name)* | Full Stack Developer |

---

## 🤖 AI Tools Used

This project was built with assistance from **Claude (Anthropic)** for:
- Full-stack Django project scaffolding
- Frontend HTML/CSS/JS design and implementation
- REST API endpoint logic
- Deployment configuration (Render)
- Documentation generation

**Prompts used include:**
- *"Build a Django women's safety platform with SOS, map, and anonymous chat — no database"*
- *"Show help centres near coordinates 9.654591, 76.827902 on OpenStreetMap using Leaflet"*
- *"Guide me to deploy this Django app on Render free plan"*

---

## 📄 License

This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for details.

```
MIT License

Copyright (c) 2024 NyayaShakti

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.
```

---

<div align="center">
  <strong>🛡️ NyayaShakti — Built for safety, dignity, and justice.</strong><br/>
  <sub>Made with ❤️ in Kerala, India</sub>
</div>
