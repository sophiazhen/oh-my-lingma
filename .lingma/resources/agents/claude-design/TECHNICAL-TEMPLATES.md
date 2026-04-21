# Technical Templates

## React + Babel CDN

<!-- React + Babel CDN - Pinned versions with integrity hashes -->
```html
<script src="https://unpkg.com/react@18.3.1/umd/react.development.js" integrity="sha384-hD6/rw4ppMLGNu3tX5cjIb+uRZ7UkRJ6BPkLpg4hAu/6onKUg4lLsHAs9EBPT82L" crossorigin="anonymous"></script>
<script src="https://unpkg.com/react-dom@18.3.1/umd/react-dom.development.js" integrity="sha384-u6aeetuaXnQ38mYT8rp6sbXaQe3NL9t+IBXmnYxwkUI2Hw4bsp2Wvmx4yRQF1uAm" crossorigin="anonymous"></script>
<script src="https://unpkg.com/@babel/standalone@7.29.0/babel.min.js" integrity="sha384-m08KidiNqLdpJqLq95G/LEi8Qvjl/xUYll3QILypMoQ65QorJ9Lvtp2RXYGBFj1y" crossorigin="anonymous"></script>
```

## React Scope Management

```js
// Global-scoped style objects - Use SPECIFIC names, never `const styles = { ... }`
const myComponentStyles = {
  container: {
    // styles here
  }
};

// When using multiple Babel script files, components don't share scope
// Export to `window` at the end of component files:
Object.assign(window, {
  MyComponent,
  // ... other exports
});

// Avoid `type="module"` on script imports - it may break things
```

## Slide Scaling

```html
<!-- Fixed-size content scaling (e.g., slide decks, presentations) -->
<!-- Default 1920×1080, 16:9 aspect ratio -->
<!-- Letterbox via transform: scale() on black background -->

<style>
  .stage {
    width: 100vw;
    height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
    background: #000;
  }
  
  .canvas {
    width: 1920px;
    height: 1080px;
    transform-origin: center center;
  }
</style>

<div class="stage">
  <div class="canvas" id="canvas">
    <!-- Slide content here -->
  </div>
</div>

<script>
  function scaleCanvas() {
    const canvas = document.getElementById('canvas');
    const scaleX = window.innerWidth / 1920;
    const scaleY = window.innerHeight / 1080;
    const scale = Math.min(scaleX, scaleY);
    canvas.style.transform = `scale(${scale})`;
  }
  
  window.addEventListener('resize', scaleCanvas);
  scaleCanvas();
</script>
```

**Key Points:**
- Slide numbering: 1-indexed, labels like "01 Title", "02 Agenda"
- Add `[data-screen-label]` attributes on slide elements
- Text minimum 24px for 1920x1080 slides
- Use localStorage for persistent playback position

## Speaker Notes

```html
<!-- Speaker Notes JSON -->
<script type="application/json" id="speaker-notes">
[
    "Slide 0 notes",
    "Slide 1 notes",
    "Slide 2 notes"
]
</script>
```

**Required:** Page MUST call `window.postMessage({slideIndexChanged: N})` on init and on every slide change.

## Tweaks System

### Setup
```html
<script>
window.addEventListener('message', (event) => {
  if (event.data?.type === '__activate_edit_mode') {
    // Show Tweaks panel
  }
  if (event.data?.type === '__deactivate_edit_mode') {
    // Hide Tweaks panel
  }
});
window.parent.postMessage({type: '__edit_mode_available'}, '*');

// When user changes a value:
// window.parent.postMessage({type: '__edit_mode_set_keys', edits: {fontSize: 18}}, '*');
</script>
```

### Persisting State
```html
<script>
const TWEAK_DEFAULTS = /*EDITMODE-BEGIN*/{
  "primaryColor": "#D97757",
  "fontSize": 16,
  "dark": false
}/*EDITMODE-END*/;
</script>
```

**Rules:**
1. Block between markers must be valid JSON (double-quoted keys and strings)
2. Exactly one such block in root HTML file
3. Must be inside inline `<script>`

### Tweaks Protocol
1. Register a `message` listener on `window` that handles:
   - `{type: '__activate_edit_mode'}` → show Tweaks panel
   - `{type: '__deactivate_edit_mode'}` → hide it
2. Call: `window.parent.postMessage({type: '__edit_mode_available'}, '*')`
3. When user changes a value, apply it live and persist:
   `window.parent.postMessage({type: '__edit_mode_set_keys', edits: {fontSize: 18}}, '*')`
