# react-pmcopilot
Berikut repository berisi readme.md untuk mereplikasi langkah-langkah pembuatan frontend

# PM Copilot Frontend

[![React](https://img.shields.io/badge/React-18+-61DAFB.svg)](https://reactjs.org/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.0+-blue.svg)](https://www.typescriptlang.org/)
[![Vite](https://img.shields.io/badge/Vite-5.0+-646CFF.svg)](https://vitejs.dev/)

Modern web application untuk **Predictive Maintenance Copilot** - monitoring kesehatan mesin industri real-time dengan AI-powered chatbot assistant.

##  Deskripsi

PM Copilot Frontend adalah dashboard interaktif yang memvisualisasikan data sensor mesin, prediksi ML, dan maintenance tickets secara real-time. Dilengkapi dengan AI chatbot untuk membantu engineer dalam diagnosis dan decision-making.

##  Fitur Utama

### 1. **Dashboard Overview**
- Real-time metrics (20 mesin, prediksi aktif, open tickets)
- Quick preview active predictions & urgent tickets
- Color-coded status indicators

### 2. **Machine Monitoring**
- Grid view 20 mesin dengan filter (All, Normal, Predictions, Maintenance)
- Live sensor data: Temperature, RPM, Torque, Tool Wear
- Search & real-time status updates

### 3. **Predictions Page**
- Detailed failure predictions dengan countdown
- AI-generated recommendations
- Direct link ke maintenance tickets
- Critical/Urgent severity indicators

### 4. **Ticket Management**
- Open/History tabs
- Priority badges (Urgent, High, Medium, Low)
- AI-generated ticket content dalam Bahasa Indonesia
- Timestamp tracking

### 5. **AI Copilot (Chatbot)**
- Floating action button (always accessible)
- Session-based conversations
- Suggested prompts untuk quick actions
- Context-aware responses

### 6. **Settings**
- Dark/Light mode toggle
- Notification preferences (Predictions, Tickets, Maintenance)
- User customization

##  Tech Stack

```json
{
  "runtime": "Node.js 18+",
  "framework": "React 18+",
  "language": "TypeScript",
  "buildTool": "Vite 5.0+",
  "styling": "CSS Modules / Tailwind CSS",
  "icons": "Lucide React",
  "stateManagement": "React Context / Zustand",
  "http": "Axios",
  "realtime": "Socket.IO Client",
  "routing": "React Router v6",
  "deployment": "Vercel"
}
