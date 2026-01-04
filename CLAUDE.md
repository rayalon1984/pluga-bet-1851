# CLAUDE.md - AI Assistant Guide

This document provides comprehensive information about the pluga-bet-1851 repository for AI assistants to understand and work with the codebase effectively.

## Project Overview

**Project Name:** פלוגה ב׳ (Company B) - Valley Defenders Fundraising Website
**Type:** Static Single-Page Application (SPA)
**Purpose:** Fundraising campaign website for Israeli military unit equipment
**Languages:** Hebrew (primary) and English
**Repository:** https://github.com/rayalon1984/pluga-bet-1851
**Live Site:** https://rayalon1984.github.io/pluga-bet-1851/

### Mission
Help raise funds to equip Company B soldiers with tactical gear, protective equipment, and personal items through transparent donation methods.

---

## Repository Structure

```
pluga-bet-1851/
├── index.html                          # Main HTML file (single-page app)
├── styles.css                          # All CSS styling
├── 6886f148-3bfd-4541-84b5-32b428736f2b.jpeg  # Company logo badge
├── ae00d74b-f38a-428d-980e-6839eaf25b83.jpeg  # Hero background image
└── .git/                               # Git version control
```

### File Purpose

- **index.html**: Complete single-page application with embedded JavaScript
- **styles.css**: All styling including responsive design, animations, RTL/LTR support
- **Images**: Logo badge and hero section background
- **No build process**: Pure HTML/CSS/JS - no bundler, no dependencies

---

## Technology Stack

### Core Technologies
- **HTML5**: Semantic markup, data attributes for translations
- **CSS3**: Custom properties (CSS variables), Grid, Flexbox, animations
- **Vanilla JavaScript**: No frameworks or libraries
- **Google Fonts**: Heebo font family (Hebrew + Latin support)

### Key Features
- **No Dependencies**: Zero npm packages, no build tools
- **Static Hosting**: GitHub Pages deployment
- **Progressive Enhancement**: Works without JavaScript (except language switching)
- **Mobile-First**: Responsive design with breakpoints at 480px, 768px

---

## Key Features & Functionality

### 1. Bilingual Support (Hebrew/English)
- **Default Language**: Hebrew (RTL)
- **Auto-Detection**: Uses IP geolocation (ipapi.co) to detect country
  - Israel (IL) → Hebrew
  - Other countries → English
- **Manual Toggle**: Fixed position button (top-left RTL, top-right LTR)
- **Persistence**: `localStorage` saves user preference
- **Implementation**: `data-he` and `data-en` attributes on translatable elements

### 2. Language Toggle Behavior
```javascript
// Shows TARGET language (where you'll go, not where you are)
// Currently Hebrew → Shows "EN 🇺🇸"
// Currently English → Shows "IL 🇮🇱"
```

### 3. Donation Methods
- **PayBox**: Online payment link
- **Bit**: Israeli mobile payment link
- **Bank Transfer**: Expandable section with copyable account details
  - Click individual fields to copy
  - "Copy All" button for complete details

### 4. Equipment Listings
Three categories with pricing in Israeli Shekels (₪):
- **Tactical Gear** (ציוד מבצעי): Red dot sights, scopes, binoculars, laser markers
- **Enhanced Protection** (הגנה משופרת): Goggles, knee pads, boots, uniforms, first aid
- **Personal Gear** (ציוד אישי): Winter jackets, sweatshirts, weapon slings, belts

### 5. WhatsApp Integration
- **Floating Button**: Bottom-right contact button (fixed position)
- **Share Button**: Footer section with pre-written bilingual messages
- **Contact**: Links to wa.me/972543320613

### 6. Visual Design
- **Hero Section**: Full-screen with background image, overlay gradients
- **Logo Badge**: Top-right corner (scrolls with page, not fixed)
- **Color Scheme**: Military-inspired olive greens, gold accents, sand tones
- **Animations**: Scroll-triggered animations using IntersectionObserver
- **Smooth Scrolling**: Anchor links scroll smoothly to sections

---

## File Organization

