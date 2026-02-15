# 📊 Projet Power BI - Analyse de Données de Santé

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-0078D4?style=for-the-badge&logo=microsoft&logoColor=white)
![Excel](https://img.shields.io/badge/Excel-217346?style=for-the-badge&logo=microsoft-excel&logoColor=white)

## 🎯 Vue d'ensemble

Ce projet présente une solution complète d'analyse de données de santé utilisant **Power BI**. Il démontre des compétences avancées en Business Intelligence, modélisation de données, création de KPI et visualisation interactive.

Le projet analyse plus de **35 000 enregistrements** sur une période de 4 ans (2022-2025) pour un établissement médical fictif.

---

## 🏥 Contexte du Projet

Ce dashboard permet de suivre et d'analyser :
- L'activité médicale (consultations, hospitalisations, analyses)
- La performance des médecins par spécialité
- Les coûts et revenus de l'établissement
- Les tendances démographiques des patients
- Les indicateurs de qualité des soins

---

## 📂 Structure des Données

### Base de données relationnelle (7 tables)

| Table | Enregistrements | Description |
|-------|----------------|-------------|
| **Patients** | 5 000 | Données démographiques des patients |
| **Médecins** | 150 | Praticiens et leurs spécialités |
| **Consultations** | 15 000 | Visites médicales et motifs |
| **Prescriptions** | 8 000 | Médicaments prescrits |
| **Hospitalisations** | 1 200 | Séjours hospitaliers |
| **Analyses** | 6 000 | Examens médicaux et résultats |
| **Calendrier** | 1 461 | Dimension temporelle (2022-2025) |

### Modèle de données
```
┌─────────────┐      ┌──────────────┐      ┌─────────────┐
│  Patients   │◄────►│Consultations │◄────►│  Médecins   │
└─────────────┘      └──────────────┘      └─────────────┘
       │                    │  │
       │                    │  │
       ▼                    ▼  ▼
┌─────────────┐      ┌──────────────┐
│Hospitali-   │      │Prescriptions │
│sations      │      │& Analyses    │
└─────────────┘      └──────────────┘
       │                    │
       │                    │
       ▼                    ▼
       └───► Calendrier ◄───┘
```

---

## 📈 KPI et Métriques Principales

### KPI Opérationnels
- ✅ **Nombre total de consultations**
- ✅ **Nombre de patients uniques**
- ✅ **Durée moyenne de séjour**
- ✅ **Taux d'occupation hospitalière**
- ✅ **Durée moyenne des consultations**

### KPI Financiers
- 💰 **Revenu total** (consultations + hospitalisations + analyses)
- 💰 **Revenu moyen par patient**
- 💰 **Coût des médicaments**
- 💰 **Revenu par spécialité médicale**

### KPI Qualité
- 🏆 **Taux de réadmission à 30 jours**
- 🏆 **Taux d'analyses anormales**
- 🏆 **Performance par médecin**
- 🏆 **Distribution des résultats d'examens**

---

## 🧮 Exemples de Formules DAX

### Mesures de base
```dax
Nb_Consultations = COUNTROWS(Consultations)

Nb_Patients_Uniques = DISTINCTCOUNT(Consultations[ID_Patient])

Revenu_Total = 
    SUM(Consultations[Montant_Facturé]) +
    SUM(Hospitalisations[Coût_Hospitalisation]) +
    SUM(Analyses[Coût_Analyse])
```

### Time Intelligence
```dax
Consult_N-1 = 
CALCULATE(
    [Nb_Consultations], 
    SAMEPERIODLASTYEAR(Calendrier[Date])
)

Croissance_YoY = 
DIVIDE(
    [Nb_Consultations] - [Consult_N-1],
    [Consult_N-1],
    0
)

Revenu_YTD = TOTALYTD([Revenu_Total], Calendrier[Date])

Consult_MA3 = 
CALCULATE(
    AVERAGEX(
        DATESINPERIOD(Calendrier[Date], LASTDATE(Calendrier[Date]), -3, MONTH),
        [Nb_Consultations]
    )
)
```

### Mesures avancées
```dax
Taux_Readmission = 
VAR PatientsReadmis = 
    COUNTROWS(
        FILTER(
            Hospitalisations,
            CALCULATE(
                COUNTROWS(Hospitalisations),
                FILTER(
                    ALL(Hospitalisations),
                    Hospitalisations[ID_Patient] = EARLIER(Hospitalisations[ID_Patient])
                    && Hospitalisations[Date_Admission] > EARLIER(Hospitalisations[Date_Sortie])
                    && Hospitalisations[Date_Admission] <= EARLIER(Hospitalisations[Date_Sortie]) + 30
                )
            ) > 0
        )
    )
RETURN DIVIDE(PatientsReadmis, COUNTROWS(Hospitalisations), 0)
```

---

## 🎨 Dashboards

Le projet comprend **5 dashboards interactifs** :

### 1. 📊 Dashboard Vue d'Ensemble
- Cartes KPI principales
- Évolution mensuelle des consultations
- Top 10 motifs de consultation
- Carte géographique des patients

### 2. 💼 Dashboard Analyse Financière
- Décomposition des revenus
- Évolution par source (consultations, hospitalisations, analyses)
- Top médicaments par coût
- Distribution revenus par ville

### 3. 👥 Dashboard Patients
- Pyramide des âges
- Distribution par groupe sanguin
- Taux de couverture mutuelle
- Analyse démographique

### 4. 🏥 Dashboard Hospitalisations
- Hospitalisations par service
- Tendances des admissions
- Distribution durées de séjour
- Types de sortie

---

## 🛠️ Compétences Démontrées

### Techniques Power BI
- ✅ Modélisation de données (schéma en étoile)
- ✅ Relations complexes entre tables
- ✅ Création de mesures DAX avancées
- ✅ Time Intelligence (YoY, YTD, MA)
- ✅ Fonctions DAX complexes (CALCULATE, FILTER, EARLIER)
- ✅ Optimisation des performances
- ✅ Création de visuels interactifs

### Analyse de données
- ✅ Définition de KPI pertinents
- ✅ Analyse multidimensionnelle
- ✅ Storytelling avec les données
- ✅ Identification de tendances
- ✅ Analyse comparative

### Design et UX
- ✅ Design cohérent et professionnel
- ✅ Navigation intuitive
- ✅ Interactivité (slicers, drillthrough)
- ✅ Palette de couleurs harmonieuse
- ✅ Tooltips personnalisés

---

## 📥 Installation et Utilisation

### Prérequis
- Power BI Desktop (version gratuite disponible sur [Microsoft](https://powerbi.microsoft.com/))
- Windows 10 ou supérieur

### Instructions
1. **Télécharger le projet**
   ```bash
   git clone https://github.com/Benouattara/Analyses_donnees_hospital_Power-BI.git
   cd Analyses_donnees_hospital_Power-BI
   ```

2. **Ouvrir le fichier Power BI**
   - Double-cliquer sur `analyse financière de l'hôpital.pbix`
   - Le fichier s'ouvrira dans Power BI Desktop

3. **Explorer les dashboards**
   - Naviguer entre les 4 pages de rapport
   - Utiliser les filtres (slicers) pour interagir
   - Cliquer sur les visuels pour filtrer dynamiquement

4. **Accéder aux données sources**
   - Le fichier `data/Données_Santé_PowerBI.xlsx` contient toutes les données
   - Ouvrir avec Excel ou tout tableur compatible

---

## 📚 Documentation

La documentation complète du projet est disponible dans le dossier `documentation/` :
- **Documentation_Projet_PowerBI.docx** : Guide complet avec toutes les formules DAX, explications des KPI, et guide d'implémentation

### Contenu de la documentation
1. Présentation du projet
2. Structure de la base de données
3. KPI et métriques principales
4. Formules DAX essentielles
5. Structure des dashboards
6. Guide d'implémentation Power BI
7. Bonnes pratiques
8. Checklist qualité
9. Publication sur GitHub
10. Annexes (dictionnaire de données, ressources)

---

## 🎓 Contexte d'Apprentissage

Ce projet a été développé pour démontrer une maîtrise complète de Power BI dans un contexte professionnel. Il illustre :

- La capacité à travailler avec des données volumineuses (35 000+ enregistrements)
- La compréhension d'un domaine métier (santé)
- La création de solutions BI end-to-end
- La documentation rigoureuse d'un projet
- Les bonnes pratiques en matière de visualisation de données

---

## 📸 Aperçus

> <img width="964" height="543" alt="vue d&#39;ensemble" src="https://github.com/user-attachments/assets/77039f50-4dfe-4a76-adaa-0b0262a25167" /> 
> <img width="993" height="565" alt="Analyse patients" src="https://github.com/user-attachments/assets/b401311b-a152-4073-8b89-745dfd7133a8" />
<img width="987" height="558" alt="Analyse hospitalisation" src="https://github.com/user-attachments/assets/4faf04d5-b67e-4022-b54d-45865a31bbdc" />
<img width="987" height="550" alt="Analyse financières" src="https://github.com/user-attachments/assets/4d7d90b8-c742-4e9c-8e23-e6324d70ceea" />



```
screenshots/
├── dashboard_overview.png
├── dashboard_financial.png
├── dashboard_patients.png
└── dashboard_hospitalization.png
```

---

## 🚀 Évolutions Futures

Améliorations possibles du projet :
- [ ] Ajout de prévisions avec machine learning (forecasting)
- [ ] Intégration de données en temps réel
- [ ] Création d'alertes automatiques sur les KPI critiques
- [ ] Analyse prédictive des réadmissions
- [ ] Dashboard mobile optimisé
- [ ] Export automatisé de rapports

---

## 📞 Contact

**Ben OUATTARA**
- LinkedIn : https://www.linkedin.com/in/ben-youssouf-ouattara-a9b912193/
- Email : benouattara3@gmail.com
- Portfolio : 

---

## 📄 Licence

Ce projet est disponible sous licence MIT. Les données sont entièrement fictives et générées aléatoirement.

---

## 🙏 Remerciements

Ce projet a été développé dans le cadre d'une recherche d'emploi en tant qu'Analyste BI / Data Analyst. Il démontre des compétences pratiques et applicables immédiatement en entreprise.

**Technologies utilisées :**
- Microsoft Power BI Desktop
- Langage DAX (Data Analysis Expressions)
- Power Query (M)
- Microsoft Excel
- Python (génération de données)

---

⭐ **Si ce projet vous intéresse, n'hésitez pas à le mettre en favoris !**

