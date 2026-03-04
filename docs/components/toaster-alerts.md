# Toaster Alert

**Status:** Alpha
**Since:** v2.3.0

Floating notification card that appears top-right, providing typed feedback with an icon, title, description, optional action link, and close button.

---

## Anatomy

```
┌─────────────────────────────────────────────────┐
│  [icon]  Title                          [close] │
│          Description text goes here.            │
│          Learn More                             │
└─────────────────────────────────────────────────┘
```

| Slot | Element | Notes |
|------|---------|-------|
| Icon | `.icon-fb-info` / `.icon-fb-success` / `.icon-fb-error` | 16×16 feedback badge |
| Title | `.toaster-title` | 16px / 500, `--text-strong` |
| Description | `.toaster-desc` | 14px / 400, `--text-subtle` |
| Action | `.btn-text` | Optional link (e.g. "Learn More") |
| Close | `.toaster-close` > `.icon .icon-close` | 16×16 close button |

---

## Variants

| Class | Border Color | Icon | Use When |
|-------|-------------|------|----------|
| `.toaster-info` | `--neutral-500` (gray) | `.icon-fb-info` | General information, upcoming events |
| `.toaster-success` | `--blue-500` (blue) | `.icon-fb-success` | Confirmed actions, new items created |
| `.toaster-error` | `--red-500` (red) | `.icon-fb-error` | Failed operations, scan errors |

---

## States

| State | Behavior |
|-------|----------|
| Hidden (default) | `opacity: 0; transform: translateX(100px)` |
| Visible | Add `.visible` → slides in from right, opacity 1 |
| Hover close | Close icon darkens to `--text-strong` |

---

## Dimensions

| Property | Value |
|----------|-------|
| Width | 485px (`max-width: calc(100vw - 40px)`) |
| Padding | `var(--space-std)` (20px) |
| Gap (icon ↔ content) | `var(--space-std)` (20px) |
| Gap (title ↔ desc) | `var(--space-tight)` (4px) |
| Gap (text ↔ action) | `var(--space-sm)` (12px) |
| Border radius | `var(--radius)` (4px) |
| Shadow | `var(--shadow-toast)` |
| Position | `fixed; top: 76px; right: 20px; z-index: 1001` |

---

## Dark Mode

All tokens auto-adapt via `[data-theme="dark"]`:
- Background: `--surface-card` (dark card surface)
- Text: `--text-strong` / `--text-subtle` swap to dark-mode values
- Shadow: `--shadow-toast` darkens
- Border colors and feedback icons remain unchanged

---

## HTML

```html
<div class="toaster toaster-info visible">
  <span class="icon-fb-info"></span>
  <div class="toaster-content">
    <div class="toaster-text">
      <div class="toaster-title">Upcoming Event</div>
      <div class="toaster-desc">You have an upcoming scan event in about an hour.</div>
    </div>
    <button class="btn-text">Learn More</button>
  </div>
  <button class="toaster-close"><span class="icon icon-close"></span></button>
</div>
```

Replace `.toaster-info` + `.icon-fb-info` with the matching variant:
- `.toaster-success` + `.icon-fb-success`
- `.toaster-error` + `.icon-fb-error`

---

## Feedback Icons

Three multi-color badge icons in `icons.css`:

| Class | Appearance |
|-------|-----------|
| `.icon-fb-info` | Navy rounded square with white "i" |
| `.icon-fb-success` | Blue rounded square with white ✓ |
| `.icon-fb-error` | Red rounded square with white ✗ |

These use `background-image` (not `mask-image`) because they are multi-color.

---

## Accessibility

- Close button has `:focus-visible` outline (2px solid `--primary`)
- Touch target: 16×16 minimum (meets WCAG 2.5.8 at 24×24 with padding)
- Color-only indicator: border color is paired with a distinct feedback icon
- `prefers-reduced-motion`: transitions disabled
- Action link inherits `.btn-text` focus styles

---

## Migration from `.top-toast`

The old `.top-toast` component (border-left stripe, circle icons) is replaced by `.toaster`:

| Old | New |
|-----|-----|
| `.top-toast` | `.toaster` |
| `.type-info` / `.type-success` / `.type-error` | `.toaster-info` / `.toaster-success` / `.toaster-error` |
| `.top-toast-icon` (inline SVG) | `.icon-fb-info` / `.icon-fb-success` / `.icon-fb-error` |
| `.top-toast-content` | `.toaster-content` |
| `.top-toast-title` | `.toaster-title` |
| `.top-toast-desc` | `.toaster-desc` |
| `.top-toast-close` | `.toaster-close` |
| `.visible` | `.visible` (unchanged) |