### index.html Structure
```
<!DOCTYPE html>
├── <head>
│   ├── Meta tags (charset, viewport, description)
│   ├── Google Fonts (Heebo)
│   ├── styles.css
│   └── Inline SVG favicon
├── <body>
│   ├── Language Toggle Button (fixed position)
│   ├── WhatsApp Float Button (fixed position)
│   ├── Hero Section
│   │   ├── Background image
│   │   ├── Overlay gradients
│   │   ├── Logo badge
│   │   └── CTA button
│   ├── Why Section (Equipment Grid)
│   │   └── 3 categories of equipment with prices
│   ├── Donate Section
│   │   ├── 3 donation cards (PayBox, Bit, Bank)
│   │   └── Expandable bank details
│   ├── Message Section (Quote)
│   ├── Share Section (WhatsApp)
│   ├── Footer
│   └── <script> (inline JavaScript)
└── </html>
```

### styles.css Structure
```css
1. CSS Variables (:root)
2. Reset & Base Styles
3. Language Toggle
4. Logo Badge
5. RTL/LTR Adjustments
6. WhatsApp Float Button
7. Hero Section
8. Equipment Grid (Why Section)
9. Donate Section & Bank Details
10. Message Section
11. Share Section
12. Footer
13. Responsive Design (768px, 480px)
14. Animations
15. Accessibility (reduced motion, focus states)
16. Print Styles
```

---

## Development Conventions

### CSS Conventions

#### 1. CSS Variables
```css
/* All colors, shadows, transitions defined in :root */
--olive-dark: #2d3a2e;
--olive: #4a5d4c;
--gold: #c9a227;
--shadow-md: 0 4px 20px rgba(0,0,0,0.12);
--transition: all 0.3s ease;
--radius: 16px;
```

#### 2. Naming Conventions
- **BEM-inspired** but not strict
- Descriptive class names: `.equipment-category`, `.donate-card`, `.bank-details`
- Section-based: `.hero`, `.why-section`, `.donate-section`
- Modifier classes: `.show`, `.animate-in`, `.copied`

#### 3. Responsive Design
- **Mobile-First** approach
- Breakpoints:
  - `@media (max-width: 768px)` - Tablet
  - `@media (max-width: 480px)` - Mobile
- `clamp()` for fluid typography: `font-size: clamp(1.8rem, 5vw, 2.5rem);`

#### 4. RTL/LTR Support
```css
/* Default styles for RTL (Hebrew) */
.lang-toggle { left: 20px; }

/* LTR overrides */
[dir="ltr"] .lang-toggle { left: auto; right: 20px; }
```

### HTML Conventions

#### 1. Bilingual Attributes
```html
<h1 data-he="יחד ננצח" data-en="Together We Stand">יחד ננצח</h1>
```
- Default content is Hebrew
- JavaScript swaps `textContent` based on language
- All user-facing text uses this pattern

#### 2. Semantic HTML
- Proper heading hierarchy (h1 → h2 → h3)
- Semantic tags: `<section>`, `<footer>`, `<blockquote>`
- Accessible links: `rel="noopener"` on external links

#### 3. Accessibility
- `title` attributes on buttons
- `alt` text on images
- Focus states for keyboard navigation
- `@media (prefers-reduced-motion: reduce)` support

### JavaScript Conventions

#### 1. Code Organization
```javascript
// 1. State variables
let currentLang = 'he';

// 2. Translation objects
const translations = { ... };

// 3. Core functions (language, bank details, etc.)
function toggleLanguage() { ... }
function copyBankDetails() { ... }

// 4. Event listeners
document.querySelector('.cta-button').addEventListener('click', ...);

// 5. Initialization
initLanguage();
```

#### 2. Async Patterns
- Uses `async/await` for IP detection
- Graceful fallback if geolocation fails
- LocalStorage preference takes priority

#### 3. DOM Manipulation
- `querySelector` / `querySelectorAll` (no jQuery)
- `classList` for class manipulation
- `setAttribute` for language/direction changes

