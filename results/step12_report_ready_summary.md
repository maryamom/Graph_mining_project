# Résumé du projet

## Dataset
10 000 CV, 2 500 Jobs et 75 000 couples positifs synthétiques, sans valeurs manquantes ni références invalides.

## Modélisation du graphe
Graphe biparti simple de 12 500 nœuds et 75 000 arêtes observées, densité bipartite 0.0030.

## Analyse structurelle
Degré moyen CV 7.50, Job 30.00; 36 composantes et 29 CV isolés.

## Communautés
37 communautés globales (Q=0.8725) et 8 communautés de skills (Q pondérée=0.7184). ARI original/enrichi=0.9996.

## Prédiction de liens
Meilleure méthode : Katz tronqué L=5, ROC-AUC test 0.9445, AP 0.9033, F1 0.9440 sur benchmark équilibré.

## Enrichissement
Consensus Top-50 : 5347 suggestions ajoutées, soit 80347 arêtes. Precision ranking test=0.00358; ce ne sont pas de nouveaux labels vrais.

## Classification
- CV seniority: Logistic Regression / SEMANTIC, macro-F1 test=0.8769.
- CV specialization proxy: Logistic Regression / STRUCTURAL, macro-F1 test=0.9393.
- Job seniority: Random Forest / STRUCTURAL, macro-F1 test=0.2989.
- Job industry: Logistic Regression / SEMANTIC, macro-F1 test=1.0000.
- Job specialization proxy: Logistic Regression / STRUCTURAL, macro-F1 test=0.8982.

## Impact de l'enrichissement
Effets faibles ou ambigus selon la tâche ; le graphe original reste la référence à cause du risque indirect de fuite.

## Profils spécialisés / polyvalents
6841 CV specialized proxy et 3159 generalist proxy ; moyenne 1.515 communautés de skills.

## Limites
Dataset synthétique, benchmark équilibré optimiste, pseudo-labels, Katz tronqué, modularité standard bipartite, liens prédits sans vérité terrain future et généralisation réelle non démontrée.

## Conclusion
La structure et le texte sont complémentaires, mais le ranking réaliste et les contrôles de fuite imposent une interprétation prudente et une validation future sur données réelles temporelles.
