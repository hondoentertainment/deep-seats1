# 🏟️ Deep Seats - Claude Code Project

**Version:** 1.0.0  
**Framework:** React 18 (Single-file Application)  
**Status:** Production Ready

---

## 📁 Project Structure

```
deep-seats-claude-code/
├── index.html          # Main application (256KB, 5700+ lines)
├── README.md           # This file
├── DEVELOPMENT.md      # Development guide
└── .clinerules         # Claude Code configuration
```

---

## 🚀 Quick Start

### Run Locally
```bash
# Option 1: Python
python3 -m http.server 8000
# Visit: http://localhost:8000

# Option 2: Node.js
npx serve
# Visit: http://localhost:3000
```

### Open Directly
```bash
# Just open in browser
open index.html  # Mac
xdg-open index.html  # Linux
start index.html  # Windows
```

---

## 🏗️ Architecture

### Single-File Application
- **HTML** (~20 lines) - Document structure
- **CSS** (~2,580 lines) - Material 3 styling
- **JavaScript** (~3,100 lines) - React components

### Technology Stack
- **React 18** - UI framework (CDN)
- **Leaflet.js 1.9.4** - Interactive maps (CDN)
- **LocalStorage API** - Data persistence
- **Material 3** - Design system
- **Babel Standalone** - JSX transformation

### Components (17)
1. App - Main container
2. NavRail - Sidebar navigation
3. ProfileHeader - Top bar with profile
4. Dashboard - Stats and calendar
5. Profile - User profile page
6. Timeline - Game history
7. DailyTrivia - Trivia game
8. Picks - Predictions system
9. CommunityGames - Shared games
10. GamePage - Individual game view
11. TrophyRoom - Achievements
12. TeamTracker - 92 teams browser
13. VenueExplorer - Map + venues
14. Calendar - Month view component
15. GameFormModal - Add/edit games
16. Snackbar - Toast notifications
17. FAB - Floating action button

---

## 💾 Data Storage

### LocalStorage Keys
```javascript
'deepseats-games'      // Array of game objects
'deepseats-profile'    // User profile object
'deepseats-trivia'     // Trivia progress
'deepseats-picks'      // Prediction array
```

### Data Schemas

**Game Object:**
```javascript
{
  id: string,
  homeTeam: string,
  awayTeam: string,
  homeScore: number,
  awayScore: number,
  date: string,
  venue: string,
  seatLocation: string,
  viewingFormat: 'Live' | 'TV' | 'Streaming',
  personalRating: 1-10,
  notes: string,
  players: string[],
  isShared: boolean
}
```

**Profile Object:**
```javascript
{
  name: string,
  username: string,
  avatar: string,  // emoji
  bio: string,
  favoriteTeam: string,
  favoritePlayer: string,
  homeCity: string
}
```

---

## 🎨 Design System

### Color Palette
```css
Primary:   #1a5fb4  /* Professional Blue */
Secondary: #535f70  /* Slate Blue-Gray */
Tertiary:  #6b5778  /* Purple */
Surface:   #fdfbff  /* Off-white */
Error:     #ba1a1a  /* Red */
```

### Spacing (8px grid)
```css
xs:  4px   (0.5 units)
sm:  8px   (1 unit)
md:  16px  (2 units)
lg:  24px  (3 units)
xl:  32px  (4 units)
2xl: 48px  (6 units)
3xl: 64px  (8 units)
```

### Typography
```css
Display Large:  57px  (Hero titles)
Display Medium: 45px  (Page headers)
Headline Large: 32px  (Section headers)
Title Large:    22px  (Card titles)
Body Large:     16px  (Body text)
Label Large:    14px  (Buttons)
```

---

## 📊 Database Contents

### Teams (92)
- NBA: 30 teams (Lakers, Celtics, Warriors, etc.)
- MLB: 30 teams (Yankees, Dodgers, Red Sox, etc.)
- NFL: 32 teams (Chiefs, Patriots, 49ers, etc.)

### Venues (92)
- NBA Arenas: 30 (Crypto.com Arena, MSG, TD Garden, etc.)
- MLB Stadiums: 30 (Yankee Stadium, Fenway, Wrigley, etc.)
- NFL Stadiums: 32 (Arrowhead, Lambeau, SoFi, etc.)

### Players (70+)
Star athletes across all leagues with jersey numbers and positions

### Features
- 10 Trivia questions
- 8 Achievements
- 4 Calendar modes
- 17 Components

---

## 🛠️ Development Guidelines

### Code Style
- **Components:** PascalCase (Dashboard, NavRail)
- **Functions:** camelCase (getStorageData, handleSave)
- **Constants:** UPPER_SNAKE_CASE (NBA_TEAMS, VENUES)
- **CSS Classes:** kebab-case (nav-rail, stat-card)

