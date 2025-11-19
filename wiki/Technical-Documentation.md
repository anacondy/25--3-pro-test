# Technical Documentation

This page provides detailed technical information about the implementation of the Visual Hierarchy Interactive Showcase.

## 🏗️ Architecture Overview

The project is built as a single-page application (SPA) using vanilla HTML, CSS, and JavaScript with no external dependencies (except Google Fonts).

### File Structure

```
25--3-pro-test/
├── index.html              # Main application file
├── README.md               # Project documentation
├── .gitignore             # Git ignore rules
├── .github/
│   └── workflows/
│       └── deploy.yml     # GitHub Pages deployment
└── wiki/                  # Documentation files
    ├── Home.md
    ├── Getting-Started.md
    ├── Design-Principles.md
    └── ...
```

## 📄 HTML Structure

### Semantic Markup

The HTML uses semantic elements for better accessibility and SEO:

```html
<body>
  <div class="glow-effect">           <!-- Background glow -->
  <div class="top-left-credit">       <!-- Creator attribution -->
  <div class="dots">                  <!-- Decorative elements -->
  <div class="carousel-window">       <!-- Main viewport -->
    <div class="carousel-track">      <!-- Sliding container -->
      <div class="glass-card">        <!-- Individual slides -->
        <div class="card-tab">        <!-- Slide label -->
        <div class="grid-background"> <!-- Grid overlay -->
        <div class="content-wrapper"> <!-- Text content -->
          <h1>, <h2>, <p>            <!-- Typography -->
        <div class="cube-wrapper">   <!-- Decorative 3D element -->
        <div class="footer-info">    <!-- Metadata -->
      </div>
    </div>
  </div>
  <div class="instructions">         <!-- User guidance -->
</body>
```

### Meta Tags

Important meta tags for SEO and social sharing:

```html
<meta name="description" content="...">
<meta name="keywords" content="...">
<meta property="og:title" content="...">
<meta property="og:description" content="...">
<meta property="og:type" content="website">
```

## 🎨 CSS Architecture

### CSS Variables (Custom Properties)

Dynamic theming using CSS variables:

```css
.glass-card {
    --theme-color: #1db954;        /* Set by JavaScript */
    --shadow-color: #1db954;       /* Matches theme */
}
```

### Glassmorphic Effect

The signature glass effect is achieved through:

```css
.glass-card {
    background: rgba(255, 255, 255, 0.03);
    backdrop-filter: blur(20px);
    -webkit-backdrop-filter: blur(20px);
    border: 1px solid rgba(255, 255, 255, 0.1);
    box-shadow: 0 20px 50px rgba(0, 0, 0, 0.5);
}
```

### Responsive Design

Media queries for different aspect ratios:

```css
/* 16:9 displays */
@media (min-aspect-ratio: 16/9) and (min-width: 1600px) {
    .carousel-window { width: 800px; height: 500px; }
    .glass-card { flex: 0 0 800px; }
}

/* Ultrawide displays (21:9+) */
@media (min-aspect-ratio: 20/9) {
    .carousel-window { width: 900px; height: 550px; }
    .glass-card { flex: 0 0 900px; }
}
```

### Responsive Typography

Using `clamp()` for fluid typography:

```css
h1 {
    font-size: clamp(2rem, 5vw, 3rem);
}
h2 {
    font-size: clamp(1.2rem, 3vw, 1.5rem);
}
```

### Animation System

#### Carousel Transitions

```css
.carousel-track {
    transition: transform 0.6s cubic-bezier(0.25, 1, 0.5, 1);
    transform: translateZ(0);
    backface-visibility: hidden;
}
```

#### Card State Transitions

```css
.glass-card {
    opacity: 0.4;
    transform: scale(0.9);
    transition: all 0.6s cubic-bezier(0.25, 1, 0.5, 1);
    will-change: transform, opacity;
}

.glass-card.active {
    opacity: 1;
    transform: scale(1);
}
```

#### Floating Animation

```css
@keyframes float {
    0%, 100% { transform: translateY(0px); }
    50% { transform: translateY(-15px); }
}

.cube-placeholder {
    animation: float 6s ease-in-out infinite;
    will-change: transform;
}
```

## ⚙️ JavaScript Implementation

### Core Variables

```javascript
const track = document.getElementById('track');
const cards = document.querySelectorAll('.glass-card');
const bgGlow = document.getElementById('bgGlow');
let currentIndex = 0;
const totalCards = cards.length;
```

### Main Update Function

