---
tags:
  - mémoire
  - académique
  - physiologie
---
# 🏛️ Documentation du Projet : Analyse & Bien-Être

## 1. Philosophie du Projet : Le "Literate Programming"

Ce Vault dépasse la simple prise de notes pour devenir un environnement de **Literate Programming**. L'idée centrale est que le contenu textuel (recherches sur la physiologie) et le code (requêtes Dataview) forment un récit cohérent.

- **Objectif :** Créer un système de connaissance autonome (_Stand-alone_) où la donnée brute est transformée en information visuelle.
    
- **Thématique :** Une approche holistique du bien-être par l'équilibre sport/repos.
    

---

## 2. Architecture Technique & Plugins

Le système repose sur une synergie entre trois piliers technologiques :

### A. Moteur de données (Dataview)

Le fichier `05_Analyse.md` agit comme un tableau de bord.

- **Automatisation :** Utilisation de métadonnées YAML pour extraire les variables `sommeil`, `energie` et `intensite`.
    
- **Intelligence calculatoire :** Mise en place de fonctions JavaScript simplifiées (`average`, `round`) pour générer des moyennes de performance hebdomadaires.
    

### B. Design System & Expérience Utilisateur (CSS)

L'interface a été entièrement refondue via un snippet CSS personnalisé :

- **Charte Graphique :** Palette "Bordeaux Académique" (`#5c1616`) sur fond "Papier Sépia" (`#fcfaf2`) pour réduire la fatigue oculaire et renforcer l'aspect prestigieux du manuscrit.
    
- **Typographie :** Sélection de polices Serif pour les corps de texte afin d'évoquer les publications de recherche médicale.
    

### C. Visualisation Spatiale (Excalidraw & Canvas)

- **Excalidraw :** Création d'un schéma de synthèse (`Synthese.excalidraw`) modélisant le triangle de la santé.
    
- **Canvas :** Utilisation du fichier `Carte_Mentale_BienEtre` pour relier visuellement les notes théoriques aux données pratiques.
    

---

## 3. Stratégie de Webscraping & API

Pour ancrer les données personnelles dans une réalité scientifique, le Vault intègre des données externes officielles.

### 🛠️ Processus de Récupération des Données

Pour garantir l'exactitude des statistiques, j'ai mis en place un pipeline d'acquisition basé sur les standards du **Global Health Observatory (GHO)** de l'OMS :

- **Source de données brute :** Utilisation de l'**API OData de l'OMS**, permettant d'extraire les indicateurs via des requêtes JSON structurées plutôt que par un simple scraping HTML instable.
    
- **Indicateurs spécifiques :** Les données concernent principalement la prévalence de l'hypertension (`NCD_HYP_PREVALENCE_A`), de l'obésité (`NCD_BMI_30A`) et les niveaux d'inactivité physique.
    
- **Précision Statistique :** Le script R a été conçu pour isoler la **valeur moyenne** des intervalles de confiance fournis par l'OMS, assurant ainsi une base comparative rigoureuse.
    

---

## 4. Automatisation et Standardisation

Le Vault intègre un système de gabarits pour assurer la qualité des données récoltées :

1. **Configuration :** Le dossier `Templates/` est défini comme source native dans les paramètres d'Obsidian.
    
2. **Usage :** Pour chaque nouveau log, le template `Nouveau_Log` génère automatiquement les clés YAML (`sommeil`, `energie`, `intensite`).
    
3. **Interopérabilité :** Ce processus garantit que 100% des fichiers du dossier `05_Journal_de_Bord` sont compatibles avec les calculs du moteur Dataview.
    

L'intégration du scraping R répond à une logique de **Data-Informed Design**. Le script `rvest` a permis de transformer une page web non structurée en une base tabulaire exploitable par les templates.

---

## 5. Visualisation & Analyse Critique

### 📊 Intégration dans le Vault

- **Stockage YAML :** Les statistiques sont converties en propriétés YAML (type: `stats-oms`) pour permettre un filtrage dynamique.
    
- **Rendu Dataview :** L'affichage compare en temps réel mes objectifs (150-300 min de cardio/semaine) avec les réalités statistiques mondiales.
    
- **Esthétique Professionnelle :** Les tableaux exploitent le thème **Bleu Ardoise et Bronze**, offrant une expérience de lecture type "Rapport d'Expert".
    

### 🔍 Bilan

1. **Force :** Centralisation totale de la chaîne de valeur (recherche -> log -> analyse -> présentation).
    
2. **Limite :** La dépendance aux plugins tiers nécessite une documentation rigoureuse pour garantir la pérennité du système.
    
3. **Perspective :** Ce modèle est exportable pour n'importe quel suivi de performance professionnelle ou médicale.
    

---

## 🔗 Références des Sources

1. **OMS GHO OData API** : [Accès technique aux bases de données mondiales](https://www.who.int/data/gho/info/gho-odata-api)
    
2. **Aide-mémoire OMS** : [Directives officielles sur l'activité physique](https://www.who.int/fr/news-room/fact-sheets/detail/physical-activity)


    

---

L'architecture logique du projet est cartographiée dans la [[Carte_Mentale_BienEtre.canvas]]. Ce document permet de visualiser les liens entre la théorie bordeaux et la pratique bleue.

[[00_Sommaire|Fin de la présentation - Retour à l'accueil]]
