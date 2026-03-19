# 🥗 NutriSnap — Smart Nutrition Tracker

<div align="center">

![NutriSnap Banner](https://img.shields.io/badge/NutriSnap-v1.0.0-FF3B30?style=for-the-badge&logo=leaf&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-22C55E?style=for-the-badge)
![HTML](https://img.shields.io/badge/HTML-Single%20File-3B82F6?style=for-the-badge&logo=html5&logoColor=white)
![No Backend](https://img.shields.io/badge/Backend-None%20Required-8B5CF6?style=for-the-badge)
![Offline](https://img.shields.io/badge/Works-Offline-F59E0B?style=for-the-badge)

**A premium, production-grade nutrition tracker for students and hostel life.**  
Track meals · Monitor macros · Stay hydrated · Get smart food suggestions

[Live Demo](#) · [Documentation](./DOCS.docx) · [Report Bug](../../issues) · [Request Feature](../../issues)

</div>

---

## 📸 Overview

NutriSnap is a fully self-contained, single-file web application that runs entirely in the browser — no backend, no login, no internet connection required after the first load. Built for Indian hostel students and busy people who want a premium nutrition tracking experience without complexity.

```
nutrisnap.html  ← The entire app lives here (1 file, ~1400 lines)
```

---

## ✨ Features

| Feature | Description |
|---|---|
| 🍽 **Meal Tracker** | Log Breakfast, Lunch, Dinner & Snacks with serving size control |
| 🔥 **Calorie Ring** | Animated SVG progress ring — live calorie goal tracking |
| 📊 **Macro Donut** | Real-time protein / carbs / fat donut chart |
| 💧 **Water Tracker** | Glass-by-glass hydration tracking with visual feedback |
| 🧠 **Smart Suggestions** | Rule-based AI-like food recommendations based on your intake |
| 📅 **Weekly History** | 7-day bar chart with water intake sub-chart |
| ⚙️ **Goal Settings** | Custom calorie, protein & water goals with 4 goal types |
| 🌙 **Dark Mode** | Smooth light/dark toggle, persisted across sessions |
| 📱 **Responsive** | Works beautifully on mobile and desktop |
| 💾 **Offline First** | Full localStorage persistence, in-memory fallback |

---

## 🗃 Food Database

> **232+ curated Indian foods** — no duplicates, no fake data, all realistic values.

| Category | Count | Examples |
|---|---|---|
| 🌅 Breakfast | 30 | Poha, Upma, Idli, Dosa, Paratha, Omelette, Oats |
| ☀️ Lunch | 30 | Dal Chawal, Rajma Rice, Biryani, Chapati + Sabzi |
| 🌙 Dinner | 23 | Dal Tadka, Paneer Bhurji, Chicken Curry, Fish Fry |
| 🍎 Snacks | 29 | Samosa, Vada Pav, Roasted Chana, Sprouts, Bhel Puri |
| 🍇 Fruit | 15 | Banana, Apple, Papaya, Mango, Guava, Pomegranate |
| 💪 Protein | 19 | Curd, Paneer, Eggs, Chicken, Tofu, Dal, Sprouts |
| ☕ Beverage | 13 | Masala Chai, Lassi, Nimbu Pani, Coconut Water |
| 🍬 Others | 32+ | Sweets, Breads, Regional Specials |

Every item includes: `name · calories · protein · carbs · fat · serving size · tags`

---

## 🚀 Quick Start

### Option 1 — Direct Download

```bash
# Clone the repo
git clone https://github.com/yourusername/nutrisnap.git

# Open in browser — that's it!
open nutrisnap.html
```

### Option 2 — GitHub Pages

1. Fork this repo
2. Go to **Settings → Pages**
3. Set source to **main branch / root**
4. Your app is live at `https://yourusername.github.io/nutrisnap/`

### Option 3 — Raw File

Download `nutrisnap.html` → double-click → runs instantly.

> ✅ No `npm install` · No build step · No server · No API key

---

## 🏗 Architecture

```
nutrisnap.html
│
├── 📐 HTML Structure
│   ├── <nav>           Navigation bar with theme toggle
│   ├── <section.hero>  Landing hero section
│   └── <div.app>       Main dashboard (2-column grid)
│       ├── Left Column
│       │   ├── Calorie Ring Card
│       │   ├── Macro Donut Card
│       │   ├── Water Tracker Card
│       │   └── Goals Card
│       └── Right Column
│           ├── Daily Totals Bar
│           ├── Meals Card (tabbed)
│           ├── Smart Suggestions Card
│           └── Weekly History Chart
│
├── 🎨 CSS (~400 lines)
│   ├── CSS Custom Properties (light/dark theme variables)
│   ├── Layout (CSS Grid + Flexbox)
│   ├── Animation System (keyframes + transitions)
│   └── Component Styles (cards, buttons, inputs)
│
└── ⚙️ JavaScript (~500 lines)
    ├── FOOD_DB[]       Hardcoded food database (232+ items)
    ├── storage{}       localStorage wrapper with in-memory fallback
    ├── state{}         App state (meals, water, goals, history)
    ├── Render fns      renderCalorieRing(), renderMacros(), etc.
    ├── Action fns      addFood(), removeFood(), updateServings()
    └── Utilities       showToast(), saveState(), getRecommendations()
```

---

## 🔄 User Flow

```
Open App
    │
    ▼
Set Goals (optional)
[Fat Loss / Maintenance / Muscle Gain / Wellness]
[Calorie Goal] [Protein Goal] [Water Goal]
    │
    ▼
Log Meals
[Search Food by Name] → [Select Item] → [Adjust Servings] → [Added to Meal]
    │
    ├──► Calorie Ring updates instantly
    ├──► Macro Donut updates instantly
    ├──► Daily Totals Bar updates instantly
    └──► Smart Suggestions refresh
    │
    ▼
Track Water
[Tap Glass Icons] or [+ Add Glass Button]
    │
    ▼
View Weekly Progress
[7-Day Bar Chart] [Water Sub-chart]
    │
    ▼
Data Auto-saved to localStorage
    │
    ▼
Next Day → Previous day saved to history, fresh slate begins
```

---

## 🧠 Recommendation Engine Logic

```
computeTotals()
      │
      ├── calories > 110% of goal ──────► Suggest LOW-CALORIE items (<100 kcal)
      │
      ├── protein deficit > 20g ─────────► Suggest HIGH-PROTEIN items (>10g protein)
      │
      ├── calories remaining > 600 ──────► Suggest FILLING & BALANCED meals
      │
      ├── calories remaining 200-600 ────► Suggest MODERATE snacks
      │
      ├── goal type = muscle-gain ───────► Always prioritize HIGH PROTEIN (>14g)
      │
      └── default (time-based) ──────────► Morning→Breakfast · Noon→Lunch
                                           Afternoon→Snacks · Evening→Dinner
```

---

## 💾 Data Persistence

```javascript
// Data structure saved to localStorage key: 'ns_state'
{
  currentDate: "2026-03-20",        // ISO date string
  meals: {
    breakfast: [{ id, cal, prot, carb, fat, servings }],
    lunch:     [...],
    dinner:    [...],
    snacks:    [...]
  },
  water: 4,                          // glasses consumed today
  goals: {
    type: "maintenance",             // fat-loss | maintenance | muscle-gain | wellness
    calories: 2000,
    protein: 80,
    water: 8
  },
  history: {
    "2026-03-19": { cal, prot, carb, fat, water },
    "2026-03-18": { ... }
    // Last 7+ days
  }
}
```

**Daily Reset Logic:** On app load, if `currentDate !== today`, previous day is archived to `history{}` and a fresh `meals` object is created.

---

## 🎨 Design System

| Token | Light Mode | Dark Mode |
|---|---|---|
| Background | `#F8F8F6` | `#0E0E0E` |
| Surface (Card) | `#FFFFFF` | `#161616` |
| Text Primary | `#111111` | `#F8F8F8` |
| Text Secondary | `#555555` | `#A0A0A0` |
| Accent (Red) | `#FF3B30` | `#FF3B30` |
| Blue | `#3B82F6` | `#3B82F6` |
| Green | `#22C55E` | `#22C55E` |
| Border | `#E8E8E4` | `#2A2A2A` |

**Typography:** Inter (Google Fonts) · Weights: 300, 400, 500, 600, 700, 800, 900

**Border Radius:** Cards `20px` · Buttons `10–12px` · Tags `6px`

**Animations:**
- Page load: `fadeUp` (opacity 0→1, translateY 16px→0, 500ms ease)
- Hover: `scale(1.02)` + shadow lift (220ms)
- Button press: `scale(0.97)` (instant)
- Charts: `stroke-dashoffset` + `width` transitions (800ms cubic-bezier)

---

## 🔍 Search System

- **Search scope:** Food name only (not tags, not category)
- **Algorithm:** `String.toLowerCase().includes(query)` — simple, fast, predictable
- **Grouped by category** with emoji headers
- **Empty query** shows first 30 items as browse mode
- **No results** shows friendly message

```
Search: "paneer"
Result: Shows only → Paneer Biryani, Paneer Butter Masala, Paneer Bhurji,
                      Palak Paneer, Matar Paneer, Paneer Tikka, Paneer Paratha...
```

---

## 📁 File Structure

```
nutrisnap/
├── nutrisnap.html      ← Complete app (single file)
├── README.md           ← This file
├── DOCS.docx           ← Full technical documentation with diagrams
└── LICENSE             ← MIT License
```

---

## 🤝 Contributing

1. Fork the repo
2. Create a feature branch: `git checkout -b feature/my-feature`
3. Commit changes: `git commit -m 'feat: add my feature'`
4. Push: `git push origin feature/my-feature`
5. Open a Pull Request

### Contribution Ideas
- [ ] Add more regional Indian foods (South Indian, Bengali, Gujarati)
- [ ] Export daily log as PDF
- [ ] BMI / TDEE calculator
- [ ] Meal templates / quick-add presets
- [ ] PWA support (service worker for full offline)
- [ ] Nutritional charts (vitamins, fiber, sodium)

---

## 📄 License

MIT © 2026 — Free to use, modify and distribute.

---

## 🙏 Acknowledgements

- Food data sourced from ICMR-NIN Indian Food Composition Tables
- Design inspired by Awwwards and Framer community
- Font: [Inter](https://rsms.me/inter/) by Rasmus Andersson

---

<div align="center">
  Made with ❤️ for hostel students everywhere
</div>
