# Request-IA-Services

![Python version](https://img.shields.io/badge/python-3.13+-blue)
![Status](https://img.shields.io/badge/status-beta-yellow)

## Présentation

Request‑IA‑Services est un projet réalisé dans le cadre de la formation **Ingénieur·e en Intelligence Artificielle** d’OpenClassrooms.
Le notebook Jupyter associé montre comment :

1. Télécharger un modèle de segmentation sémantique des vêtements hébergé sur **Hugging Face Hub** ;
2. Pré‑traiter une image et l’envoyer au modèle ;
3. Reconstituer le masque de segmentation et générer une visualisation finale où chaque pièce du vêtement est colorée différemment.

Le dépôt fournit le code, la configuration *Poetry* et les dépendances nécessaires pour reproduire l’expérience sur votre propre machine.

## Table des matières

* [Pré‑requis](#pré‑requis)
* [Installation](#installation)
* [Variables d’environnement](#variables-denvironnement)
* [Exécution rapide](#exécution-rapide)
* [Structure du projet](#structure-du-projet)
* [Personnaliser le modèle](#personnaliser-le-modèle)

## Pré‑requis

* **Python ≥ 3.13**
* **Poetry ≥ 2.0**
* Un compte gratuit sur Hugging Face Hub si vous souhaitez utiliser des modèles privés.

Toutes les dépendances Python spécifiques sont déclarées dans `pyproject.toml` et seront installées automatiquement par Poetry.

## Installation

```bash
# 1. Clonez le dépôt
git clone https://github.com/Davidouu/request-ia-services.git
cd request-ia-services

# 2. Installez les dépendances dans un environnement virtuel isolé
poetry install

# 3. Activez l'environnement
poetry shell
```

## Variables d’environnement

Le notebook lit certaines variables à partir d’un fichier `.env` (chargé avec **python‑dotenv**):

| Clé             | Description                                                   | Valeur par défaut                  |
| --------------- | ------------------------------------------------------------- | ---------------------------------- |
| `HF_MODEL_NAME` | Identifiant du modèle sur le Hub Hugging Face                 | `facebook/detr-resnet-50-panoptic` |
| `HF_API_TOKEN`  | Jeton d’accès personnel (facultatif pour les modèles publics) | —                                  |

Créez un fichier `.env` à la racine du projet si vous souhaitez surcharger la configuration :

```ini
HF_MODEL_NAME=mynamespace/my-custom-fashion-seg
HF_API_TOKEN=hf_XXXXXXXXXXXXXXXXXXXXXXXX
```

## Exécution rapide

Lancez JupyterLab puis ouvrez le notebook :

```bash
poetry run jupyter lab
```

1. Chargez vos imagse haute résolution (JPEG/PNG).
2. Exécutez toutes les cellules ; les masques segmentés sont enregistrés dans `outputs/` et affichés en fin d’exécution.

> **Astuce** : Vous pouvez tester rapidement avec les images fournies dans le dossier `test-data/IMG`.

## Structure du projet

```
.
├── test-data/
│   └── IMG/                # Images d'exemple
├── request-service.ipynb   # Note book pricipale
├── .env.example            # Variables d'environnement d'exemple
├── .gitignore
├── pyproject.toml
└── README.md               # VOUS ÊTES ICI ⭐
```

## Personnaliser le modèle

Le notebook est volontairement générique : changez simplement la variable `HF_MODEL_NAME` pour essayer d’autres modèles de segmentation (Mask R‑CNN, DETR, SAM, etc.).
Si la sortie de votre modèle diffère (ex. type de tenseur, couleur des classes), modifiez la cellule **Post‑traitement du masque** en conséquence.
