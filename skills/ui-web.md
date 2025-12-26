# UI Design Skill

*Load with: base.md + react-web.md (or react-native.md)*

## Core Philosophy

**Beautiful UI is not decoration - it's communication.** Every visual choice should serve clarity, hierarchy, and user confidence. Default to elegance and restraint.

## Design Principles

### 1. Visual Hierarchy
```
Primary Action    → Bold, high contrast, prominent
Secondary Action  → Subtle, lower contrast
Tertiary/Links    → Minimal, text-style
```

### 2. Spacing System (8px Grid)
```typescript
// Tailwind spacing scale - USE CONSISTENTLY
const spacing = {
  xs: 'p-1',      // 4px  - tight internal
  sm: 'p-2',      // 8px  - compact
  md: 'p-4',      // 16px - default
  lg: 'p-6',      // 24px - comfortable
  xl: 'p-8',      // 32px - spacious
  '2xl': 'p-12',  // 48px - section gaps
};

// Rule: More whitespace = more premium feel
// Rule: Consistent spacing > perfect spacing
```

### 3. Typography Scale
```typescript
// Limit to 3-4 font sizes per page
const typography = {
  hero: 'text-4xl md:text-5xl font-bold tracking-tight',
  heading: 'text-2xl md:text-3xl font-semibold',
  subheading: 'text-lg md:text-xl font-medium',
  body: 'text-base leading-relaxed',
  caption: 'text-sm text-gray-500',
};

// Rule: Never use more than 2 font families
// Rule: Line height 1.5-1.7 for body text
```

## Glassmorphism (Web)

### Base Glass Card
```tsx
// Modern glass effect - use sparingly for emphasis
const GlassCard = ({ children, className = '' }) => (
  <div className={`
    backdrop-blur-xl
    bg-white/10
    border border-white/20
    rounded-2xl
    shadow-xl
    shadow-black/5
    ${className}
  `}>
    {children}
  </div>
);
```

### Glass Variants
```tsx
// Light mode glass
const lightGlass = `
  backdrop-blur-xl
  bg-white/70
  border border-white/50
  shadow-lg shadow-gray-200/50
`;

// Dark mode glass
const darkGlass = `
  backdrop-blur-xl
  bg-gray-900/70
  border border-white/10
  shadow-xl shadow-black/20
`;

// Frosted sidebar
const frostedSidebar = `
  backdrop-blur-2xl
  bg-gradient-to-b from-white/80 to-white/60
  border-r border-white/30
`;

// Floating action glass
const floatingGlass = `
  backdrop-blur-md
  bg-white/90
  rounded-full
  shadow-lg shadow-black/10
  border border-white/50
`;
```

### When to Use Glassmorphism
```
✓ Hero sections with image backgrounds
✓ Floating cards over gradients
✓ Modal overlays
✓ Navigation bars (subtle)
✓ Feature highlights

✗ Every card (overuse kills the effect)
✗ Text-heavy content areas
✗ Forms (reduces contrast)
✗ Data tables
```

## Color System

### Semantic Colors
```typescript
const colors = {
  // Actions
  primary: 'bg-blue-600 hover:bg-blue-700',
  secondary: 'bg-gray-100 hover:bg-gray-200 text-gray-900',
  danger: 'bg-red-600 hover:bg-red-700',
  success: 'bg-green-600 hover:bg-green-700',

  // Surfaces
  background: 'bg-gray-50 dark:bg-gray-950',
  surface: 'bg-white dark:bg-gray-900',
  elevated: 'bg-white dark:bg-gray-800 shadow-lg',

  // Text
  textPrimary: 'text-gray-900 dark:text-white',
  textSecondary: 'text-gray-600 dark:text-gray-400',
  textMuted: 'text-gray-400 dark:text-gray-500',
};
```

### Gradient Backgrounds
```tsx
// Subtle mesh gradient (modern, premium)
const meshGradient = `
  bg-gradient-to-br
  from-blue-50 via-white to-purple-50
  dark:from-gray-950 dark:via-gray-900 dark:to-gray-950
`;

// Vibrant hero gradient
const heroGradient = `
  bg-gradient-to-r
  from-blue-600 via-purple-600 to-pink-600
`;

// Subtle radial glow
const radialGlow = `
  bg-[radial-gradient(ellipse_at_top,_var(--tw-gradient-stops))]
  from-blue-200/40 via-transparent to-transparent
`;
```

## Component Patterns

