
<h1>🛡️ NyayaShakti</h1>
<h3>Women's Safety Platform — Your Safety Is Non-Negotiable. Your Power Is Real.</h3>


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
git clone https://github.com/hannashereef/nyayashakthi
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


---




**Keyword routing logic:**

| Keywords | Response Type |
|---|---|
| help, danger, unsafe, scared, fear | Direct to SOS + 112 |
| abuse, hit, hurt, violence, beat | Women Helpline 1091 referral |
| police, report, fir, complaint | FIR guidance + map redirect |
| thank, ok, okay, good | Positive affirmation |
| *(no match)* | Random from 9 supportive responses |

---
Demo video
https://drive.google.com/file/d/1InghM9OetR6UjbxjFwY5A_piGM5q4sZL/view?usp=drive_link
