# Perspective Studio

A browser-based perspective drafting tool, from 1-point perspective up to a full 360° 6-point view. Build boxes that snap to the grid, divide their faces in perspective and export the drawing as a PNG.

Live at https://landonsw21.github.io/perspective-studio/

## Perspective modes

Choose the mode from the perspective dropdown on the toolbar, which lists 4-point's fisheye and panorama as separate choices.

- **1-point:** one vanishing point on the horizon; depth edges run to it while widths stay horizontal and heights vertical, so box fronts are true rectangles. The VP drags anywhere, and the horizon line moves with it. Comes with a starburst of rays plus horizontal and vertical guides
- **2-point:** two vanishing points on the horizon, vertical edges stay vertical
- **3-point:** a third vanishing point above or below the horizon that vertical edges run to. A camera check in the panel says whether the setup matches a real camera. A setup that doesn't still works, but its boxes look stretched and carry their proportions to other modes only approximately
- **4-point:** two styles. *Fisheye* looks at a box's corner, like 2-point seen through a curved lens: the box's two horizontal directions vanish at VP1 and VP2 on the horizon, always 90° apart, and vertical lines curve to up and down VPs above and below. *Panorama* is a 360° strip with four vanishing points on the horizon, each horizontal direction vanishing at two points 180° apart, and straight verticals
- **5-point:** a fisheye looking straight ahead: depth lines run straight to a center vanishing point, lines across curve to the left and right VPs, and lines up and down curve to the up and down VPs
- **6-point:** the whole sphere in one continuous view: the front vanishing point at the center, left, right, up and down around the 90° ring, and the back vanishing point stretched around the outer rim, where every line heading behind you meets

## Curved views (4-, 5- and 6-point)

- **Horizontal and vertical curvature are set separately.** Horizontal curvature bends the lines that run left and right, and vertical curvature the lines that run up and down. 100% is an even fisheye, 0% makes those lines straight (straight verticals with curved horizontals, for example), and higher values bend them further. A panorama's vertical lines always stay straight, so it has horizontal curvature only
- **Every vanishing point moves on its own.** Drag a VP and only that one moves, while the lens reshapes on that side to match:
  - In 5- and 6-point, the left, right, up and down VPs slide along their lines, and the center slides between the left and right VPs. In 6-point, dragging the back rim grows or shrinks it, and the rim stays put while the other VPs move
  - In the 4-point fisheye, dragging VP1 or VP2 works like 2-point: the other one stays put while the lens turns and resizes, and the up and down VPs keep their places
  - In the panorama, each of the four VPs slides along the horizon on its own
  - **Even out VPs**, on the toolbar next to Fit view, puts them back in an even layout
- Lens size, the lens center, 5-point's coverage, the 6-point back rim and the 4-point turn are in the Perspective panel
- Every curved view projects true 3D lines through its camera, so boxes, snapping and face divisions work the same way everywhere. Setups saved with the earlier single curvature setting open with their lens rings exactly where they were

## Boxes

- Rectangular prisms that snap to ray intersections, guide lines and the corners of other boxes, shown solid, ghosted or as wireframes. A ghosted box's opacity slider runs from see-through to completely opaque, the faces behind included (they show where a face is hidden). Shift-click a face to hide it
- Set a box's width, length and height exactly under Size in the panel's Boxes section. Sizes are in pixels as the box looks where the middle of its base sits, so sliding the box sideways leaves them alone. Width and length grow out from the middle of the base and height grows upward, so the box stays in place and its other two sizes don't change; equal sizes make a true cube. A size too big for the view stops at the largest one it can show
- Drag a base corner to reshape the base, or a top corner to change the height. A base corner can't be dragged across the horizon, where the box's far edges would shoot back out of the vanishing points
- Drag a box's body to move it. The move is rigid: the box keeps its real proportions wherever it goes, in every mode. Dragged across eye level, it hops over the horizon rather than flattening onto it
- In 1-, 2- and 3-point, an edit stops before a box reaches so far to the side that it would stretch out toward infinity
- Perspective-correct face divisions (1/2, 1/4, 1/8 …) and diagonals

## Boxes keep their place, size and proportions

- **Switching perspective** keeps every box at the same place and size on screen, with the same real proportions. Each box is read as a 3D shape through the current mode's camera and rebuilt in the new one, so nothing needs re-zooming or re-placing after a switch
- **Switching into 4-, 5- or 6-point** grows the lens or panorama (it never shrinks on its own) until every box fits at its old size and place. In 6-point it also keeps boxes that were in front of you in front of you, rather than wrapped around toward the rim
- **Moving the horizon or a vanishing point** in 1-, 2- or 3-point rebuilds every box on the new grid at the same place and size, with the same proportions
- **In 4-, 5- and 6-point**, moving the horizon, dragging a lens VP or changing the curvature, lens size, center, coverage, back rim or turn keeps boxes where they stand in the scene, so they move with the view
- Where a view can't show a box that large or that far out, the box gets as close as it can, and switching back restores it exactly

