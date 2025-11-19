# Visual Hierarchy Design Carousel - Wiki

Welcome to the Visual Hierarchy Design Carousel wiki! This documentation provides in-depth information about the project, its design principles, and how to use and customize it.

## Table of Contents

1. [Getting Started](#getting-started)
2. [Design Principles](#design-principles)
3. [Technical Architecture](#technical-architecture)
4. [Customization Guide](#customization-guide)
5. [Performance Optimization](#performance-optimization)
6. [Browser Compatibility](#browser-compatibility)
7. [Troubleshooting](#troubleshooting)

---

## Getting Started

### Prerequisites

- A modern web browser (Chrome, Firefox, Safari, or Edge)
- Basic understanding of HTML, CSS, and JavaScript (for customization)

### Installation

1. **Clone the repository:**
   ```bash
   git clone https://github.com/anacondy/25--3-pro-test.git
   cd 25--3-pro-test
   ```

2. **Open the project:**
   - Simply open `index.html` in your web browser
   - Or run a local server:
     ```bash
     python -m http.server 8080
     ```

3. **Navigate the carousel:**
   - Use `←` and `→` arrow keys
   - Or swipe on touch devices

---

## Design Principles

### 1. Glassmorphism

**What is it?**
Glassmorphism is a design trend featuring semi-transparent backgrounds with blur effects, creating a frosted glass appearance.

**Implementation:**
```css
background: rgba(255, 255, 255, 0.03);
backdrop-filter: blur(20px);
-webkit-backdrop-filter: blur(20px);
border: 1px solid rgba(255, 255, 255, 0.1);
```

**Key Elements:**
- Low opacity backgrounds
- Backdrop blur for depth
- Subtle borders for definition
- Layered elements for hierarchy

### 2. Visual Hierarchy

The carousel demonstrates visual hierarchy through:
- **Size**: Large headings draw attention first
- **Color**: High contrast for important elements
- **Position**: Strategic placement of content
- **Typography**: Different weights and sizes guide the eye

### 3. Color Theory

Each card uses a distinct color theme:
- **Green (#1db954)**: Growth, harmony (Card 1)
- **Purple (#8e44ad)**: Creativity, wisdom (Card 2)
- **Blue (#2980b9)**: Trust, professionalism (Card 3)
- **Orange (#d35400)**: Energy, enthusiasm (Card 4)
- **Red (#c0392b)**: Passion, importance (Card 5)
- **Teal (#16a085)**: Balance, clarity (Card 6)

### 4. Typography

**Font Family:** Inter
- Clean, modern sans-serif
- Excellent readability at all sizes
- Multiple weights available

**Fluid Typography:**
```css
font-size: clamp(2rem, 5vw, 3rem);
```
- Scales smoothly across devices
- Maintains readability
- No abrupt size changes

### 5. White Space

Strategic use of white space:
- Padding around content areas
- Margins between elements
- Empty space for visual breathing room
- Grid patterns as subtle texture

### 6. Accessibility

**Current Features:**
- High contrast text
- Keyboard navigation
- Semantic HTML structure
- Readable font sizes

**Future Improvements:**
- ARIA labels for screen readers
- Focus indicators
- Reduced motion support

---

## Technical Architecture

### HTML Structure

```
body
├── .glow-effect (dynamic background)
├── .top-left-credit (attribution)
├── .dots (decorative element)
├── .carousel-window (viewport)
│   └── .carousel-track (sliding container)
│       └── .glass-card × 6 (content cards)
└── .instructions (user guidance)
```

### CSS Architecture

**Organization:**
1. Global reset
2. Background & body
3. Glow effects
4. Carousel structure
5. Card styles
6. Typography
7. Responsive media queries
8. Animations

**Key Techniques:**
- CSS Custom Properties for theming
- Flexbox for card layout
- CSS Grid for decorative elements
- `clamp()` for responsive typography
- `will-change` for performance

### JavaScript Functionality

**Core Functions:**

1. **updateCarousel()**
   - Calculates card width dynamically
   - Moves track via `translateX`
   - Updates active card styling
   - Changes theme colors

2. **Keyboard Navigation**
   - Listens for arrow key events
   - Updates current index
   - Prevents navigation beyond bounds

3. **Touch/Swipe Support**
   - Detects touch start/end positions
   - Calculates swipe direction
   - Triggers carousel update

4. **Resize Handling**
   - Debounced resize event listener
   - Recalculates layout on window resize
   - Maintains correct card position

---

## Customization Guide

### Adding a New Card

1. **Copy existing card HTML:**
   ```html
   <div class="glass-card" data-theme="#your-color" data-index="7">
       <div class="card-tab">Your Title</div>
       <div class="grid-background"></div>
       <div class="content-wrapper">
           <div class="meta-header">
               <span>Category</span>
               <span>Date</span>
           </div>
           <h1>Your Main<br>Heading</h1>
           <h2>Subheading;</h2>
           <p class="description">Your description text.</p>
           <a href="#" class="btn">Call to action...</a>
       </div>
       <div class="cube-wrapper">
           <div class="cube-placeholder"></div>
       </div>
       <div class="footer-info">
           <span>/// Footer text</span>
           <span class="pagination">7 of 7 >></span>
       </div>
   </div>
   ```

2. **Update the theme color** in `data-theme`
3. **Update the pagination** counter
4. **Add your content**

### Changing Animation Speed

**Carousel transition:**
```css
.carousel-track {
    transition: transform 0.6s cubic-bezier(0.25, 1, 0.5, 1);
}
```

**Card scaling:**
```css
.glass-card {
    transition: all 0.6s cubic-bezier(0.4, 0, 0.2, 1);
}
```

**Floating cube:**
```css
animation: float 6s ease-in-out infinite;
```

### Customizing Colors

**Background gradient:**
```css
body {
    background-color: #050505;
}
```

**Glow effect:**
```css
.glow-effect {
    background: var(--theme-color, #1db954);
    opacity: 0.15;
}
```

**Glass transparency:**
```css
.glass-card {
    background: rgba(255, 255, 255, 0.03);
}
```

### Responsive Breakpoints

**Modify existing breakpoints:**
```css
/* Desktop 16:9 */
@media (aspect-ratio: 16/9) { }

/* Ultrawide 20:9 */
@media (min-aspect-ratio: 20/9) { }

/* Tablet */
@media (max-width: 1024px) { }

/* Mobile */
@media (max-width: 768px) { }

/* Small mobile */
@media (max-width: 480px) { }
```

---

## Performance Optimization

### Current Optimizations

1. **CSS `will-change`**
   ```css
   .glass-card {
       will-change: transform, opacity;
   }
   ```
   - Hints browser for GPU acceleration
   - Smoother animations

2. **Cubic-bezier Easing**
   - Natural, smooth motion
   - Better than linear transitions

3. **Debounced Resize**
   - Prevents excessive recalculations
   - 250ms delay between resize events

4. **Passive Event Listeners**
   ```javascript
   { passive: true }
   ```
   - Improves scroll performance
   - Used for touch events

### Best Practices

- Keep backdrop blur radius reasonable (20px)
- Limit simultaneous animations
- Use `transform` instead of `left/top`
- Optimize image assets (if added)
- Minify CSS/JS for production

---

## Browser Compatibility

### Fully Supported

- ✅ Chrome/Edge 88+
- ✅ Firefox 103+
- ✅ Safari 15.4+
- ✅ Opera 74+

### Feature Support

| Feature | Chrome | Firefox | Safari | Edge |
|---------|--------|---------|--------|------|
| backdrop-filter | 76+ | 103+ | 15.4+ | 79+ |
| CSS Grid | 57+ | 52+ | 10.1+ | 16+ |
| Flexbox | 29+ | 28+ | 9+ | 12+ |
| CSS Custom Props | 49+ | 31+ | 9.1+ | 15+ |
| Touch Events | 22+ | 52+ | 3.2+ | 12+ |

### Fallbacks

For older browsers without backdrop-filter:
```css
@supports not (backdrop-filter: blur(20px)) {
    .glass-card {
        background: rgba(255, 255, 255, 0.1);
    }
}
```

---

## Troubleshooting

### Common Issues

**1. Carousel not sliding**
- Check JavaScript console for errors
- Ensure JavaScript is enabled
- Verify card elements have correct classes

**2. Blur effect not working**
- Check browser support for backdrop-filter
- Try updating your browser
- Check for conflicting CSS

**3. Touch/swipe not responding**
- Verify touch events are supported
- Check for touch event conflicts
- Test swipe threshold (50px minimum)

**4. Colors not changing**
- Verify `data-theme` attributes are set
- Check CSS custom property support
- Inspect element styles in DevTools

**5. Layout breaks on resize**
- Check media query syntax
- Verify clamp() function support
- Test with browser DevTools responsive mode

### Debug Mode

Add to JavaScript for debugging:
```javascript
console.log('Current index:', currentIndex);
console.log('Card width:', cards[0].offsetWidth);
console.log('Theme color:', card.getAttribute('data-theme'));
```

### Performance Issues

If experiencing lag:
1. Reduce blur radius (e.g., 10px instead of 20px)
2. Simplify animations
3. Test on different devices
4. Check for heavy background processes

---

## Contributing

Contributions are welcome! Please:
1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

---

## Additional Resources

- [MDN Web Docs - backdrop-filter](https://developer.mozilla.org/en-US/docs/Web/CSS/backdrop-filter)
- [CSS Tricks - Glassmorphism](https://css-tricks.com/glassmorphism/)
- [Web.dev - Performance](https://web.dev/performance/)
- [A11y Project - Accessibility](https://www.a11yproject.com/)

---

**Last Updated:** November 2025
**Version:** 1.0.0
