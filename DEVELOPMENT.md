# Development Guide - Deep Seats

## 🎯 Purpose

This guide helps you work with the Deep Seats codebase effectively, whether you're:
- Adding new features
- Fixing bugs
- Refactoring code
- Optimizing performance
- Enhancing UI/UX

---

## 🏗️ Architecture Overview

### Single-File Application

Deep Seats is intentionally a **single HTML file** for:
- ✅ Zero build process
- ✅ Easy deployment
- ✅ Simple debugging
- ✅ Instant development

### Three Sections

1. **HTML** (Lines 1-40, 2595-2597)
   - Meta tags and external scripts
   - Loading screen
   - React root container

2. **CSS** (Lines 41-2594)
   - Material 3 design tokens
   - Component styles
   - Responsive layouts
   - Animations

3. **JavaScript** (Lines 2598-5700)
   - React components
   - Application logic
   - Data constants
   - Utility functions

---

## 🔧 Development Setup

### Prerequisites
```bash
# You need:
- Modern web browser (Chrome/Firefox/Edge)
- Text editor (VS Code recommended)
- Python 3 or Node.js (for local server)
```

### Local Development
```bash
# Method 1: Python (recommended)
cd deep-seats-claude-code
python3 -m http.server 8000
# Visit: http://localhost:8000

# Method 2: Node.js
npx serve
# Visit: http://localhost:3000

# Method 3: VS Code
# Install "Live Server" extension
# Right-click index.html → Open with Live Server
```

---

## 📂 Code Organization

### Component Locations

| Component | Line Range | Purpose |
|-----------|------------|---------|
| NavRail | ~3150-3220 | Left sidebar navigation |
| ProfileHeader | ~3220-3290 | Top header with profile |
| Dashboard | ~3450-3680 | Main stats view |
| Profile | ~3680-3800 | User profile page |
| Timeline | ~3800-3950 | Game history |
| DailyTrivia | ~3950-4100 | Trivia game |
| Picks | ~4100-4300 | Predictions |
| CommunityGames | ~4300-4450 | Shared games |
| TrophyRoom | ~4450-4600 | Achievements |
| TeamTracker | ~4100-4300 | Team browser |
| VenueExplorer | ~4600-4850 | Map + venues |
| Calendar | ~3700-3850 | Month calendar |
| GameFormModal | ~4900-5200 | Add/edit games |

### Data Constants

| Constant | Line Range | Contains |
|----------|------------|----------|
| NBA_TEAMS | ~2615-2680 | 30 NBA teams |
| MLB_TEAMS | ~2680-2745 | 30 MLB teams |
| NFL_TEAMS | ~2745-2810 | 32 NFL teams |
| PLAYERS | ~2900-2980 | 70+ players |
| VENUES | ~2810-2900 | 92 venues |
| TRIVIA_QUESTIONS | ~3000-3050 | 10 questions |

---

## 🎨 Styling Guide

### Design Tokens

Always use CSS custom properties:

```css
/* Colors */
var(--md-sys-color-primary)           /* #1a5fb4 */
var(--md-sys-color-primary-container) /* #d5e3ff */
var(--md-sys-color-surface)           /* #fdfbff */
var(--md-sys-color-on-surface)        /* #1a1c1e */

/* Spacing */
var(--spacing-sm)   /* 8px */
var(--spacing-md)   /* 16px */
var(--spacing-lg)   /* 24px */
var(--spacing-xl)   /* 32px */

/* Typography */
var(--md-sys-typescale-headline-large)  /* 32px */
var(--md-sys-typescale-title-large)     /* 22px */
var(--md-sys-typescale-body-large)      /* 16px */

/* Elevation */
var(--md-sys-elevation-level1)  /* Subtle shadow */
var(--md-sys-elevation-level2)  /* Medium shadow */
var(--md-sys-elevation-level3)  /* Deep shadow */

/* Shape */
var(--shape-corner-small)        /* 8px */
var(--shape-corner-medium)       /* 12px */
var(--shape-corner-large)        /* 16px */
```

