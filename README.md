# MeDo-hackathon-app
# Gigu&Me 🌥️

**An AI-powered emotional wellness and productivity companion for students.**

---

## What is Gigu&Me?

Gigu&Me is an all-in-one lifestyle tracker that helps students manage their emotional well-being, daily habits, and academic organization in a single privacy-first app. At the heart of the experience is **Gigu** — a cloud companion that reflects your emotions and guides you through your day.

---

## Features

- **Emotional Diary** — Log your daily mood, triggers, sleep, water, exercise, and daily purpose. Multiple entries per day supported.
- **Monthly Progress Ring** — A visual ring that fills day by day, colored by your dominant emotion for each day.
- **AI Insights** — Powered by Groq (llama-3.3-70b-versatile), analyzes your emotional patterns, diary entries, and personal goals to generate personalized daily recommendations.
- **Emotion Timeline** — Horizontal chart showing how your mood evolved throughout the day by hour.
- **Photo Gallery** — Upload and organize personal photos automatically sorted by week and year.
- **Smart Calendar** — Monthly and daily views with custom event categories and color classification.
- **Pomodoro Timer** — Built-in focus timer with Gigu animation cycles (concentrated → excited → calm) and session tracking integrated into Insights.
- **Insights Dashboard** — Weekly, monthly, and yearly statistics for emotions, sleep, water, exercise, and focus sessions.
- **8 Languages** — Full i18n support for English, Spanish, French, German, Portuguese, Italian, Japanese, and Chinese Simplified.
- **Dark & Light Mode** — Full theme support across all screens.
- **Demo Data** — New users get pre-loaded sample data to explore the app immediately after onboarding.

---

## Meet Gigu 🌥️

Gigu is the app's cloud companion with 8 emotional expressions that dynamically reflect the user's most recent mood:

| Expression | Mood |
|------------|------|
| 😊 Happy | Golden yellow |
| 😢 Sad | Soft blue |
| 😰 Anxious | Coral orange |
| 😌 Calm | Mint green |
| 😠 Angry | Soft red |
| 🤩 Excited | Vibrant purple |
| 😴 Tired | Teal |
| 🙏 Grateful | Pink |

Gigu appears across every screen with a unique contextual pose — holding a camera in Photos, wearing glasses in Calendar, holding a book during Pomodoro breaks, and more.

---

## Tech Stack

| Layer | Technology |
|-------|------------|
| Frontend | React + TypeScript |
| Styling | Tailwind CSS + shadcn/ui |
| Build Tool | Vite |
| Backend | Supabase (PostgreSQL) |
| Edge Functions | Deno |
| AI | Groq API (llama-3.3-70b-versatile) |
| Storage | localStorage (client-side) |
| i18n | Custom translation system |
| Platform | MeDo |

---

## AI Integration

The AI engine runs as a **Supabase Edge Function** on Deno. On first app load each day, the frontend sends the following data to the edge function:

- User profile (name, age, gender, occupation, goals)
- All emotions logged today and this week with timestamps
- Diary entries from this week with full text
- Sleep, water, and exercise data
- Completed Pomodoro sessions

The edge function calls the **Groq API** and returns a structured JSON response with a home tip and detailed insights. The response is cached in localStorage and shared between the Home screen and Insights dashboard — only one API call per day.

### Known Limitation
AI-generated content is currently delivered in English only. When the language parameter was passed to the model, it translated the JSON response keys alongside the content — breaking the frontend's data parser. The correct fix (Groq's structured JSON output mode with a strict schema) is planned for the next version.

---

## Architecture

```
src/
├── components/
│   ├── mascot/          # Gigu expressions and poses
│   ├── home/            # PhotoCarousel, MotivationalCard, EmotionQuickAdd, PomodoroSection
│   ├── diary/           # EmotionTimeline, ProgressRing, DailyEntry
│   ├── insights/        # EmotionWeekChart, StatCards, AIRecommendations
│   └── calendar/        # MonthView, DayView, EventForm
├── hooks/
│   └── useAppData.ts    # Central data layer — all localStorage operations
├── pages/               # Home, Diary, Calendar, Photos, Insights, Settings
├── i18n/
│   └── translations.ts  # All strings for 8 languages
supabase/
└── functions/
    └── ai-insights/     # Deno edge function — Groq API integration
```

---

## Getting Started

### Prerequisites
- Node.js 18+
- Supabase account
- Groq API key (free tier at [console.groq.com](https://console.groq.com))

### Installation

```bash
git clone https://github.com/your-username/giguandme
cd giguandme
npm install
```

### Environment Variables

```bash
VITE_SUPABASE_URL=your_supabase_url
VITE_SUPABASE_ANON_KEY=your_supabase_anon_key
```

### Supabase Edge Function Secret

```bash
supabase secrets set GROQ_API_KEY=your_groq_api_key
```

### Run locally

```bash
npm run dev
```

---

## What's Next

- Full multilingual AI responses using Groq's structured JSON output mode
- Secure backend with user authentication and cross-device sync
- Enhanced Gigu animations and interactive companion experience
- Meditation and calm spaces recommended by AI based on real-time mood patterns
- Apple Watch companion app

---

## Built With

Built entirely through conversational prompts with **[MeDo](https://medo.dev)** — from requirements to deployed production app in under a week.

---

## License

MIT

---

*Made with 💜 by Liss — UDLAP Systems Engineering Student*  
*Build with MeDo Hackathon 2026*
