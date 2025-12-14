# react-pmcopilot
Berikut repository berisi readme.md untuk mereplikasi langkah-langkah pembuatan frontend

# PM Copilot Frontend

[![React](https://img.shields.io/badge/React-18+-61DAFB.svg)](https://reactjs.org/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.0+-blue.svg)](https://www.typescriptlang.org/)
[![Vite](https://img.shields.io/badge/Vite-5.0+-646CFF.svg)](https://vitejs.dev/)

Modern web application untuk **Predictive Maintenance Copilot** - monitoring kesehatan mesin industri dengan AI-powered chatbot assistant.

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
```

##  Installation

### Prerequisites

```bash
Node.js >= 18.0.0
npm >= 9.0.0
```

### Setup Steps

1. **Clone repository**


2. **Setup environment variables**
```bash
cp .env.example .env
```
3. **Setup environment variables**

Edit `.env`:
```env
VITE_API_BASE_URL=http://localhost:3000
VITE_SOCKET_URL=http://localhost:3000
VITE_APP_NAME=PM Copilot
```
4. **Start development server**
```bash
npm run dev
```

App akan berjalan di `http://localhost:5173`

##  Project Structure

```
src/
├── assets/                 # Images, fonts, etc
├── components/
│   ├── common/            # Reusable components
│   │   ├── Button/
│   │   ├── Card/
│   │   ├── Badge/
│   │   ├── Modal/
│   │   └── Loader/
│   ├── layout/            # Layout components
│   │   ├── Sidebar/
│   │   ├── Navbar/
│   │   └── Container/
│   ├── machine/           # Machine-related components
│   │   ├── MachineCard/
│   │   ├── MachineGrid/
│   │   └── SensorDisplay/
│   ├── prediction/        # Prediction components
│   │   ├── PredictionCard/
│   │   └── CountdownTimer/
│   ├── ticket/            # Ticket components
│   │   ├── TicketCard/
│   │   └── TicketList/
│   └── chatbot/           # Chatbot components
│       ├── ChatBubble/
│       ├── ChatInput/
│       └── ChatSidebar/
├── pages/
│   ├── Landing/           # Marketing landing page
│   ├── Dashboard/
│   │   ├── Overview/
│   │   ├── Machines/
│   │   ├── Predictions/
│   │   ├── Tickets/
│   │   └── Settings/
│   └── NotFound/
├── hooks/                 # Custom React hooks
│   ├── useMachines.ts
│   ├── usePredictions.ts
│   ├── useTickets.ts
│   ├── useSocket.ts
│   └── useChat.ts
├── services/              # API services
│   ├── api.ts            # Axios instance
│   ├── machineService.ts
│   ├── ticketService.ts
│   └── chatService.ts
├── context/               # React Context
│   ├── ThemeContext.tsx
│   ├── NotificationContext.tsx
│   └── AuthContext.tsx
├── utils/                 # Utility functions
│   ├── formatters.ts     # Date, number formatters
│   ├── constants.ts      # App constants
│   └── helpers.ts
├── types/                 # TypeScript types
│   ├── machine.ts
│   ├── prediction.ts
│   ├── ticket.ts
│   └── chat.ts
├── App.tsx               # Root component
├── main.tsx              # Entry point
└── vite-env.d.ts
```

##  Component Library

### Machine Components
```typescript
<MachineCard 
  machineId="L_001"
  status="normal"
  sensorData={{...}}
  onClick={handleClick}
/>

<MachineGrid 
  machines={machines}
  filter="predictions"
/>
```

### Prediction Components
```typescript
<PredictionCard
  prediction={prediction}
  onViewTicket={handleView}
/>

<CountdownTimer
  targetDate={forecastTimestamp}
  urgency="critical"
/>
```

### Ticket Components
```typescript
<TicketCard
  ticket={ticket}
  onStatusChange={handleChange}
/>
```

### Chatbot Components
```typescript
<ChatSidebar
  isOpen={isOpen}
  onClose={handleClose}
/>

<ChatBubble
  message="Status mesin H_001?"
  sender="user"
/>
```

##  API Integration

### Axios Configuration

```typescript
// services/api.ts
import axios from 'axios';

const api = axios.create({
  baseURL: import.meta.env.VITE_API_BASE_URL,
  timeout: 10000,
});

// Request interceptor
api.interceptors.request.use((config) => {
  const token = localStorage.getItem('token');
  if (token) config.headers.Authorization = `Bearer ${token}`;
  return config;
});

// Response interceptor
api.interceptors.response.use(
  (response) => response.data,
  (error) => {
    // Handle errors
    return Promise.reject(error);
  }
);

export default api;
```

### Socket.IO Integration

```typescript
// hooks/useSocket.ts
import { useEffect } from 'react';
import { io } from 'socket.io-client';

export const useSocket = () => {
  useEffect(() => {
    const socket = io(import.meta.env.VITE_SOCKET_URL);
    
    socket.on('prediction:new', (data) => {
      // Update UI
    });
    
    socket.on('ticket:created', (data) => {
      // Show notification
    });
    
    return () => socket.disconnect();
  }, []);
};
```

##  Custom Hooks

### useMachines Hook

```typescript
export const useMachines = (filter?: string) => {
  const [machines, setMachines] = useState([]);
  const [loading, setLoading] = useState(true);
  
  useEffect(() => {
    fetchMachines(filter)
      .then(setMachines)
      .finally(() => setLoading(false));
  }, [filter]);
  
  return { machines, loading, refetch };
};
```

### useChat Hook

```typescript
export const useChat = () => {
  const [messages, setMessages] = useState([]);
  const [loading, setLoading] = useState(false);
  
  const sendMessage = async (text: string) => {
    setLoading(true);
    const response = await chatService.send(text);
    setMessages([...messages, response]);
    setLoading(false);
  };
  
  return { messages, sendMessage, loading };
};
```

##  Styling

### Color System

```css
/* Dark Theme (Default) */
:root {
  --color-primary: #00D9FF;
  --color-secondary: #14B8A6;
  --color-background: #0A1929;
  --color-surface: #1A2332;
  --color-success: #22C55E;
  --color-warning: #F59E0B;
  --color-danger: #EF4444;
  --color-text: #F8FAFC;
  --color-text-muted: #94A3B8;
}
```

### Responsive Breakpoints

```css
/* Tailwind-style breakpoints */
sm: 640px   /* Mobile landscape */
md: 768px   /* Tablet */
lg: 1024px  /* Desktop */
xl: 1280px  /* Large desktop */
```

##  Routes

```typescript
/                           → Landing Page
/dashboard                  → Redirect to /dashboard/overview
/dashboard/overview         → Dashboard Overview
/dashboard/machines         → Machines Grid
/dashboard/predictions      → Predictions List
/dashboard/tickets          → Tickets Management
/dashboard/settings         → User Settings
```

## 🧪 Testing

### Run Tests

```bash
npm run test
```

### E2E Testing

```bash
npm run test:e2e
```

##  Build & Deploy

### Production Build

```bash
npm run build
```

Output: `dist/` folder

### Preview Production Build

```bash
npm run preview
```

### Deploy to Vercel

```bash
vercel --prod
```


### Design System

```
Color Palette:         9 semantic colors
Typography Scales:     5 levels (12px - 48px)
Spacing System:        8px base unit
Border Radius:         4 variants (4px, 8px, 12px, full)
Shadow Depths:         3 levels
Animation Easing:      Custom cubic-bezier
Icon Set:              50+ icons (Lucide React)
```

### Debug Mode

```bash
# Enable verbose logging
VITE_DEBUG=true npm run dev

# Check build analysis
npm run build -- --mode analyze
```



