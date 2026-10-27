# Two-Point Perspective Studio

A browser-based perspective drafting tool, from 1-point perspective up to a full 360° 6-point view. Build boxes that snap to the grid, divide their faces in perspective and export the drawing as a PNG.

Live at https://landonsw21.github.io/perspective-studio/

## Perspective modes

Switch modes from the toolbar or the Perspective panel.

- **1-point:** one vanishing point on the horizon; depth edges run to it while widths stay horizontal and heights vertical, so box fronts are true rectangles. Comes with a starburst of rays plus horizontal and vertical guides
- **2-point:** two vanishing points on the horizon, vertical edges stay vertical
- **3-point:** a third vanishing point above or below the horizon that vertical edges run to. A camera check in the panel says whether the setup matches a real camera. A setup that doesn't still works, but its boxes look stretched and carry their proportions to other modes only approximately
- **4-point:** two styles. *Fisheye* puts left, right, up and down vanishing points on a lens circle, with lines curving between each pair. *Panorama* is a 360° strip with four vanishing points on the horizon, each horizontal direction vanishing at two points 180° apart, and straight verticals
- **5-point:** a fisheye looking straight ahead: depth lines run to a center vanishing point, and lines across or up and down curve to the four points on the 90° circle
- **6-point:** the whole sphere in one continuous circle: the front vanishing point at the center, left, right, up and down on the 90° ring, and the back vanishing point stretched around the outer rim, where every line heading behind you meets

The curved modes (4-, 5- and 6-point) all project true 3D lines through the same camera, with curvature from stereographic (50%) through equidistant (100%) and equisolid (150%) to orthographic (200%), so boxes, snapping and face divisions work the same way everywhere.

## Boxes

- Rectangular prisms that snap to ray intersections, guide lines and the corners of other boxes, shown solid, ghosted or as wireframes. Shift-click a face to hide it
- Drag a base corner to reshape the base, or a top corner to change the height. A base corner can't be dragged across the horizon, where the box's far edges would shoot back out of the vanishing points
- Drag a box's body to move it. The move is rigid: the box keeps its real proportions wherever it goes, in every mode. Dragged across eye level, it hops over the horizon rather than flattening onto it
- In 1-, 2- and 3-point, an edit stops before a box reaches so far to the side that it would stretch out toward infinity
- Perspective-correct face divisions (1/2, 1/4, 1/8 …) and diagonals

## Boxes keep their place, size and proportions

- **Switching perspective** keeps every box at the same place and size on screen, with the same real proportions. Each box is read as a 3D shape through the current mode's camera and rebuilt in the new one, so nothing needs re-zooming or re-placing after a switch
- **Switching into 4-, 5- or 6-point** grows the lens or panorama (it never shrinks on its own) until every box fits at its old size and place. In 6-point it also keeps boxes that were in front of you in front of you, rather than wrapped around toward the rim
- **Moving the horizon or a vanishing point** in 1-, 2- or 3-point rebuilds every box on the new grid at the same place and size, with the same proportions
- **In 4-, 5- and 6-point**, moving the horizon or changing the lens size, center, curvature, coverage or panorama turn keeps boxes where they stand in the scene, so they move with the view
- Where a view can't show a box that large or that far out, the box gets as close as it can, and switching back restores it exactly

## Everything else

- Editable horizon line: eye level, center, tilt, color, weight, line style
- Draggable vanishing points, with an optional cone of vision
- Ray fans from each vanishing point: even spacing or even angles, any count, alternating A/B/skip patterns
- A sized export area that renders to PNG at up to 8× (capped at 64 megapixels)
- Number boxes accept values past the end of each slider, and the slider stretches to fit; releasing a slider at its end doubles its range
- Undo from the toolbar or with Ctrl/⌘ Z; redo with Ctrl/⌘ Shift Z or Ctrl/⌘ Y
- Save a setup as a JSON file and load it back later. A file that isn't a setup is refused. In one that is, values that don't make sense fall back to the defaults, and boxes with unusable corners are left out

Everything runs in a single `index.html` with no build step. Work is saved in the visitor's own browser.

## Testing

Stress tested on 27 October 2026 with scripted runs in the browser, covering all six modes and both 4-point styles:

- **Switching perspective:** 225 random switches on nine scenes of 20 random boxes of different sizes, shapes and positions. Every box kept its proportions exactly, its size to within 0.4% and its center to within 1.6% of its size
- **Dragging:** 2,469 random drags on 84 scenes of 8 boxes, covering base corners, tops, bodies, the horizon, vanishing points and lens handles. A moved box always kept its proportions and the other boxes stayed exactly where they were. Moving the horizon or a vanishing point kept every box's proportions, and in 1-, 2- and 3-point its place and size too. No base ended up lying on or straddling the horizon. Every drag that changed anything was undone and redone, and both restored the drawing exactly
- **Panel values:** 2,110 random edits to the horizon, vanishing points and lens settings, 840 of them at extreme values, many past the slider ends. No box changed proportions, every box in 1-, 2- and 3-point kept its place and size, and every edit undid and redid exactly
- **Export, save and load:** PNG export in every mode at 1× and 2×, the 64-megapixel cap, setups surviving a save and load exactly, and files that aren't setups being refused
- **Speed and layout:** with 34 boxes, each with face divisions and diagonals, a full redraw took about 3 ms in 1-, 2- and 3-point and 9–11 ms in the curved modes. Each step of a drag took at most about 4 ms and a switch at most 43 ms. On a 375 px wide phone screen, nothing scrolls sideways

## Run locally

Open `index.html` in a browser.

## Hosting

Served with GitHub Pages from the `main` branch, root folder.