#### 4. Animation Patterns
- **IntersectionObserver** for scroll animations
- CSS classes added when elements enter viewport
- Staggered animations with `transition-delay`

---

## Bilingual Implementation Guide

### How Language Switching Works

1. **Initial Load**
   ```javascript
   // Priority order:
   1. Check localStorage for saved preference
   2. Detect country via IP (ipapi.co/json)
   3. Default to Hebrew if detection fails
   ```

2. **Language Application**
   ```javascript
   function applyLanguage(lang) {
     // Set HTML attributes
     document.documentElement.setAttribute('lang', lang);
     document.documentElement.setAttribute('dir', lang === 'he' ? 'rtl' : 'ltr');

     // Update all translatable elements
     document.querySelectorAll('[data-he][data-en]').forEach(el => {
       el.textContent = el.getAttribute(`data-${lang}`);
     });
   }
   ```

3. **Toggle Button Display**
   - Shows TARGET language (where clicking will take you)
   - Hebrew mode → Shows "EN 🇺🇸"
   - English mode → Shows "IL 🇮🇱"

### Adding New Translatable Text

1. **HTML Elements**
   ```html
   <element data-he="עברית" data-en="English">עברית</element>
   ```

2. **Dynamic JavaScript Text**
   ```javascript
   const translations = {
     copySuccess: { he: '✓ הועתק!', en: '✓ Copied!' }
   };
   // Access: translations.copySuccess[currentLang]
   ```

---

## Color Scheme & Visual Design

### Brand Colors
```css
Olive Green (Primary):
  --olive-dark: #2d3a2e  (headings, dark text)
  --olive: #4a5d4c       (footer, accents)
  --olive-light: #6b7d6c (borders, subtle elements)

Gold (Accent):
  --gold: #c9a227        (CTA buttons, highlights)
  --gold-light: #e8c547  (hover states)

Sand (Backgrounds):
  --sand: #d4c5a9
  --sand-light: #e8dcc6
  --off-white: #f8f6f1   (main background)

Service Colors:
  --paybox-color: #00a651  (green)
  --bit-color: #3dcdab     (teal)
  --bank-color: #2c5282    (blue)
```

### Visual Hierarchy
1. **Hero**: Full-screen, dark overlay, white text, gold CTA
2. **Content Sections**: White/off-white backgrounds, clean spacing
3. **Dark Sections**: Olive-dark for quotes and share section
4. **Cards**: White with subtle shadows, hover effects with color borders

---

## Git Workflow & Conventions

### Branch Naming
- Main branch: (not specified, likely `main` or `master`)
- Feature branches: `claude/feature-name-XXXXX` (for Claude AI work)

### Commit Message Patterns (from history)
```
✓ "Update language toggle: show target language (EN 🇺🇸 / IL 🇮🇱)"
✓ "Move logo inside hero section (scrolls with page, not fixed)"
✓ "Fix bank details to show full content including button"
✓ "Add WhatsApp share button in footer with pre-written message"
```

**Convention**:
- Imperative mood ("Add", "Fix", "Update", not "Added", "Fixed")
- Descriptive but concise
- Include emoji context when relevant (🇺🇸 🇮🇱)

### Development Workflow
1. All changes are direct commits (no build process)
2. Test locally by opening `index.html` in browser
3. Commit and push to GitHub
4. GitHub Pages auto-deploys from repository

---

## Deployment

### GitHub Pages
- **Hosting**: GitHub Pages (static site hosting)
- **URL**: https://rayalon1984.github.io/pluga-bet-1851/
- **Deployment**: Automatic on push to main branch
- **No Build**: Files served directly (HTML/CSS/JS)

### Testing Checklist
Before committing changes, verify:
- [ ] Both Hebrew and English display correctly
- [ ] RTL/LTR layouts work properly
- [ ] Mobile responsive (test at 375px, 768px, 1024px)
- [ ] All links work (WhatsApp, donation methods)
- [ ] Copy-to-clipboard functions work
- [ ] Smooth scrolling works
- [ ] Animations trigger on scroll
- [ ] Logo and images load correctly

