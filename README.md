# Frontend Mentor - Browser extensions manager UI solution

This is a solution to the [Browser extensions manager UI challenge on Frontend Mentor](https://www.frontendmentor.io/challenges/browser-extension-manager-ui-yNZnOfsMAp).

## Table of contents

- [Overview](#overview)
  - [The challenge](#the-challenge)
  - [Links](#links)
- [My process](#my-process)
  - [Built with](#built-with)
  - [What I learned](#what-i-learned)
  - [Useful resources](#useful-resources)
- [Author](#author)

## Overview

### The challenge

Users should be able to:

- Toggle extensions between active and inactive states.
- Filter active and inactive extensions.
- Remove extensions from the list.
- **Bonus**: All these states (filters, active toggle, removed items) persist after page reload using LocalStorage.
- Select their color theme (Light/Dark mode) with system preference detection.
- View the optimal layout for the interface depending on their device's screen size.
- See hover and focus states for all interactive elements on the page.

### Links

- Solution URL: [GitHub Repository](https://github.com/bhzeuscagd/browser-extension-manager)
- Live Site URL: [Vercel Deployment](https://browser-extension-manager-tawny.vercel.app)

## My process

### Built with

- Semantic HTML5 markup
- CSS custom properties
- CSS Grid & Flexbox
- Mobile-first workflow
- **[Astro](https://astro.build/)** - The web framework for content-driven websites.
- **[Tailwind CSS v4](https://tailwindcss.com/)** - For utility-first styling (configured with `@tailwindcss/vite`).
- **TypeScript** - For type safety.
- **LocalStorage API** - For state persistence without a backend.

### What I learned

This project was a deep dive into **state management without JavaScript frameworks** (like React's useState) to keep the client bundle minimal.

#### 1. CSS-Only Filtering
I implemented a robust filtering system using the "Checkbox Hack" with advanced CSS selectors. This allows filtering items based on their data attributes without a single line of JS for the visual logic.

```astro
<ul class="
    peer-checked/active:[&_li[data-status=false]]:hidden
    peer-checked/inactive:[&_li[data-status=true]]:hidden
">
   <!-- List items -->
</ul>
```

#### 2. LocalStorage Persistence Pattern
I created a reusable pattern to sync DOM state with `localStorage`. This ensures that if a user removes an extension or toggles it off, it stays that way.

```javascript
/* Logic to persist removals */
const removedStates = JSON.parse(localStorage.getItem(REMOVED_KEY) || "{}");
if (removedStates[name]) {
    input.closest("li")?.remove(); // Remove before paint if possible
}
```

#### 3. Modern Dark Mode
Used the new `@custom-variant` directive from Tailwind CSS v4 to create a theme selector that respects both system preferences and manual overrides.

```css
@custom-variant dark (&:where(.dark, .dark *));
```

### Useful resources

I have documented the core techniques used in this project in the `docs/` folder:

- [CSS Filtering Logic](./docs/CSS_FILTERING_NOTE.md) - How the CSS-only filter works.
- [JS State Sync Pattern](./docs/REUSABLE_JS_STATE_SYNC.md) - The reusable script for DOM-State synchronization.
- [LocalStorage Persistence](./docs/LOCAL_STORAGE_PERSISTENCE.md) - Pattern for saving form states.
- [Tailwind Dark Mode](./docs/TAILWIND_DARK_MODE.md) - Guide to the dark mode implementation.

## Author

- Portfolio - [Cagd](https://portfolio-cagd.vercel.app/)
- GitHub - [Cagd](https://github.com/bhzeuscagd)
- Frontend Mentor - [@bhzeuscagd](https://www.frontendmentor.io/profile/bhzeuscagd)
