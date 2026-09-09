# Laboratoire 2 — Solutions

### Exercice 1 — `42₁₀` en binaire (8 bits)

```
42 ÷ 2 = 21 r 0
21 ÷ 2 = 10 r 1
10 ÷ 2 =  5 r 0
 5 ÷ 2 =  2 r 1
 2 ÷ 2 =  1 r 0
 1 ÷ 2 =  0 r 1
```

Restes de bas en haut : `101010` → sur 8 bits : **`00101010₂`**

### Exercice 2 — `200₁₀` en binaire (8 bits)

```
200 = 128 + 64 + 8
    = 11001000₂
```

**Réponse : `11001000₂`**

### Exercice 3 — Plus grand non signé

- 8 bits : `11111111₂` = **255**
- 16 bits : `1111111111111111₂` = **65 535**

Formule générale : `2ⁿ − 1`.

### Exercice 4 — `−12` en complément à deux (8 bits)

```
12          = 00001100
inversion   = 11110011
      + 1   = 11110100
```

**Réponse : `11110100₂`**

### Exercice 5 — `−1` en complément à deux (8 bits)

```
1           = 00000001
inversion   = 11111110
      + 1   = 11111111
```

**Réponse : `11111111₂`**

### Exercice 6 — Décoder `11110000₂` (signé)

Le bit de signe est 1 → nombre négatif. On applique le complément à deux :

```
11110000 → inversion : 00001111 → +1 : 00010000 = 16
```

**Réponse : `−16`**

### Exercice 7 — Décoder `10000000₂` (signé)

Bit de signe 1 → négatif :

```
10000000 → inversion : 01111111 → +1 : 10000000 = 128
```

**Réponse : `−128`**

### Exercice 8 — Plage des entiers signés

- 8 bits : **−128 à 127**
- 16 bits : **−32 768 à 32 767**

Formule : `−2ⁿ⁻¹` à `2ⁿ⁻¹ − 1`.

### Exercice 9 — Codes ASCII

| Caractère | Décimal | Hexadécimal |
|-----------|---------|-------------|
| `'A'` | 65 | 0x41 |
| `'Z'` | 90 | 0x5A |
| `'a'` | 97 | 0x61 |
| `'z'` | 122 | 0x7A |
| `'0'` | 48 | 0x30 |
| `'9'` | 57 | 0x39 |

### Exercice 10 — Décoder `72 105 33`

```
72 = 'H', 105 = 'i', 33 = '!'
```

**Réponse : `Hi!`**

### Exercice 11 — `255 + 1` sur 8 bits non signés

```
11111111 + 00000001 = 100000000  (9 bits)
```

Le 9ᵉ bit ne tient pas sur 8 bits → **dépassement de capacité (overflow)**.
Résultat sur 8 bits : `00000000`, soit `0`.

### Exercice 12 — Complément à deux de `01101010₂`

```
01101010 → inversion : 10010101 → +1 : 10010110
```

**Réponse : `10010110₂`**

### Exercice 13 — Encoder `+10.25` en IEEE 754 (32 bits)

```
10 = 1010₂        0.25 = 1/4 = 0.01₂
→ 10.25₁₀ = 1010.01₂

Normalisation : 1010.01₂ = 1.01001₂ × 2³
→ e = 3, mantisse = 01001

Signe : positif → S = 0

Exposant biaisé (offset +127) : E = e + 127 = 3 + 127 = 130 = 10000010₂

Mantisse sur 23 bits : 01001000000000000000000
```

**Réponse : `0 10000010 01001000000000000000000₂`**

### Exercice 14 — Encoder `−3.75` en IEEE 754 (32 bits)

```
3 = 11₂        0.75 = 1/2 + 1/4 = 0.11₂
→ 3.75₁₀ = 11.11₂

Normalisation : 11.11₂ = 1.111₂ × 2¹
→ e = 1, mantisse = 111

Signe : négatif → S = 1

Exposant biaisé (offset +127) : E = e + 127 = 1 + 127 = 128 = 10000000₂

Mantisse sur 23 bits : 11100000000000000000000
```

**Réponse : `1 10000000 11100000000000000000000₂`**

### Exercice 15 — Décoder `0 10000010 01100000000000000000000₂`

```
S = 0 → positif
E = 10000010₂ = 130 → e = E − 127 = 130 − 127 = 3
mantisse = 1.011₂ (1 implicite + 011 stockés)
valeur = 1.011₂ × 2³ = 1011.0₂ = 11₁₀
```

**Réponse : `+11`**

### Exercice 16 — Exposant biaisé pour `e = 0`

```
E = e + 127 = 0 + 127 = 127 = 01111111₂
```

**Réponse : `E = 127 = 01111111₂`** — c'est cette valeur (127) qui sert de référence
(« zéro » de l'exposant) grâce à l'offset de −127 utilisé pour décoder : `e = E − 127`.