```javascript
function updateCarousel() {
    // Dynamic card width calculation for responsiveness
    const firstCard = cards[0];
    const cardWidth = firstCard ? firstCard.offsetWidth : 700;
    const translateX = -(currentIndex * cardWidth);
    track.style.transform = `translateX(${translateX}px)`;
    
    // Update active states and theme colors
    cards.forEach((card, index) => {
        if(index === currentIndex) {
            card.classList.add('active');
            const themeColor = card.getAttribute('data-theme');
            bgGlow.style.setProperty('--theme-color', themeColor);
            card.style.setProperty('--theme-color', themeColor);
            card.style.setProperty('--shadow-color', themeColor);
        } else {
            card.classList.remove('active');
        }
    });
}
```

### Keyboard Navigation

```javascript
document.addEventListener('keydown', (e) => {
    if (e.key === 'ArrowRight' && currentIndex < totalCards - 1) {
        currentIndex++;
        updateCarousel();
    } else if (e.key === 'ArrowLeft' && currentIndex > 0) {
        currentIndex--;
        updateCarousel();
    }
});
```

### Touch/Swipe Support

```javascript
let touchStartX = 0;
let touchEndX = 0;

carousel.addEventListener('touchstart', (e) => {
    touchStartX = e.changedTouches[0].screenX;
}, { passive: true });

carousel.addEventListener('touchend', (e) => {
    touchEndX = e.changedTouches[0].screenX;
    handleSwipe();
}, { passive: true });

function handleSwipe() {
    const swipeThreshold = 50;
    const swipeDistance = touchStartX - touchEndX;
    
    if (Math.abs(swipeDistance) > swipeThreshold) {
        if (swipeDistance > 0 && currentIndex < totalCards - 1) {
            currentIndex++;
            updateCarousel();
        } else if (swipeDistance < 0 && currentIndex > 0) {
            currentIndex--;
            updateCarousel();
        }
    }
}
```

### Resize Handling

```javascript
let resizeTimeout;
window.addEventListener('resize', () => {
    clearTimeout(resizeTimeout);
    resizeTimeout = setTimeout(() => {
        updateCarousel();
    }, 150);
});
```

## 🚀 Deployment

### GitHub Pages Setup

The project uses GitHub Actions for automated deployment:

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches: [ main ]
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
      - name: Setup Pages
        uses: actions/configure-pages@v4
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: '.'
      - name: Deploy to GitHub Pages
        uses: actions/deploy-pages@v4
```

### Deployment Process

1. Code is pushed to `main` branch
2. GitHub Actions workflow triggers
3. Files are uploaded as artifact
4. Pages are deployed to GitHub Pages
5. Site becomes available at `https://anacondy.github.io/25--3-pro-test/`

## 🎯 Data Attributes

Each card uses data attributes for dynamic theming:

```html
<div class="glass-card" data-theme="#1db954" data-index="1">
  <!-- Green theme -->
</div>

<div class="glass-card" data-theme="#8e44ad" data-index="2">
  <!-- Purple theme -->
</div>
```

Theme colors:
- Slide 1: `#1db954` (Green)
- Slide 2: `#8e44ad` (Purple)
- Slide 3: `#2980b9` (Blue)
- Slide 4: `#d35400` (Orange)
- Slide 5: `#c0392b` (Red)
- Slide 6: `#16a085` (Teal)

## 🔧 Browser Compatibility

### Required Features

- CSS `backdrop-filter` (glassmorphism)
- CSS Variables
- CSS Grid and Flexbox
- ES6+ JavaScript (const, let, arrow functions)
- Touch Events API

### Fallbacks

For browsers without `backdrop-filter`:
```css
@supports not (backdrop-filter: blur(20px)) {
    .glass-card {
        background: rgba(255, 255, 255, 0.15);
    }
}
```

## 📊 Performance Considerations

### Hardware Acceleration

Properties that trigger GPU acceleration:
- `transform: translateZ(0)`
- `will-change: transform, opacity`
- `backface-visibility: hidden`

### Optimizations

1. **Debounced resize**: Prevents excessive recalculations
2. **Passive event listeners**: Improves scroll performance
3. **CSS containment**: Limits repaints to specific elements
4. **Optimized selectors**: Efficient DOM queries
5. **Minimal reflows**: CSS changes are batched

## 🧪 Testing Checklist

- [ ] Keyboard navigation (arrow keys)
- [ ] Touch/swipe on mobile
- [ ] Responsive behavior on resize
- [ ] Transitions are smooth (60fps)
- [ ] All slides display correctly
- [ ] Theme colors change appropriately
- [ ] Works on different aspect ratios
- [ ] Browser compatibility (Chrome, Firefox, Safari, Edge)

---

[← Back to Design Principles](Design-Principles.md) | [Next: Responsive Design →](Responsive-Design.md)
