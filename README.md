#  Graph Mining CV–Job

Projet académique de Graph Mining modélisant le recrutement par un graphe biparti entre CV et offres d’emploi.

**Auteurs :** Mariem Omrani et Anas Cherni .

## Objectifs

- construire et analyser le graphe biparti CV–Job ;
- détecter des communautés globales et des communautés de compétences ;
- comparer la prédiction de liens sémantique aux méthodes structurelles adaptées ;
- construire un scénario d’enrichissement prudent ;
- créer des représentations de nœuds et classifier CV et Jobs.

## Dataset et résultats clés

Dataset Hugging Face : `michaelozon/candidate-matching-synthetic`.

- 10 000 CV, 2 500 Jobs et 75 000 couples positifs ;
- graphe original : 12 500 nœuds, 75 000 arêtes, densité bipartite `0.003` ;
- 37 communautés globales, modularité `0.8725` ;
- 73 compétences, 8 communautés, modularité pondérée `0.7184` ;
- meilleure link prediction : Katz tronqué L=5, ROC-AUC test `0.9445` ;
- ranking Katz à K=50 : Precision@50 `0.00325`, Recall@50 `0.04992` ;
- scénario enrichi : 5 347 liens candidats, 80 347 arêtes.

| Classification | Configuration retenue | Macro-F1 test |
|---|---|---:|
| CV seniority | Régression logistique + embeddings safe | 0.8769 |
| CV specialization proxy | Régression logistique + structure originale | 0.9393 |
| Job seniority | Random Forest + structure originale | 0.2989 |
| Job industry | Régression logistique + embeddings safe | 1.0000 |
| Job specialization proxy | Régression logistique + structure originale | 0.8982 |

`specialized/generalist` est un pseudo-label dérivé des communautés de compétences, pas une annotation humaine.

## Organisation

```text
notebooks/          notebooks 01 à 12
data/processed/     graphes et embeddings
results/            métriques CSV/JSON
figures/            figures des analyses
requirements.txt    dépendances Python
```

Les notebooks doivent être exécutés dans l’ordre numérique. Ils couvrent l’audit, la construction du graphe, l’analyse structurelle, les communautés, la prédiction de liens, l’enrichissement, les features, la classification et la synthèse.

## Installation

```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
pip install -r requirements.txt
jupyter notebook
```

Le premier téléchargement du dataset et du modèle `sentence-transformers/all-MiniLM-L6-v2` nécessite Internet.

## Reproductibilité et anti-fuite

- seed principale `42` ;
- split de link prediction 60 000 / 7 500 / 7 500 positifs ;
- négatifs absents des 75 000 positifs complets ;
- topologie d’évaluation calculée uniquement depuis `G_train` ;
- embeddings de classification sans champs cibles directs ;
- preprocessing ajusté uniquement sur le train ;
- test jamais utilisé pour sélectionner un modèle ou hyperparamètre.

## Rapport

- PDF : `report/rapport_graph_mining.pdf`

