# Two-Point Perspective Studio

A browser-based perspective drafting tool with six modes:

- **2-point:** two vanishing points on the horizon, vertical edges stay vertical
- **3-point:** a third vanishing point above or below the horizon that vertical edges run to, with a check that the setup matches a real camera
- **4-point:** two styles. *Fisheye* puts left, right, up and down vanishing points on a lens circle, with lines curving between each pair. *Panorama* is a 360° strip with four vanishing points on the horizon, each horizontal direction vanishing at two points 180° apart, and straight verticals
- **5-point:** a fisheye looking straight ahead: depth lines run to a center vanishing point, and lines across or up and down curve to the four points on the 90° circle
- **6-point:** the whole sphere in one continuous circle: the front vanishing point at the center, left, right, up and down on the 90° ring, and the back vanishing point stretched around the outer rim, where every line heading behind you meets
- **Curvilinear:** a 2-point fisheye where straight edges bend around the lens center. Curvature runs from 0% (matches 2-point exactly) through stereographic (50%), equidistant (100%) and equisolid (150%) to orthographic (200%), and up to 295% for even stronger bending with a narrower view

The curved modes all project true 3D lines through the same camera, so boxes, snapping and face divisions work the same way everywhere. Turning a panorama or resizing a lens keeps boxes where they stand in the scene.

Switching perspective keeps every box at the same place and size on screen, with the same real proportions: 2- and 3-point boxes are read as 3D through their equivalent pinhole cameras and rebuilt in the new mode. Where a view can't show a box that large or that far out (outside a fisheye circle, say), it gets as close as it can, and switching back restores the box exactly.

In every mode:

- Editable horizon line: eye level, center, tilt, color, weight, line style
- Draggable vanishing points, with an optional cone of vision
- Ray fans from each vanishing point: even spacing or even angles, any count, alternating A/B/skip patterns
- Rectangular prisms that snap to ray intersections, with solid, ghosted and wireframe modes and hideable faces
- Perspective-correct face divisions (1/2, 1/4, 1/8 …) and diagonals
- A sized export area that renders to PNG at up to 8× (capped at 64 megapixels)
- Number boxes accept values past the end of each slider, and the slider stretches to fit; releasing a slider at its end doubles its range
- Switch perspective from the toolbar or the Perspective panel; undo from the toolbar or with Ctrl/⌘ Z, redo with Ctrl/⌘ Shift Z or Ctrl/⌘ Y

Everything runs in a single `index.html` with no build step. Work is saved in the visitor's own browser.

## Run locally

Open `index.html` in a browser.

## Hosting

Served with GitHub Pages from the `main` branch, root folder.
