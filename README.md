# AIAG12: Automated Damage Assessment & Insurance Triage Agent System

## Overview
An AI-based multi-agent damage assessment system that analyzes imagery, estimates structural and financial damage, and assigns claims to priority categories for human verification.

## 🤖 Agentic Architecture

This system implements three specialized AI agents:

1. **Image Analysis Agent** - Interprets satellite/drone photos to identify damage types and severity
2. **Risk Assessment Agent** - Quantifies financial loss and assigns priority scores
3. **Audit Agent** - Validates outputs for consistency and flags anomalies

## 🚀 Features

- **Vision-based Damage Detection**: Upload property damage images for automated analysis
- **Multi-Agent Collaboration**: Agents work together to provide comprehensive assessments
- **Priority Triage**: Automatic claim categorization (Critical/High/Medium/Low)
- **Interactive Dashboard**: Real-time visualization of claim assessments
- **Human-in-the-Loop**: Final decisions augment AI recommendations

## 🛠️ Tech Stack

- **Frontend**: React + Vite + Tailwind CSS
- **Backend**: FastAPI (Python)
- **AI Framework**: Google Gemini 1.5 Pro (Vision + Text)
- **Deployment**: Vercel (Frontend) + Render (Backend)

## 📋 Project Structure

```
jones/
├── backend/
│   ├── app/
│   │   ├── agents/          # Multi-agent system
│   │   ├── models/          # Data models
│   │   └── routes/          # API endpoints
│   ├── requirements.txt
│   └── main.py
├── frontend/
│   ├── src/
│   │   ├── components/      # React components
│   │   ├── services/        # API client
│   │   └── App.jsx
│   └── package.json
└── README.md
```

## 🔧 Setup Instructions

### Backend Setup
```bash
cd backend
pip install -r requirements.txt
uvicorn main:app --reload
```

### Frontend Setup
```bash
cd frontend
npm install
npm run dev
```

### Environment Variables
Create a `.env` file in the backend directory:
```
GEMINI_API_KEY=your_gemini_api_key_here
```

## 🌐 Deployment

- **Frontend**: Deploy to Vercel using `vercel.json`
- **Backend**: Deploy to Render using `render.yaml`

## 📊 How It Works

1. User uploads damage imagery through the dashboard
2. **Image Analysis Agent** identifies damage patterns and severity
3. **Risk Assessment Agent** estimates financial impact and assigns priority
4. **Audit Agent** validates the assessment for consistency
5. Dashboard displays prioritized claim with recommendations
6. Human inspector reviews and finalizes the decision

## 🎯 Agentic Behavior Demonstration

The system showcases true agentic capabilities:
- **Autonomous Decision Making**: Each agent independently analyzes its domain
- **Tool Usage**: Agents use vision models, calculation tools, and validation logic
- **Multi-Agent Coordination**: Agents communicate and refine assessments
- **Reasoning**: Transparent thought process shown in agent logs

## � Getting Gemini API Key

1. Go to [Google AI Studio](https://makersuite.google.com/app/apikey)
2. Sign in with your Google account
3. Click "Get API Key" or "Create API Key"
4. Copy your API key and add it to the `.env` file

## �📝 License

MIT License - Built for AIAG12 Hackathon
