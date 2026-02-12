# Rapport de Projet - Graphisme par Ordinateur

**Lien Shadertoy :** [Ajouter votre lien ici]

## Description de la Scène

La scène représente un **avion rouge volant au-dessus de l'eau**, avec une vue du dessus. L'environnement comprend :
- Un avion rouge contrôlable (corps + ailes + cockpit bleu)
- Une surface d'eau animée avec des vagues
- Des bâtiments qui défilent
- Un phare avec lumière jaune la nuit
- Des oiseaux blancs qui volent avec battement d'ailes

Les éléments du décor défilent de manière infinie pour simuler le mouvement de l'avion.

## Implémentation des Exigences

### 1. Plusieurs sources de lumière
- **Cycle jour/nuit** : Le soleil (source blanche intense) traverse le ciel, suivi de la lune (source blanche faible). Le fond passe du bleu clair au noir.
- **Phare** : Source de lumière jaune ponctuelle visible la nuit, avec atténuation en fonction de la distance.
- **Ombres douces** : Calculées avec soft shadow pour les ombres réalistes.

### 2. Déplacement de la caméra
La caméra suit l'avion en restant positionnée haut et derrière, regardant toujours devant l'avion. L'avion peut être contrôlé horizontalement avec les flèches gauche/droite du clavier.

### 3. Disque découpé dans un plan non aligné
Un disque orange/cuivre traverse la scène périodiquement. Il est incliné avec des rotations non-alignées. Représenté par un cylindre très fin.

### 4. Cylindre
Le phare est composé de trois cylindres empilés :
- Base grise (île)
- Tour grise
- Salle des lampes jaune (source lumineuse)

### 5. Miroir (plan)
L'eau agit comme miroir avec :
- Réflexion calculée par rayon réfléchi
- Effet Fresnel : "mi-bleu et mi-miroir" selon l'angle de vue
- Couleur de l'eau mélangée avec la réflexion du ciel et des objets

### 6. Objet articulé (Oiseau)
L'oiseau blanc possède **2 articulations** :
- **Corps** : Ellipsoïde fixe
- **Ailes** : Deux ellipsoïdes symétriques qui battent avec une rotation sinusoïdale

**Schéma de l'objet articulé (Vue de Face) :**

![[schema.svg]]

Les ailes oscillent sinusoïdalement avec une fréquence de 15 Hz pour simuler le battement des ailes.

### 7. Effet supplémentaire - Contrôle clavier
L'avion est contrôlable avec le clavier (flèches gauche/droite) grâce à un Buffer A qui :
- Lit l'état du clavier
- Maintient la position horizontale de l'avion
- Limite les déplacements entre -7 et +7 unités
- Stocke l'état entre les frames via feedback buffer

## Difficultés Rencontrées

### Gestion du clavier et buffer
La mise en place du contrôle clavier a été **complexe et confuse** car elle nécessite :
1. **Deux passes de rendu** : Buffer A pour la logique, Image pour le rendu
2. **Configuration des canaux** : iChannel0 (Keyboard) et iChannel1 (Buffer A lui-même pour le feedback)
3. **Compréhension du feedback** : Le buffer doit se lire lui-même pour conserver l'état entre frames
4. **Synchronisation** : La position calculée dans Buffer A doit être correctement lue dans le shader principal

Après plusieurs essais et compréhension du mécanisme de feedback des buffers dans Shadertoy, le système fonctionne correctement et permet un contrôle fluide de l'avion.

## Capture d'écran

*[Screenshots à insérer ici]*
