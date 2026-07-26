# Orbitalis — Design QA

## Vérité visuelle et méthode

- Référence acceptée : `/Users/fabricecoroller/Documents/workspace/orbitalis/mockup-2.png`.
- Implémentation : `/Users/fabricecoroller/Documents/workspace/orbitalis/solar-system.html`.
- Capture principale : `/private/tmp/orbitalis-qa-desktop-final.png`, produite dans le navigateur intégré depuis le serveur local.
- Comparaison complète : `/private/tmp/orbitalis-design-comparison.png`.
- Comparaison ciblée de la fiche : `/private/tmp/orbitalis-info-comparison.png`.
- Viewport de référence et de capture : `1672 × 941` pixels CSS, DPR `1`. Les deux images font exactement `1672 × 941`; aucune normalisation de densité n’a été nécessaire.
- État QA : français forcé, date figée au 26 juillet 2026, Jupiter sélectionnée et suivie, Mars survolée, `1×`, zoom `1,8×`, perspective, orbites, noms et échelle condensée.
- Inspection : référence, rendu, comparaison côte à côte et crop de la fiche examinés avec l’outil d’inspection d’images; responsive inspecté à `1024 × 768` et `390 × 844`.

## Surfaces comparées

1. Composition globale : marque en haut à gauche, date centrée, langue en haut à droite, simulation en bas à gauche, mini-carte et fiche à droite.
2. Traitement HUD : fond spatial `#02070b`, panneaux froids translucides, fines bordures, texte ivoire/gris bleuté et accent ambre.
3. Typographie : capitales espacées, hiérarchie sans-serif/monospace, valeurs tabulaires et densité conformes à la V2 avec polices système.
4. Fiche Jupiter : grand portrait procédural, titre/type, six rangées statistiques, séparateurs, bouton de fermeture et fait contextuel.
5. Contrôles : slider, zoom segmenté, interrupteurs, sélecteur d’échelle, état actif ambre et cibles cohérentes.
6. Mini-carte : système complet indépendant, corps, orbites, sélection et polygone du viewport utile.
7. Responsive : panneaux réduits sur tablette; focus de Jupiter maintenu au-dessus de la bottom sheet et contrôles masqués rendus inertes sur mobile.

## Copie et divergences approuvées

- La copie visible et la casse suivent la V2 : `Distance actuelle`, `CONDENSÉE` et `RÉELLE`; le tooltip précise la distance simulée.
- Les valeurs de distance courante diffèrent de la maquette car elles proviennent de la date et des positions képlériennes calculées.
- La scène astronomique suit les éléments J2000 et non la composition illustrative; le HUD reste la vérité visuelle.
- Les planètes sont exclusivement procédurales : palette, éclairage, anneaux et détails distinctifs sont conservés sans image externe.
- Aucun cadre extérieur arrondi, conformément à la divergence validée.

## Historique des corrections P0–P2

### Itération 1

- P1 : portrait Jupiter trop petit — canevas et rayon du portrait agrandis.
- P1 : coût des orbites proche de 17 fps — matrices orbitales et chemins normalisés mis en cache; cadence remontée à 60 fps et plus dans le navigateur de QA.
- P1 : suivi 3D et suivi rapide inexacts — ajout de la coordonnée caméra `z` et transport de la caméra par le delta orbital du corps suivi.
- P1 : éléments masqués encore interactifs — synchronisation `inert`, `aria-hidden`, `tabIndex` et restitution du focus au Canvas.
- P2 : mini-carte trop basse et viewport imprécis — repositionnement et projection du viewport depuis les coins de la zone visible.
- P2 : statistiques trop petites/faibles — taille, contraste et espacement augmentés.
- P2 : libellés `Relative` et `Diamètre moyen` — corrigés en `Réelle` et `Diamètre`.
- P2 : clic simple repické après 220 ms — picking mémorisé immédiatement, action seule différée pour préserver le double-clic.
- P2 : Lune et orbite visuelle divergentes — objet orbital unique partagé par la propagation, la ligne et les tests.

### Itération 2

- Tablette : interrupteur Perspective débordant — réduction contrôlée du gap, de la typographie et du switch au breakpoint.
- Mobile : Jupiter partiellement masquée — point de focus calculé depuis la hauteur finale de la bottom sheet.
- Mobile : cibles FR/EN sous 44 px — largeur minimale portée à 44 px; aucune cible active mesurée sous `44 × 44`.
- Desktop : médaillon Jupiter remonté et porté à 196 px sans agrandir le disque planétaire; mini-carte portée à `320 × 145`.
- Données : métriques portées à 12,2 px sur desktop, 12 px sur mobile et fait contextuel à 13/12,5 px.
- Copie : `Distance actuelle` restauré et sélecteur d’échelle affiché en capitales.
- Accessibilité : ajout du focus visible Canvas, placeholder du sélecteur, infobulle `aria-hidden`, labels invisibles non cliquables et contrôles mobiles inertes sous la fiche.
- Performance : cache des formateurs `Intl`, mise à jour des astéroïdes à cadence visuelle adaptée, suspension/reprise idempotente de l’unique RAF.
- Résultat visuel après correction : aucun écart P0–P2 restant dans la composition HUD, la fiche et les breakpoints testés.

## Vérifications fonctionnelles

- `?selftest=1` : `88/88` tests réussis (résidu de Kepler, périhélie/aphélie, périodicité des neuf corps et de la Lune, temps `0×/1×/100×`, échelles et astéroïdes seedés).
- État initial normal : UTC réelle, `1×`, `1,8×`, Jupiter sélectionnée/suivie; en mouvement réduit : `0×`, `EN PAUSE`, transitions ramenées à `1e-06s`.
- Interactions vérifiées : sélection Canvas et DOM, suivi continu jusqu’à Mercure à `100×`, pan libérant le suivi, molette ancrée, zoom `−/+`, clic/double-clic, fermeture/Échap, dock mobile, toggles, deux vues, deux échelles et traduction FR/EN immédiate.
- Suivi haute vitesse : Mercure mesurée exactement au focus mobile (`195`, `261,64`) à `100×`.
- Responsive : captures `1024 × 768` et `390 × 844`; bottom sheet à `57,1 vh`, mini-carte `132 × 72`, aucune cible active sous 44 px.
- Réseau : aucun script, style, police, image ou média externe; favicon vide inline pour éviter une requête implicite du navigateur.
- Console : aucune erreur ni avertissement; uniquement le journal de succès des auto-tests.
- Performance : cache orbital validé à 60 fps dans l’audit indépendant et métriques supérieures à 60 fps sur les captures DPR 1.
- Stabilité longue : même instance laissée active 5 030 s (83 min 50 s), de septembre 2026 à juillet 2103 simulé; nœuds DOM `147 → 147`, labels `10 → 10`, Canvas `3 → 3`, 86,4 fps en fin de mesure et aucune erreur/alerte.
- Cycle de vie : une seule boucle RAF, arrêt en onglet masqué/pagehide, reprise avec horloge et métriques réinitialisées, listeners nettoyés par `AbortController`.
- L’ouverture `file://` n’a pas pu être automatisée par le navigateur intégré à cause de sa politique de navigation locale. La compatibilité directe a été contrôlée statiquement : document unique, module inline sans import, stockage optionnel protégé et aucune dépendance URL.

## Résultat

final result: passed