### React Patterns
```javascript
// Functional components with hooks
function Component({ props }) {
  const [state, setState] = useState(initial);
  
  useEffect(() => {
    // Side effects
  }, [dependencies]);
  
  return <div>JSX</div>;
}
```

### Adding Features
1. Add component function
2. Import necessary hooks
3. Add to App component render
4. Update navigation if needed
5. Test in browser

---

## 🧪 Testing

### Manual Testing
```bash
# Start server
python3 -m http.server 8000

# Test checklist:
✓ App loads without errors
✓ Navigation switches views
✓ Can log a game
✓ Data persists on refresh
✓ Map loads on Venues page
✓ Trivia game works
✓ Calendar displays
✓ Profile saves changes
```

### Browser Console
```javascript
// Check stored data
localStorage.getItem('deepseats-games')
localStorage.getItem('deepseats-profile')

// Clear data (testing)
localStorage.clear()

// Check React
console.log(React.version) // Should show 18.x
```

---

## 📝 Common Tasks

### Add New Team
```javascript
// In NBA_TEAMS, MLB_TEAMS, or NFL_TEAMS array
{ 
  id: 'unique-id',
  name: 'Team Name',
  league: 'NBA',
  logo: '🏀',
  color: '#hexcode'
}
```

### Add New Venue
```javascript
// In VENUES array
{
  id: 'venue-id',
  name: 'Venue Name',
  city: 'City',
  state: 'ST',
  capacity: 20000,
  homeTeam: 'team-id',
  lat: 40.7128,
  lng: -74.0060,
  league: 'NBA'
}
```

### Add New Achievement
```javascript
// In achievements array
{
  id: 'unique-id',
  name: 'Achievement Name',
  description: 'How to unlock',
  icon: '🏆',
  condition: (stats) => stats.gamesAttended >= 10
}
```

---

## 🐛 Debugging

### Common Issues

**Problem:** Blank page
```bash
# Check browser console (F12)
# Look for errors in red
# Common: CDN scripts blocked
```

**Problem:** Map not loading
```bash
# Check internet connection
# Verify Leaflet.js loaded
# Check console for errors
```

**Problem:** Data not saving
```bash
# Check localStorage available
# Not in incognito mode?
# Browser storage not full?
```

### Debug Mode
```javascript
// Add to console
localStorage.setItem('debug', 'true')

// Check React components
console.log(document.getElementById('root'))

// View all games
JSON.parse(localStorage.getItem('deepseats-games'))
```

---

## 🚀 Deployment

### GitHub Pages
```bash
1. Push index.html to GitHub repo
2. Settings → Pages → Enable
3. Deploy from main branch
4. Visit: username.github.io/repo
```

### Netlify
```bash
1. Drag index.html to netlify.com/drop
2. Get instant URL
3. Share anywhere
```

### Custom Hosting
```bash
1. Upload index.html to server
2. Configure web server
3. Point domain
4. Enable HTTPS
```

---

## 📚 Resources

### External Dependencies
- React 18: https://react.dev
- Leaflet.js: https://leafletjs.com
- Material 3: https://m3.material.io
- OpenStreetMap: https://openstreetmap.org

### Documentation
- README.md - Project overview
- FEATURES.md - Feature documentation
- CODE_REVIEW.md - Technical analysis
- DEPLOYMENT.md - Hosting guide

---

## 🎯 Next Steps for Claude Code

### Potential Enhancements
- [ ] Add data export/import
- [ ] Implement more achievements
- [ ] Add player statistics
- [ ] Create advanced filters
- [ ] Build analytics dashboard
- [ ] Add dark mode
- [ ] Implement PWA features
- [ ] Add unit tests
- [ ] Optimize performance
- [ ] Enhance mobile UX

### Refactoring Opportunities
- [ ] Extract components to separate files
- [ ] Add TypeScript types
- [ ] Implement state management (Zustand)
- [ ] Create build process
- [ ] Add code splitting
- [ ] Optimize bundle size
- [ ] Add service worker
- [ ] Implement caching

---

## ⚡ Quick Commands

```bash
# Start development
python3 -m http.server 8000

# View in browser
open http://localhost:8000

# Check file size
ls -lh index.html

# Search code
grep -n "function Dashboard" index.html

# Count lines
wc -l index.html

# View structure
head -100 index.html
```

---

## 📊 Project Stats

- **Total Lines:** 5,700+
- **Components:** 17
- **File Size:** 256KB
- **Teams:** 92
- **Venues:** 92
- **Players:** 70+
- **Features:** 9 main views
- **Achievements:** 8
- **Code Quality:** A-

---

## 🤝 Contributing

When working with Claude Code:
1. Read code comments
2. Follow existing patterns
3. Test changes locally
4. Document new features
5. Maintain design consistency

---

**Ready to develop Deep Seats with Claude Code!** 🚀

**Current Status:** Production-ready single-file application  
**Best Use:** Enhancements, features, optimizations  
**Framework:** React 18 with Hooks
