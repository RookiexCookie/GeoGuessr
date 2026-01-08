# 🌍 GeoSphere Challenge

An immersive, AI-driven geography guessing game built with **Google Street View** and **Google Maps**. Explore random locations around the world, make educated guesses on an interactive map, and earn points based on accuracy and speed.

---

## 📋 Overview

**GeoSphere Challenge** is a single-player geography game where:

1. Players are shown a random **Google Street View panorama** from anywhere on Earth
2. They click on a **world map** to guess the location
3. The game calculates the **geographic distance** (using Haversine formula) between their guess and the actual location
4. Points are awarded based on **proximity** and **remaining time**
5. Each game consists of **5 rounds** with a **60-second timer** per round

### Scoring System
- **Distance bonus**: Full points (95) for guesses within 100 km, decreasing to 0 points for 7000+ km away
- **Time bonus**: Bonus points awarded for quick submissions (45s+ = 100 pts, 30s+ = 60 pts, 15s+ = 30 pts)
- **Max score**: ~500 points per round (perfect guess + full time bonus) = 2500 for all 5 rounds

### Rank Tiers
- **Globetrotter**: ≥3500 total points
- **Traveler**: ≥2200 total points
- **Wanderer**: <2200 total points

---

## ✅ What's Working

### Core Gameplay
- ✓ Random Street View location loading
- ✓ Map click-to-guess functionality
- ✓ Distance calculation (Haversine formula)
- ✓ Scoring and round progression
- ✓ 5-round game flow with 60-second timer
- ✓ Results modal showing distance and points
- ✓ Summary screen with final score and rank
- ✓ Play again functionality

### UI & Visuals
- ✓ Dark neon-amber aurora theme with glassmorphism
- ✓ Responsive intro screen with start button
- ✓ Loading screen during location fetch
- ✓ Game header showing round, score, and timer
- ✓ Street View panel with interactive panorama
- ✓ Map panel with clickable world map
- ✓ Round result modal with mini-map showing guess vs. actual location
- ✓ Summary screen with final score, rank, and round chart
- ✓ Skip button for quick location submission
- ✓ Particle/stars background animation

### Controls
- ✓ Start button to begin game
- ✓ Map clicking to place guess
- ✓ Submit Guess button (enabled when guess is placed)
- ✓ Next Round button (appears after result modal)
- ✓ Skip Round button
- ✓ Play Again button (returns to intro)
- ✓ Share Score button (copies to clipboard or uses native share)

### API Integration
- ✓ Google Street View Service (random panorama fetching)
- ✓ Google Maps (map rendering and marker placement)
- ✓ Geocoding (location details logging)

---

## 📂 Project Structure

```
GeoGuessr/
├── index.html                 # Main HTML (pages, containers, scripts)
├── style.css                  # Dark theme, glassmorphism, animations
├── script.js                  # Game logic, scoring, UI glue
├── mapHandler.js              # Map init, guess placement, markers
├── streetviewHandler.js       # Street View loading, controls
├── config.js                  # Google Maps API key
├── README.md                  # This file
└── assets/
    ├── bg/                    # Background images (optional)
    │   ├── aurora.png        
    │   └── stars.png         
    └── icons/                # Icon assets (optional)
```

### Key Files Explained

