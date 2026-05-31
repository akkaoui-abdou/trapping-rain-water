# LeetCode 42 - Trapping Rain Water

## Énoncé

On te donne un tableau `height` représentant une carte d'élévation où la largeur de chaque barre est de `1`.

L'objectif est de calculer la quantité totale d'eau qui peut être retenue après une pluie.

### Exemple

```python
height = [0,1,0,2,1,0,1,3,2,1,2,1]
```

Représentation :

```text
          █
    █~~~~~██~
█~~~██~██████
```

Résultat :

```python
6
```

---

## Principe

Pour qu'une position puisse retenir de l'eau, il faut :

* une barrière suffisamment haute à gauche ;
* une barrière suffisamment haute à droite.

La hauteur maximale d'eau à une position `i` est :

```python
min(max_left, max_right)
```

L'eau retenue est alors :

```python
min(max_left, max_right) - height[i]
```

---

## Solution Optimale : Deux Pointeurs

### Complexité

* Temps : **O(n)**
* Mémoire : **O(1)**

### Algorithme

1. Initialiser deux pointeurs :

   * `left` au début du tableau.
   * `right` à la fin du tableau.

2. Garder en mémoire :

   * `left_max` : hauteur maximale rencontrée à gauche.
   * `right_max` : hauteur maximale rencontrée à droite.

3. Comparer les hauteurs aux extrémités :

   * Si `height[left] < height[right]`, traiter le côté gauche.
   * Sinon, traiter le côté droit.

4. Calculer l'eau piégée à chaque étape.

---

## Implémentation Python

```python
from typing import List

class Solution:
    def trap(self, height: List[int]) -> int:
        left = 0
        right = len(height) - 1

        left_max = 0
        right_max = 0
        water = 0

        while left < right:
            if height[left] < height[right]:

                if height[left] >= left_max:
                    left_max = height[left]
                else:
                    water += left_max - height[left]

                left += 1

            else:

                if height[right] >= right_max:
                    right_max = height[right]
                else:
                    water += right_max - height[right]

                right -= 1

        return water
```

---

## Exemple d'Exécution

```python
height = [0,1,0,2,1,0,1,3,2,1,2,1]

sol = Solution()
print(sol.trap(height))
```

### Sortie

```text
6
```

---

## Explication Pas à Pas

Pour :

```python
height = [4,2,0,3,2,5]
```

L'eau retenue par position :

| Index | Hauteur | Eau retenue |
| ----- | ------- | ----------- |
| 0     | 4       | 0           |
| 1     | 2       | 2           |
| 2     | 0       | 4           |
| 3     | 3       | 1           |
| 4     | 2       | 2           |
| 5     | 5       | 0           |

Total :

```python
2 + 4 + 1 + 2 = 9
```

Résultat :

```python
9
```

---

## Points Clés à Retenir

* Une position retient de l'eau uniquement si elle est encadrée par des barres plus hautes.
* Le niveau d'eau dépend de la plus petite des deux hauteurs maximales (gauche et droite).
* La technique des deux pointeurs permet d'obtenir une solution optimale :

  * **O(n)** en temps.
  * **O(1)** en mémoire.

Cette solution est la plus souvent attendue lors des entretiens techniques et sur LeetCode.



## Exemple
Pour :

```python
height = [0,1,0,2]
```

Calculons l'eau retenue à chaque position.

## Étape 1 : Trouver les max à gauche et à droite

| Index | Height | Max Gauche | Max Droite |
| ----- | ------ | ---------- | ---------- |
| 0     | 0      | 0          | 2          |
| 1     | 1      | 1          | 2          |
| 2     | 0      | 1          | 2          |
| 3     | 2      | 2          | 2          |

---

## Étape 2 : Calculer l'eau retenue

Formule :

```python
water[i] = min(max_left[i], max_right[i]) - height[i]
```

### Index 0

```python
min(0, 2) - 0 = 0
```

Eau = **0**

### Index 1

```python
min(1, 2) - 1 = 0
```

Eau = **0**

### Index 2

```python
min(1, 2) - 0 = 1
```

Eau = **1**

### Index 3

```python
min(2, 2) - 2 = 0
```

Eau = **0**

---

## Résultat final

| Index | Eau retenue |
| ----- | ----------- |
| 0     | 0           |
| 1     | 0           |
| 2     | 1           |
| 3     | 0           |

Total :

```python
0 + 0 + 1 + 0 = 1
```

✅ **Réponse :**

```python
height = [0,1,0,2]

output = 1
```

### Visualisation

```text
Hauteurs :

      █
  █   █
  █ ~ █
__█_█_█__

~ = eau
```

La case d'index `2` est coincée entre une barre de hauteur `1` à gauche et une barre de hauteur `2` à droite, elle peut donc retenir **1 unité d'eau**.

