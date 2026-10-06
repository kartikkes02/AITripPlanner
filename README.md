# AI TRIP PLANNER (TripNova)
## Technical Working Explanation & Project Roadmap

---

## 🛠️ PART 1: How the System Works (Technical Explanation for Evaluators)

When a professor asks: **"Explain how your system works step-by-step behind the scenes,"** use this detailed explanation:

```
┌─────────────────┐        1. POST /api/generate-trip        ┌──────────────────┐
│                 │ ───────────────────────────────────────► │                  │
│  React + Vite   │                                          │  FastAPI Backend │
│  Frontend (UI)  │ ◄─────────────────────────────────────── │  (Python Server) │
└─────────────────┘        6. Structured JSON Response       └────────┬─────────┘
                                                                      │
        ┌─────────────────────────────────────────────────────────────┼─────────────────────────────────────────────────────────────┐
        │ 2. Prompt Construction & LLM Call                           │ 3. Weather Fetching                                         │ 4. Database Persistence & Email
        ▼                                                             ▼                                                             ▼
┌───────────────────────────────┐                             ┌───────────────────────────────┐                             ┌───────────────────────────────┐
│ Google Gemini / Groq LLM API  │                             │      OpenWeather Map API      │                             │    MongoDB Atlas & Brevo API  │
│ (Generates Day-by-Day Plan)   │                             │   (Retrieves Forecast Data)   │                             │  (Saves Trip & Sends Email)   │
└───────────────────────────────┘                             └───────────────────────────────┘                             └───────────────────────────────┘
```

---

### Step-by-Step Technical Execution Flow

#### 1. User Input & Request Initiation (Frontend)
- The user fills out the trip form on the React SPA (Destination e.g., *"Tokyo"*, Duration e.g., *"5 Days"*, Budget e.g., *"Moderate"*, Interests e.g., *"Food, Culture"*).
- When the user clicks **"Generate Itinerary"**, React uses **Axios** to send an asynchronous `POST` HTTP request containing JSON data to the FastAPI backend endpoint (`/api/generate-trip`).

#### 2. Request Handling & Auth Verification (Backend API Gateway)
- The **FastAPI** server receives the request payload and validates the data structure using **Pydantic** models.
- If the route requires authentication, FastAPI checks the **JWT (JSON Web Token)** header or session cookie validated against **MongoDB Atlas**.

#### 3. AI Prompt Engineering & LLM Processing (Core AI Engine)
- The backend dynamically constructs a system-engineered prompt incorporating user constraints:
  > *"Act as an expert travel guide. Create a detailed 5-day trip itinerary for Tokyo under a Moderate budget focusing on Food and Culture. Return the response strictly as a structured JSON object containing daily activities, recommended places, estimated costs, and timing."*
- FastAPI sends this payload to the **Google Gemini API** (or **Groq API** as a high-speed fallback).
- Gemini returns a structured JSON payload detailing morning, afternoon, and evening activities for each day.

#### 4. Real-time External Data Augmentation
- **Weather Integration:** Simultaneously, FastAPI makes an asynchronous request to the **OpenWeather API** using the destination coordinates to retrieve live temperature, rainfall probability, and climate forecasts for those dates.
- **Location Discovery Fallback:** If specific venue coordinates or images are missing, FastAPI queries **SerpAPI / Tavily / Serper** to fetch verified Google Places information.

#### 5. Database Storage & Response Delivery
- FastAPI saves the generated itinerary, weather data, and user reference into **MongoDB Atlas**.
- The server sends a `200 OK` JSON response back to the React frontend.
- React updates its state and dynamically renders the itinerary UI, daily schedule cards, weather widgets, and interactive maps.

#### 6. Email Dispatch Service
- If the user clicks **"Send to Email"**, FastAPI calls the **Brevo API** (or SMTP service) to format the itinerary as an HTML document and dispatch it directly to the user's registered email address.

---

## 🔐 PART 2: How Authentication & Security Work

- **Social Login (OAuth 2.0):** Users can authenticate using Google, GitHub, or LinkedIn. The frontend redirects to the OAuth provider, receives an authorization code, exchanges it via FastAPI for user profile details, and issues a secure JWT token.
- **OTP Email Verification:** For standard email registration, FastAPI generates a random 6-digit One-Time Password (OTP), stores it temporarily with an expiration timestamp in MongoDB, and mails it to the user via Brevo SMTP. Once verified, account creation completes.

---

## 🗺️ PART 3: Project Development Roadmap (Timeline)

If your teacher asks for the **Implementation Phases / Development Roadmap**, present these 6 structured phases:

```
Phase 1: Requirements & Design  ──►  Phase 2: Backend & Database Setup  ──►  Phase 3: AI & API Integration
                                                                                       │
Phase 6: Deployment & Hosting   ◄──  Phase 5: Testing & Security Verification ◄── Phase 4: Frontend Development
```

### 🗓️ Phase 1: Requirement Analysis & Architectural Design
- Defined problem statement, user personas, and core functional requirements.
- Selected tech stack: React + Vite (Frontend), FastAPI + Python (Backend), MongoDB (Database).
- Created system architecture, sequence diagrams, and REST API specification endpoints.

### 🗓️ Phase 2: Backend Development & Database Schema Setup
- Setup FastAPI project structure with Uvicorn server.
- Designed MongoDB Atlas schemas for Users, Saved Itineraries, Auth Sessions, and OTP logs.
- Developed JWT-based session management and OAuth 2.0 integrations (Google, GitHub, LinkedIn).

### 🗓️ Phase 3: AI Engine & External API Integration
- Integrated Google Gemini API and Groq LLM API for natural language itinerary generation.
- Designed system prompt templates to enforce structured JSON output formats from LLMs.
- Connected OpenWeather API for real-time climate forecasting and SerpAPI/Tavily for Google Places fallback search.

### 🗓️ Phase 4: Frontend UI/UX Development
- Created single-page application structure using React.js and Vite.
- Implemented client-side routing using `react-router-dom` and state management.
- Designed dynamic forms for preference entry, interactive itinerary display cards, weather widgets, and AI chatbot drawer.

### 🗓️ Phase 5: Testing, Security & Optimization
- Conducted unit testing and API route validation using Postman.
- Configured CORS (Cross-Origin Resource Sharing) policies in FastAPI to protect backend endpoints.
- Optimised LLM request latency and structured fallback mechanisms to ensure 99.9% API uptime.

### 🗓️ Phase 6: Cloud Deployment & Final Delivery
- Deployed React Frontend to **Netlify** and **Vercel** with automatic CI/CD deployment pipelines.
- Deployed FastAPI Backend to **Render** web services connected to MongoDB Atlas cloud database.
- Performed end-to-end integration testing and prepared college minor project documentation and presentation deck.
