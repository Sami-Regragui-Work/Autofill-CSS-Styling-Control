# Autofill-CSS-Styling-Control

A demonstration of how to style browser autofill inputs with CSS, including various approaches to handling the notorious "corner gaps" rendering issue.

## The Problem

When styling autofill inputs with custom colors, browsers apply their own default background. The common workaround using `box-shadow inset` combined with `border-radius` creates tiny antialiasing artifacts (0.1-0.5px gaps) at the corners.

## Solutions Demonstrated

### 1. Default Autofill

Shows the browser's default autofill styling.

### 2. With Issue

Demonstrates the corner gap problem when using:

-   `-webkit-box-shadow: 0 0 0 5000px inset`
-   `border-radius: 12px`

**Issue**: Visible gaps at rounded corners due to browser antialiasing.

### 3. Transition Delay Fix

Uses a 5000s transition delay to override autofill:

```css
transition: background-color 5000s ease-in-out 0s;
```

**Pros**: 100% eliminates corner gaps  
**Cons**: Relies on a hacky transition delay

### 4. Ongoing Fix (Best Current Solution)

Uses `-webkit-background-clip: padding-box;` to minimize gaps:

```css
-webkit-background-clip: padding-box;
```

**Pros**: Most elegant solution  
**Cons**: Still has microscopic 0.1px gaps when zoomed (browser rendering limitation)

## Usage

1. Open `index.html` in your browser
2. Fill out any form and submit to create autofill suggestions
3. Click on inputs to see autofill styling
4. Zoom to 500% to observe the corner gap differences

## Browser Compatibility

Tested on:

-   Brave v1.84.132 (Oct 29, 2025)
-   Chrome/Chromium-based browsers

**Note**: This issue has existed for years across multiple browsers.

## Customization

Edit the CSS variables in `css.css`:

```css
:root {
    --body-clr: black;
    --label-clr: cadetblue;
    --bg-clr: blueviolet;
    --text-clr: aquamarine;
    --min-w: 15rem;
    --padding-h: 12px;
    --padding-v: 6px;
    --rounded: 12px;
}
```

## Key Takeaways

-   The corner gap is a **browser rendering artifact**, not a CSS bug
-   `-webkit-background-clip: padding-box;` is currently the best non-hacky solution
-   The transition delay hack works perfectly but feels wrong
-   Some browsers/zoom levels may not show the gaps at all

## License

Feel free to use and modify for your projects.
