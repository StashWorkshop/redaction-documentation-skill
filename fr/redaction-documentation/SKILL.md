---
name: redaction-documentation
description: Rédiger ou améliorer un manuel de montage, de fabrication ou d'utilisation d'un projet DIY de l'utilisateur (électronique, PCB à souder, pièces imprimées en 3D, câblage, firmware), en Markdown et en PDF, avec illustrations par étape. Utilise ce skill dès que l'utilisateur demande de documenter un projet, d'écrire un guide, une notice, des instructions de montage, une nomenclature (BOM), un README de projet matériel ou de « rendre la doc plus claire », même sans dire « skill » ni « manuel ».
---

# Rédaction de documentation de montage

Un manuel réussi permet à quelqu'un qui n'a jamais vu le projet de le refaire
seul, sans erreur coûteuse (polarité, composant grillé, pièce imprimée pour
rien). Écris pour ce lecteur, pas pour l'utilisateur.

## 1. Avant d'écrire : rassembler, et combler les manques

Fais l'inventaire de tout ce que le manuel va citer : pièces, modèles 3D,
fichiers STEP/STL, Gerber, datasheets, firmware, photos, outils.

**Quand un élément cité est absent du contexte (pas de modèle 3D d'un
composant, pas de datasheet, pas de photo, firmware manquant…), ne le
contourne pas en silence et ne l'invente pas : propose à l'utilisateur de le
télécharger.** Donne pour chacun la source probable (site du fabricant,
GrabCAD, bibliothèque KiCad, dépôt GitHub), le nom de fichier attendu et où le
ranger dans le projet. Pour une pièce simple, propose en alternative de la
modéliser aux cotes standard ; c'est à l'utilisateur de choisir.

Pourquoi : un manuel qui décrit une pièce qu'on ne voit nulle part, ou une
cote devinée, est exactement là où le lecteur se trompe. Exemple : un jack DC et un
interrupteur absents de la 3D donnent des vues de montage qui ne les montrent pas.

Les faits se vérifient, ils ne se supposent pas : mesure dans Fusion (longueur
de vis, sens d'ouverture d'un logement), lis la netlist pour les polarités.
Ce que l'utilisateur seul sait (pièce imprimée ou récupérée, ordre réel de montage),
demande-le en QCM.

## 2. Structure

Chapitres numérotés dans l'ordre de fabrication, un fichier Markdown chacun
(`docs/00-version.md`, `01-presentation.md`…), assemblés en PDF :

0. Version, conventions de lecture, historique des révisions
1. Présentation, vue éclatée numérotée, durée et difficulté, sécurité
2. Nomenclature à cocher (composants, achats, pièces imprimées, visserie),
   vis à l'échelle 1:1, outils
3. Carte électronique : commande, ordre de soudure, polarités
4. Impression 3D : réglages, orientation, pièces de test
5. Assemblage mécanique, étape par étape
6. Câblage : schéma + tableau des connexions
7. Firmware et premier essai **boîtier ouvert**
8. Fermeture
9. Dépannage (symptôme → cause → test)

## 3. Procédés qui rendent un manuel lisible

- **Une opération = une étape = une image.** La pièce posée en couleur, le
  reste en gris, une flèche et une étiquette.
- **Un repère unique par pièce**, identique dans la nomenclature, l'image et
  le texte : repères PCB (R1, D1, J2), P = imprimé, V = vis, E = acheté.
- **En-tête d'étape** : durée, outils, pièces (avec quantités).
- **Encadrés typés et rares** : Note, Attention, Danger, Contrôle.
- **Un contrôle à la fin de chaque chapitre** (continuité, tension, jeu).
- **Annonce les gestes irréversibles avant** de les faire faire.
- **Code couleur unique** pour les fils (rouge +12 V, orange +5 V, noir GND).
- Version + historique en page 2.

## 4. Illustrations

- Vues 3D générées **par script** depuis Fusion (reproductibles pour la
  version suivante), document refermé sans enregistrer ensuite.
- Flèches et étiquettes ajoutées par script, avec une vérification
  automatique qu'aucune étiquette ne sort de l'image.
- Schémas 2D (câblage, soudure, vis 1:1) en SVG générés par script.
- Regarde chaque image produite avant de l'intégrer.

## 5. Livrer

- PDF régénéré par une commande du projet (par exemple `python tools/build_pdf.py`,
  script à écrire dans le projet, non fourni par ce skill), contrôlé page
  par page (planche d'aperçu).
- Signale ce qui n'est pas vérifié (cote supposée, échelle 1:1 à mesurer).
