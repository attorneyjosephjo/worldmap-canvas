# Requirements: Office Markers World Map

## Overview

An interactive world map displaying office locations as clickable red markers. When a user clicks a marker, a tooltip bubble shows the office address. The map will be embedded in WordPress using Elementor Pro's HTML widget.

## User Story

As a website visitor, I want to see office locations on a world map so that I can quickly understand the company's global presence and find address details for each office.

## Acceptance Criteria

- [ ] World map displays with minimal, clean design (light gray countries on white background)
- [ ] 4 office locations shown as red circle markers
- [ ] Clicking a marker shows a tooltip bubble with the office address
- [ ] Clicking elsewhere on the map closes the tooltip
- [ ] Map is responsive and works on mobile devices (touch support)
- [ ] All code is self-contained in a single HTML block for Elementor

## Office Locations

| Office | Address |
|--------|---------|
| San Francisco | 1 Sansome Street, Suite 3500, San Francisco, CA 94104, USA |
| Los Angeles | 11150 West Olympic Boulevard, Suite 1050, Los Angeles, CA 90064, USA |
| Seoul | 6F, 7, Bangbaecheon-ro 2-gil, Seocho-gu, Seoul 06693, South Korea |
| Tashkent | Toshkent shahar, Mirobod tumani, ul. Xamal, dom 29/9, kv. 2 |

## Design Specifications

### Color Scheme (Minimal & Clean)
| Element | Color |
|---------|-------|
| Background/Ocean | White `#F5F5F5` |
| Countries/Land | Light gray `#E5E5E5` |
| Country borders | Very light gray `#D0D0D0` (subtle) |
| Markers | Solid red `#D32F2F` |

### Interactions
- Cursor changes to pointer when hovering over markers
- Tooltip appears next to clicked marker
- Tooltip has white background with subtle shadow

## Integration Method

**WordPress + Elementor Pro HTML Widget**
- Self-contained HTML/CSS/JS in single block
- No external dependencies
- Paste directly into Elementor's HTML widget

## Dependencies

- Base library: `worldmap.js` (worldmap-canvas from GitHub)
- Extended with custom marker functionality
