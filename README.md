# Portfolio — Columbia

Portfolio interactif en 3D (site en anglais), en hommage au menu principal de **BioShock Infinite** (Irrational Games, 2013).
Le visiteur arrive directement devant une enseigne en bois suspendue dans une rue ensoleillée de Columbia : c'est le menu.
Elizabeth, en version chibi, l'accompagne et réagit à ses actions.

**Site en ligne : https://portfolio-tau-lyart-c9cwpvkk90.vercel.app/**

> Projet personnel, non commercial. BioShock Infinite et ses personnages appartiennent à Irrational Games / 2K.

---

## Aperçu

| Écran | Ce qu'on y trouve |
|---|---|
| **Menu** | Enseigne en papier vieilli, entièrement en anglais : *About me*, *My projects*, *Skills*, *Download CV*, *Contact* |
| **Pages** | L'enseigne pivote et affiche le contenu au dos, dans le style des écrans d'options du jeu (curseurs pour les compétences, etc.) |
| **Elizabeth** | Suit le curseur, sautille au survol, fait une pirouette à l'ouverture d'une page ; au clic, elle lance une Silver Eagle (« Booker, catch! ») qui s'ajoute au compteur en haut à gauche, comme dans le jeu |

Navigation : souris ou clavier (`↑` `↓`, `Entrée`, `Échap`). Le son démarre au premier clic ou à la première touche (règle des navigateurs).

---

## Projets présentés (« My projects »)

Au survol d'un projet, un aperçu façon photo d'époque apparaît à côté de l'enseigne (captures dans [`assets/projects/`](assets/projects/)).

