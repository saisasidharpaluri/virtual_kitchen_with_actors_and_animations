# 3D Kitchen Model

An interactive, isometric-style 3D kitchen built with Three.js. The scene showcases a modern L-shaped kitchen, dining setup, rich materials (granite, tile, wood, metal), small appliances, and subtle lighting.

## Project structure

- `index.html` – Base page, loads Tailwind, Three.js, and OrbitControls, and wires the UI panels. Sets the header title shown on-page.
- `assets/css/styles.css` – Custom styles for layout and info panels.
- `assets/js/main.js` – Your Three.js scene code, interactions, and animation loop.

## Run locally

You can open `index.html` directly in a browser. If controls or textures fail due to CORS on some browsers, use a simple static server.

On Windows PowerShell you can run a tiny static server (recommended to avoid CORS issues):

```powershell
# Python 3
python -m http.server 5500 ; Start-Process http://localhost:5500/index.html

# Or Node (if installed)
npx serve . -l 5500 ; Start-Process http://localhost:5500/index.html
```

Or, just double-click `index.html` to open it directly in Chrome/Edge/Firefox.

## Controls

- Orbit: Left mouse drag
- Zoom: Mouse wheel / trackpad pinch
- Pan: Right mouse drag (limited)
- Click on highlighted items to view details in the right info panel

## Features

- External CDNs are used for Three.js r128 and OrbitControls to match your original file.
- Info panel content is sourced from `userData` on intersected meshes; components created with either `details.description` or `details.desc` will display correctly.

## Current scene highlights

- Enlarged kitchen with L-shaped base cabinets and granite countertops.
- Dining table (6 chairs) positioned near the front-right, chairs arranged and oriented realistically.
- Dark, high-contrast backsplash applied across counter-mounted walls; decorative panels retained with trim.
- Small appliances and details: 4-burner cooktop with oven, sink with faucet, toaster, kettle, spice rack, utensil holder, fruit bowl, and a detailed coffee maker.
- Wall-mounted drinking water purifier (replaces geyser), colored white with navy accent and translucent tank window.
- Upper cabinet doors with brass handles and a warm under-cabinet light bar.
- Realistic bar stools behind the island: round wood seat, black metal legs, chrome footrest ring.
- Left wall has a colored wainscot with chair rail and baseboard for visual interest.
- Door removed from the scene per latest request.

### New in this version: Actors and props

- Mother character near the stove, wearing a daily-use dress and apron. Rising steam particles over the pan.
- Extra utensils near the cooktop (spatula, lid) for cooking context.
- Two kids seated at the dining table with plates of snacks and cups. Light head-nod and hand-to-mouth nibble animation.

Customization hints (in `assets/js/main.js`):

- Change mother placement: search for `createMother(` and adjust `momX`, `momZ`.
- Adjust kids’ chairs: look for `kid1Seat` / `kid2Seat` and related `placeLocalToWorld` calls.
- Snack variety: tweak `addPlateWithSnacks()` to add fruit or different shapes/colors.

### Latest updates (October 2025)

**Animation & Character Improvements:**
- Mother now stirs the bowl with dynamic hand selection and occasionally lifts the spatula to her mouth for a quick taste.
- Mother's body is rotated 180° with legs and head independently oriented to face the countertop.
- Hands automatically work in front of her body (toward the granite/countertop) using dynamic IK.
- Side apron added on the countertop-facing side instead of front apron.
- Facial expressions: animated blinking, subtle smiling, and eyebrow movements for natural look.
- Hair styled as a ponytail at the back of the head with side bangs at front.
- Indian skin tones applied; realistic facial features (eyes, nose, mouth, eyebrows, ears).

**Kids' Eating Animation:**
- Kids now actually "eat" with a full state machine: reach → pick snack from plate → bring to mouth → chew (snack shrinks/disappears) → return → idle → repeat.
- Each plate tracks individual snack items that get consumed during the animation.
- Natural head nodding and periodic blinking.

**Scene & Setup:**
- Mother stands clearly in front of the opposite-side counter and faces the cooking area.
- Additional cooking context: mixing bowl with ingredients, chopping board with veggies, measuring cup on the counter.
- Legs grouped for independent rotation from torso.

Tweak pose and animation (in `assets/js/main.js`):

- Toggle stirring: set `actorAnim.mother.staticPose = true` to stop stirring (right arm holds a straight pose toward the bowl). Set to `false` to enable stirring.
- Stirring radius/speed: look for the comment `Mother arm control: right hand stirs, left hand rests` inside `animate()` and adjust the radius `r` and the time multiplier.
- Stirring height above bowl: adjust the `+ new THREE.Vector3(Math.cos(...)*r, 0.07, Math.sin(...)*r)` value (the `0.07` sets the hand height above the bowl center).
- Left-hand rest offset: in the same block, tweak the offset added to `workTarget` (defaults to something like `(-0.18, counterY+0.02, 0.0)`) to place her palm closer/farther/left/right of the bowl.
- Move the bowl if needed: look for `addCookingContainers()` and change the `bowl.position.set(...)` coordinates.

Kids’ eating loop controls (in `animate()` under "kids"):

- Durations: adjust `reachDur`, `toMouthDur`, `chewDur`, `returnDur`, `idleDur` to speed up or slow down the cycle.
- Hand angles: tweak `downAngle` and `mouthAngle` to refine reach and eating pose.
- Plate snacks: each plate returns a list of snack meshes; when a kid reaches the plate, one visible snack is hidden from the plate and the hand-held snack is shown.

## Technical notes

- Three.js r128 and OrbitControls are loaded from CDNs to keep setup simple.
- The renderer and all CanvasTextures are configured for sRGB to keep colors accurate.
- Many materials use MeshStandardMaterial with tuned roughness/metalness for realism.
- Geometry is built from primitives for clarity and easy tweaking; dimensions are parameterized.

## Troubleshooting

- Black screen: reload the page and check the browser console. Texture encodings and materials are set, but errors will appear here if something is off.
- Colors look washed out: verify your display color profile and browser settings. sRGB is enabled in the renderer and textures.
- Slow performance: reduce window size or device pixel ratio (add `renderer.setPixelRatio(window.devicePixelRatio*0.75)` in `main.js`).

## Deploy

- GitHub Pages: enable Pages in repo Settings → Pages → Source: Deploy from a branch → `main` → `/root` to host `index.html`.
- Any static host: upload the repository files as-is (no build step required).

## License

This project is for educational purposes. Add a license if you plan to reuse or share broadly.
