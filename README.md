# Kael — La voie de l'Orc

Ce dépôt contient le lore et l'historique de Kael, depuis sa naissance jusqu'au
point où commencent ses aventures jouées dans la campagne « Alan pas riche ».

📖 **[Lire la dernière version de La voie de l'Orc](https://leroilion.github.io/kael/)**

Le texte cherche à donner à cet historique la forme d'un véritable récit : les
événements qui l'ont construit, ses rencontres, ses apprentissages, ses liens et
les choix qui expliquent le personnage qu'il est devenu.

Les règles d'écriture et de réécriture sont décrites dans [STYLE.md](STYLE.md).
Ce fichier est notamment prévu pour être fourni à une IA avec un chapitre afin
qu'elle puisse l'enrichir sans modifier le canon du personnage ni transformer
le lore en récit de campagne.

## Structure

```text
dnd-kael/
├── .github/
│   └── workflows/
│       └── build-pdf.yml
├── chapter/
│   ├── 0000_preambule.tex
│   ├── 0100_le_village.tex
│   └── ...
├── img/
├── Dockerfile
├── Makefile
├── main.tex
├── config.tex
├── references.tex
├── STYLE.md
└── README.md
```

Le fichier `.chapters.generated.tex` est généré automatiquement lors de la
compilation et ne doit pas être modifié manuellement.

## Ajouter un chapitre

Créer un fichier `.tex` dans `chapter/` avec un préfixe numérique sur quatre
chiffres :

```text
0100_le_village.tex
0200_premiere_epreuve.tex
0250_evenement_intermediaire.tex
0300_la_traque.tex
```

Les numéros servent uniquement à déterminer l'ordre d'import. Ils peuvent être
espacés pour permettre l'insertion ultérieure d'un chapitre.

Chaque fichier contient son propre titre :

```latex
\chapter{Le village}

Texte du chapitre...
```

La numérotation affichée est gérée automatiquement par LaTeX.

## Illustrations

Les images sont placées dans `img/` et intégrées avec :

```latex
\illustration[0.75\textwidth]
  {image.png}
  {Légende de l'image.}
  {identifiant-unique}
```

Le premier paramètre est facultatif. Par défaut, l'image occupe
`0.85\textwidth`.

## Séparation de scènes

Pour marquer une vraie rupture narrative à l'intérieur d'un chapitre :

```latex
\scenebreak
```

## Références littéraires

`references.tex` contient l'annexe expliquant les clins d'œil et inspirations
littéraires utilisés dans le lore.

La commande `\referencebreak` sépare visuellement la référence originale de son
adaptation dans l'histoire de Kael.

## Compilation locale

Compiler avec :

```bash
make
```

Le PDF produit est :

```text
kael.pdf
```

Le Makefile génère `.chapters.generated.tex`, puis effectue deux passes LaTeX
pour mettre à jour le sommaire et les références.

Pour afficher l'ordre des chapitres :

```bash
make show-chapters
```

Pour nettoyer :

```bash
make clean
```

## Compilation avec Docker

Construire l'image une fois :

```bash
docker build -f Dockerfile . --tag latex_builder
```

Puis, depuis le dossier du dépôt :

```bash
# Windows PowerShell
docker run --rm --volume ${PWD}:/data latex_builder

# Windows cmd
docker run --rm --volume %cd%:/data latex_builder

# Linux
docker run --rm --volume $(pwd):/data latex_builder
```

## Compilation et publication automatiques

Une GitHub Action compile automatiquement le livre à chaque push sur `main`.

La pipeline :

1. installe TeX Live ;
2. compile `kael.pdf` ;
3. prépare un site GitHub Pages ;
4. publie la nouvelle version du PDF.

Le lien vers le PDF contient le SHA du commit courant afin d'éviter qu'un
navigateur ne conserve une ancienne version en cache.

Le job de déploiement utilise l'environnement GitHub `github-pages`, comme le
dépôt « Alan pas riche ».

## Frontière avec « Alan pas riche »

Ce dépôt raconte **comment Kael est devenu Kael**.

Il retrace son histoire personnelle, ses origines, ses rencontres, ses
apprentissages et les événements qui l'ont façonné jusqu'au début de ses
aventures en tant que personnage joueur.

À partir du moment où commencent les événements réellement joués avec les autres
personnages, leur narration appartient au projet de campagne
**[Alan pas riche](https://github.com/leroilion/alan-pas-riche)**.

➡️ **L'histoire continue dans « Alan pas riche ».**