### Adding New Styles

```css
/* Good - Uses tokens */
.my-component {
    background: var(--md-sys-color-surface);
    padding: var(--spacing-lg);
    border-radius: var(--shape-corner-medium);
    box-shadow: var(--md-sys-elevation-level2);
}

/* Bad - Hard-coded values */
.my-component {
    background: #fdfbff;
    padding: 24px;
    border-radius: 12px;
    box-shadow: 0 1px 3px rgba(0,0,0,0.1);
}
```

---

## ⚛️ React Patterns

### Component Template

```javascript
function ComponentName({ prop1, prop2 }) {
    // 1. State
    const [state, setState] = useState(initialValue);
    
    // 2. Effects
    useEffect(() => {
        // Side effects
        return () => {
            // Cleanup
        };
    }, [dependencies]);
    
    // 3. Event handlers
    const handleAction = () => {
        setState(newValue);
    };
    
    // 4. Render
    return (
        <div className="component-container">
            {/* JSX */}
        </div>
    );
}
```

### State Management

```javascript
// Good - Functional updates
setState(prev => [...prev, newItem]);

// Bad - Direct mutation
setState(state.push(newItem));

// Good - Immutable updates
setState({ ...state, key: newValue });

// Bad - Mutation
state.key = newValue;
setState(state);
```

### useEffect Best Practices

```javascript
// Good - Clean dependencies
useEffect(() => {
    fetchData(id);
}, [id]);

// Bad - Missing dependencies
useEffect(() => {
    fetchData(id);
}, []); // 'id' missing!

// Good - Cleanup
useEffect(() => {
    const timer = setTimeout(() => {}, 1000);
    return () => clearTimeout(timer);
}, []);
```

---

## 💾 Data Management

### LocalStorage Structure

```javascript
// Games array
[
  {
    id: "game-1",
    homeTeam: "lakers",
    awayTeam: "celtics",
    homeScore: 110,
    awayScore: 105,
    date: "2026-01-10",
    venue: "Crypto.com Arena",
    seatLocation: "Section 101",
    viewingFormat: "Live",
    personalRating: 9,
    notes: "Amazing overtime finish!",
    players: ["lebron-james", "anthony-davis"],
    isShared: false
  }
]

// Profile object
{
  name: "John Doe",
  username: "@johndoe",
  avatar: "🏀",
  bio: "Lakers fan since 2000",
  favoriteTeam: "lakers",
  favoritePlayer: "lebron-james",
  homeCity: "Los Angeles, CA"
}
```

### Storage Functions

```javascript
// Get data
const getStorageData = (key, defaultValue) => {
    try {
        const item = localStorage.getItem(key);
        return item ? JSON.parse(item) : defaultValue;
    } catch {
        return defaultValue;
    }
};

// Set data
const setStorageData = (key, value) => {
    try {
        localStorage.setItem(key, JSON.stringify(value));
        return true;
    } catch {
        return false;
    }
};
```

---

## 🆕 Adding Features

### Example: Add New Achievement

**Step 1: Define achievement**
```javascript
// In achievements array (~line 3300)
{
    id: 'rivalry-games',
    name: 'Rivalry Fanatic',
    description: 'Attend 5 rivalry games',
    icon: '⚔️',
    unlocked: false,
    progress: 0,
    total: 5
}
```

**Step 2: Add unlock logic**
```javascript
// In calculateAchievements function
const rivalryGames = games.filter(g => 
    isRivalryGame(g.homeTeam, g.awayTeam)
).length;

if (rivalryGames >= 5) {
    achievements.find(a => a.id === 'rivalry-games').unlocked = true;
}
```

**Step 3: Create helper function**
```javascript
const isRivalryGame = (team1, team2) => {
    const rivalries = {
        'lakers': ['celtics'],
        'celtics': ['lakers'],
        // ... more rivalries
    };
    return rivalries[team1]?.includes(team2);
};
```

### Example: Add New View

