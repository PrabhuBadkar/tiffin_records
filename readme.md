# Tiffin Tracker

**A simple, multilingual tiffin delivery management application for low-literacy users.**

---

## 📂 Project Structure
```text
├── backend
│   ├── Dockerfile
│   ├── requirements.txt
│   ├── app
│   │   ├── main.py
│   │   ├── models.py
│   │   ├── schemas.py
│   │   ├── crud.py
│   │   └── database.py
│   └── README.md        ← Backend-specific instructions
└── frontend
    ├── package.json
    ├── vite.config.js
    ├── tailwind.config.js
    ├── public
    │   └── index.html
    ├── src
    │   ├── App.jsx
    │   ├── main.jsx
    │   └── components
    │       ├── CustomerForm.jsx
    │       ├── DeliveryScreen.jsx
    │       └── BillingSummary.jsx
    └── README.md        ← Frontend-specific instructions

# README.md          ← Global overview & deployment guide
```

---

## README.md

### 📖 Overview
`Tiffin Tracker` is a full-stack web application designed to help small-scale tiffin vendors (especially those with limited literacy and tech exposure) manage:

- **Customer records** (name, address, custom rate per tiffin)  
- **Daily deliveries** (number of tiffins delivered per customer)  
- **Monthly billing** (auto-calculation of totals)  
- **Payment tracking** (paid/unpaid statuses)

The app uses **voice input**, **icon-driven UIs**, and **multilingual support** to minimize text dependence.

### 🔧 Tech Stack
| Layer      | Technology               |
|------------|--------------------------|
| Backend    | FastAPI, Python, SQLite  |
| Frontend   | React, Vite, TailwindCSS |
| Container  | Docker                   |
| Deployment | Render (backend), Vercel (frontend) |

---

## 🛠️ Getting Started

### Prerequisites
- Node.js ≥ 18, npm
- Python ≥ 3.10
- Docker & Docker CLI
- Git

Clone the repo:
```bash
git clone https://github.com/your-org/tiffin-tracker.git
cd tiffin-tracker
```

---

## 🚀 Backend Setup (Render)

1. **Navigate to the `backend` folder**
   ```bash
   cd backend
   ```

2. **Configure environment (optional)**
   - The default uses `sqlite://./tiffin.db`.
   - To switch to PostgreSQL, set `SQLALCHEMY_DATABASE_URL` in `app/database.py` or via env var `DATABASE_URL`.

3. **Render Deployment**
   - Push your backend Dockerfile to GitHub.
   - In Render dashboard, create a **Web Service**:
     - Connect your repo, choose the `backend/` folder.
     - Build command: **none** (Dockerfile used).
     - Start command: `uvicorn app.main:app --host 0.0.0.0 --port $PORT`.
     - Set env var `PORT` = `10000` (or leave default 10000).

4. **Health Check**
   - After deploy, visit `https://<your-backend>.onrender.com/docs` to view FastAPI Swagger UI.

---

## 🚀 Frontend Setup (Vercel)

1. **Navigate to the `frontend` folder**
   ```bash
   cd frontend
   ```

2. **Install dependencies & run locally**
   ```bash
   npm install
   npm run dev            # http://localhost:5173
   ```

3. **Update API endpoint**
   - In `src/crud.js` (create if needed), set:
     ```js
     export const API_URL = 'https://<your-backend>.onrender.com';
     ```

4. **Deploy on Vercel**
   - Push to GitHub.
   - In Vercel, import the repo, select `frontend/` as root.
   - Build command: `npm run build`.
   - Output directory: `dist`.

5. **Post-Deployment**
   - Visit `https://<your-frontend>.vercel.app` to interact with the app.

---

## 🌐 Usage Flow

1. **Add Customer**: Set name (voice or typing), address (optional), and ₹ per tiffin.  
2. **Record Deliveries**: Each morning, select the number of tiffins for each customer and tap “Deliver.”  
3. **View Billing Summary**: At month's end, view total tiffins × rate for each customer.  
4. **Track Payments**: Mark paid/unpaid statuses and view outstanding balances.

---

## 🔊 Voice + Localization
- Integrates the **Web Speech API** for Hindi/Regional language prompts.  
- UI labels sourced from `public/locales/{hi,en}.json`.  
- Fallback to icons for core actions (➕, 📦, 💰).

---

## 📝 File Details

- **backend/app/**: Contains all FastAPI code & SQLAlchemy models.  
- **frontend/src/components/**: React components for form input, delivery tracking, and billing.  
- **Dockerfile**: Production container for backend.  

---

## 🤝 Contributing
Pull requests welcome! For major changes, open an issue first to discuss.

---

## 🎁 A Gift to Our Hero
This solution is open-source and forever **free** for our tiffin-selling entrepreneur. 🌟

Thank you for empowering local businesses! ❤️
