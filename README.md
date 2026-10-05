# Portfolio — Columbia

An interactive 3D portfolio, built as a tribute to the main menu of **BioShock Infinite** (Irrational Games, 2013).
Visitors land straight in front of a wooden sign hanging in a sunlit street of Columbia: that sign is the menu.
A chibi version of Elizabeth keeps them company and reacts to what they do.

**Live site: https://portfolio-tau-lyart-c9cwpvkk90.vercel.app/**

> Personal, non-commercial project. BioShock Infinite and its characters belong to Irrational Games / 2K.

---

## Overview

| Screen | What you'll find |
|---|---|
| **Menu** | An aged paper sign: *About me*, *My projects*, *Skills*, *Download CV*, *Contact* |
| **Pages** | The sign flips around and shows the content on its back, styled like the game's options screens (sliders for skills, etc.) |
| **Elizabeth** | Follows the cursor, hops when you hover an item and spins when a page opens. Click her and she tosses you a Silver Eagle ("Booker, catch!") that adds up in a counter at the top left, just like in the game |

Navigation: mouse or keyboard (`↑` `↓`, `Enter`, `Esc`). Sound starts on the first click or key press (a browser rule).

---

## Featured projects ("My projects")

Hovering a project shows a vintage-photo preview next to the sign (screenshots in [`assets/projects/`](assets/projects/)).

