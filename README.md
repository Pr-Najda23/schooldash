# 📊 Dashboard de Pilotage Académique & Performance Éducative

## 📑 Présentation du Projet
Ce projet consiste en la conception et le développement d'une solution de Business Intelligence (BI) complète sur **Power BI** pour analyser, piloter et optimiser la performance globale d'un établissement académique. L'objectif est de centraliser les données relatives aux **élèves**, aux **enseignants**, et aux **cours**, afin d'apporter des éclairages stratégiques (Insights) permettant de lutter contre l'échec scolaire, d'optimiser la charge enseignante et de fiabiliser les données.

---

## 🛠️ Architecture de la Solution

### 1. Profilage & Nettoyage des Données (Power Query)
Une phase rigoureuse d'exploration (Data Profiling) a été menée pour identifier les anomalies au sein des sources de données raw (`students.csv`, `teachers.csv`, `courses.csv`). 
* **Imputation des valeurs manquantes :** Traitement des données vides détectées sur les notes (`average_grade`, `grade`) et les absences (`absences_count`).
* **Cohérence logique :** Alignement dynamique entre les notes numériques et le statut binaire de réussite (`pass_fail`).
* **Typage strict :** Standardisation des dimensions temporelles au format `Date` (`birth_date`, `enrollment_date`, `hire_date`).

### 2. Modélisation des Données (Modèle en Étoile)
Le modèle de données a été structuré selon les meilleures pratiques du domaine pour optimiser les performances des calculs DAX :
* **Table de Faits :** `courses` (centralisant les sessions de cours, heures effectuées et notes).
* **Tables de Dimensions :** `students` (profils des élèves), `teachers` (corps enseignant) et `DimDate` (table calendrier générée pour le suivi temporel).
* **Organisation :** Centralisation exclusive de toutes les mesures calculées au sein d'un dossier dédié nommé `_Mesures`.

---

## 📈 Structure du Rapport Power BI

Le rapport interactif est articulé autour de **3 pages analytiques majeures** respectant une charte graphique épurée et *Minimalist* (visuels espacés, suppression des axes redondants, palettes de couleurs harmonieuses) :

### 🗂️ Page 1 : Vue Élèves (Performance & Profils)
* **KPIs stratégiques :** Nombre total d'élèves, Moyenne générale globale, Taux de réussite global (%), et Volume total d'absences cumulées.
* **Analyses Graphiques :**
  * Répartition des élèves par niveau scolaire et par section (*Clustered bar chart*).
  * Corrélation entre le taux d'absentéisme et la moyenne générale des élèves (*Scatter chart*).
* **Tableau de Pilotage :** Liste exhaustive des élèves identifiés **"À Risque"** (filtrés dynamiquement sur un fort taux d'absentéisme couplé à une moyenne critique).

### 🗂️ Page 2 : Vue Enseignants (Charge & Évaluation)
* **KPIs stratégiques :** Nombre total d'enseignants actifs, Ancienneté moyenne (calculée dynamiquement en DAX depuis la date de recrutement), Volume d'heures hebdomadaires moyennes, et Note d'évaluation managériale moyenne.
* **Analyses Graphiques :**
  * Répartition du corps enseignant par matière enseignée (`subject`) et par type de contrat (CDI/CDD).
  * Analyse de la distribution des notes d'évaluation via un histogramme ajusté de manière catégorique.
* **Tableau de Pilotage :** Analyse dynamique permettant d'isoler instantanément le Top 5 et le Flop 5 des enseignants selon leur note de performance via le tri contextuel.

### 🗂️ Page 3 : Vue Cours & Résultats
* **KPIs stratégiques :** Nombre de cours dispensés, Taux de réalisation moyen du programme (%), et Taux de réussite global par semestre.
* **Analyses Graphiques :**
  * Proportion de Réussite/Échec empilée à 100% par matière enseignante.
  * Courbe d'évolution temporelle des notes moyennes analysable par année et par semestre (*Line chart* ordonné chronologiquement).
* **Tableau de Pilotage :** Extraction automatique des matières d'excellence ayant enregistré une moyenne générale supérieure ou égale à **12/20**.

---

## 🕹️ Interactivité & Filtres Dynamiques
Pour offrir une expérience utilisateur fluide et granulaire, le dashboard intègre :
* **Slicers Synchronisés :** Filtrage global par *Année scolaire*, *Niveau scolaire*, *Matière*, *Type de contrat*, et *Semestre* configurés sous forme de menus déroulants (Dropdowns).
* **Boutons de Réinitialisation (Reset Buttons) :** Ajout sur chaque page d'un bouton d'action de réinitialisation relié à un *Selected Visuals Bookmark* permettant de vider instantanément l'ensemble des filtres appliqués sans altérer la mise en page des graphiques.

---

## 💡 Principaux Insights & Recommandations Stratégiques
1. **Alerte Absences :** Le graphique de corrélation démontre un impact direct et immédiat de l'absentéisme sur la chute des notes dès le dépassement d'un certain seuil critique. **Action :** Implémenter un système de détection précoce des absences pour déclencher un tutorat de remédiation.
2. **Soutien Pédagogique Ciblé :** Les matières scientifiques affichent le taux d'échec le plus élevé parallèlement à un léger retard dans la complétude du programme. **Action :** Réallouer des heures de soutien spécifiques sur ces modules.
3. **Équilibrage de la Charge Enseignante :** Une disparité est observée entre la charge de certains contrats CDD (sous-chargés) et CDI (proches de la saturation). **Action :** Procéder à une redistribution équitable des volumes horaires hebdomadaires pour optimiser l'engagement et la notation managériale globale.