### Buttons
```tsx
// Primary button - bold, confident
const PrimaryButton = ({ children, ...props }) => (
  <button
    className="
      px-6 py-3
      bg-gray-900 dark:bg-white
      text-white dark:text-gray-900
      font-medium
      rounded-xl
      transition-all duration-200
      hover:bg-gray-800 dark:hover:bg-gray-100
      hover:shadow-lg hover:shadow-gray-900/20
      active:scale-[0.98]
      disabled:opacity-50 disabled:cursor-not-allowed
    "
    {...props}
  >
    {children}
  </button>
);

// Secondary button - subtle
const SecondaryButton = ({ children, ...props }) => (
  <button
    className="
      px-6 py-3
      bg-gray-100 dark:bg-gray-800
      text-gray-900 dark:text-white
      font-medium
      rounded-xl
      transition-all duration-200
      hover:bg-gray-200 dark:hover:bg-gray-700
      active:scale-[0.98]
    "
    {...props}
  >
    {children}
  </button>
);

// Ghost button - minimal
const GhostButton = ({ children, ...props }) => (
  <button
    className="
      px-4 py-2
      text-gray-600 dark:text-gray-400
      font-medium
      rounded-lg
      transition-colors duration-200
      hover:text-gray-900 dark:hover:text-white
      hover:bg-gray-100 dark:hover:bg-gray-800
    "
    {...props}
  >
    {children}
  </button>
);
```

### Cards
```tsx
// Clean card with subtle elevation
const Card = ({ children, className = '' }) => (
  <div className={`
    bg-white dark:bg-gray-900
    rounded-2xl
    border border-gray-200 dark:border-gray-800
    shadow-sm
    hover:shadow-md
    transition-shadow duration-300
    ${className}
  `}>
    {children}
  </div>
);

// Interactive card
const InteractiveCard = ({ children, onClick }) => (
  <button
    onClick={onClick}
    className="
      w-full text-left
      bg-white dark:bg-gray-900
      rounded-2xl
      border border-gray-200 dark:border-gray-800
      p-6
      transition-all duration-300
      hover:border-gray-300 dark:hover:border-gray-700
      hover:shadow-lg
      hover:-translate-y-1
      active:scale-[0.99]
    "
  >
    {children}
  </button>
);
```

### Input Fields
```tsx
const Input = ({ label, error, ...props }) => (
  <div className="space-y-2">
    {label && (
      <label className="block text-sm font-medium text-gray-700 dark:text-gray-300">
        {label}
      </label>
    )}
    <input
      className={`
        w-full px-4 py-3
        bg-gray-50 dark:bg-gray-800
        border-2 rounded-xl
        text-gray-900 dark:text-white
        placeholder-gray-400 dark:placeholder-gray-500
        transition-all duration-200
        focus:outline-none focus:ring-0
        ${error
          ? 'border-red-500 focus:border-red-500'
          : 'border-transparent focus:border-blue-500 focus:bg-white dark:focus:bg-gray-900'
        }
      `}
      {...props}
    />
    {error && (
      <p className="text-sm text-red-500">{error}</p>
    )}
  </div>
);
```

## Micro-Interactions

### Transitions
```typescript
// Standard transitions - ALWAYS use
const transitions = {
  fast: 'transition-all duration-150',      // Hover states
  normal: 'transition-all duration-200',    // Most interactions
  slow: 'transition-all duration-300',      // Card hovers, modals
  spring: 'transition-all duration-500 ease-out', // Page transitions
};

// Rule: Everything interactive should transition
// Rule: 150-300ms feels responsive, >500ms feels slow
```

### Hover Effects
```tsx
// Scale on hover (buttons, cards)
className="hover:scale-105 active:scale-95 transition-transform"

// Lift on hover (cards)
className="hover:-translate-y-1 hover:shadow-xl transition-all"

// Glow on hover (CTAs)
className="hover:shadow-lg hover:shadow-blue-500/25 transition-shadow"

// Border highlight (inputs, cards)
className="hover:border-gray-300 transition-colors"
```

### Loading States
```tsx
// Skeleton loader
const Skeleton = ({ className = '' }) => (
  <div className={`
    animate-pulse
    bg-gray-200 dark:bg-gray-800
    rounded-lg
    ${className}
  `} />
);

// Spinner
const Spinner = ({ size = 'md' }) => (
  <div className={`
    animate-spin rounded-full
    border-2 border-gray-200 dark:border-gray-700
    border-t-blue-600
    ${size === 'sm' ? 'w-4 h-4' : size === 'lg' ? 'w-8 h-8' : 'w-6 h-6'}
  `} />
);

// Button loading state
<button disabled className="relative">
  <span className="opacity-0">Submit</span>
  <Spinner className="absolute inset-0 m-auto" />
</button>
```