---

## AI Assistant Guidelines

### When Working on This Project

#### 1. Understand the Context
- This is a military fundraising site for an Israeli unit
- Content is sensitive and should be respectful
- Hebrew is primary language, English is secondary
- Cultural context: Israeli military service, IDF units

#### 2. Code Modification Principles
- **NO frameworks**: Don't suggest React, Vue, etc.
- **NO build tools**: Don't add webpack, npm, etc.
- **Keep it simple**: This is intentionally vanilla HTML/CSS/JS
- **Maintain bilingual**: Every change needs Hebrew + English
- **Preserve RTL/LTR**: Test both directions

#### 3. When Adding Features
```javascript
// ✅ Good: Pure JavaScript
function newFeature() {
  const element = document.querySelector('.target');
  element.classList.add('active');
}

// ❌ Bad: Don't add libraries
import React from 'react'; // NO
const $ = require('jquery'); // NO
```

#### 4. When Modifying Styles
- Use existing CSS variables
- Follow mobile-first approach
- Add RTL/LTR overrides if needed
- Keep animations performant (transform, opacity only)

#### 5. When Adding Text
```html
<!-- ✅ Always add both languages -->
<p data-he="טקסט עברית" data-en="English text">טקסט עברית</p>

<!-- ❌ Don't add single language -->
<p>English only text</p>
```

#### 6. Common Tasks

**Adding a new section:**
1. Add HTML structure to `index.html`
2. Add bilingual attributes (`data-he`, `data-en`)
3. Add styles to `styles.css` (use CSS variables)
4. Add responsive breakpoints (768px, 480px)
5. Add RTL/LTR adjustments if needed
6. Test both languages

**Modifying colors:**
1. Update CSS variables in `:root`
2. Don't use inline styles or hardcoded colors
3. Maintain contrast ratios for accessibility

**Adding JavaScript functionality:**
1. Add functions before event listeners
2. Update initialization section
3. Handle both Hebrew and English states
4. Test without JavaScript for progressive enhancement

#### 7. Translation Guidelines
- **Hebrew**: Right-to-left, use proper Hebrew typography
- **English**: Left-to-right, clear and concise
- **Don't translate**: Prices (₪), brand names (PayBox, Bit)
- **Emoji context**: 🇮🇱 for Israel, 🇺🇸 for USA in language toggle

#### 8. File Size Considerations
- Keep images optimized (both images are ~500-700KB)
- Minimize external dependencies (only Google Fonts)
- Inline small assets (SVG icons, favicon)

#### 9. Accessibility Requirements
- Keyboard navigation must work
- Focus states visible
- Color contrast WCAG AA minimum
- `alt` text on images
- ARIA labels where needed

#### 10. Testing Checklist for AI Assistants
Before suggesting code changes, verify:
- [ ] Change works in both Hebrew and English
- [ ] RTL and LTR layouts both work
- [ ] Mobile responsive (320px minimum width)
- [ ] No JavaScript errors in console
- [ ] CSS doesn't break existing styles
- [ ] No external dependencies added
- [ ] Git commit message follows conventions

---

## Common Modification Patterns

### Adding a New Equipment Item
```html
<!-- In appropriate .equipment-list -->
<div class="equipment-item">
    <span class="item-name" data-he="שם הפריט" data-en="Item Name">שם הפריט</span>
    <span class="item-price">₪X,XXX</span>
</div>
```

### Adding a New Donation Method
```html
<a href="[URL]" class="donate-card [color-class]" target="_blank" rel="noopener">
    <div class="donate-icon">
        <!-- SVG icon -->
    </div>
    <h3>Service Name</h3>
    <p data-he="תיאור בעברית" data-en="English description">תיאור בעברית</p>
    <span class="donate-cta" data-he="לתרומה ←" data-en="Donate →">לתרומה ←</span>
</a>
```

### Updating Bank Details
```html
<!-- Update values in #bank-details section -->
<span class="value" id="bank-name">[Bank Name]</span>
<span class="value" id="bank-branch">[Branch Number]</span>
<span class="value" id="bank-account">[Account Number]</span>
<span class="value" id="bank-holder">[Account Holder Name]</span>
```

