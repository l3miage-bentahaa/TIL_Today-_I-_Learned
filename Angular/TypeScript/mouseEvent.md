# Résumé : Gestion de la couleur sur un Pixel Art avec Angular

## 1. Événements de souris essentiels

| Événement      | Quand il se déclenche                       | Notes importantes |
|----------------|--------------------------------------------|-----------------|
| `mousedown`    | Dès qu’un bouton de souris est **enfoncé** | Permet de détecter que l’utilisateur commence à “peindre” |
| `mouseup`      | Dès qu’un bouton de souris est **relâché** | Permet de savoir quand arrêter de “peindre” |
| `click`        | Après un appui + relâchement               | Ne convient pas pour “peindre en glissant” |
| `mouseenter`   | Quand la souris **entre** dans un élément  | Utilisé pour colorier chaque cellule traversée |
| `contextmenu`  | Clic droit → ouvre le menu contextuel      | On peut l’annuler avec `event.preventDefault()` |

---

## 2. La propriété `event.button`

Indique quel bouton de la souris déclenche l’événement :

| Valeur | Bouton |
|--------|--------|
| 0      | Gauche |
| 1      | Molette / milieu |
| 2      | Droit  |

- Utile pour savoir si l’utilisateur utilise le clic droit ou gauche.  
- Disponible dans `mousedown`, `mouseup`, `click`, etc.