## Layout Patterns

### Container
```tsx
// Consistent max-width and padding
const Container = ({ children, className = '' }) => (
  <div className={`
    max-w-7xl mx-auto
    px-4 sm:px-6 lg:px-8
    ${className}
  `}>
    {children}
  </div>
);
```

### Section Spacing
```tsx
// Consistent vertical rhythm
const Section = ({ children }) => (
  <section className="py-16 md:py-24">
    <Container>{children}</Container>
  </section>
);
```

### Grid Systems
```tsx
// Feature grid
<div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
  {features.map(f => <FeatureCard key={f.id} {...f} />)}
</div>

// Bento grid (modern asymmetric)
<div className="grid grid-cols-2 md:grid-cols-4 gap-4">
  <div className="col-span-2 row-span-2">Large</div>
  <div className="col-span-1">Small</div>
  <div className="col-span-1">Small</div>
  <div className="col-span-2">Medium</div>
</div>
```

## Dark Mode

### Implementation
```tsx
// Always design for both modes
// Use CSS variables or Tailwind dark: prefix

// Theme toggle
const ThemeToggle = () => {
  const [dark, setDark] = useState(false);

  useEffect(() => {
    document.documentElement.classList.toggle('dark', dark);
  }, [dark]);

  return (
    <button onClick={() => setDark(!dark)}>
      {dark ? <SunIcon /> : <MoonIcon />}
    </button>
  );
};
```

### Color Pairing
```
Light Mode          Dark Mode
─────────────────────────────────
white               gray-950
gray-50             gray-900
gray-100            gray-800
gray-200            gray-700
gray-900 (text)     white (text)
gray-600 (secondary) gray-400
blue-600            blue-500
```

## Accessibility

### Contrast Requirements
```
WCAG AA: 4.5:1 for normal text, 3:1 for large text
WCAG AAA: 7:1 for normal text, 4.5:1 for large text

// Test: Use browser devtools or contrast checker
// Rule: Never use gray-400 on white for body text
```

### Focus States
```tsx
// Always visible focus rings
className="
  focus:outline-none
  focus-visible:ring-2
  focus-visible:ring-blue-500
  focus-visible:ring-offset-2
"

// Never remove focus styles without replacement
// ✗ outline-none (alone)
// ✓ outline-none + focus-visible:ring
```

### Screen Readers
```tsx
// Visually hidden but accessible
const srOnly = "absolute w-px h-px p-0 -m-px overflow-hidden whitespace-nowrap border-0";

// Icon buttons need labels
<button aria-label="Close menu">
  <XIcon className="w-6 h-6" />
</button>

// Announce dynamic content
<div role="status" aria-live="polite">
  {message}
</div>
```

## Anti-Patterns

### Never Do
```
✗ More than 3 font sizes on a page
✗ Random spacing values (use 8px grid)
✗ Pure black (#000) on pure white (#fff)
✗ Colored text on colored backgrounds without checking contrast
✗ Animations longer than 500ms for UI elements
✗ Glassmorphism everywhere
✗ Drop shadows on everything
✗ Gradients on text (hard to read)
✗ Auto-playing animations that can't be stopped
✗ Removing focus indicators
✗ Gray text below 4.5:1 contrast
✗ Tiny click targets (< 44px)
```

### Common Mistakes
```tsx
// ✗ Too many shadows
className="shadow-sm shadow-md shadow-lg" // Pick ONE

// ✗ Inconsistent rounding
className="rounded-sm rounded-lg rounded-2xl" // System: sm, lg, xl, 2xl

// ✗ Competing focal points
// One primary CTA per viewport

// ✗ Over-decorated
// If it doesn't serve function, remove it
```

## Quick Reference

### Modern Defaults
```tsx
// Border radius: 12-16px (rounded-xl to rounded-2xl)
// Shadow: subtle (shadow-sm to shadow-md)
// Font: Inter, SF Pro, system-ui
// Primary: Near-black or brand color
// Transitions: 200ms ease-out
// Spacing: 8px grid (Tailwind default)
```

### Premium Feel Checklist
```
□ Generous whitespace
□ Subtle shadows (not harsh)
□ Smooth transitions on all interactions
□ Consistent border radius
□ Limited color palette (2-3 colors max)
□ Typography hierarchy (3 sizes max)
□ High-quality imagery
□ Micro-interactions on hover/focus
□ Dark mode support
```
