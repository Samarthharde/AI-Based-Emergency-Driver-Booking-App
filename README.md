# 🚗 AI-Based Emergency Driver Booking App

**Driver-as-a-Service Platform** — Final Year Project

## 📋 Features

- ✅ User registration and JWT authentication
- ✅ AI-based driver matching (distance + rating optimization)
- ✅ Emergency booking mode (prioritizes nearest + best rated)
- ✅ Real-time driver availability tracking
- ✅ Booking history with filters
- ✅ SQLite database with SQLAlchemy ORM
- ✅ FastAPI backend with Swagger docs
- ✅ Streamlit frontend with clean UI
- ✅ Pre-seeded with 5 sample drivers

## 🛠️ Tech Stack

- **Backend:** FastAPI (Python)
- **Frontend:** Streamlit (Python)
- **Database:** SQLite + SQLAlchemy ORM
- **Auth:** JWT tokens with bcrypt password hashing
- **Server:** Uvicorn

## 📁 Project Structure

```
driver_app/
├── backend/
│   ├── main.py              # FastAPI app entry
│   ├── database.py          # DB config + seeding
│   ├── models.py            # SQLAlchemy models
│   ├── schemas.py           # Pydantic schemas
│   ├── auth.py              # JWT helpers
│   ├── routes/
│   │   ├── user.py          # Register, login
│   │   ├── driver.py        # Driver CRUD
│   │   └── booking.py       # Booking endpoints
│   └── services/
│       └── ai_matching.py   # AI driver matching logic
├── frontend/
│   ├── app.py               # Streamlit main
│   └── pages/
│       ├── login.py
│       ├── register.py
│       ├── dashboard.py
│       ├── book_driver.py
│       └── history.py
├── requirements.txt
├── setup.bat                # Windows setup script
├── run_backend.bat
└── run_frontend.bat
```

## 🚀 Setup Instructions

### Windows

```bat
# 1. Create virtual environment
python -m venv venv

# 2. Activate
venv\Scripts\activate

# 3. Install dependencies
pip install -r requirements.txt
```

### Mac/Linux

```bash
# 1. Create virtual environment
python3 -m venv venv

# 2. Activate
source venv/bin/activate

# 3. Install dependencies
pip install -r requirements.txt
```

## ▶️ Run the Application

### Option 1: Manual (Recommended for development)

**Terminal 1 — Backend:**
```bat
venv\Scripts\activate
uvicorn backend.main:app --reload
```
Backend runs on: `http://localhost:8000`  
API Docs (Swagger): `http://localhost:8000/docs`

**Terminal 2 — Frontend:**
```bat
venv\Scripts\activate
streamlit run frontend/app.py
```
Frontend runs on: `http://localhost:8501`

### Option 2: Quick Start (Windows)

```bat
# Setup (first time only)
setup.bat

# Run backend
run_backend.bat

# Run frontend (in another terminal)
run_frontend.bat
```

## 🧪 Testing

1. **Backend API:** Visit `http://localhost:8000/docs` for interactive Swagger UI
2. **Sample Drivers:** 5 drivers are auto-seeded on first run (phone: 9000000001-5, password: driver123)
3. **Test Flow:**
   - Register a user
   - Login
   - Book a driver (emergency or regular)
   - View booking history

## 🤖 AI Matching Logic

Located in `backend/services/ai_matching.py`:

- **Haversine formula** for accurate distance calculation
- **Emergency mode:** Scores drivers using `0.6 * distance + 0.4 * (5 - rating)`
- **Normal mode:** Sorts purely by distance
- **Max radius:** 50 km search area
- Returns the best matched driver instantly

## 📊 Database Schema

**Users:** id, name, phone, hashed_password, role, location  
**Drivers:** id, user_id, name, phone, vehicle_type, lat, lng, availability, rating, total_rides  
**Bookings:** id, user_id, driver_id, pickup_lat, pickup_lng, status, emergency, timestamp

## 🔐 Security

- Passwords hashed with bcrypt
- JWT tokens with 24-hour expiry
- Protected API routes
- Input validation with Pydantic

## 📦 Dependencies

```
fastapi
uvicorn[standard]
sqlalchemy
pydantic[email]
pydantic-settings
python-jose[cryptography]
bcrypt==4.2.1
python-multipart
streamlit
requests
```

## 🎯 API Endpoints

### Auth
- `POST /register` — Register user
- `POST /login` — Login and get JWT token
- `GET /me` — Get current user profile

### Drivers
- `POST /driver/register` — Register driver
- `GET /driver/drivers` — List available drivers
- `GET /driver/all` — List all drivers
- `PUT /driver/status` — Toggle availability
- `GET /driver/{id}` — Get driver by ID

### Bookings
- `POST /book-driver` — Book driver (AI matching)
- `GET /booking/{id}` — Get booking details
- `GET /user/bookings` — Get user's booking history
- `PATCH /booking/{id}/complete` — Mark completed

## 📝 Notes

- Database file: `driver_app.db` (auto-created on first run)
- Sample drivers have phone numbers 9000000001-5 with password `driver123`
- Frontend stores JWT in Streamlit session state
- CORS enabled for local development

## 🎓 Final Year Project Checklist

- ✅ Complete working code
- ✅ AI/ML component (driver matching algorithm)
- ✅ Database with ORM
- ✅ Authentication system
- ✅ REST API with documentation
- ✅ Clean UI
- ✅ Production-ready structure
- ✅ Setup instructions
- ✅ Test data included

---

**Built with ❤️ for final year project submission**
