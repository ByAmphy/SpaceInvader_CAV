# Space Invaders – Projet C / Ncurses & SDL3
Desmet Romain/Janda Thomas
## Description

Jeu **Space Invaders** en C avec deux interfaces graphiques :  

- **Ncurses** : version textuelle dans le terminal.  
- **SDL3** : version graphique avec sprites et couleurs (`vue_sdl.c` / `vue_sdl.h`).  

## Architecture MVC

### Modèle (`modele.c / modele.h`)
- Contient toutes les données du jeu :
  - Joueur, ennemis, projectiles, boucliers
  - Score, vies, niveau, état du jeu
- Fournit des fonctions pour :
  - Initialiser le jeu
  - Déplacer le joueur
  - Mettre à jour les ennemis
  - Gérer les projectiles et collisions
  - Vérifier les conditions de victoire/perte

### Vue (`vue_ncurses.c / vue_sdl.c`)
- **ncurses** : affichage ASCII dans le terminal
- **SDL3** : affichage graphique avec textures et sprites
- Fournit des fonctions pour :
  - Dessiner le joueur, les ennemis, projectiles et boucliers
  - Afficher le HUD (score, vies, niveau)
  - Afficher les écrans de Game Over et victoire
- Le modèle ne connaît pas la vue : séparation stricte

### Contrôleur (`controleur.c / controleur.h`)
- Gère la communication entre le modèle et la vue
- Récupère les entrées clavier ou SDL
- Met à jour le modèle en conséquence (déplacement du joueur, tirs)
- Appelle la vue pour afficher l’état actuel du jeu
- Vérifie les écrans Game Over et victoire et les interactions avec l’utilisateur
- **Ne contient pas la logique interne du jeu** (collision, score, mouvement des ennemis, projectiles…) qui est dans le modèle

---

## Fonctionnalités

- Mouvement du joueur (gauche/droite)  
- Tir de projectiles  
- Ennemi en formation, déplacement et tir aléatoire  
- Boucliers destructibles  
- Gestion de niveaux et de la difficulté  
- Écrans Game Over et Victoire  
- Choix du mode d’affichage : Ncurses ou SDL3  

---
Compilation
- gcc *.c -I./external/SDL3/include -L./external/SDL3/lib -lSDL3 -lncurses -Wl,-rpath,'$ORIGIN/external/SDL3/lib' -o space_invaders
- Choisir 1 ou 2, pour le mode.
---
Exécution:
- ./space_invaders
---

Commandes clavier
| Touche       | Action                                      |
|-------------|--------------------------------------------|
| Flèche gauche | Déplacer le joueur à gauche               |
| Flèche droite| Déplacer le joueur à droite               |
| Espace       | Tirer un projectile                        |
| Q            | Quitter le jeu                             |
| Entrée       | Recommencer après Game Over ou victoire    |
| N            | Passer au niveau suivant (victoire SDL uniquement) |

---

Structure des fichiers
Structure des fichiers
```
SpaceInvaders/
├─ modele.c
├─ modele.h
├─ controleur.c
├─ controleur.h
├─ vue_ncurses.c
├─ vue_ncurses.h
├─ vue_sdl.c
├─ vue_sdl.h
├─ utils/
│  └─ texture/
│     ├─ ship_2.png
│     ├─ monstre_1.png
│     ├─ shield_1.png
│     ├─ shield_2.png
│     ├─ projectile_0.png
│     └─ projectile_1.png
└─ README.md

```
## Dépendances
### Ncurses
```bash
sudo apt install libncurses5-dev libncursesw5-dev