---

## Performance Considerations

### Current Performance
- **No build step**: Instant deployment
- **Minimal HTTP requests**: 3 files + 1 font
- **Small bundle**: ~45KB HTML + ~25KB CSS
- **Optimized images**: JPEG compression

### Best Practices
- Keep CSS in single file (HTTP/2 makes splitting unnecessary)
- Keep JavaScript inline (one less HTTP request)
- Use CSS Grid/Flexbox (better than float/table layouts)
- Leverage browser caching (static assets)
- Use `loading="lazy"` for below-fold images if adding more

---

## Browser Support

### Target Browsers
- **Modern browsers**: Chrome 90+, Firefox 88+, Safari 14+, Edge 90+
- **Mobile**: iOS Safari 14+, Chrome Android 90+
- **NO IE11 support** (uses CSS Grid, CSS custom properties)

### Fallbacks
- CSS Grid with `repeat(auto-fit, minmax())` degrades gracefully
- IntersectionObserver has broad support (90%+ browsers)
- `clamp()` fallback: min-font-size browsers ignore it

---

## Security Considerations

### Current Implementation
- **No user input**: No forms, no XSS risk
- **External links**: All use `rel="noopener"` (prevents tabnabbing)
- **No authentication**: Public fundraising page
- **No sensitive data**: Bank details are public donation info

### Third-Party Services
- **ipapi.co**: IP geolocation (may fail, has fallback)
- **Google Fonts**: Trusted CDN
- **WhatsApp**: wa.me links (safe, no data exchange)

---

## Future Enhancement Ideas

### Potential Improvements (for AI assistants to consider)
1. **Analytics**: Add Google Analytics or privacy-friendly alternative
2. **Social Meta Tags**: OpenGraph for better social sharing
3. **Progress Bar**: Show fundraising goal progress
4. **Testimonials**: Section with soldier testimonials
5. **Gallery**: Photos of equipment in use
6. **Newsletter**: Email signup for updates
7. **Live Chat**: Integration with messaging platform
8. **Donation Tracking**: Display recent donations (with privacy)

### Technical Improvements
1. **PWA**: Make installable as Progressive Web App
2. **Service Worker**: Offline functionality
3. **WebP Images**: Better compression with JPEG fallback
4. **Dark Mode**: CSS `prefers-color-scheme` support
5. **A11y Audit**: Full WCAG AAA compliance
6. **SEO**: Schema.org structured data

---

## Contact & Support

### Repository Owner
- **GitHub**: rayalon1984
- **WhatsApp**: +972-54-332-0613 (from website)

### For AI Assistants
When making changes:
1. Follow conventions in this guide
2. Test thoroughly in both languages
3. Commit with clear messages
4. Don't break existing functionality
5. Keep it simple and maintainable

---

## Document Version

**Version**: 1.0
**Last Updated**: 2026-01-04
**Codebase State**: Commit 123a713 (Language toggle update)

---

## Quick Reference

### Key Files
- `index.html` - All HTML and inline JS
- `styles.css` - All CSS styling

### Key Functions (JavaScript)
- `toggleLanguage()` - Switch between he/en
- `applyLanguage(lang)` - Apply language to DOM
- `toggleBankDetails()` - Show/hide bank section
- `copyBankDetails()` - Copy all bank info
- `initLanguage()` - Initialize language on load

### Key CSS Classes
- `.hero` - Full-screen hero section
- `.equipment-category` - Equipment cards
- `.donate-card` - Donation method cards
- `.bank-details` - Expandable bank info
- `.animate-in` - Scroll animation trigger
- `.show` - Display toggle modifier

### Key Data Attributes
- `data-he` - Hebrew translation
- `data-en` - English translation
- `dir="rtl"` / `dir="ltr"` - Text direction

---

**End of Document**

This guide should enable any AI assistant to understand and work effectively with this codebase. Update this document when significant changes are made to the project structure or conventions.
