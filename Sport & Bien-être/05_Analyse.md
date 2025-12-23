---
tags:
  - sommeil
  - habitudes
  - physiologie
---


Ce chapitre analyse l'évolution du bien-être à travers la mise en pratique d'une routine sportive régulière sur une période donnée.

> [!ABSTRACT] Méthodologie
> Cette analyse repose sur un suivi longitudinal de 30 jours, documenté via les "Daily Logs" d'Obsidian, permettant de croiser des données subjectives (énergie) et objectives (intensité).

### 5.1 Collecte de données

Les données ont été recueillies via des logs quotidiens dans Obsidian, mesurant trois indicateurs clés : l'énergie, le sommeil et l'intensité du sport.


### 5.2 Visualisation des données (Registre d'Entraînement)

> [!ABSTRACT] Note de l'Auteur
> Le tableau suivant est généré dynamiquement par le moteur *Dataview*. Il croise les variables physiologiques (sommeil) et psychologiques (énergie) collectées lors du suivi longitudinal.

```dataview
TABLE 
    sommeil AS "Repos (h)", 
    energie AS "Vitalité (/10)", 
    intensite AS "Effort (/10)",
    mood AS "État"
FROM "05_Journal_de_Bord"
WHERE type = "daily-log"
SORT file.name ASC
```

```dataview
TABLE WITHOUT ID round(average(rows.sommeil), 2) + " h" AS "Moyenne Sommeil", round(average(rows.energie), 2) + "/10" AS "Moyenne Énergie", round(average(rows.intensite), 2) + "/10" AS "Moyenne Intensité" FROM "05_Journal_de_Bord" WHERE type = "daily-log" GROUP BY type
```

---
### 🏁 Comparaison aux normes (Scraping R)
Selon les données extraites via R dans la note [[05c_Scraping_R]], l'objectif pour un adulte est de **150 à 300 minutes** de sport par semaine.

* **Statut actuel :** `$= dv.pages('"05_Journal_de_Bord"').intensite.array().reduce((a, b) => a + b, 0) >= 150 ? "✅ Objectif OMS Atteint" : "⚠️ Objectif OMS non atteint"`
* **Écart :** Ma pratique réelle est mise en perspective avec les données tabulaires de la base OMS.
### Analyse des résultats
L'observation de ce tableau met en évidence une **corrélation directe** entre la qualité du sommeil et le pic d'énergie le lendemain. On remarque que lorsque le repos est inférieur à 7h, l'intensité de l'effort chute de manière significative, validant ainsi les théories de la récupération abordées dans le chapitre [[04_Hygiène_Vie]].




> [!NOTE|no-icon] 🧭 Navigation
> [[00_Sommaire|Accueil]]  •  [[05_Analyse|📊 Data]]  •  [[Test_Donnees_Externes|🌍 Normes OMS]]  •  [[99_Documentation|🛠️ Doc]]

---