| # | Projet | Description | Lien |
|---|---|---|---|
| I | **SUNGA** | Site de SUNGA, partenaire numérique et IT : applications web, mobiles et outils métier sur mesure | [sunga.be](https://sunga.be/fr) |
| II | **Kulabox** | Plateforme de réservation d'expériences culinaires africaines (recherche par envie, ville, date ; pages hôtes) | [staging.kulabox.eu](https://staging.kulabox.eu/fr/experiences) |
| III | **KRAFT** | Projet d'équipe : ateliers créatifs (linogravure…) dans des bars à café ; concept, problème, cible et site | [kraft-neon.vercel.app](https://kraft-neon.vercel.app/) |
| IV | **Wutai · FF VII** | Le village de Wutai (Final Fantasy VII) recréé dans **Blender**, puis exploré dans une app **React Three Fiber** : bâtiments cliquables, caméra animée avec **GSAP**, physique **Rapier**, easter egg des Materia cachées de Yuffie | démo en local |

### Wutai, en détail
- **Modélisation** : village, pagode, maisons, rivière et statue modélisés dans Blender (fichiers `Wutai.blend`, `Wutai houses.blend`), exportés en GLB (≈ 95 Mo).
- **App web** : Vite + React + TypeScript, `@react-three/fiber`, `@react-three/drei`, `@react-three/rapier`, `gsap`.
- **Interactions** : raycasting au clic sur les bâtiments, avec une fiche et un zoom de caméra ; easter egg dans le garage, qui fait tomber des Materia avec une vraie physique ; musique d'ambiance ; écran d'accueil avec Yuffie.
- **Démarche** : réalisée pour le cours *Technology 3*. Les idées (easter egg, design de l'UI) sont les miennes, et l'IA a servi d'assistant pour expliquer des concepts et débloquer du code complexe, comme indiqué dans les commentaires du code.

---

## Références et intentions

### Le menu de BioShock Infinite
- Vidéo de référence : [BioShock Infinite – Menu Screens (PC)](https://www.youtube.com/watch?v=BAJw2XH-E5o)
- Captures de référence : [`docs/references/`](docs/references/)
  - `bioshock-menu-principal.webp` : menu principal (enseigne, lierre, fanions, soleil au bout de la rue)

Éléments repris :
- **Composition** : enseigne à gauche, rue qui file vers le soleil à droite.
- **UI** : papier vieilli, double filet, coins ornés d'étoiles, sélection en forme de parchemin enroulé, indications `[Esc] BACK` sur bandeau sombre.
- **Lumière** : contre-jour doré, rayons de soleil, halo (bloom), brume chaude, vignettage et grain.
- **Décor** : lierre, fanions délavés, drapeaux étoilés, bannière « Columbia Raffle and Fair 1912 », enseigne « Groceries & Meat ».

### Le personnage qui réagit
- Inspiration : un [post LinkedIn](https://lnkd.in/p/egtRvVPE) présentant un portfolio inspiré de la Wii, avec un petit personnage qui suit le curseur et s'anime au survol des options.
- Ici, ce rôle est tenu par Elizabeth.

### Typographies
Les polices officielles du jeu ne sont pas documentées publiquement (le logo est un lettrage sur mesure). Équivalents libres choisis à l'œil, via Google Fonts :

| Usage | Police |
|---|---|
| Menu, indications, textes | **Oswald** (linéale condensée, proche « Alternate Gothic ») |
| Bannière, détails | **Old Standard TT** |

---

## Elizabeth chibi : processus de création

Démarche : utiliser l'IA comme un outil de production, au service d'une direction artistique définie au départ.

1. **Concept 2D** : illustration générée avec **Gemini** (Google), à partir de ma description du personnage : Elizabeth en chibi, robe bleue, corset gris, boléro, collier camée, ancre à la main.
   → [`docs/elizabeth/elizabeth-concept-gemini.jpg`](docs/elizabeth/elizabeth-concept-gemini.jpg)
2. **Passage en 3D** : l'image a été convertie en modèle 3D texturé (PBR) avec **[Form From Light](https://formfromlight.com/)**, puis exportée au format GLB.
   → [`elizabeth.glb`](elizabeth.glb) (≈ 6,8 Mo, maillage unique, sans squelette)
3. **Intégration** : modèle chargé dans Three.js, mis à l'échelle et posé au sol automatiquement, orientation corrigée.
4. **Animation procédurale** : comme le modèle n'a pas de squelette, il est animé en code :
   - rotation vers le curseur ;
   - sauts avec écrasement / étirement à l'atterrissage ;
   - pirouette à l'ouverture d'une page ;
   - légère « respiration » ;
   - réplique aléatoire quand on clique dessus.

> Pour remplacer le personnage : déposer un autre fichier nommé `elizabeth.glb` à côté de `index.html`. Si l'orientation est mauvaise, ajuster `LIZ_YAW` dans le script. Sans fichier, le site fonctionne simplement sans personnage.

---

## Outils et technologies

| Domaine | Outil |
|---|---|
| Rendu 3D | [Three.js](https://threejs.org/) r160 (WebGL), chargé par CDN, sans build |
| Post-traitement | Rayons de soleil (shader maison), UnrealBloom, étalonnage chaud (shader maison) |
| Décor | Généré en code : façades, enseignes et textures dessinées en Canvas 2D |
| Son | Web Audio API (ambiance et effets synthétisés, aucun fichier audio) |
| Concept du personnage | Gemini |
| Modèle 3D du personnage | [Form From Light](https://formfromlight.com/) |
| Développement | Code écrit avec l'aide de Claude (Anthropic) |

---

## Structure

```
index.html                  le site complet (HTML + CSS + JS)
elizabeth.glb               modèle 3D d'Elizabeth
README.md                   ce fichier
assets/projects/            aperçus des projets (captures d'écran)
docs/
  references/               captures du jeu servant de référence
  elizabeth/                concept 2D du personnage
```

---

## Personnaliser le contenu

Tout le contenu se trouve dans l'objet `PROFILE`, en haut du script de `index.html` :

- `first`, `last`, `title` : nom et titre
- `about`, `tagline`, `photo` : page « À propos »
- `projects` : nom, technos, description, lien de chaque projet
- `skills` : compétences et niveau (0 à 1)
- `contact` : e-mail, LinkedIn, GitHub…
- `cv` : chemin du CV (déposer `cv.pdf` à côté de `index.html`)

---

## Lancer en local

Le site doit être servi par un petit serveur, car le modèle `.glb` ne se charge pas en ouvrant le fichier directement :

```bash
python -m http.server 5173
```

Puis ouvrir http://localhost:5173

## Mise en ligne

Il n'y a pas d'étape de build : le dossier peut être publié tel quel sur GitHub Pages, Netlify ou Vercel.

---

## Accessibilité et performances

- Une version texte du contenu, cachée à l'écran, est fournie pour les lecteurs d'écran.
- Les animations sont réduites si le système demande `prefers-reduced-motion`.
- Si l'animation rame (GPU intégré, PC portable), la résolution de rendu baisse automatiquement.
