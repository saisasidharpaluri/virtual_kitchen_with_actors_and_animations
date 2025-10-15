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

- Mother stands clearly in front of the opposite-side counter and faces the cooking area.
- Indian skin tones applied to mother and kids; more human facial features for mother (eyes, ears, nose, mouth) and hair (cap, bun, side strands).
- Arm control switched to an IK-based pose targeting a fixed point just above the bowl. Hand/wrist kept straight and steady (no stirring motion) as requested.
- Additional cooking context: mixing bowl with ingredients, chopping board with veggies, measuring cup on the counter.

Tweak the static pose/target (in `assets/js/main.js`):

- Fixed target height above bowl: search for `workTarget` and adjust the `+ new THREE.Vector3(0, 0.07, 0)` value.
- Move the bowl if needed: look for `addCookingContainers()` and change the `bowl.position.set(...)` coordinates.
- Re-enable motion: set `actorAnim.mother.staticPose = false` and (optionally) restore the circular stir target.

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
