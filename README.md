# Visual Hierarchy - Glassmorphic Design Carousel

[![Live Demo](https://img.shields.io/badge/demo-live-brightgreen)](https://anacondy.github.io/25--3-pro-test/)
[![GitHub Pages](https://img.shields.io/badge/GitHub-Pages-blue)](https://github.com/anacondy/25--3-pro-test)

A stunning, interactive glassmorphic design carousel showcasing visual design principles. Features smooth animations, responsive layouts optimized for 16:9 and 20:9 displays, and an elegant glass-morphism aesthetic.

## ✨ Features

- 🎨 **Glassmorphic Design** - Beautiful frosted glass effect with backdrop blur
- 🎭 **Interactive Carousel** - 6 unique design cards with smooth transitions
- 🌈 **Dynamic Color Themes** - Each card has its own color palette
- 📱 **Fully Responsive** - Optimized for desktop, tablet, and mobile devices
- 🖥️ **Aspect Ratio Support** - Perfect rendering on 16:9 and 20:9 displays
- ⌨️ **Keyboard Navigation** - Use arrow keys to navigate between slides
- 👆 **Touch Support** - Swipe gestures for mobile devices
- ✨ **Smooth Animations** - Hardware-accelerated transitions and effects
- 🎯 **Optimized Performance** - CSS animations with `will-change` for better FPS

## 📸 Screenshots

### Desktop View (16:9)
![Desktop View 1](https://github.com/user-attachments/assets/e9496d8d-ffad-4d5b-97dd-6250f660352a)

### Color Theme Transitions
![Desktop View 2](https://github.com/user-attachments/assets/c9c55310-53e6-454c-a733-84bed1b8803f)

### Standard Display (1920x1080)
![1920x1080 View](https://github.com/user-attachments/assets/a74b3525-eba7-4eb6-8ed1-65ff1f34ef1c)

### Ultrawide Display (20:9)
![Ultrawide View](https://github.com/user-attachments/assets/bc563649-61c8-4fc4-abff-230d80afdb67)

## 🚀 Live Demo

Visit the live site: **[https://anacondy.github.io/25--3-pro-test/](https://anacondy.github.io/25--3-pro-test/)**

## 🎯 Design Topics Covered

1. **Visual Hierarchy** - Guiding the Eye
2. **Color Theory** - Emotional Impact
3. **Typography** - Voice & Tone
4. **UX Design** - Solving Problems
5. **White Space** - Room to Breathe
6. **Accessibility** - Design for Everyone

## 🛠️ Technologies Used

- **HTML5** - Semantic markup
- **CSS3** - Advanced styling with glassmorphism
  - Backdrop filters
  - CSS Grid & Flexbox
  - CSS Custom Properties (variables)
  - CSS Animations & Transitions
  - Media queries for responsive design
- **Vanilla JavaScript** - No dependencies
  - Dynamic carousel functionality
  - Touch/swipe event handling
  - Responsive resize handling

## 🎨 Key Design Elements

### Glassmorphism Effect
- Semi-transparent backgrounds with `rgba(255, 255, 255, 0.03)`
- Backdrop blur filter for frosted glass effect
- Subtle borders and shadows
- Grid pattern overlay for depth

### Responsive Typography
- Fluid font sizes using `clamp()` function
- Scales smoothly across all device sizes
- Maintains readability on all screens

### Smooth Animations
- `cubic-bezier` easing functions for natural motion
- 600ms transition duration for carousel slides
- Floating cube animation with `ease-in-out`
- Color theme transitions on card change

## 📱 Responsive Breakpoints

The design adapts seamlessly to different screen sizes:

- **Desktop (16:9)**: 1920x1080 and similar
- **Ultrawide (20:9)**: 2560x1080 and similar
- **Tablet**: 768px - 1024px
- **Mobile**: < 768px

## ⌨️ Usage

### Keyboard Controls
- `→` (Right Arrow) - Next slide
- `←` (Left Arrow) - Previous slide

### Touch Controls
- **Swipe Left** - Next slide
- **Swipe Right** - Previous slide

## 🚀 Getting Started

### Quick Start

1. Clone the repository:
```bash
git clone https://github.com/anacondy/25--3-pro-test.git
```

2. Open `index.html` in your browser:
```bash
cd 25--3-pro-test
open index.html  # macOS
# or
xdg-open index.html  # Linux
# or simply drag and drop into your browser
```

### Local Development Server

Using Python:
```bash
python -m http.server 8080
```

Using Node.js:
```bash
npx http-server
```

Then visit `http://localhost:8080` in your browser.

## 📁 Project Structure

```
25--3-pro-test/
├── index.html          # Main carousel page (recommended)
├── index1.html         # Single card variant
├── index2.html         # Original carousel implementation
└── README.md           # This file
```

## 🎯 Browser Support

- ✅ Chrome/Edge 88+
- ✅ Firefox 103+
- ✅ Safari 15.4+
- ✅ Opera 74+

**Note:** Backdrop filters require modern browser support. For best results, use the latest browser versions.

## 🔧 Customization

### Changing Colors

Each card has a `data-theme` attribute with a color value:

```html
<div class="glass-card" data-theme="#1db954">
```

Modify these values to customize the color themes.

### Adding New Cards

1. Copy an existing card structure
2. Update the content (title, description, etc.)
3. Set a new `data-theme` color
4. Update the pagination counter

### Adjusting Animation Speed

Modify the transition duration in CSS:

```css
.carousel-track {
    transition: transform 0.6s cubic-bezier(0.25, 1, 0.5, 1);
}
```

## 🎓 Educational Purpose

This project demonstrates:
- Modern CSS techniques (glassmorphism, backdrop filters)
- Responsive design best practices
- JavaScript carousel implementation
- Touch event handling
- Performance optimization with `will-change`
- Accessibility considerations

## 📄 License

This project is open source and available under the MIT License.

## 👨‍💻 Credits

**Design & Development**: midecreativestudio

## 🤝 Contributing

Contributions, issues, and feature requests are welcome!

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📞 Contact

For questions or feedback, please open an issue on GitHub.

---

**Enjoy the glassmorphic design experience!** ✨
