# 🛡️ NyayaShakti — Women's Safety Platform

> **"Your Safety Is Non-Negotiable. Your Power Is Real."**

A full-stack Django women's safety web application with Emergency SOS, interactive help maps, anonymous support chat, and mobile-first design. **No database required.**

---

## ✨ Features

| Feature | Description |
|---------|-------------|
| 🚨 **Emergency SOS Button** | One-press sends live GPS location via WhatsApp/SMS to emergency contacts |
| 📍 **Nearby Help Map** | Interactive OpenStreetMap showing police stations, hospitals & support centres |
| 💬 **Anonymous Support Chat** | AI-powered keyword-aware chat — no storage, vanishes on refresh |
| 📱 **Mobile-First Design** | Responsive, big touch buttons, sticky nav, works on any device |

---

## 🚀 Quick Start (Local)

### Prerequisites
- Python 3.11+
- pip

### 1. Clone & Install

```bash
git clone <your-repo>
cd nyayashakthi
pip install -r requirements.txt
```

### 2. Run Development Server

```bash
python manage.py runserver
```

Visit: **http://localhost:8000**

---

## 🌐 Vercel Deployment

### Step 1 — Install Vercel CLI
```bash
npm install -g vercel
```

### Step 2 — Login
```bash
vercel login
```

### Step 3 — Set Secret Key Environment Variable
In Vercel dashboard → Project → Settings → Environment Variables:

```
DJANGO_SECRET_KEY = your-super-secret-random-key-here-min-50-chars
DEBUG = False
```

Generate a key:
```python
python -c "import secrets; print(secrets.token_urlsafe(60))"
```

### Step 4 — Deploy
```bash
vercel --prod
```

That's it! Your app will be live at `https://nyayashakthi.vercel.app`

---

## 📁 Project Structure

```
nyayashakthi/
├── config/
│   ├── settings.py          # Django settings (WhiteNoise, Vercel-ready)
│   ├── urls.py              # Root URL config
│   └── wsgi.py              # WSGI entry (Vercel uses `app = application`)
├── nyayashakthi/
│   ├── views.py             # All app logic (SOS API, chat, map data)
│   ├── urls.py              # App routes
│   ├── templates/
│   │   └── nyayashakthi/
│   │       ├── base.html    # Sticky nav, toast system, footer
│   │       ├── index.html   # Homepage with hero + features
│   │       ├── sos.html     # Emergency SOS page
│   │       ├── map.html     # OpenStreetMap help centres
│   │       └── chat.html    # Anonymous support chat
│   └── static/              # CSS / JS / images (if any)
├── manage.py
├── requirements.txt
├── vercel.json              # Vercel build + route config
├── build_files.sh           # collectstatic for Vercel
└── runtime.txt              # Python 3.11
```

---

## 🔌 API Endpoints

| Method | URL | Description |
|--------|-----|-------------|
| `POST` | `/api/sos-alert/` | Receive GPS coords, return alert payload + WhatsApp link |
| `GET`  | `/api/help-centers/` | Return all help centres (filter by `?type=police/hospital/support`) |
| `POST` | `/api/chat-response/` | Return volunteer response (keyword-aware, stateless) |

### SOS Alert Request
```json
POST /api/sos-alert/
{ "lat": 13.0827, "lng": 80.2707, "accuracy": 12 }
```

### SOS Alert Response
```json
{
  "success": true,
  "timestamp": "15 Jun 2024, 10:45 AM IST",
  "maps_link": "https://www.google.com/maps?q=13.0827,80.2707",
  "whatsapp_link": "https://wa.me/?text=...",
  "sms_text": "🚨 EMERGENCY SOS...",
  "contacts": [...]
}
```

---

## 🎨 Design System

| Token | Value |
|-------|-------|
| Primary | `#C8102E` Crimson |
| Accent | `#FF8C00` Saffron |
| Background | `#FAF7F2` Warm Ivory |
| Font Display | Cormorant Garamond |
| Font Body | DM Sans |

---

## 🛡️ Privacy & Safety Design

- **No database** — zero persistent storage
- **Anonymous chat** — messages exist only in browser memory
- **CSRF protected** — all POST APIs require Django CSRF token
- **No login required** — instant access in emergencies
- **Geolocation optional** — SOS still works if GPS is denied

---

## 📞 Emergency Numbers (India)

| Service | Number |
|---------|--------|
| National Emergency | 112 |
| Women Helpline | 1091 |
| Police | 100 |
| Ambulance | 108 |
| Domestic Abuse | 181 |
| Child Helpline | 1098 |

---

## 📜 License

MIT — Free to use, adapt, and deploy for women's safety initiatives.

---

*Built with ❤️ for safety, justice, and dignity.*