| # | Project | Description | Link |
|---|---|---|---|
| I | **SUNGA** | Website for SUNGA, a digital & IT partner: custom web apps, mobile apps and business tools | [sunga.be](https://sunga.be/fr) |
| II | **Kulabox** | Booking platform for African culinary experiences (search by craving, city and date; host pages) | [staging.kulabox.eu](https://staging.kulabox.eu/fr/experiences) |
| III | **KRAFT** | Team project: creative workshops (linocut printing…) in coffee bars; concept, problem, audience and website | [kraft-neon.vercel.app](https://kraft-neon.vercel.app/) |
| IV | **Wutai · FF VII** | The village of Wutai (Final Fantasy VII) rebuilt in **Blender**, then explorable in a **React Three Fiber** app: clickable buildings, camera moves with **GSAP**, **Rapier** physics, and Yuffie's hidden Materia as an easter egg | **3D viewer inside the portfolio** |

### Wutai in detail
- **Modelling**: village, pagoda, houses, river and statue modelled in Blender (`Wutai.blend`, `Wutai houses.blend`), exported to GLB (≈ 95 MB).
- **Web app**: Vite + React + TypeScript, `@react-three/fiber`, `@react-three/drei`, `@react-three/rapier`, `gsap`.
- **Interactions**: raycasting on click shows an info card for each building and zooms the camera in; an easter egg in the garage drops Materia orbs with real physics; background music; a welcome screen featuring Yuffie.
- **In this portfolio**: clicking the project opens a window with the model in real-time 3D (drag to rotate, scroll to zoom). For the web, the model was optimised with [glTF-Transform](https://gltf-transform.dev/): textures resized to 1024 px and converted to WebP, geometry Draco-compressed, going from **95 MB to 7.6 MB**.
- **Approach**: made for the *Technology 3* course. The ideas (easter egg, UI design) are my own; AI was used as an assistant to explain concepts and unblock complex code, as noted in the code comments.

---

## References and intentions

### The BioShock Infinite menu
- Reference video: [BioShock Infinite – Menu Screens (PC)](https://www.youtube.com/watch?v=BAJw2XH-E5o)
- Reference screenshots: [`docs/references/`](docs/references/)
  - `bioshock-menu-principal.webp`: main menu (sign, ivy, bunting, sun at the end of the street)

What was carried over:
- **Composition**: the sign on the left, the street running towards the sun on the right.
- **UI**: aged paper, double rules, star-ornamented corners, a rolled-scroll selection highlight, `[Esc] BACK` prompts on a dark band.
- **Lighting**: golden backlight, sun rays, bloom, warm haze, vignette and film grain.
- **Set dressing**: ivy, faded bunting, star-spangled flags, a "Columbia Raffle and Fair 1912" banner.

### The reactive character
- Inspiration: a [LinkedIn post](https://lnkd.in/p/egtRvVPE) showing a Wii-inspired portfolio with a little character that follows the cursor and gets excited when you hover the options.
- Here, Elizabeth plays that role.

### Typography
The game's official fonts are not publicly documented (the logo is custom lettering). Free look-alikes were picked by eye from Google Fonts:

| Use | Font |
|---|---|
| Menu, prompts, body text | **Oswald** (condensed sans, close to "Alternate Gothic") |
| Banner, details | **Old Standard TT** |

---

## Chibi Elizabeth: creative process

The idea: use AI as a production tool, in service of an art direction defined up front.

1. **2D concept**: illustration generated with **Gemini** (Google) from my description of the character: chibi Elizabeth, blue dress, grey corset, bolero, cameo choker, anchor in hand.
   → [`docs/elizabeth/elizabeth-concept-gemini.jpg`](docs/elizabeth/elizabeth-concept-gemini.jpg)
2. **Into 3D**: the image was turned into a textured (PBR) 3D model with **[Form From Light](https://formfromlight.com/)** and exported as GLB.
   → [`elizabeth.glb`](elizabeth.glb) (≈ 6.8 MB, single mesh, no skeleton)
3. **Integration**: the model is loaded in Three.js, scaled and placed on the ground automatically, with its orientation corrected.
4. **Procedural animation**: since the model has no skeleton, it is animated in code:
   - turning towards the cursor;
   - hops with squash & stretch on landing;
   - a spin when a page opens;
   - gentle "breathing";
   - a random line of dialogue when clicked.

> To swap the character: drop another file named `elizabeth.glb` next to `index.html`. If it faces the wrong way, adjust `LIZ_YAW` in the script. Without the file, the site simply runs without a character.

---

## Tools and technologies

| Area | Tool |
|---|---|
| 3D rendering | [Three.js](https://threejs.org/) r160 (WebGL), loaded from a CDN, no build step |
| Post-processing | Sun rays (custom shader), UnrealBloom, warm colour grading (custom shader) |
| Environment | Generated in code: façades, signs and textures drawn with Canvas 2D |
| Sound | Web Audio API (synthesised ambience and effects, no audio files) |
| Character concept | Gemini |
| Character 3D model | [Form From Light](https://formfromlight.com/) |
| Development | Code written with the help of Claude (Anthropic) |

---

## Structure

```
index.html                  the whole site (HTML + CSS + JS)
elizabeth.glb               Elizabeth's 3D model
cv.pdf                      CV (Download CV button)
README.md                   this file
assets/photo.jpg            portrait for the About me page
assets/projects/            project previews (screenshots)
assets/wutai.glb            optimised Wutai model for the 3D viewer
docs/
  references/               game screenshots used as reference
  elizabeth/                2D concept of the character
```

---

## Editing the content

All the content lives in the `PROFILE` object at the top of the script in `index.html`:

- `first`, `last`, `title`: name and title
- `about`, `tagline`, `photo`: About me page
- `projects`: name, tags, description, link and preview image for each project (add `model: 'path.glb'` to open a 3D viewer instead of a link)
- `skills`: skills and level (0 to 1)
- `contact`: e-mail, LinkedIn, GitHub…
- `cv`: path to the CV (put `cv.pdf` next to `index.html`)

---

## Running locally

The site needs a small local server, because the `.glb` model won't load when opening the file directly:

```bash
python -m http.server 5173
```

Then open http://localhost:5173

## Deployment

There is no build step: the folder is deployed as-is on Vercel (it would also work on GitHub Pages or Netlify). Every push to `main` redeploys the site.

---

## Accessibility and performance

- A hidden text version of the content is provided for screen readers.
- Animations are reduced when the system requests `prefers-reduced-motion`.
- If rendering struggles (integrated GPU, laptop), the render resolution drops automatically.
