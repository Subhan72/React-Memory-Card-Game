# React Memory Card Game

An engaging memory card matching game built with React featuring multiple themes, difficulty levels, and a comprehensive scoring system. Test your memory skills while enjoying smooth animations and competitive gameplay.

## 🎮 Game Features

### Core Gameplay
- **Card Matching**: Flip cards to find matching pairs in a 4x4 grid
- **Memory Challenge**: Cards flip back after 1 second if they don't match
- **Progressive Difficulty**: Multiple grid sizes and complexity levels
- **Theme Variety**: Multiple card themes for diverse gameplay experiences
- **Animated Interactions**: Smooth card flip animations and visual feedback

### Scoring System
- **Match Rewards**: 100 points for each successful pair match
- **Time Bonus**: Extra points for quick completion times
- **Mismatch Penalty**: -10 points for incorrect matches
- **High Score Tracking**: Persistent leaderboard with best performances
- **Performance Analytics**: Track completion time and accuracy

### User Experience
- **Responsive Design**: Optimized for desktop, tablet, and mobile play
- **Visual Feedback**: Clear indicators for matched, selected, and available cards
- **Game Statistics**: Real-time score, time, and moves counter
- **Reset Functionality**: Restart game at any time with new card arrangement

## 📸 Screenshots

![image](https://github.com/user-attachments/assets/3e498667-1a06-4426-81b3-a4f4dab7a33b)


## 🛠️ Technical Implementation

### Game State Management

```javascript
const [gameState, setGameState] = useState({
  cards: [],
  flippedCards: [],
  matchedPairs: [],
  score: 0,
  moves: 0,
  timeElapsed: 0,
  gameStatus: 'ready', // ready, playing, completed
  difficulty: 'normal'
});
```

### Card Data Structure

```javascript
const cardSchema = {
  id: "unique-identifier",
  value: "card-content-identifier",
  isFlipped: false,
  isMatched: false,
  theme: "animals|symbols|colors|numbers"
};
```

### Core Game Logic

**Card Initialization**
- Generate pairs of matching cards
- Shuffle card positions randomly
- Initialize game state and timers

**Flip Logic**
- Track currently flipped cards (maximum 2)
- Check for matches when two cards are flipped
- Handle match/mismatch scenarios with appropriate delays

**Match Detection**
```javascript
const checkForMatch = (card1, card2) => {
  if (card1.value === card2.value) {
    // Handle successful match
    updateScore(100);
    setMatchedPairs(prev => [...prev, card1.id, card2.id]);
    checkGameCompletion();
  } else {
    // Handle mismatch with penalty
    updateScore(-10);
    setTimeout(() => flipCardsBack(card1.id, card2.id), 1000);
  }
};
```

## 🎯 Component Architecture

### GameBoard Component
- Manages overall game state and logic
- Handles card grid rendering
- Controls game flow and status transitions
- Integrates timer and scoring systems

### Card Component
- Renders individual card with flip animations
- Handles click events and state updates
- Displays card content based on theme
- Manages card appearance states (flipped, matched, default)

### ScoreBoard Component
- Displays current score, moves, and time
- Shows real-time game statistics
- Handles score calculations and bonuses
- Manages high score comparisons

### ThemeSelector Component
- Allows players to choose card themes
- Dynamically loads theme-specific assets
- Handles theme switching during gameplay
- Provides theme preview functionality

### Timer Component
- Tracks game duration with precision
- Calculates time-based bonuses
- Handles pause/resume functionality
- Displays formatted time (MM:SS)

## 🎨 Visual Design

### Card Themes
- **Animals**: Cute animal illustrations with vibrant colors
- **Symbols**: Geometric shapes and mathematical symbols
- **Colors**: Solid color blocks with subtle gradients
- **Numbers**: Stylized numeric characters
- **Emojis**: Popular emoji sets for fun gameplay

### Animation System
- **Card Flip**: 3D CSS transforms for realistic card turning
- **Match Success**: Celebratory bounce and glow effects
- **Mismatch**: Subtle shake animation for incorrect pairs
- **Game Completion**: Confetti animation and victory screen

### Color Scheme
- **Primary**: Deep blue (#1e40af) for game board
- **Secondary**: Warm orange (#f97316) for active states
- **Success**: Green (#10b981) for matched pairs
- **Warning**: Red (#ef4444) for mismatches
- **Neutral**: Gray tones for card backs and UI elements

## ⚡ Game Mechanics

### Difficulty Levels
- **Easy**: 3x2 grid (6 pairs) - Perfect for beginners
- **Normal**: 4x4 grid (8 pairs) - Standard gameplay
- **Hard**: 6x4 grid (12 pairs) - Advanced challenge
- **Expert**: 6x6 grid (18 pairs) - Ultimate memory test

### Scoring Algorithm
```javascript
const calculateScore = (matches, mismatches, timeElapsed) => {
  const baseScore = matches * 100;
  const penalty = mismatches * 10;
  const timeBonus = Math.max(0, 1000 - timeElapsed);
  return baseScore - penalty + timeBonus;
};
```

### High Score System
- Persistent storage using localStorage
- Separate leaderboards for each difficulty level
- Player name input for high score entries
- Score sharing functionality

## 🎮 Gameplay Flow

### Game Initialization
1. Select difficulty level and theme
2. Cards are shuffled and placed face-down
3. Timer starts on first card flip
4. Score initialized to zero

### Playing Phase
1. Player clicks on face-down card to flip it
2. Second card selection triggers match check
3. Successful matches remain face-up
4. Mismatches flip back after 1-second delay
5. Score updates based on match/mismatch results

### Game Completion
1. All pairs matched triggers victory state
2. Final score calculated with time bonus
3. High score comparison and potential entry
4. Option to play again or change settings

## 📱 Responsive Design

### Mobile Optimizations
- **Touch-friendly**: Large card sizes for easy tapping
- **Gesture Support**: Swipe gestures for navigation
- **Adaptive Layout**: Dynamic grid sizing based on screen size
- **Performance**: Optimized animations for mobile devices

### Breakpoint Strategy
- **Mobile (320px+)**: 3x2 or 4x3 grid with large cards
- **Tablet (768px+)**: 4x4 grid with medium cards
- **Desktop (1024px+)**: Full-size grids with detailed animations

## 🚀 Performance Features

### Optimization Techniques
- **Memoization**: React.memo for Card components to prevent unnecessary re-renders
- **Lazy Loading**: Dynamic theme asset loading
- **Animation Optimization**: CSS transforms over JavaScript animations
- **State Efficiency**: Minimal state updates for smooth gameplay

### Memory Management
```javascript
// Efficient card flip handling
const handleCardClick = useCallback((cardId) => {
  if (flippedCards.length < 2 && !isCardFlipped(cardId)) {
    setFlippedCards(prev => [...prev, cardId]);
  }
}, [flippedCards]);
```

## 🎯 Key Learning Outcomes

This project demonstrates proficiency in:

- **React State Management**: Complex game state with useState
- **Effect Hooks**: useEffect for timers, animations, and side effects
- **Component Lifecycle**: Proper cleanup and state management
- **Event Handling**: User interactions and game logic
- **Array Manipulation**: Shuffling, filtering, and mapping operations
- **Conditional Rendering**: Dynamic UI based on game state
- **CSS Animations**: Smooth transitions and visual feedback
- **Local Storage**: Persistent high score data
- **Performance Optimization**: Efficient rendering and state updates

## 🔧 Technologies Used

- **React** (Hooks, State Management, Component Architecture)
- **JavaScript ES6+** (Array methods, destructuring, async operations)
- **CSS3** (Animations, Transforms, Grid Layout, Flexbox)
- **HTML5** (Semantic markup, accessibility features)
- **Local Storage API** (High score persistence)
- **CSS Grid & Flexbox** (Responsive layout systems)

## 🎉 Getting Started

1. Clone the repository
2. Install dependencies: `npm install`
3. Start development server: `npm start`
4. Open http://localhost:3000 to start playing

## 🎮 How to Play

1. **Choose Your Theme**: Select from available card themes
2. **Select Difficulty**: Pick your preferred grid size
3. **Start Matching**: Click cards to flip and find matching pairs
4. **Score Points**: Earn 100 points per match, lose 10 for mismatches
5. **Beat the Clock**: Complete faster for time bonus points
6. **Achieve High Scores**: Compete for the top leaderboard positions

## 🏆 Advanced Features

### Timer System
- Precise millisecond timing
- Pause/resume functionality
- Time-based bonus calculations
- Best time tracking per difficulty

### Statistics Tracking
- Games played counter
- Average completion time
- Best streak tracking
- Accuracy percentage

### Accessibility Features
- Keyboard navigation support
- Screen reader compatibility
- High contrast mode option
- Reduced motion preferences

## 🔮 Future Enhancements

- **Multiplayer Mode**: Compete against friends in real-time
- **Custom Themes**: Upload personal images for card themes
- **Power-ups**: Special abilities like peek, hint, or shuffle
- **Tournament Mode**: Structured competitions with brackets
- **Social Features**: Share scores on social media
- **Sound Effects**: Audio feedback for flips, matches, and completion
- **Progressive Difficulty**: Adaptive difficulty based on performance
- **Achievement System**: Unlockable badges and rewards

## 🎯 Educational Value

### Memory Skills Development
- **Visual Memory**: Remembering card positions and patterns
- **Working Memory**: Holding multiple card locations in mind
- **Pattern Recognition**: Identifying matching pairs quickly
- **Concentration**: Sustained attention throughout gameplay

### Cognitive Benefits
- **Problem Solving**: Strategic thinking about card selection
- **Decision Making**: Risk assessment for card choices
- **Attention Training**: Focus improvement through gameplay
- **Speed Processing**: Quick recognition and response times

---

*This memory card game combines entertainment with cognitive training, showcasing advanced React development skills while providing an engaging user experience that challenges and improves memory capabilities.*
