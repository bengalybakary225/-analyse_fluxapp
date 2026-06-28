# Rapport de synthèse — Projet FluxApp

**Auteur :** Bengaly Bakary  
**Programme :** Master Data & Intelligence Artificielle — HETIC

---

## 1. Ce que j'ai découvert sur les données

J'ai travaillé sur une base de 1 500 clients FluxApp. Avant de commencer l'analyse, j'ai dû traiter quelques valeurs manquantes sur l'âge et la dépense mensuelle.

Ce qui m'a le plus frappé c'est le taux de churn global qui est de 38.7%. Ça veut dire que presque 2 clients sur 5 ont résilié leur abonnement, ce qui est vraiment élevé pour une application SaaS.

En creusant un peu plus, j'ai remarqué que les clients du plan Basic sont les plus à risque avec un taux de churn de 46.3%. À l'opposé, les clients Business churnen beaucoup moins (20.6%), probablement parce qu'ils sont plus investis dans le produit.

Du côté des canaux d'acquisition, les clients venus via les publicités payantes (Ads) partent le plus souvent (43.2%). Ce qui est intéressant c'est que les clients moins actifs sur l'application ont aussi tendance à partir davantage — en moyenne les clients churnés font 12 sessions sur 30 jours contre 13.6 pour les actifs. Enfin, plus un client reste longtemps, moins il risque de partir — les clients de plus de 25 mois churnen à seulement 30.3%.

---

## 2. Ma recommandation pour optimiser le budget marketing

Le revenu mensuel récurrent de FluxApp généré par les clients actifs est de 25 703 EUR.

En calculant le coût d'acquisition (CAC) et la valeur à vie (LTV) de chaque canal, j'ai pu voir clairement quels canaux sont vraiment rentables.

Le canal Organic est gratuit et génère une LTV de 56.81 EUR — c'est clairement le meilleur. Le canal Referral coûte 12.54 EUR par client acquis pour une LTV de 61.71 EUR, ce qui donne un ratio LTV/CAC de 4.92 — au dessus du seuil recommandé de 3, donc rentable.

En revanche le canal Ads est problématique : il coûte 42.25 EUR par client pour une LTV de seulement 51.06 EUR, soit un ratio de 1.21 — très en dessous du seuil. C'est le canal le plus cher et le moins rentable.

Ma recommandation est de réduire le budget Ads d'au moins 30% et de réinvestir cet argent sur le Referral, qui attire des clients plus fidèles à moindre coût.

Concernant le test A/B sur le nouveau parcours d'onboarding, la variante B montre un uplift de +10.94% par rapport à la variante A. Cependant la p-value est de 0.0721, ce qui est au dessus du seuil de 5%. Cela veut dire que ce résultat pourrait être dû au hasard. Je recommande donc de ne pas déployer la variante B pour l'instant et de prolonger le test avec plus d'utilisateurs.

---

## 3. Comment intégrer le modèle dans FluxApp

J'ai entraîné deux modèles pour prédire le churn : une Régression Logistique et une Forêt Aléatoire. Après comparaison, j'ai choisi la Régression Logistique car elle obtient le meilleur AUC-ROC (0.6953).

Pour intégrer ce modèle dans le produit, je propose un système de batch nocturne : chaque nuit, le modèle calcule un score de risque pour chaque client actif. Selon ce score, différentes actions peuvent être déclenchées automatiquement — une offre commerciale pour les clients très à risque, une notification in-app pour ceux qui le sont modérément, et aucune action pour les clients stables.

Cependant ce modèle a des limites qu'il faut prendre en compte. Premièrement, il peut être biaisé si certains groupes de clients sont mal représentés dans les données. Deuxièmement, cibler des clients stables avec des offres peut les inciter à demander des réductions inutilement. Troisièmement, le comportement des clients évolue avec le temps, donc le modèle devra être ré-entraîné régulièrement. Enfin, l'utilisation des données comportementales doit respecter le RGPD.

---

_Notebook complet : `analyse_fluxapp.ipynb`_