| File | Purpose |
|------|---------|
| `index.html` | Entry point; defines all screen layouts (intro, loading, game, summary) and loads scripts |
| `style.css` | All styling; dark theme, neon accents (#8A4FFF, #5C67FF), glass panels, animations |
| `script.js` | Game orchestration: round management, scoring, timer, event listeners, screen transitions |
| `mapHandler.js` | Manages Google Map instance; handles click guesses, marker placement, distance visualization |
| `streetviewHandler.js` | Loads random Street View panoramas; tracks current location |
| `config.js` | Stores Google Maps API key (required) |

---

## 🚀 Getting Started

### Requirements
- Modern web browser (Chrome, Firefox, Safari, Edge)
- **Google Maps API key** with Street View and Maps enabled

### Setup

1. **Clone/download** the project
2. **Add your API key** to `config.js`:
   ```javascript
   const GOOGLE_API_KEY = "YOUR_API_KEY_HERE";
   ```
3. **Open `index.html`** in a browser
4. Click **"Start Exploring"** to begin

### Google Maps API Setup
1. Go to [Google Cloud Console](https://console.cloud.google.com/)
2. Create a new project
3. Enable:
   - **Maps JavaScript API**
   - **Street View API**
   - **Geocoding API** (optional, for location logging)
4. Create an API key (restrict to HTTP referrers for production)
5. Paste the key into `config.js`

---

## 🎮 How to Play

1. **Start Game** → Click "Start Exploring" on intro screen
2. **View Location** → Google Street View loads a random location
3. **Explore** → Click & drag on Street View to look around
4. **Guess** → Click on the world map to place your guess marker
5. **Submit** → Click "Submit Guess" to lock in your answer
6. **Result** → See distance, points, and mini-map comparison
7. **Next** → Click "Next Round" or "Continue" to proceed
8. **Summary** → After 5 rounds, view final score and rank

---

## 🛠️ Development Notes

### Game Flow
```
intro-screen 
  → loading-screen (fetch location)
    → game-screen (Street View + Map, 60s timer)
      → round-result (show distance & points)
        → game-screen (next round) OR summary-screen (game over)
          → intro-screen (play again)
```

### Scoring Formula
```javascript
basePoints = scoreFromDistance(km)  // Haversine distance
finalPoints = basePoints + timeBonus(secondsRemaining)
```

### Time Zones & Geocoding
- Street View locations are logged via Google Geocoding API (country, region shown in console)
- No time zone conversions needed; all times in client seconds

### Known Limitations
- Requires valid Google Maps API key
- Street View coverage varies by region (some areas have limited imagery)
- Game does not save progress (no backend)
- No leaderboard or multiplayer features
- No sound files included (audio references in code but assets missing)

---

## 🎨 Styling & Theme

- **Primary Colors**: Dark purple (#0D0B14), Neon purple (#8A4FFF), Secondary blue (#5C67FF)
- **Effects**: Glassmorphism (backdrop blur), glow effects, smooth animations
- **Typography**: Poppins & Montserrat fonts
- **Responsive**: Adapts to tablet (768px) and mobile (480px) screens

---

## 📝 License

Open source. Use freely, modify, and redistribute as needed.

---

## 📧 Feedback

Found a bug? Have a suggestion? Feel free to open an issue or reach out!

Happy exploring! 🌍✨
  - `icons/` — map pins and UI icons
    - `pin-actual.png`
    - `pin-guess.png`
    - `neon-globe.svg` (optional)
  - `sounds/` — short sound effects
    - `correct.mp3`
    - `wrong.mp3`

## Features

- Random global Street View location selection with graceful retry if imagery isn't available
- Dual pane UI: a Street View pane and an interactive world map for guessing
- Scoring uses Haversine distance and a time bonus for faster guesses
- Neon-glass UI with aurora/stars background and subtle particle effects
- Animated reveal sequence: pins, amber beam, and auto-zoom to the correct location
- 5-round game with summary and share options

## Setup (developer)

1. Create a Google Cloud project and enable the following APIs:
   - Maps JavaScript API
   - Street View Static/Service (if applicable)

2. Add your API key to `config.js` in the project root. Example `config.js`:

```js
// config.js (do not commit your real key)
const CONFIG = {
  GOOGLE_MAPS_API_KEY: 'YOUR_API_KEY_HERE'
};

export default CONFIG;
```

3. Run a local static server to serve the files. Example (requires Node.js):

```powershell
npx serve .
```

Open the printed URL in your browser (commonly http://localhost:3000).

Notes on security: restrict your API key to the specific domain(s) or local development origin in the Google Cloud Console.

## Local development tips

- Use the browser devtools to inspect console logs for Street View load errors (imagery missing, quota issues).
- If Street View imagery isn't available for a selected location the game retries with a new random point.
- To speed up styling edits, use a live-reload server or browser extension.

## Deployment

- This project is suitable for static hosting (GitHub Pages, Netlify, Vercel). Ensure your API key restrictions allow the hosted domain.
- For GitHub Pages: push to the `main` branch and enable Pages in repository settings.

## Contributing

- Issues and pull requests are welcome. Label changes or big UI rewrites as "WIP" until stable.
- Please do not commit API keys. Use `config.js` locally and add a note in `.gitignore` if you create a file with secrets.

## File checklist (recommended additions)

- Add or confirm these assets exist in `assets/`:
  - `assets/icons/pin-guess.png`
  - `assets/icons/pin-actual.png`
  - `assets/icons/neon-globe.svg`
  - `assets/bg/aurora.mp4` or `assets/bg/aurora.png`
  - `assets/bg/stars.webp` or `assets/bg/stars.png`
  - `assets/sounds/correct.mp3`
  - `assets/sounds/wrong.mp3`

## Notes for maintainers

- Movement in Street View is disabled by default for fairness (`clickToGo=false` and `linksControl=false`), so tests and UI rely on the fixed camera.
- Scoring thresholds live in `script.js` — tweak to balance difficulty and scoring fairness.

## License

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

© 2025 Prince Raj Singh, K. Harish (Group Carnage Sentinels) · SPDX: MIT

This project is released under the MIT License. 
Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, 
INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. 
IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, 
WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

---
