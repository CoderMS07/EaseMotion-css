# Dismissible Alert

A color-coded alert component — success, error, warning, info — that slides
out smoothly when the user dismisses it. The slide-out animation is handled
entirely in CSS via the `--da-duration` custom property; JavaScript's only
job is to toggle a class and remove the element once the transition
finishes.

## Features

- ✅ Four color-coded types: `success`, `error`, `warning`, `info`
- ✅ Smooth slide-out transition on dismiss (transform + opacity + collapse)
- ✅ Animated close button (rotates on hover/focus)
- ✅ Slide speed/easing controlled via the `--da-duration` CSS custom property
- ✅ Respects `prefers-reduced-motion` for accessibility
- ✅ `role="alert"` for screen reader announcements
- ✅ No external dependencies
- ✅ Fully responsive

## Files

```
dismissible-alert/
├── demo.html   # Standalone demo page with all four alert types
├── style.css   # Component styles, color coding, and animations
└── README.md   # This file
```

## Usage

Include `style.css`, then add the markup below. A small dismiss handler
(shown in `demo.html`) toggles the `da-alert--dismissing` class on the
close button click; the actual slide-out animation is all CSS.

```html
<div class="da-alert da-alert--success" role="alert">
  <span class="da-alert__icon" aria-hidden="true">✔</span>
  <div class="da-alert__content">
    <p class="da-alert__title">Success</p>
    <p class="da-alert__message">Your changes have been saved successfully.</p>
  </div>
  <button class="da-alert__close" type="button" aria-label="Dismiss alert" onclick="dismissAlert(this)">
    <span class="da-alert__close-icon"></span>
  </button>
</div>
```

```js
function dismissAlert(button) {
  var alertEl = button.closest('.da-alert');
  if (!alertEl || alertEl.classList.contains('da-alert--dismissing')) return;

  alertEl.classList.add('da-alert--dismissing');

  var removed = false;
  var remove = function () {
    if (removed) return;
    removed = true;
    alertEl.remove();
  };

  alertEl.addEventListener('transitionend', remove, { once: true });
  var duration = parseFloat(getComputedStyle(alertEl).getPropertyValue('--da-duration')) || 350;
  setTimeout(remove, duration + 100); // fallback safety net
}
```

### Available types

Swap the modifier class to change the color coding:

| Class                | Use case                          |
|-----------------------|------------------------------------|
| `da-alert--success`  | Confirmations, completed actions   |
| `da-alert--error`    | Failures, blocking issues          |
| `da-alert--warning`  | Cautions, time-sensitive notices   |
| `da-alert--info`     | Neutral, informational messages    |

## Customization

The slide-out speed and easing are exposed as CSS custom properties, so the
animation can be retuned per-alert without editing `style.css`:

```html
<div class="da-alert da-alert--info" style="--da-duration: 500ms;">
  ...
</div>
```

| Variable        | Default                          | Description                     |
|------------------|-----------------------------------|-----------------------------------|
| `--da-duration` | `350ms`                          | Slide-out transition duration    |
| `--da-easing`   | `cubic-bezier(0.4, 0, 0.2, 1)`   | Slide-out transition easing      |
| `--da-radius`   | `10px`                           | Alert corner radius              |

Color tokens (`--da-success-*`, `--da-error-*`, `--da-warning-*`,
`--da-info-*`) are also defined on `:root` and can be overridden globally.

## Accessibility

- Each alert uses `role="alert"` so screen readers announce it when it
  appears.
- The close button has an `aria-label="Dismiss alert"` for non-visual
  users.
- All transitions are disabled (near-instant) when the user's system has
  `prefers-reduced-motion: reduce` set.

## Browser Support

Tested and working on the latest versions of:

- Chrome
- Firefox
- Safari
- Edge

Relies on standard CSS custom properties and `transition` — no vendor
prefixes required for modern browsers.

## Checklist

- [x] Alert slides out on dismiss
- [x] Color coded types
- [x] Close button with animation
- [x] Smooth slide transition