# AIAG12 Setup Guide

## Quick Start

### Prerequisites
- Python 3.11+
- Node.js 18+
- Google Gemini API Key (get from https://makersuite.google.com/app/apikey)

### Backend Setup

1. Navigate to backend directory:
```bash
cd backend
```

2. Create virtual environment:
```bash
python -m venv venv
# Windows
venv\Scripts\activate
# Mac/Linux
source venv/bin/activate
```

3. Install dependencies:
```bash
pip install -r requirements.txt
```

4. Create `.env` file:
```bash
cp .env.example .env
```

5. Add your Gemini API key to `.env`:
```
GEMINI_API_KEY=your-gemini-key-here
```

Get your Gemini API key from: https://makersuite.google.com/app/apikey

6. Run the backend:
```bash
uvicorn main:app --reload
```

Backend will run at `http://localhost:8000`

### Frontend Setup

1. Navigate to frontend directory:
```bash
cd frontend
```

2. Install dependencies:
```bash
npm install
```

3. Create `.env` file:
```bash
cp .env.example .env
```

4. Update `.env` if needed (default points to localhost:8000):
```
VITE_API_URL=http://localhost:8000
```

5. Run the frontend:
```bash
npm run dev
```

Frontend will run at `http://localhost:3000`

## Testing the Application

1. Open `http://localhost:3000` in your browser
2. Upload a property damage image (you can use sample images of damaged buildings)
3. Select property type (residential/commercial/industrial)
4. Click "Run Multi-Agent Assessment"
5. Watch the multi-agent system analyze the damage:
   - **Image Analysis Agent** identifies damage types and severity
   - **Risk Assessment Agent** estimates financial loss and priority
   - **Audit Agent** validates consistency
6. View the comprehensive assessment results with agent reasoning

## Using Sample Images

For testing, you can use:
- Google Images: Search for "storm damaged house" or "hurricane damage"
- Free stock photos from Unsplash/Pexels
- Any image showing building damage (roof damage, structural damage, flood damage, etc.)

## Deployment

### Deploy Frontend to Vercel

1. Install Vercel CLI:
```bash
npm i -g vercel
```

2. From frontend directory:
```bash
vercel
```

3. Follow prompts and deploy
4. Update `VITE_API_URL` in Vercel environment variables to point to your backend URL

### Deploy Backend to Render

1. Create account at https://render.com
2. Connect your GitHub repository
3. Create new Web Service
4. Point to `backend` directory
5. Add environment variable `OPENAI_API_KEY`
6. Deploy!

Alternatively, use the `render.yaml` file for one-click deploy.

## Architecture

### Multi-Agent System Flow

```
User Upload Image
    ↓
[Image Analysis Agent - GPT-4 Vision]
    ↓ (damage analysis)
[Risk Assessment Agent - GPT-4]
    ↓ (financial + priority)
[Audit Agent - GPT-4]
    ↓ (validation)
Orchestrator
    ↓
Dashboard Display
```

### Agent Descriptions

**Image Analysis Agent:**
- Uses Gemini 1.5 Pro Vision
- Identifies damage types (structural, roof, water, fire, etc.)
- Scores severity 0-10
- Lists affected areas
- Provides confidence score

**Risk Assessment Agent:**
- Receives image analysis
- Uses Gemini 1.5 Pro for financial analysis
- Estimates repair costs in USD
- Assigns priority (Critical/High/Medium/Low)
- Calculates urgency and displacement risk
- Estimates repair timeline

**Audit Agent:**
- Uses Gemini 1.5 Pro for validation
- Validates consistency between agents
- Flags anomalies (severity-cost mismatches, etc.)
- Provides quality score
- Makes final recommendations

**Orchestrator:**
- Coordinates agent workflow
- Manages inter-agent communication
- Synthesizes final assessment
- Generates next steps for human inspectors

## API Endpoints

### `POST /assess-damage`
Upload damage image for assessment

**Parameters:**
- `file`: Image file (multipart/form-data)
- `property_type`: residential/commercial/industrial
- `claim_id`: Optional claim identifier

**Returns:**
- Complete `ClaimAssessment` object with all agent outputs

### `GET /health`
Health check endpoint

### `GET /`
API info

## Troubleshooting

**Backend won't start:**
- Ensure Python 3.11+ installed
- Check virtual environment is activated
- Verify all dependencies installed: `pip install -r requirements.txt`

**Frontend won't start:**
- Ensure Node.js 18+ installed
- Delete `node_modules` and reinstall: `rm -rf node_modules && npm install`

**API errors:**
- Check GEMINI_API_KEY is set correctly in backend `.env`
- Verify Gemini API key is valid (get from https://makersuite.google.com/app/apikey)
- Gemini API is free for testing with rate limits
- Check CORS settings in `main.py` if frontend on different domain

**Image upload fails:**
- Ensure file is valid image format (PNG, JPG, etc.)
- Check file size (recommend < 5MB)

## Demo Tips

For the best demo experience:

1. Use clear, high-quality damage images
2. Show variety: minor damage vs severe damage
3. Demonstrate different damage types (roof, structural, flood)
4. Show the agent reasoning section to highlight agentic behavior
5. Point out the multi-agent collaboration metrics
6. Explain how each agent has a specialized role

## License

MIT License - Built for AIAG12 Hackathon
