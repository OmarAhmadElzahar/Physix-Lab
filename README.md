# PhysiX Lab (مختبر الميكانيكا)

**PhysiX Lab** is a production-grade, commercial EdTech SaaS and Interactive Physics Simulation Platform built with a vector-grid blueprint aesthetic, FastAPI backend, and dual-mode database persistence (Supabase PostgreSQL / local SQLite).

---

## 🚀 Key Platform Features

### 1. Interactive Vector Simulation Engine
- **Crisp Vector Grid Aesthetic**: Engineering paper (`#f2f5ef`) and Dark Blueprint (`#121a2e`) with real-time vector arrows, axis rulers, and HUD telemetry.
- **Bilingual Interface**: One-click instant switching between English (LTR) and Arabic (RTL) with localized terminology.
- **3-Star Mastery System**: 3 progressive challenge levels across 6 core curriculum modules:
  1. **Newton's Laws (`قوانين نيوتن`)**: Box mass $m$, applied force $F$, track distance $D$, live acceleration $a = F/m$, and arrival time tolerance window.
  2. **Vectors & Resultant (`المتجهات والمحصلة`)**: Interactive forces $F_1, F_2$, component projections ($R_x, R_y$), and resultant vector $R$ targeting precision circular sensors.
  3. **Force Equilibrium (`اتزان القوى`)**: Multi-force particle balance ($\Sigma F_x = 0, \Sigma F_y = 0$).
  4. **Projectile Motion (`المقذوفات والتسارع`)**: Launch velocity $v_0$, angle $\theta$, apex marker, parabolic trail, and ground landing zone.
  5. **Inclined Plane & Friction (`السطح المائل والاحتكاك`)**: Ramp angle $\theta$, static/kinetic friction ($\mu_s, \mu_k$), with live vector decomposition arrows ($N$, $mg\sin\theta$, $mg\cos\theta$, $f_k$) and slip condition detection ($\tan\theta > \mu_s$).
  6. **Collisions & Momentum (`التصادم وكمية الحركة`)**: Linear track carts with masses $m_1, m_2$, velocities $v_1, v_2$, and restitution coefficient $e$ pushing mass into sensor pads.
- **Live Telemetry Charts**: Real-time velocity vs. time ($v-t$) and displacement vs. time ($s-t$) plotted synchronously below the simulation.

### 2. Smart Inverse & Forward Equation Solver
- Select any mechanics topic (Kinematics, Projectiles, Inclined Plane, Vectors, Momentum).
- Enter known variables and leave **any unknown variable blank**.
- The solver algebraically isolates the unknown, displays step-by-step mathematical derivations, and allows one-click loading into the live simulation.

### 3. AI Physics Tutor & Vision Scanner
- **Step-by-Step AI Professor**: Analyzes student parameters, explains physical laws, calculates numerical derivations, warns against common misconceptions, and gives tips.
  - Powered by Gemini 2.5 Flash via `google-genai` (with intelligent built-in pedagogical solver fallback when no API key is provided).
- **Snap & Simulate (Vision OCR)**: Upload or drag & drop an image of a textbook mechanics problem to extract parameters and populate the Smart Solver.

### 4. B2B Instructor Portal & Anti-Cheat Lab Exams
- **Frictionless Login & Auto-Resume**: Enter institutional email, full name, and role (`Student` or `Instructor`). Progress and mastery stars are preserved permanently.
- **Anti-Cheat Lab Sheet Generator**: Instructors generate unique exam codes (e.g., `MECH-2026`). Each student receives deterministic randomized numerical parameters generated from their email seed.
- **Cohort Analytics & Weak-Spot Detection**: Visual error breakdown identifying curriculum topics needing reinforcement.
- **One-Click CSV / Excel Export**: UTF-8 BOM formatted grade rosters compatible with Excel.

---

## 🛠️ Architecture & Dual-Mode Persistence

```
Physix-Lab/
├── api/
│   └── index.py            # FastAPI backend with dual-mode Supabase/SQLite persistence
├── public/
│   ├── index.html          # HTML5 Canvas vector simulation UI
│   ├── style.css           # High-contrast grid paper & blueprint styling (RTL/LTR)
│   └── app.js              # Simulation loop, telemetry plotter, i18n & state sync
├── requirements.txt        # Backend dependencies
├── vercel.json             # Vercel serverless routing configuration
├── .env.example            # Environment variables template
└── physix_lab.db           # Persistent local SQLite database
```

### Dual-Mode Database Support:
- **Local Out-of-the-Box**: Works 100% locally with zero setup using SQLite (`physix_lab.db`).
- **Cloud Production**: Automatically connects to Supabase PostgreSQL when `SUPABASE_URL` and `SUPABASE_KEY` are provided in `.env`.

---

## 💻 Local Setup & Execution

1. **Install dependencies**:
   ```bash
   pip install -r requirements.txt
   ```

2. **Configure environment (Optional)**:
   ```bash
   cp .env.example .env
   # Add your GEMINI_API_KEY or SUPABASE credentials if desired
   ```

3. **Start the local server**:
   ```bash
   uvicorn api.index:app --reload --host 127.0.0.1 --port 8000
   ```

4. **Access the application**:
   Open [http://localhost:8000](http://localhost:8000) in your web browser.

---

## ☁️ Vercel Deployment

Deploy directly using the Vercel CLI or Git repository integration:
```bash
vercel deploy --prod
```
The included `vercel.json` routes `/api/*` requests to the serverless Python FastAPI handler in `api/index.py` and serves static files from `public/`.
