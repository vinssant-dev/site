---
title: Introduction et présentation de la science des données
sidebar_label: 1 - Intro
sidebar_position: 1
---

## Introduction à la science des données

La science des données (Data science) est un nouveau domaine qui étudie de grands volumes de données utilisant des techniques modernes d'informatique, statistiques et d'intelligence artificielle. Le domaine de la science de la donnée inclut plusieurs secteurs qui permettent de couvrir le cycle de vie d'une problématique.

### Cycle de vie de science des données

* Détermination des requis : Étudiez avec le client les problématiques à résoudre.
* Minage (Data Mining) : Regroupez les sources de données pertinentes pour le projet.
* Filtrage (Data Cleaning) : Inspectez et travaillez sur les données pour ne pas avoir de données incongrues, manquantes ou extrêmes.
* Exploration (Data Exploration) : L'analyse des données avec des statistiques, apprentissage machine, etc.
* Visualisation : La présentation des données sous forme palpable (graphiques, rapport) pour prise de décision et réponse à la problématique.

Le but de ce cours est d'explorer les différentes étapes du cycle. Nous utiliserons un langage de programmation (Python) pour mettre en application les étapes précédentes. Nous regarderons donc :

* L'ingestion et le traitement de données
* La mise en place de base de données pour stocker les données de manières structurées.
* L'analyse de données avec des programmes d'analyse
* La visualisation des données ou des résultats d'analyse à l'aide de tableau de bord
* [Liste d'exemple de visualisation](https://dash.gallery/Portal/)

### Rôles dans la science des données

Il existe une panoplie de rôles entourant la science des données. Certain sont générale et d'autre très spécifique.

* Scientifique de la donnée (Data Scientist) : Nom original pour ceux qui travaillent en science des données. Leurs tâches sont maintenant spécialisées sous d'autres noms (Data Engineer, Data Analyst, Data Architect). Le Data scientist moderne identifie les sources données, les analyse et collabore à la visualisation des résultats.

* Administrateur de base de données (DBA: Database Administrator) : Les bases de données sont le premier outil pour la collecte et sauvegarde de données structurées. Le DBA construit, entretient et opère les bases de données qui seront utilisées en science des données.

* Ingénieur d'apprentissage machine (Machine Learning Engineer) : Travail avec les data scientist sur l'analyse des données en créant des modèles d'apprentissage qui permettront de voir des tendances ou de faire des prédictions sur les données ou les problématiques.

## Bases de données
Toute organisation/compagnie/application veut sauvegarder des données qui seront stockées de manière semi-permanente pour consultation future. Différents systèmes de données existent comme des fichiers textes et classeur Excel.

Pour des systèmes de données plus complexes, des bases de données sont utilisées pour sauvegarder les données. Les bases de données ont des systèmes de gestion qui permettent d'éviter les problèmes typiques suivants :

* La duplication de données dans différents endroits.
* Le conflit entre des données contradictoires.
* La mise à jour de données sur tout le système.

Les bases de données sont des systèmes centraux qui peuvent être consultés et mis à jour par plusieurs personnes en même temps.

### Famille des bases de données (SQL/NoSQL)

Il existe plusieurs types de base de données qui ont tous leurs avantages et leurs désavantages.

### Base de données relationnelle (SQL)

Les bases de données relationnelles sont basées sur le concept de tables. Une table contient des colonnes avec différentes informations et chaque ligne représente un enregistrement des différentes colonnes de la table. Le principe de relation vient aussi avec la possibilité de relier des informations d'une table à une autre pour éviter la duplication et faciliter la segmentation des informations.

Pour interfacé avec les bases de données relationnelles, un langage de sélection est utilisé, le SQL ( Structured Query Language).

Les bases de données relationnelles viennent habituellement dans des logiciels complexes qui sont des systèmes de gestion de base de données relationnels (RDBMS).

Dans la gestion de données, les bases de données relationnelles sont utilisées la majorité du temps.

### Autres types de base de données

Il existe d'autres types de bases de données que nous étudierons dans la deuxième moitié du cours.

* Document
* Clé-valeur
* Graphe
* Colonne-famille

Nous regarderons rendu à ceux-ci les lacunes des bases de données SQL et les avantages de chaque type.

## Présentation des données et leurs types

Les données doivent être sauvegardées pour les conserver. En informatique, le format fondamental est le binaire et les autres types de données l'utilisent pour représenter leurs valeurs. Il est important de comprendre ce principe pour être informé de la place que prennent les différents types de données.

### Types de données numériques

#### Binaire/booléen

Le type fondamental des données en informatique est le binaire ayant deux valeurs possibles : le 0 ou le 1. Il est donc facilement possible de sauvegarder ce genre de donné.

Dans d'autre contexte, la valeur binaire est aussi souvent utilisée pour représenter une valeur booléenne logique. Les deux valeurs possibles dans ce cas sont `Vrai`(`True`) ou `Faux`(`False`).

#### Nombres entiers

Les nombres entiers sont conservés en mémoire à partir de valeur binaire. Pour ce faire une conversion sera faite. Pour faciliter la gestion de la mémoire en binaire, une représentation en hexadécimal est souvent utilisé pour une représentation sur une base 16 (comparativement à une base 10 en décimal).

| Décimal | Binaire | Hexadécimal |
| -- | -- | -- |
| 0 | 0 | 0 |
| 1 | 1 | 1 |
| 2 | 10 | 2 |
| 3 | 11 | 3 |
| 4 | 100 | 4 |
| 5 | 101 | 5 |
| 6 | 110 | 6 |
| 7 | 111 | 7 |
| 8 | 1000 | 8 |
| 9 | 1001 | 9 |
| 10 | 1010 | A |
| 11 | 1011 | B |
| 12 | 1100 | C |
| 13 | 1101 | D |
| 14 | 1110 | E |
| 15 | 1111 | F |
| 16 | 10000 | 10 |

Il est aussi possible de faire la représentation de nombre entier négatif avec des stratégies de représentation en mémoire comme le [Complément de deux](https://en.wikipedia.org/wiki/Two%27s_complement).

#### Nombre fractionnaire/réel/point flottant

Il est beaucoup plus difficile de sauvegarder des nombres ayant des parties fractionnaires en informatiques. Des techniques spécialisées ont été développées pour représenter les nombres sous formes scientifiques (`1.237x10^12`) et que le signe, l'exposant et la partie significative soient sauvegardés sous forme binaire. Vous pouvez regarder une [visualisation ici](https://bartaz.github.io/ieee754-visualization/).

Il faut faire particulièrement attention aux nombres fractionnaires/réels, car ceux-ci vont souffrir d'un [manque possible de précision](https://en.wikipedia.org/wiki/Floating-point_arithmetic).

### Type de données textuelles

La représentation de texte se fait avec une base binaire, comme toute autre donnée en informatique. Il faut donc convertir la donnée textuelle sous forme numérique. Pour ce faire, une table de traduction doit être invoquée pour représenter ce que chaque "nombre" représente comme caractère. La table reconnue est la [table ASCII](https://en.wikipedia.org/wiki/ASCII) pour les caractères simples et nous avons aussi la [norme Unicode](https://en.wikipedia.org/wiki/Unicode) qui permet de représenter toute forme de texte humain (incluant les émojis).

#### String / chaine de caractères

La majorité des informations textuelles est habituellement, une suite de caractères et les types de données sont créés en conséquence. La majorité des systèmes ont des représentations pour les chaines de caractères (`String`) pour sauvegarder une phrase de texte.

### Type de données structurées (data structures)

Nous devons souvent regrouper des données ensemble pour mieux attaquer une problématique, les données structurées sont les types qui nous permettent de regrouper plusieurs éléments (parfois de différents types) ensemble.

#### Liste (`list`, `array`, `sequence`)
Les listes sont de regroupements de valeurs (habituellement de même type) qui sont regroupés en dans un ordre numérique. On peut retrouver les informations avec la position de l'élément dans la liste.

#### Enregistrement (`record`, `tuple`, `struct`)
L'enregistrement est un regroupement de différents éléments, pas nécessairement du même type. C'est la structure la plus simple et elle est beaucoup utilisée dans les bases de données (une ligne d'information est un enregistrement).
