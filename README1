# CampusConnect

A centralized Technical Event Management System built for a college hackathon by team **Brainy Beams**. CampusConnect manages the complete lifecycle of technical events — from event creation and student registration to QR-based attendance, judge evaluation, certificate generation, and role-based analytics.

---

## Tech Stack

**Backend:** Python, FastAPI, MySQL, SQLAlchemy (ORM), PyMySQL, Pydantic, JWT (python-jose), Passlib + bcrypt, smtplib + Gmail SMTP, Uvicorn

**Frontend:** Flutter/Dart — `http`, `shared_preferences`, `mobile_scanner`, `qr_flutter`, `pdf` + `printing`, `fl_chart`

---

## Roles & Features

### 🎓 Student
- Browse and discover events (search + category filters)
- Register individually or as a team (with a project idea field)
- Unique QR ticket per registration, with a refresh option (old code is invalidated)
- Certificate of Participation / Achievement (auto-ranked — top 3 get "Achievement" certificates with their placement)
- Event feedback (star rating + comment)
- Live team leaderboard
- In-app notifications (new events, registration status, attendance, scores)
- Profile management

### 🧑‍🏫 Faculty / Coordinator
- Create and manage events (category, capacity, team toggle, banner)
- Approve / reject registrations
- View checked-in participants
- Per-event analytics (registrations, attendance rate, average rating, daily trend)
- View and manage teams for an event
- Assign volunteers to events

### 🙋 Volunteer
- QR camera scanner + manual entry check-in
- Duplicate check-in protection
- Check-in history with search
- "Today's Assignment" dashboard (based on events assigned by faculty/admin)

### ⚖️ Judge
- View teams assigned for evaluation
- Score teams on 4 criteria (Innovation, Technical Implementation, Presentation, Problem Solving)
- Live team leaderboard preview
- Evaluation progress dashboard

### 🛠️ Admin
- System-wide dashboard (users, events, registrations, attendance rate, recent activity)
- User management (search, filter by role, change role, activate/deactivate)
- Event management (system-wide catalog with status)
- Analytics Portal (new users, avg attendance, registrations trend, popular categories)
- **Role Performance Analytics** — ranked lists + individual dashboards for Faculty, Volunteer, and Judge activity
- Notification broadcast to role groups
- Create staff accounts (Faculty/Volunteer/Judge/Admin) — self-signup for these roles is disabled by design; only Admin can create them, with a temporary password emailed to the new account
- System settings (registration buffer hours, max team size, session timeout)
- Public certificate verification (no login required)

---

## Key Security & Integrity Features

- JWT-based authentication, role-based access control on every backend endpoint
- Only Admin can create Faculty/Volunteer/Judge/Admin accounts; Students self-register with email OTP verification
- Deactivated accounts are blocked from logging in
- Registration capacity enforcement (no overbooking past `max_participants`)
- Registration deadline enforcement (closes automatically before the event, configurable buffer)
- QR refresh invalidates the old code immediately; only the registration owner can refresh
- Auto-refresh (30s polling) + pull-to-refresh on Admin Analytics, Leaderboards, and Notifications

---

## Project Structure

```
CampusConnect/
  backend/
    app/
      models/       — SQLAlchemy ORM models
      schemas/       — Pydantic request/response schemas
      services/      — business logic
      routers/        — FastAPI route definitions
      utils/           — security, email, role-email helpers
      dependencies.py, database.py, config.py, main.py
    create_tables.py
    seed_data.py              — demo accounts + 15 sample events
    simulate_activity.py      — realistic registrations/scores/feedback for demo
    reset_database.py         — wipes all data (use with care)
    add_*.py                  — one-off migration scripts
    .env                      — DATABASE_URL, SECRET_KEY, EMAIL_ADDRESS, EMAIL_APP_PASSWORD
  frontend/
    lib/
      screens/
        student/, faculty/, volunteer/, judge/, admin/, auth/, shared/
      services/api_service.dart
      main.dart
    pubspec.yaml
```

---

## Setup Instructions

### Backend
```bash
cd backend
conda activate campusconnect   # or your virtualenv
python create_tables.py
# run any pending add_*.py migration scripts (see project history)
uvicorn app.main:app --reload --host 0.0.0.0 --port 8000
```

Create a `.env` file in `backend/` with:
```
DATABASE_URL=mysql+pymysql://<user>:<password>@localhost/campusconnect
SECRET_KEY=your-secret-key
ALGORITHM=HS256
ACCESS_TOKEN_EXPIRE_MINUTES=60
REFRESH_TOKEN_EXPIRE_DAYS=7
EMAIL_ADDRESS=your-gmail@gmail.com
EMAIL_APP_PASSWORD=your-16-char-app-password
```

### Frontend (physical Android device)
```bash
cd frontend
flutter pub get
adb reverse tcp:8000 tcp:8000   # tunnels phone's localhost:8000 to your backend
flutter run
```
`baseUrl` in `lib/services/api_service.dart` is set to `http://127.0.0.1:8000`, which works through `adb reverse` without needing your LAN IP.

### Demo Data
```bash
python reset_database.py     # wipes existing data
python seed_data.py          # creates 6 accounts per role + 15 events
python simulate_activity.py  # adds realistic registrations, scores, feedback
```
All seeded accounts use the password `Test@123`. See `seed_data.py` output for sample logins.

---

## First Admin Account

Since only an Admin can create Faculty/Volunteer/Judge/Admin accounts, running `seed_data.py` also creates the first Admin (`admin@admin.in` / `Test@123`). From there, use **Admin → Profile → Create Staff Account** to create any further accounts for other roles.

---

## Team

**Brainy Beams**