## Everything else

- Editable horizon line: eye level, center, tilt, color, weight, line style
- Draggable vanishing points whose markers take the color of their primary rays, with an optional cone of vision
- Ray fans from each vanishing point: even spacing or even angles, any count, and a repeating pattern of letters. Each letter from A to Z is a ray style with its own color, weight, opacity slider and line: solid, dashed, dotted, dash-dot, long dash or dash-dot-dot (the horizon and guides offer the same six). A dot skips a ray, and a letter gets a row in the style table as soon as it's typed. VP1 and VP2 can be edited together, sharing everything but their colors
- A sized export area that renders to PNG at up to 8× (capped at 64 megapixels)
- Number boxes accept values past the end of each slider, and the slider stretches to fit; releasing a slider at its end doubles its range
- Undo from the toolbar or with Ctrl/⌘ Z; redo with Ctrl/⌘ Shift Z or Ctrl/⌘ Y
- Save a setup as a JSON file and load it back later. A file that isn't a setup is refused. In one that is, values that don't make sense fall back to the defaults, and boxes with unusable corners are left out

Everything runs in a single `index.html` with no build step. Work is saved in the visitor's own browser.

## Testing

Stress tested on 27 October 2026 with scripted runs in the browser, covering all six modes and both 4-point styles:

- **The curved-view lens:** 14,023 directions sent to the screen and back under random settings, including 0% and very high curvature and uneven sides, came back to within 0.000002°. At 0% vertical curvature every vertical box edge in the 4-point fisheye, 5- and 6-point is straight to the pixel (0.0000 px off), and so is every horizontal edge in 5-point at 0% horizontal curvature and every edge of a box in front of you in a panorama at 0%; at 100% they bend by 3–31 px. Four setups saved with the old single curvature setting reopened with their 90° rings and 6-point rims exactly where they were
- **Moving VPs one at a time:** 475 random drags of single lens VPs, across all four curved views. Each moved only that VP, landed under the pointer (or at its limit, such as a 6-point ring point meeting the back rim), left every box's proportions alone, and undid and redid exactly
- **Switching perspective:** 225 random switches on nine scenes of 20 random boxes of different sizes, shapes and positions. Every box kept its proportions exactly, its size to within 0.5% and its center to within 1.6% of its size
- **Dragging:** 2,468 random drags on 84 scenes of 8 boxes, covering base corners, tops, bodies, the horizon, vanishing points and lens VPs. A moved box always kept its proportions and the other boxes stayed exactly where they were. Moving the horizon or a vanishing point kept every box's proportions, and in 1-, 2- and 3-point its place and size too. No base ended up lying on or straddling the horizon. Every drag that changed anything was undone and redone, and both restored the drawing exactly. In 1-point, 40 more drags took the VP up to 400 px in any direction on level and tilted horizons: each time the VP landed under the pointer with the horizon running through it, and every box kept its place, size and proportions
- **Panel values:** 2,070 random edits to the horizon, vanishing points and lens settings, 1,160 of them at extreme values or on a randomly reshaped lens. No box changed proportions, every box in 1-, 2- and 3-point kept its place and size, and every edit undid and redid exactly
- **Ray patterns:** in all six modes and both 4-point styles, every letter of a pattern was drawn in its own color, weight, line and opacity, with the A rays on top, in the view and in the exported PNG. Dots skipped exactly the rays they should, setups saved with the earlier A/B styles opened looking the same, and typing a pattern or changing a letter's style undid and redid exactly
- **Box sizes:** 126 random width, length and height edits on random boxes in all six modes and both 4-point styles. Every typed size came out exactly (4 far too big for the view stopped at the largest it could show instead), the other two sizes and the middle of the base never moved, and every edit undid and redid exactly. Setting all three sizes equal gave a true cube in every view
- **Export, save and load:** PNG export in every mode at 1× and 2×, the 64-megapixel cap, setups surviving a save and load exactly, and files that aren't setups being refused
- **Speed and layout:** with 34 boxes, each with face divisions and diagonals, a full redraw took 2–3 ms in 1-, 2- and 3-point and 10–14 ms in the curved views. Each step of a drag took at most about 6.5 ms and a switch at most 47 ms. On a 375 px wide phone screen, nothing scrolls sideways

## Run locally

Open `index.html` in a browser.

## Hosting

Served with GitHub Pages from the `main` branch, root folder.
