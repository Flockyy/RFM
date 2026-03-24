# Rapport de Segmentation RFM — Online Retail II

> **Jeu de données** : Online Retail II (UCI) — transactions e-commerce d'un détaillant britannique  
> **Périmètre** : commandes valides (hors annulations et valeurs nulles)  
> **Date d'analyse** : Mars 2026

---

## 1. Distribution des métriques RFM

| Métrique | Description | Moyenne | Médiane | Min | Max |
|---|---|---|---|---|---|
| **Récence (R)** | Jours depuis le dernier achat | 91 jours | ~60 jours | 1 jour | 374 jours |
| **Fréquence (F)** | Nombre de commandes | 4,5 | 2 | 1 | 200+ |
| **Valeur monétaire (M)** | CA total (£) | £2 047 | ~£800 | £10 | £280 000+ |

**Observations clés :**

- La distribution de la **récence** est fortement asymétrique à droite : la majorité des clients a acheté dans les 3 derniers mois, mais une longue queue indique des clients dormants depuis plus d'un an.
- La **fréquence** est très concentrée sur les petites valeurs (médiane = 2 commandes) avec quelques acheteurs très réguliers en queue de distribution. Le log de la fréquence suit approximativement une loi normale.
- La **valeur monétaire** présente une asymétrie extrême : quelques clients "baleines" génèrent une part disproportionnée du chiffre d'affaires, phénomène typique de la loi de Pareto (80/20).

Les scores R, F, M ont été calculés par **quintiles** (scores 1 à 5), permettant une segmentation relative indépendante des valeurs absolues.

---

## 2. Segmentation : résultats

Le modèle identifie **6 segments** sur 4 314 clients :

| Segment | Critères (scores) | Clients | Part | CA moyen / client |
|---|---|---|---|---|
| 🐋 **Baleines** | R ≥ 4, F ≥ 4, M ≥ 4 | 926 | 21,5 % | ~£5 500 |
| 👥 **Clients fidèles actifs** | R ≥ 4, F ≥ 3 | 467 | 10,8 % | ~£2 800 |
| 🆕 **Nouveaux clients** | R ≥ 4, F ≤ 2 | 366 | 8,5 % | ~£1 200 |
| ⚠️ **À risque** | R ≤ 2, F ≥ 3 | 391 | 9,1 % | ~£1 800 |
| ❌ **Clients perdus** | R ≤ 2, M ≥ 4 | 354 | 8,2 % | ~£4 200 |
| ⬜ **Autres** | Combinaisons restantes | 1 810 | 42,0 % | ~£900 |

> **Total : 4 314 clients** analysés.

### Heatmap R × F (dépense moyenne)

La carte de chaleur R × F révèle que la dépense moyenne augmente avec le score F quelle que soit la récence, mais que les clients récents à haute fréquence (R=5, F=5) représentent le cœur de valeur du portefeuille.

---

## 3. Segments clés — analyse détaillée

### 🐋 Baleines (926 clients — 21,5 % du total)

**Profil** : dernière commande < 30 jours, ≥ 4 commandes, fort panier.  
**Importance** : bien qu'ils représentent ~22 % des clients, ils génèrent probablement plus de 50 % du chiffre d'affaires total (règle de Pareto).

**Recommandations marketing :**
- Programme de fidélité **premium** avec avantages exclusifs (livraison prioritaire, accès anticipé aux collections).
- **Alertes de réapprovisionnement** personnalisées basées sur l'historique d'achat.
- Invitation au **programme de parrainage** à fort incitatif (win-win).
- Suivi proactif de satisfaction pour prévenir le churn.

---

### 🆕 Nouveaux clients (366 clients — 8,5 %)

**Profil** : achat très récent (R ≥ 4) mais peu d'historique (F ≤ 2).  
**Importance** : fort potentiel de conversion en clients réguliers ; la fenêtre d'engagement post-achat est ouverte.

