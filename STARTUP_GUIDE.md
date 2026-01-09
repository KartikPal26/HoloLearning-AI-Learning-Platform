# 🚀 HoloLearning Startup Guide

## Quick Start - Run Both Frontend & Backend Together

### Prerequisites
- Python 3.8+ installed
- Node.js & npm installed
- Virtual environment created and activated (for Python)
- `.env` file with `CEREBRAS_API_KEY` set

### Step 1: Install Dependencies

**Install Node packages (one time):**
```bash
npm install
```

**Install Python packages (in virtual environment):**
```bash
pip install -r requirements.txt
```

### Step 2: Run Everything with One Command

```bash
npm run dev
```

This will automatically start:
- 🐍 **Backend** (Flask server on http://localhost:5000)
- ⚛️ **Frontend** (React app on http://localhost:3000)

Both will run in the same terminal with color-coded output.

---

## Alternative: Run Separately

### Run Only Backend
```bash
python main.py
```
Server runs on: `http://localhost:5000`

### Run Only Frontend
```bash
npm start
```
App runs on: `http://localhost:3000`

---

## How It Works

The `npm run dev` command uses **concurrently** package to:
1. Spawn Python process running `main.py` (backend)
2. Spawn Node process running `npm start` (frontend)
3. Run both simultaneously in one terminal
4. Stop both when you press `Ctrl+C`

---

## Environment Variables

Create a `.env` file in the project root with:
```
CEREBRAS_API_KEY=your_api_key_here
REACT_APP_API_URL=http://localhost:5000
```

---

## Troubleshooting

**Port already in use?**
- Change Flask port: Edit `main.py` and add `app.run(port=5001)`
- Change React port: Run `PORT=3001 npm start`

**Python not found?**
- Use full path: `C:\path\to\venv\Scripts\python main.py`
- Or ensure virtual environment is activated

**Backend not responding?**
- Check if `CEREBRAS_API_KEY` is set in `.env`
- Verify Flask is printing initialization messages

