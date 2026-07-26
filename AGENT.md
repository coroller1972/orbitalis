Build a single, self-contained solar-system.html file (no external files, no CDN imports) that renders an interactive, visually impressive simulation of our Solar System. All CSS and JavaScript must be inline. Use the HTML5 Canvas API (no Three.js, no libraries).
VISUAL REQUIREMENTS

Render the Sun at center with a glowing radial gradient (yellows/oranges) and animated corona pulse effect
All 8 planets rendered with distinct color gradients and surface detail (rings for Saturn and Uranus, Great Red Spot hint on Jupiter, polar caps on Mars, cloud swirl suggestion on Venus/Neptune, etc.)
Each planet casts a soft drop-shadow glow matching its color
Draw orbital paths as faint elliptical rings with slight transparency
Background: deep space with ~300 randomly placed stars of varying sizes and opacity (some twinkling)
Add the asteroid belt as a subtle scattered particle band between Mars and Jupiter
Pluto included as a dwarf planet (visually differentiated — smaller, dimmer)

ORBITAL MECHANICS

Orbits must be elliptical (use real eccentricity values approximated per planet)
Orbital speeds must be proportional to real relative periods (Mercury fastest, Neptune slowest) — use actual sidereal year ratios
Planets rotate on their axes (spin animation visible via a surface stripe or gradient shift)
Orbital inclinations: apply a subtle 2D tilt offset to each orbit to suggest 3D depth (perspective foreshortening)
Time speed control: a slider to go from 0× (paused) to 100× real speed
Include a date/year counter that advances with simulation time

INTERACTIVITY & CONTROLS

Zoom: mouse scroll wheel (smooth, clamped between 0.2× and 20×), plus +/− buttons in the UI
Pan: click and drag to move the view; double-click to re-center on the Sun
Planet focus: single-click any planet or the Sun to smoothly camera-pan and zoom to it, keeping it centered; click empty space to release focus
Info panel: when a body is focused/clicked, show a side panel (or modal) with: name, type, diameter (km), mass, distance from Sun (AU), orbital period, number of moons, one interesting fact, and a small rendered "portrait" of the planet drawn on a mini canvas
Hover tooltip: hovering over a planet shows its name and current distance from Sun in AU
Toggle labels: a button to show/hide planet name labels that float above each planet
Toggle orbits: a button to show/hide the orbital path rings
Top-down vs Perspective toggle: a button that animates transitioning the view angle between flat top-down and a slight isometric/perspective tilt

UI / UX

Dark theme HUD overlay with semi-transparent glass-morphism style panels (backdrop blur, subtle border)
Control panel in bottom-left corner with: Speed slider, Zoom buttons, Labels toggle, Orbits toggle, View toggle
Info panel slides in from the right when a body is selected, with a close (×) button
All font: system monospace or a space-appropriate sans-serif, in white/light-gray
Planet name labels should have a subtle line connecting them to the planet when label mode is on
Show a mini-map / overview in the corner showing the full solar system at 1× zoom regardless of current camera position

TECHNICAL & PERFORMANCE

Use requestAnimationFrame for the render loop
Delta-time based animation (consistent speed regardless of frame rate)
All planet and orbital data stored in a clean JavaScript data structure / array of objects at the top of the script — easy to read and modify
Canvas must fill the full browser viewport and resize responsively on window resize
No memory leaks — clean up any intervals or listeners properly
The code should be well-commented, organized into clearly named functions (e.g., drawSun(), drawPlanet(), drawOrbit(), handleClick())

DATA TO INCLUDE (approximate, scaled for visual clarity)
Include at minimum: Mercury, Venus, Earth (with Moon orbiting it), Mars, Jupiter, Saturn (with rings), Uranus (with faint rings, tilted), Neptune, Pluto. Orbital radii should be logarithmically scaled so all planets are visible without zooming out excessively, but zoom out should reveal true relative spacing.