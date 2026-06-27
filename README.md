# Projet Deep Learning — EMSI (MLP / CNN / RNN-Classification de sentiment)

Projet individuel de fin de module Deep Learning (cycle MSI, EMSI Casablanca, 2025–2026). Implémentation et comparaison de trois familles d'architectures de réseaux de neurones — MLP, CNN, RNN/LSTM/GRU — sur trois types de données réelles (tabulaire, image, texte).

**Travail individuel.** Conformément au cahier des charges, ce projet a été réalisé seul ; aucune partie n'a été produite en binôme ou en groupe.

## Structure du dépôt

```
deep_learning_project/
├── README.md
├── requirements.txt
├── notebooks/
│   ├── part1_mlp.ipynb     # Partie I   – MLP sur winequality-red.csv
│   ├── part2_cnn.ipynb     # Partie II  – CNN sur Fashion-MNIST
│   └── part3_rnn.ipynb     # Partie III – RNN/LSTM/GRU pour l'analyse de sentiment sur IMDB-Dataset.csv
├── data/
│   ├── winequality-red.csv # Données tabulaires (Partie I)
│   └── IMDB-Dataset.csv    # 50 000 critiques de films réelles, positives/négatives (Partie III)
├── saved_models/
│   ├── part1_mlp_best.pth
│   ├── part2_cnn_best.pth
│   └── part3_rnn_sentiment_best.pth   # généré à l'exécution du notebook part3 (voir ci-dessous)
├── utils/
│   └── utils.py
└── rapport/
    ├── Rapport_DeepLearning_EMSI.md        # Rapport scientifique de résultats (à lire en premier)
    └── Sujet_Projet_DeepLearning_EMSI.md   # Énoncé / cahier des charges original
```

## Installation

```bash
python -m venv .venv
# Windows : .venv\Scripts\activate
# macOS/Linux : source .venv/bin/activate
pip install -r requirements.txt
```

## Exécution

Les trois notebooks sont indépendants mais doivent être exécutés **dans l'ordre** (Partie I, puis II, puis III) en partant d'un noyau Jupyter dont le répertoire de travail est `notebooks/` (les chemins relatifs `../data/...` et `../saved_models/...` en dépendent) :

```bash
jupyter notebook notebooks/part1_mlp.ipynb
jupyter notebook notebooks/part2_cnn.ipynb
jupyter notebook notebooks/part3_rnn.ipynb
```

Lancer chaque notebook avec « Exécuter tout » (Run All). Le jeu de données Fashion-MNIST utilisé en Partie II n'est pas inclus dans `data/` ; il est téléchargé automatiquement par `torchvision` (`download=True`) à la première exécution du notebook `part2_cnn.ipynb`, dans un sous-dossier créé localement.

### Note sur la Partie III (RNN)

La Partie III a été refaite intégralement sur un **vrai jeu de données** : *IMDB Dataset of 50K Movie Reviews* (`data/IMDB-Dataset.csv`), 50 000 critiques de films réelles et équilibrées (25 000 positives, 25 000 négatives). La tâche est désormais une **classification binaire de sentiment** (et non plus une traduction automatique sur un corpus inventé de 40 phrases). Pour garder un temps d'entraînement raisonnable sur CPU, le notebook tire un sous-échantillon équilibré de 8 000 critiques parmi les 50 000 disponibles (ce choix est documenté en détail dans le notebook et dans le rapport) ; l'ensemble du fichier `IMDB-Dataset.csv` reste disponible si l'on souhaite entraîner sur un échantillon plus grand. Le notebook `part3_rnn.ipynb` a été **exécuté intégralement** avant la livraison de cette version : tous les tableaux, courbes et le fichier `saved_models/part3_rnn_sentiment_best.pth` sont déjà générés et visibles dans le notebook fourni.

### Note sur les Parties I et II

Les notebooks `part1_mlp.ipynb` et `part2_cnn.ipynb` contiennent des cellules d'analyse complémentaires (comparaison des stratégies d'initialisation, étude architecturale du CNN, comparaisons détaillées) qui nécessitent un environnement local avec PyTorch et torchvision pour être exécutées si elles ne l'ont pas encore été ; voir le rapport pour le détail de ce qui est déjà exécuté.

## Modèles sauvegardés

- `part1_mlp_best.pth` et `part2_cnn_best.pth` sont déjà présents (issus de l'exécution initiale du projet).
- `part3_rnn_sentiment_best.pth` est généré automatiquement par la dernière cellule de sauvegarde du notebook `part3_rnn.ipynb` (sélection du modèle — RNN, LSTM ou GRU — ayant le meilleur F1 sur l'ensemble de test).

## Rapport

Le document `rapport/Rapport_DeepLearning_EMSI.md` constitue le rapport scientifique du projet (introduction, méthodologie, résultats, interprétation, limites, conclusion, discussion transversale). Le document `rapport/Sujet_Projet_DeepLearning_EMSI.md` est l'énoncé original du projet, conservé à titre de référence.
