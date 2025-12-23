---
tags:
  - sport
  - nutrition
  - habitudes
---


Ce document archive le processus technique utilisé pour importer les données externes dans le Vault.

## 🛠 Script R (rvest)
J'ai utilisé la bibliothèque `rvest` pour extraire les tableaux de recommandations sanitaires.

👉 **[https://www.who.int/data/gho/info/gho-odata-api](https://www.who.int/data/gho/info/gho-odata-api)**

```r
# Chargement des bibliothèques
library(httr)
library(jsonlite)
library(dplyr)

# 1. URL de l'indicateur : Hypertension (Pression artérielle ≥ 140/90)
# Code indicateur OMS : NCD_HYP_PREVALENCE_A
url_api <- "https://ghoapi.azureedge.net/api/NCD_HYP_PREVALENCE_A"

# 2. Requête sécurisée pour éviter les erreurs "Access Denied"
response <- GET(url_api, add_headers(`User-Agent` = "Mozilla/5.0"))

# 3. Vérification du succès de la requête
if (status_code(response) == 200) {
  # Extraction et conversion du contenu JSON
  content_json <- content(response, as = "text", encoding = "UTF-8")
  data_raw <- fromJSON(content_json)
  
  # 4. Nettoyage pour un tableau "Ultra-Pro"
  # On filtre pour l'année la plus récente et on sélectionne les colonnes clés
  tableau_hypertension <- data_raw$value %>%
    select(SpatialDim, TimeDim, Dim1, Value) %>%
    rename(Pays = SpatialDim, Annee = TimeDim, Sexe = Dim1, Prevalence = Value) %>%
    filter(Annee == max(Annee)) %>% # Garde l'année la plus récente
    head(10) # Top 10 pour l'exemple
    
  print("Données récupérées avec succès !")
  print(tableau_hypertension)
  
  # Export pour Obsidian
  write.csv(tableau_hypertension, "data_hypertension_oms.csv", row.names = FALSE)
  
} else {
  print(paste("Erreur lors de l'accès à l'API. Code :", status_code(response)))
}
```


| Source      | Donnée extraite           | Objectif            |
| :---------- | :------------------------ | :------------------ |
| OMS (via R) | Activité physique modérée | 150-300 min/semaine |


![[Pasted image 20251223110913.png]]
## 📊 Données Extraites et Intégrées

Le tableau résultant du script a été converti au format Markdown pour être exploité dans le Vault :

| Catégorie d'âge | Recommandation Cardio (min/semaine) | Renforcement musculaire |
| :--- | :--- | :--- |
| **Enfants (5-17 ans)** | 60 min / jour (modéré à vigoureux) | 3 fois / semaine |
| **Adultes (18-64 ans)** | 150 - 300 min (modéré) | 2 fois / semaine |
| **Seniors (65+ ans)** | 150 - 300 min (varié) | 3 fois / semaine |

https://www.who.int/fr/news-room/fact-sheets/detail/physical-activity

```r
library(rvest)
library(dplyr)

url <- "https://www.who.int/fr/news-room/fact-sheets/detail/physical-activity"
page <- read_html(url)

# Tentative 1 : Extraction des tableaux classiques
tables <- page %>% html_nodes("table") %>% html_table(fill = TRUE)

if (length(tables) > 0) {
  print("Tableau trouvé via la méthode classique !")
  print(tables[[1]])
} else {
  # Tentative 2 : Extraction via les sélecteurs CSS de contenu si les tables sont absentes
  print("Aucun tableau standard trouvé. Extraction des recommandations textuelles...")
  
  # On cible les éléments de liste qui contiennent souvent les chiffres clés (min/semaine)
  recommendations <- page %>% 
    html_nodes("ul li") %>% 
    html_text() %>% 
    # On filtre pour ne garder que les lignes parlant de minutes ou d'activité
    grep("minutes|activité|renforcement", ., value = TRUE)
  
  if (length(recommendations) > 0) {
    print("Données trouvées dans les listes :")
    print(head(recommendations, 10))
  } else {
    print("Échec critique : Le site bloque peut-être l'accès ou a totalement changé de structure.")
  }
}
```

![[Pasted image 20251223052225.png]]

```
library(rvest)
library(dplyr)

# URL d'une page de statistiques sportives (ex: Classement des médailles JO)
url <- "https://fr.wikipedia.org/wiki/Tableau_des_m%C3%A9dailles_des_Jeux_olympiques_d%27%C3%A9t%C3%A9_de_2024"

# Lecture de la page
page <- read_html(url)

# Extraction de TOUS les tableaux
tables <- page %>% html_nodes("table.wikitable") %>% html_table(fill = TRUE)

# On prend le premier tableau (le classement des médailles)
sport_stats <- tables[[1]]

# Nettoyage des noms de colonnes (pour éviter les erreurs de caractères spéciaux)
colnames(sport_stats) <- make.names(colnames(sport_stats))

# Affichage du résultat ultra-pro
print(head(sport_stats))

# Export pour votre Obsidian
write.csv(sport_stats, "stats_sport_obsidian.csv", row.names = FALSE)
```

![[Pasted image 20251223053401.png]]