# AITripPlanner
#- Created system architecture, sequence diagrams, and REST API specification endpoints.
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
