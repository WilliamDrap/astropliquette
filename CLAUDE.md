# Contexte du projet Astropliquette

Ce dépôt rassemble les appliquettes interactives de William Drapeaud, secrétaire des Groupes Scientifiques d'Arras (GSA), astrophotographe amateur et vulgarisateur, avec un niveau universitaire en astrophysique. Les raisonnements physiques peuvent être menés jusqu'au bout, équations comprises. Les appliquettes portent en pied de page le logo GSA (discret, lien vers gsa-asso.fr) et la mention « Une appliquette des Groupes Scientifiques d'Arras/WD ».

## Règles d'écriture

Toutes les réponses et tous les textes sont en français. William demande des réponses courtes, le point principal d'abord, en phrases suivies, sans tirets ni listes à puces. Les documents produits sont en Markdown. En cas de demande ambiguë, poser une question plutôt que deviner.

Les textes affichés dans les appliquettes s'adressent à la fois aux enfants des ateliers (dès 8 ans) et au grand public. La règle est de parler simple sans parler bébé : pas de mascotte ni de ton enfantin, un visuel réaliste et sobre, des textes courts. Un panneau « Pour aller plus loin » a été essayé puis retiré car jugé peu utile ; la note sur les échelles non respectées reste affichée sous les vues. Les jeux utilisent le tutoiement. Veiller à ne jamais formuler une phrase qui renforce l'idée reçue combattue (par exemple « la Lune change de forme »).

## Conventions techniques

Chaque appliquette est un fichier HTML unique et autonome dans son propre dossier (`nom/index.html`), avec CSS et JavaScript intégrés. Les bibliothèques sont chargées en UMD depuis cdnjs à une version figée (Three.js r128). Les images sont intégrées en data URI pour que la page reste publiable telle quelle comme artefact Claude. La page doit être responsive, fonctionner au doigt sur téléphone, gérer le thème clair et sombre, respecter `prefers-reduced-motion` et rester utilisable au clavier.

La racine contient `index.html`, la galerie qui pointe vers chaque appliquette, à mettre à jour à chaque ajout, ainsi que le README.

## Appliquette des phases de la Lune (`phases-lune/`)

L'état actuel est le niveau 1. La vue de l'espace est un canvas 2D vu depuis le pôle Nord, Soleil hors champ à droite et rayons parallèles. La vue depuis la Terre est une Lune Three.js texturée, vue depuis l'hémisphère nord. Une option affiche en bleu la moitié de la Lune tournée vers la Terre. Un mode Explorer donne le nom de la phase et une phrase d'explication. Un mode défi enchaîne six phases (deux faciles parmi pleine Lune et quartiers, puis les croissants, puis les gibbeuses), tolérance de 15°, indices selon l'erreur (mauvais côté, trop ou pas assez de lumière). L'énoncé du défi est dans un bandeau au dessus des deux vues, l'objectif en vignette dans la vue depuis la Terre.

L'angle θ est l'angle Soleil, Terre, Lune, nul à la nouvelle Lune, croissant dans le sens direct. Dans le repère de l'observateur (x vers sa droite, z vers lui), la direction du Soleil vaut (sin θ, 0, −cos θ). La fraction éclairée vaut (1 − cos θ)/2.

L'éclairage est un ShaderMaterial en loi de Lommel‑Seeliger, I ∝ cos i / (cos i + cos e), choisie parce que la loi de Lambert faisait paraître les croissants trop fins et éteints. Exposition 5, compression douce 1 − exp(−x), conversion sRGB manuelle. La lumière cendrée est un terme ambiant bleuté, plus fort vers la nouvelle Lune.

La texture est la carte couleur LROC 2k du CGI Moon Kit de la NASA (svs.gsfc.nasa.gov/4720), recompressée en JPEG et intégrée en base64. Elle est centrée sur la longitude 0, d'où `moon.rotation.y = −π/2` pour tourner la face visible vers l'observateur, mer des Crises à droite. Le crédit NASA doit rester en pied de page.

## Feuille de route

Le niveau 2 ajoutera la rotation de la Terre, un personnage et une horloge autour de la question « pourquoi voit‑on parfois la Lune en plein jour ? », puis l'inclinaison du terminateur selon la latitude en déplaçant l'observateur d'Arras vers l'équateur et l'hémisphère sud. Le niveau 0, destiné aux réseaux sociaux, reste à choisir entre une courte boucle vidéo verticale tirée de l'appliquette et un carrousel à fausse interactivité. Le relief tiré de la carte d'altitude LOLA est une option écartée pour l'instant. Une vidéo fulldome pour planétarium sur le même sujet est prévue ensuite.

Point à surveiller : sur téléphone, les deux vues s'empilent et les défis demandent un peu de défilement.
