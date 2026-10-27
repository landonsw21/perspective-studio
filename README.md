# Two-Point Perspective Studio

A browser-based perspective drafting tool with three modes:

- **2-point:** two vanishing points on the horizon, vertical edges stay vertical
- **3-point:** a third vanishing point above or below the horizon that vertical edges run to, with a check that the setup matches a real camera
- **Curvilinear:** a fisheye lens model where straight edges bend around the lens center, with adjustable curvature (0% matches 2-point exactly) and lens coverage

In every mode:

- Editable horizon line: eye level, center, tilt, color, weight, line style
- Draggable vanishing points, with an optional cone of vision
- Ray fans from each vanishing point: even spacing or even angles, any count, alternating A/B/skip patterns
- Rectangular prisms that snap to ray intersections, with solid, ghosted and wireframe modes and hideable faces
- Perspective-correct face divisions (1/2, 1/4, 1/8 …) and diagonals
- A sized export area that renders to PNG

Everything runs in a single `index.html` with no build step. Work is saved in the visitor's own browser.

## Run locally

Open `index.html` in a browser.

## Hosting

Served with GitHub Pages from the `main` branch, root folder.