**Step 1: Create component**
```javascript
function MyNewView() {
    const [data, setData] = useState([]);
    
    return (
        <div className="view-container">
            <h1>My New View</h1>
            {/* Content */}
        </div>
    );
}
```

**Step 2: Add to App**
```javascript
// In App component render
{currentView === 'mynewview' && <MyNewView />}
```

**Step 3: Add navigation**
```javascript
// In NavRail items array
{ id: 'mynewview', icon: '🆕', label: 'New View' }
```

---

## 🐛 Debugging

### Browser DevTools

```javascript
// Open console (F12)

// Check React
console.log(React.version);

// View stored data
console.log(localStorage);
console.log(JSON.parse(localStorage.getItem('deepseats-games')));

// Check component state
// (Add to component)
console.log('Component rendered', { state, props });

// Debug effect runs
useEffect(() => {
    console.log('Effect running', dependencies);
}, [dependencies]);
```

### Common Issues

**Issue: Component not rendering**
```javascript
// Check:
1. Is component function defined?
2. Is it called in App render?
3. Are props passed correctly?
4. Console errors?
```

**Issue: State not updating**
```javascript
// Check:
1. Using setState correctly?
2. Not mutating state directly?
3. Dependencies in useEffect?
4. Async state updates?
```

**Issue: Data not persisting**
```javascript
// Check:
1. LocalStorage available? (not incognito)
2. Calling setStorageData?
3. Correct key names?
4. JSON.stringify working?
```

---

## ✅ Testing Checklist

### Before Committing Changes

- [ ] Code runs without console errors
- [ ] All views render correctly
- [ ] Navigation works
- [ ] Data persists on refresh
- [ ] Forms submit successfully
- [ ] Map loads (if modified)
- [ ] Responsive on mobile
- [ ] No broken styles
- [ ] Performance acceptable
- [ ] LocalStorage not corrupted

### Manual Test Flow

```bash
1. Open app
2. Add a game
3. Refresh page
4. Verify game persists
5. Switch between views
6. Edit profile
7. Check trophies
8. Try trivia
9. Make a pick
10. View map
```

---

## 📈 Performance Tips

### Optimize Re-renders

```javascript
// Use memo for expensive components
const MemoizedComponent = React.memo(ExpensiveComponent);

// Use callback for handlers
const handleClick = useCallback(() => {
    // handler
}, [dependencies]);

// Use useMemo for calculations
const stats = useMemo(() => {
    return calculateStats(games);
}, [games]);
```

### Reduce Bundle Size

```javascript
// Lazy load components (future)
const MapView = React.lazy(() => import('./MapView'));

// Conditional loading
{showMap && <MapComponent />}
```

---

## 🚀 Deployment

### Pre-Deploy Checklist

- [ ] Remove console.logs
- [ ] Test in production mode
- [ ] Verify CDN URLs work
- [ ] Check file size (<500KB)
- [ ] Test on multiple browsers
- [ ] Verify mobile experience
- [ ] Update version number
- [ ] Update CHANGELOG

### Quick Deploy

```bash
# GitHub Pages
git add index.html
git commit -m "Update Deep Seats"
git push origin main

# Netlify
drag index.html to netlify.com/drop

# Manual
upload index.html to web server
```

---

## 📚 Resources

### External Docs
- React: https://react.dev
- Leaflet: https://leafletjs.com/reference.html
- Material 3: https://m3.material.io
- LocalStorage: https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage

### Internal Docs
- README.md - Project overview
- .clinerules - Claude Code config
- CODE_REVIEW.md - Technical details

---

## 🤝 Best Practices

1. **Read before modifying** - Understand existing code
2. **Follow patterns** - Use established conventions
3. **Test frequently** - After each change
4. **Document changes** - Add comments
5. **Preserve structure** - Keep single-file format
6. **Use tokens** - Don't hard-code values
7. **Handle errors** - Add try-catch
8. **Think mobile** - Test responsive
9. **Optimize** - Minimize re-renders
10. **Have fun!** - Enjoy the code

---

**Happy coding with Deep Seats!** 🏟️⚡

**Questions?** Check .clinerules or README.md