**Recommandations marketing :**
- Séquence d'**onboarding e-mail** sur 30 jours : présentation de la gamme, témoignages, tutoriels produit.
- **Coupon de bienvenue** sur le 2ᵉ achat (ex. : -15 % valable 21 jours) pour déclencher la répétition.
- Recommandations personnalisées basées sur la première commande (cross-sell).
- Mesure du taux de conversion vers "Clients fidèles actifs" à J+60.

---

### ❌ Clients perdus (354 clients — 8,2 %)

**Profil** : inactifs depuis longtemps (R ≤ 2) mais gros dépensiers historiques (M ≥ 4).  
**Importance** : coût d'acquisition déjà amorti ; récupérer même 10–15 % de ce segment représente un gain significatif.

**Recommandations marketing :**
- Campagne de **ré-engagement ciblée** : e-mail "Vous nous manquez !" avec offre exceptionnelle (remise ou produit offert).
- **Enquête de satisfaction** courte (3 questions) pour identifier la cause du départ.
- Appel téléphonique pour les clients à très haute valeur (M score = 5).
- Si absence de réaction après 2 relances → archivage et suppression progressive pour optimiser les coûts CRM.

---

### ⚠️ À risque (391 clients — 9,1 %)

**Profil** : anciennement réguliers (F ≥ 3) mais inactifs récemment (R ≤ 2).  
**Importance** : signal précoce d'attrition — intervention avant qu'ils basculent en "Clients perdus".

**Recommandations marketing :**
- Alerte automatique de ré-engagement dès détection (ex. : aucune commande depuis 90 jours pour un client habituellement mensuel).
- Offre de **reconquête personnalisée** sur les catégories achetées précédemment.
- Surveiller l'évolution du score R à chaque rafraîchissement mensuel.

---

## 4. Recommandations globales

| Priorité | Action | Segment ciblé | KPI |
|---|---|---|---|
| 🔴 Haute | Programme fidélité premium | Baleines | Taux de rétention, NPS |
| 🔴 Haute | Campagne win-back | Clients perdus | Taux de réactivation |
| 🟡 Moyenne | Séquence onboarding | Nouveaux clients | Taux de 2ᵉ achat à J+30 |
| 🟡 Moyenne | Alerte ré-engagement | À risque | Réduction taux de churn |
| 🟢 Standard | Upsell / cross-sell | Clients fidèles actifs | Augmentation du panier moyen |
| ⬜ Faible | Communication standard | Autres | Fréquence d'achat |

> **Principe de Pareto appliqué** : concentrer 70 % des investissements marketing sur les Baleines et les Clients fidèles actifs, qui représentent ~32 % des clients mais vraisemblablement plus de 65 % du CA.

---

## 5. Limites et pistes d'amélioration

1. **Segmentation statique** : les segments sont calculés à un instant T. Une mise à jour mensuelle automatique (cron + pipeline pandas) est recommandée.
2. **Quintiles vs seuils métier** : les scores par quintiles garantissent une distribution équilibrée mais peuvent masquer des seuils métier pertinents (ex. : un client avec 3 commandes vs 100 commandes sont tous deux en F=5 si la distribution l'exige).
3. **Valeur vie client (CLV)** absente : le calcul du CLV prévisionnel (modèle BG/NBD + Gamma-Gamma) permettrait de prioriser les segments par valeur future et pas seulement historique.
4. **Segmentation k-means** : une approche non supervisée sur les scores RFM standardisés permettrait de découvrir des sous-groupes plus nuancés — voir notebook bonus `bonus_kmeans.ipynb`.

---

## Annexe — Données sources

| Fichier | Contenu |
|---|---|
| `data/cleaned_online_retail.csv` | Données nettoyées (hors annulations, nulls, prix négatifs) |
| `data/rfm_segments.csv` | Scores RFM + segment par client (4 314 lignes) |
| `first_cleaning.ipynb` | Pipeline de nettoyage détaillé |
| `rfm.ipynb` | Calcul des métriques et attribution des scores |
| `rfm_visualization.ipynb` | Visualisations et interprétation |
