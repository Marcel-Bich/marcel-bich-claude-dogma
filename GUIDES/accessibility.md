# Accessibility Guide

<mobile_first>
## Mobile-First Design

**Principle:** Design for the smallest viewport first, then enhance for larger screens.

**Breakpoints (min-width):**
| Name | Size | Target |
|------|------|--------|
| Base | 320px | Small phones |
| sm | 640px | Large phones |
| md | 768px | Tablets |
| lg | 1024px | Laptops |
| xl | 1280px | Desktops |

```css
/* Mobile-first CSS */
.container {
  padding: 1rem;           /* Mobile default */
}

@media (min-width: 768px) {
  .container {
    padding: 2rem;         /* Tablet+ */
  }
}

@media (min-width: 1024px) {
  .container {
    padding: 3rem;         /* Desktop */
    max-width: 1200px;
  }
}
```

**Touch targets:**
```css
/* Minimum 44x44px for touch */
button, a, input[type="checkbox"] {
  min-height: 44px;
  min-width: 44px;
}
```

**Viewport meta tag (required):**
```html
<meta name="viewport" content="width=device-width, initial-scale=1">
```

**Test:** Chrome DevTools > Toggle device toolbar (Ctrl+Shift+M)
</mobile_first>

<wcag_basics>
## WCAG 2.1 Basics

**Levels:**
- **A** - Minimum (must have)
- **AA** - Standard (recommended target)
- **AAA** - Enhanced (specific cases)

**Principles (POUR):**
- **Perceivable** - Users can perceive content
- **Operable** - Users can interact with UI
- **Understandable** - Content is clear
- **Robust** - Works with assistive tech
</wcag_basics>

<keyboard>
## Keyboard Navigation

```html
<!-- Interactive elements must be focusable -->
<button>Click me</button>  <!-- Focusable by default -->
<a href="/page">Link</a>   <!-- Focusable by default -->

<!-- Custom elements need tabindex -->
<div role="button" tabindex="0" onclick="...">
  Custom button
</div>

<!-- Skip to main content (add to start of page) -->
<a href="#main" class="skip-link">Skip to main content</a>
```

**Test:** Tab through entire page. Every interactive element should be reachable.
</keyboard>

<aria>
## ARIA Labels

```html
<!-- Label non-text elements -->
<button aria-label="Close dialog">
  <svg>...</svg>  <!-- Icon only, no text -->
</button>

<!-- Describe element purpose -->
<nav aria-label="Main navigation">...</nav>
<nav aria-label="Footer navigation">...</nav>

<!-- Live regions for dynamic content -->
<div aria-live="polite" aria-atomic="true">
  <!-- Screen reader announces changes here -->
</div>

<!-- States -->
<button aria-expanded="false" aria-controls="menu">
  Menu
</button>
<ul id="menu" hidden>...</ul>
```

**Rule:** Use semantic HTML first. ARIA only when HTML isn't enough.
</aria>

<color_contrast>
## Color Contrast

| Element | Minimum Ratio | Example |
|---------|---------------|---------|
| Normal text | 4.5:1 | #595959 on #ffffff |
| Large text (18pt+) | 3:1 | #767676 on #ffffff |
| UI components | 3:1 | Borders, icons |

**Tools:**
- Chrome DevTools: Inspect > Color picker shows ratio
- https://webaim.org/resources/contrastchecker/

**Don't rely on color alone:**
```html
<!-- BAD: Color is only indicator -->
<span class="error" style="color: red">Required</span>

<!-- GOOD: Icon + color + text -->
<span class="error">
  <svg aria-hidden="true">...</svg> <!-- Error icon -->
  Required field
</span>
```
</color_contrast>

<images>
## Images and Alt Text

```html
<!-- Meaningful image: describe content -->
<img src="chart.png" alt="Sales increased 50% in Q4 2024">

<!-- Decorative image: empty alt -->
<img src="decoration.png" alt="">

<!-- Complex image: provide long description -->
<figure>
  <img src="infographic.png" alt="Market analysis summary">
  <figcaption>
    Full description: The infographic shows...
  </figcaption>
</figure>

<!-- Background/decorative: use CSS instead -->
<div class="hero" style="background-image: url(bg.jpg)">
  <!-- No alt needed for CSS backgrounds -->
</div>
```
</images>

<focus>
## Focus Management

```css
/* Never remove focus outline entirely */
button:focus {
  /* BAD */
  outline: none;
}

/* Customize but keep visible */
button:focus-visible {
  outline: 2px solid #0066cc;
  outline-offset: 2px;
}

/* Hide outline for mouse, show for keyboard */
button:focus:not(:focus-visible) {
  outline: none;
}
button:focus-visible {
  outline: 2px solid #0066cc;
}
```

**Modal focus trap:**
```typescript
// Trap focus inside modal when open
const modal = document.getElementById('modal');
const focusableElements = modal.querySelectorAll(
  'button, [href], input, select, textarea, [tabindex]:not([tabindex="-1"])'
);
const firstElement = focusableElements[0];
const lastElement = focusableElements[focusableElements.length - 1];

modal.addEventListener('keydown', (e) => {
  if (e.key === 'Tab') {
    if (e.shiftKey && document.activeElement === firstElement) {
      e.preventDefault();
      lastElement.focus();
    } else if (!e.shiftKey && document.activeElement === lastElement) {
      e.preventDefault();
      firstElement.focus();
    }
  }
});
```
</focus>

<testing>
## Testing Accessibility

**Manual tests:**
1. Tab through page - all interactive elements reachable?
2. Use screen reader (VoiceOver, NVDA) - content makes sense?
3. Zoom to 200% - layout still works?
4. Turn off CSS - content still readable?

**Automated tools:**
- Chrome DevTools > Lighthouse > Accessibility
- axe DevTools browser extension
- `pnpm add -D @axe-core/playwright` for E2E tests

**Axe in Playwright:**
```typescript
import AxeBuilder from '@axe-core/playwright';

test('homepage has no a11y violations', async ({ page }) => {
  await page.goto('/');
  const results = await new AxeBuilder({ page }).analyze();
  expect(results.violations).toEqual([]);
});
```
</testing>

<checklist>
## Quick Checklist

- [ ] All interactive elements keyboard accessible
- [ ] Tab order logical
- [ ] Focus visible on all elements
- [ ] Color contrast sufficient
- [ ] Images have alt text
- [ ] Forms have labels
- [ ] Error messages clear and associated
- [ ] Page works at 200% zoom
- [ ] No reliance on color alone
</checklist>
