# Cours 2 — Représentation binaire des données

## 1. Rappels : bit, octet, n bits

- Un **bit** (binary digit) vaut 0 ou 1.
- Un **octet** = 8 bits.
- Avec **n bits**, on peut représenter **2ⁿ** valeurs différentes.

## 2. Entiers positifs (non signés)

Représentation « binaire pur » : chaque bit est pondéré par une puissance de 2.

**Plage** : avec n bits, de `0` à `2ⁿ − 1`.

| Nombre de bits | Plage (non signé) |
|----------------|-------------------|
| 8 bits (1 octet) | 0 à 255 |
| 16 bits | 0 à 65 535 |
| 32 bits | 0 à 4 294 967 295 |

**Exemple** : `42₁₀` sur 8 bits :

```
42 ÷ 2 = 21 r 0
21 ÷ 2 = 10 r 1
10 ÷ 2 =  5 r 0
 5 ÷ 2 =  2 r 1
 2 ÷ 2 =  1 r 0
 1 ÷ 2 =  0 r 1
→ 101010₂, sur 8 bits : 00101010
```

## 3. Entiers signés (positifs et négatifs)

Quatre méthodes, dont seul le complément à deux est utilisé aujourd'hui pour les entiers
(le décalage, lui, est repris plus loin pour l'exposant des nombres réels).

### 3.1 Signe et magnitude

Le bit le plus significatif indique le signe (0 = positif, 1 = négatif), le reste représente
la magnitude.

- `+5` sur 8 bits → `00000101`
- `−5` sur 8 bits → `10000101`

Inconvénients : deux zéros (`00000000` et `10000000`), addition compliquée.

### 3.2 Complément à un

On inverse tous les bits pour obtenir l'opposé.

- `+5` → `00000101`
- `−5` → `11111010`

Inconvénient : encore deux zéros.

### 3.3 Complément à deux (standard)

**Méthode** : pour obtenir `−N`, on inverse tous les bits de `N` puis on **ajoute 1**.

**Exemple** : `−5` sur 8 bits :

```
+5        = 00000101
inversion = 11111010
   +1     = 11111011
→ −5 = 11111011₂
```

**Vérification** : `11111011` + `00000101` = `100000000` → le 9ᵉ bit déborde, résultat 0. ✓

**Plage du complément à deux sur n bits** : de `−2ⁿ⁻¹` à `2ⁿ⁻¹ − 1`.

| Nombre de bits | Plage (signé) |
|----------------|----------------|
| 8 bits | −128 à 127 |
| 16 bits | −32 768 à 32 767 |
| 32 bits | −2 147 483 648 à 2 147 483 647 |

### 3.4 Décoder un nombre signé

Si le bit de signe est 1, le nombre est négatif : on applique le complément à deux pour
trouver sa valeur absolue.

**Exemple** : `10000001₂` (8 bits, signé) :

```
10000001 → inversion : 01111110 → +1 : 01111111 = 127
→ le nombre est −127
```

### 3.5 Représentation par décalement (biais ou offset)

**Principe** : on additionne un **biais** fixe (souvent `2ⁿ⁻¹`, soit la moitié de la plage
possible) à la valeur réelle avant de la stocker en binaire pur. Le nombre stocké est donc
toujours **positif ou nul**, ce qui simplifie certaines comparaisons (on compare directement
les représentations comme des nombres non signés). Cette méthode s'appelle aussi
« représentation biaisée » ou « excess-K » (K étant le biais), et c'est exactement celle
utilisée par l'exposant du format IEEE 754 (voir section 4, biais de 127).

**Formule** (sur n bits, biais `K = 2ⁿ⁻¹`) :

```
valeur stockée (binaire pur) = valeur réelle + K
valeur réelle = valeur stockée (binaire pur) − K
```

**Exemple** : sur 8 bits, biais `K = 2⁷ = 128`. Représenter `−5` :

```
valeur stockée = −5 + 128 = 123
123₁₀ = 01111011₂
→ −5 (par décalement, biais 128) = 01111011₂
```

**Exemple** : représenter `+5` (même biais) :

```
valeur stockée = 5 + 128 = 133
133₁₀ = 10000101₂
→ +5 (par décalement, biais 128) = 10000101₂
```

**Décoder** `01111011₂` (8 bits, biais 128) :

```
01111011₂ = 123₁₀
valeur réelle = 123 − 128 = −5
```

**Plage par décalement sur n bits** (biais `K = 2ⁿ⁻¹`) : de `−2ⁿ⁻¹` à `2ⁿ⁻¹ − 1`, la même
plage que le complément à deux, mais l'ordre des bits croît directement avec la valeur (le
zéro biaisé — le plus petit nombre représentable — correspond au patron tout à zéro
`00000000`, et non à `10000000` comme en complément à deux).

