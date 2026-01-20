# Implementation Plan: Office Markers World Map

## Overview

Extend the worldmap-canvas library with marker support and create a self-contained HTML file that can be pasted into Elementor Pro's HTML widget. The map will display 4 office locations with clickable markers that show address tooltips.

## Phase 1: Extend WorldMap Library

Add marker functionality to the existing worldmap.js library.

### Tasks

- [x] Add `markers` parameter to WorldMap function signature
- [x] Create `latLonToCanvas()` function for coordinate conversion
- [x] Implement marker drawing after country rendering
- [x] Add click/touch event listeners to canvas
- [x] Implement hit-testing to detect marker clicks
- [x] Create tooltip positioning and display logic

### Technical Details

**Coordinate Conversion (Mercator Projection):**
```javascript
function latLonToCanvas(lat, lon, canvasWidth, canvasHeight, padding) {
    // Convert longitude to x (simple linear mapping)
    var x = ((lon + 180) / 360) * canvasWidth;

    // Convert latitude to y (Mercator projection)
    var latRad = lat * Math.PI / 180;
    var mercN = Math.log(Math.tan((Math.PI / 4) + (latRad / 2)));
    var y = (canvasHeight / 2) - (canvasWidth * mercN / (2 * Math.PI));

    return { x: x, y: y };
}
```

**Marker Drawing:**
```javascript
// Draw red circle marker
oCTX.fillStyle = "#D32F2F";
oCTX.beginPath();
oCTX.arc(markerX, markerY, 8, 0, 2 * Math.PI);
oCTX.fill();
```

**Hit Testing (click detection):**
```javascript
function isClickOnMarker(clickX, clickY, markerX, markerY, radius) {
    var distance = Math.sqrt(
        Math.pow(clickX - markerX, 2) +
        Math.pow(clickY - markerY, 2)
    );
    return distance <= radius;
}
```

**Office Coordinates:**
| Office | Latitude | Longitude |
|--------|----------|-----------|
| San Francisco | 37.7749 | -122.4194 |
| Los Angeles | 34.0522 | -118.2437 |
| Seoul | 37.4837 | 127.0324 |
| Tashkent | 41.2995 | 69.2401 |

## Phase 2: Create Elementor-Ready HTML

Build a self-contained HTML file with all code inline.

### Tasks

- [x] Create `worldmap-elementor.html` with inline CSS styles
- [x] Embed modified worldmap.js code with marker support
- [x] Configure office markers with addresses
- [x] Add tooltip HTML element and styling
- [x] Implement responsive canvas sizing
- [x] Add touch event support for mobile

### Technical Details

**File Structure:**
```
worldmap-elementor.html
├── <style> - All CSS inline
├── <div class="worldmap-container">
│   ├── <canvas id="office-worldmap">
│   └── <div id="worldmap-tooltip">
└── <script> - Complete JS with worldmap + markers
```

**CSS for Tooltip:**
```css
.worldmap-tooltip {
    position: absolute;
    background: #ffffff;
    padding: 12px 16px;
    border-radius: 8px;
    box-shadow: 0 2px 10px rgba(0,0,0,0.15);
    display: none;
    max-width: 250px;
    font-size: 14px;
    line-height: 1.5;
    z-index: 100;
    pointer-events: none;
}

.worldmap-tooltip h4 {
    margin: 0 0 8px 0;
    font-size: 14px;
    font-weight: 600;
    color: #333;
}

.worldmap-tooltip p {
    margin: 0;
    color: #666;
}
```

**Map Color Configuration:**
```javascript
WorldMap({
    id: "office-worldmap",
    bgcolor: "#F5F5F5",      // Background/ocean
    fgcolor: "#E5E5E5",      // Countries/land
    bordercolor: "#D0D0D0",  // Country borders (subtle)
    borderwidth: 0.5,
    markers: [/* office data */]
});
```

**Responsive Canvas:**
```javascript
function resizeCanvas() {
    var container = document.querySelector('.worldmap-container');
    var canvas = document.getElementById('office-worldmap');
    canvas.width = container.offsetWidth;
    canvas.height = container.offsetWidth * 0.5; // 2:1 aspect ratio
    // Redraw map
}
window.addEventListener('resize', resizeCanvas);
```

## Phase 3: Testing & Documentation

Verify functionality and prepare for deployment.

### Tasks

- [ ] Test in standalone browser (open HTML file directly)
- [ ] Verify all 4 markers display at correct positions
- [ ] Test tooltip appears with correct address on click
- [ ] Test tooltip closes when clicking elsewhere
- [ ] Test on mobile device (touch interactions)
- [ ] Document Elementor integration steps

### Technical Details

**Browser Testing:**
1. Open `worldmap-elementor.html` directly in browser
2. Check console for any JavaScript errors
3. Click each marker and verify address content

**Elementor Integration Steps:**
1. In WordPress, edit page with Elementor
2. Add "HTML" widget to desired section
3. Copy entire contents of `worldmap-elementor.html`
4. Paste into HTML widget code area
5. Update/Preview page
6. Test marker interactions

**Mobile Testing Checklist:**
- Touch on marker shows tooltip
- Touch elsewhere closes tooltip
- Map displays correctly on narrow screens
- No horizontal scrolling issues
