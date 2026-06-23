# Experiential tier — 3D, WebGL, physics, smooth scroll

Load this file **only** when the user picked the Experiential tier in Step 2 and the
content earns it. Treat it as a real engineering system, never a gimmick, and never let
it break the taste, responsiveness, feedback, or accessibility laws in SKILL.md.

## Toolkit
- **3D / WebGL:** Three.js (or React-Three-Fiber + drei). One component per scene/object,
  logic out of the view. Author looks with GLSL shaders. **The DOM still owns all real
  text/headings/CTAs — never bake copy into the canvas.**
- **Physics:** add a real engine only when motion should feel physical — Rapier
  (preferred) or Cannon-es / Matter.js (2D). For momentum/gravity/collisions/draggable
  inertia, not decoration.
- **Smooth / virtual scroll:** Lenis (preferred) or Locomotive, **synced to GSAP
  ScrollTrigger** so scroll-linked 3D/pins/parallax stay frame-accurate.
- **Page transitions:** Barba.js (multi-page) or the framework's view-transition / route
  animation; never block content from becoming readable.
- **Ready-made motion:** Spline (embeddable 3D), Lottie (vector micro-animations) — where
  they beat hand-coding, lazy-loaded.
- **Asset pipeline:** ship glTF/GLB compressed with Draco/Meshopt; optimize poly/texture;
  lazy-load and code-split the 3D bundle off the critical path.

## Hard gates (non-negotiable)
- **Performance:** target 60fps; budget draw calls/geometry/texture memory; animate on
  the GPU; pause rendering when the canvas is offscreen; 3D bundle is
  lazy/dynamically imported, never in the critical path.
- **Mobile & fallback:** fully responsive; on low-power/mobile fall back to a lighter
  scene, a static poster, or the Standard layout. Detect WebGL support and degrade
  gracefully; the page is fully usable with no canvas.
- **Accessibility:** `prefers-reduced-motion` **disables the immersive scene** and shows
  the static equivalent. Canvas carries accessible alternative content; keyboard/focus
  ignore the decorative canvas and still reach every real control; reserve canvas
  dimensions to avoid layout shift.

## Build note
The Standard page renders and is usable **before and without** the 3D layer. The scene
lives behind a ready/fallback boundary and is dynamically imported. Never force 3D onto a
brief that didn't ask; never flatten an immersive brief that did.