| Nombre de bits | Biais `K = 2ⁿ⁻¹` | Plage (signé) |
|----------------|-------------------|----------------|
| 8 bits | 128 | −128 à 127 |
| 16 bits | 32 768 | −32 768 à 32 767 |
| 32 bits | 2 147 483 648 | −2 147 483 648 à 2 147 483 647 |

## 4. Réels (virgule flottante)

Norme **IEEE 754** : un réel est décomposé en **signe**, **exposant** et **mantisse**.

- `float` (simple précision) : 32 bits → 1 bit de **signe**, 8 bits d'**exposant**, 23 bits de **mantisse**
- `double` (double précision) : 64 bits → 1 bit de signe, 11 bits d'exposant, 52 bits de mantisse

```
 1 bit    8 bits         23 bits
[ S ][ E E E E E E E E ][ M M M M M M M M M M M M M M M M M M M M M M M ]
signe   exposant (biaisé)         mantisse (partie fractionnaire)
```

### 4.1 La mantisse normalisée

Tout réel non nul peut s'écrire sous forme normalisée `1.xxxx × 2ᵉ` (le `1.` initial
est toujours présent pour un nombre normalisé, donc on ne le stocke pas : il est
**implicite**). Seule la partie `xxxx` après la virgule est enregistrée dans les
23 bits de mantisse.

### 4.2 L'exposant biaisé (offset de −127)

Sur 32 bits, l'exposant réel `e` (qui peut être négatif) n'est pas stocké tel quel :
on stocke plutôt un **exposant biaisé** `E = e + 127`. Ce biais de 127 permet de
représenter des exposants négatifs et positifs avec une simple suite de bits non
signée sur 8 bits (plage `E` : 0 à 255, donc `e` utile : −126 à 127).

```
E (biaisé, stocké) = e (réel) + 127
e (réel) = E (biaisé, stocké) − 127
```

### 4.3 Exemple complet : encoder `+6.5` en IEEE 754 (32 bits)

**Étape 1 — Binaire pur**

```
6 = 110₂        0.5 = 1/2 = 0.1₂
→ 6.5₁₀ = 110.1₂
```

**Étape 2 — Normalisation** (forme `1.xxxx × 2ᵉ`, on déplace la virgule après le
premier `1`) :

```
110.1₂ = 1.101₂ × 2²
```

On lit directement : exposant réel `e = 2`, mantisse (sans le `1.` implicite) = `101`.

**Étape 3 — Signe**

```
6.5 est positif → signe S = 0
```

**Étape 4 — Exposant biaisé** (offset **+127**, donc `E = e + 127`) :

```
E = e + 127 = 2 + 127 = 129
129₁₀ = 10000001₂  (sur 8 bits)
```

**Étape 5 — Mantisse sur 23 bits**

On complète `101` par des zéros à droite jusqu'à 23 bits :

```
101 → 10100000000000000000000  (23 bits)
```

**Étape 6 — Assemblage des 32 bits**

```
 S    E (8 bits)   M (23 bits)
 0  10000001  10100000000000000000000

→ +6.5 = 0 10000001 10100000000000000000000₂
```

### 4.4 Décoder un IEEE 754 32 bits

Pour retrouver la valeur décimale à partir des 32 bits, on fait le chemin inverse :

1. **Signe** `S` : 0 = positif, 1 = négatif.
2. **Exposant réel** : `e = E (biaisé) − 127`.
3. **Mantisse** : on remet le `1.` implicite devant les bits stockés → `1.xxxx`.
4. **Valeur** : `(−1)^S × 1.xxxx₂ × 2ᵉ`, qu'on reconvertit ensuite en décimal.

**Exemple** : `0 10000001 10100000000000000000000₂`

```
S = 0 → positif
E = 10000001₂ = 129 → e = 129 − 127 = 2
mantisse = 1.101₂ (1 implicite + 101 stockés)
valeur = 1.101₂ × 2² = 110.1₂ = 6.5₁₀
```

## 5. Caractères

Les caractères sont stockés sous forme de **codes numériques**.

### Table ASCII (extraits)

| Caractère | Code décimal | Code hexa |
|-----------|--------------|-----------|
| espace | 32 | 0x20 |
| `0` | 48 | 0x30 |
| `9` | 57 | 0x39 |
| `A` | 65 | 0x41 |
| `Z` | 90 | 0x5A |
| `a` | 97 | 0x61 |
| `z` | 122 | 0x7A |

**Unicode** étend ASCII pour représenter les caractères de toutes les langues (ex. UTF-8).
