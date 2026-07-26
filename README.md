# Orbitalis

Une simulation interactive et immersive du Système solaire, réalisée avec les API natives du navigateur.

Orbitalis calcule les positions orbitales à partir d’éléments J2000, puis restitue le Soleil, les huit planètes, Pluton, la Lune, la ceinture d’astéroïdes et un ciel étoilé dans une interface inspirée d’un observatoire spatial.

## Points forts

- Moteur orbital képlérien avec résolution de l’équation de Kepler par Newton-Raphson.
- Deux échelles de distance : condensée logarithmique et relative.
- Vue du dessus ou perspective avec caméra amortie et suivi des astres.
- Rendu Canvas entièrement procédural : planètes, textures, halos, anneaux, étoiles et astéroïdes.
- Zoom, pan, picking, survol, double-clic, pincement et raccourcis clavier.
- Fiche détaillée pour chaque corps et mini-carte indépendante.
- Interface bilingue français/anglais.
- Mise en page responsive pour desktop, tablette et mobile.
- Accessibilité clavier, régions live, états ARIA et prise en charge de `prefers-reduced-motion`.
- Aucune bibliothèque, dépendance, police, image de production ou requête externe.

## Démonstration locale

Aucune installation ni compilation n’est nécessaire.

### Ouverture directe

Ouvrir simplement [`index.html`](./index.html) dans un navigateur moderne.

### Serveur local

Depuis la racine du projet :

```bash
python3 -m http.server 4173
```

Puis ouvrir [http://localhost:4173](http://localhost:4173).

## Contrôles

| Action | Souris / tactile | Clavier |
| --- | --- | --- |
| Sélectionner un astre | Clic ou toucher | Sélecteur d’astre accessible |
| Déplacer la caméra | Glisser | — |
| Zoomer | Molette ou pincement | `+` / `-` |
| Revenir à la vue d’ensemble | Double-clic ou double-tap | — |
| Fermer la fiche | Bouton de fermeture | `Échap` |
| Afficher ou masquer les noms | Contrôle **Noms** | `L` |
| Afficher ou masquer les orbites | Contrôle **Orbites** | `O` |
| Changer de perspective | Contrôle **Perspective** | `V` |

`1×` correspond à un jour simulé par seconde. La vitesse peut varier de `0×` à `100×`.

## Modes de QA

Des paramètres d’URL facilitent les vérifications reproductibles :

| Paramètre | Effet |
| --- | --- |
| `?selftest=1` | Exécute les 88 auto-tests numériques et déterministes |
| `?qa=1` | Force l’état visuel de référence en français |
| `?reduced=1` | Simule le mode de mouvement réduit et démarre à `0×` |

Ils peuvent être combinés, par exemple :

```text
http://localhost:4173/?qa=1&selftest=1
```

Le compte-rendu de validation détaillé est disponible dans [`design-qa.md`](./design-qa.md).

## Architecture

L’application est volontairement contenue dans un seul fichier HTML autonome. Son script est organisé en modules internes lisibles :

- `Data` — corps célestes, étoiles et astéroïdes seedés ;
- `I18n` — traductions, nombres, dates et attributs accessibles ;
- `Clock` — date julienne et vitesse simulée ;
- `OrbitalEngine` — propagation des orbites et résolution de Kepler ;
- `ScaleMapper` — interpolation entre les deux représentations des distances ;
- `Camera` — suivi 3D, pan, zoom et projection orthographique ;
- `Renderer` — scène principale, portraits procéduraux et mini-carte ;
- `Picking` et `Interactions` — sélection et gestes ;
- `UI` — HUD, labels et fiche des astres ;
- `Lifecycle` — boucle RAF, redimensionnement et nettoyage ;
- `SelfTest` — validation numérique intégrée.

Les Canvas sont dimensionnés à la taille CSS multipliée par un DPR plafonné à `2`. Le rendu utilise une seule boucle `requestAnimationFrame` et suspend son activité lorsque l’onglet est masqué.

## Données scientifiques

Les éléments orbitaux approximatifs J2000 et les données physiques proviennent des tables du Jet Propulsion Laboratory :

- [Approximate Positions of the Planets — JPL](https://ssd.jpl.nasa.gov/planets/approx_pos.html)
- [Planetary Physical Parameters — JPL](https://ssd.jpl.nasa.gov/planets/phys_par.html)

Les comptes de lunes sont figés au 26 juillet 2026. La simulation privilégie une représentation pédagogique et visuelle ; elle ne remplace pas un éphéméride de haute précision.

## Structure du dépôt

```text
.
├── index.html       # Application autonome
├── README.md        # Présentation et documentation
├── design-qa.md     # Rapport d’acceptation visuelle et fonctionnelle
├── AGENT.md         # Brief initial du projet
├── mockup-1.png     # Première direction visuelle
└── mockup-2.png     # Référence visuelle retenue
```

## Déploiement

Orbitalis est un site entièrement statique. Le dépôt peut être publié tel quel avec GitHub Pages, Vercel, Netlify ou n’importe quel serveur HTTP, sans commande de build.

Pour GitHub Pages, sélectionner la branche principale et le dossier racine dans **Settings → Pages**.

## Compatibilité

Une version récente de Chrome, Edge, Firefox ou Safari est recommandée. Les interactions tactiles nécessitent un navigateur prenant en charge les Pointer Events.

## Licence

Aucune licence n’est fournie pour le moment. Ajouter un fichier `LICENSE` avant d’autoriser explicitement la réutilisation ou la redistribution du projet.
