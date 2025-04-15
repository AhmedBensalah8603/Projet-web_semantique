# Notre projet d'ontologie
    
Bienvenue dans mon projet d'ontologie sémantique dédié au domaine de **l'agriculture**.

# 🌱 Ontologie pour l'Agriculture

## 🎯 Domaine choisi

Ce projet consiste à modéliser un domaine lié à l'agriculture en utilisant des technologies sémantiques (RDF, RDFS, OWL, SPARQL, SWRL). L'objectif est de créer une ontologie permettant de gérer des concepts comme les **cultures**, **sols**, **engrais**, **climats**, **irrigation**, et d'autres éléments essentiels à la gestion agricole.

## ✅ Justification du choix

LeLe choix du domaine Agriculture s'explique par plusieurs raisons :

🌱 Pertinence sociétale : L’agriculture est un pilier fondamental pour la sécurité alimentaire, la durabilité environnementale et le développement économique, ce qui en fait un domaine d’étude stratégique et d’intérêt public.

🌾 Richesse conceptuelle : Ce domaine englobe une grande variété d'entités interconnectées telles que les cultures, les sols, les pratiques agricoles, les fertilisants, les conditions climatiques, les maladies des plantes, etc. Cela en fait un excellent candidat pour la modélisation sémantique.

🧠 Utilité pratique : Une ontologie agricole permettrait de :

+ recommander des cultures adaptées en fonction des propriétés du sol, du climat et des nutriments (NPK),

+ structurer des bonnes pratiques agricoles en fonction des cultures ou des saisons,

+ suivre l’évolution de la santé des plantes ou détecter des risques environnementaux (maladies, sécheresse, etc.),

+ optimiser l’utilisation des ressources comme l’eau et les engrais via des systèmes intelligents de conseil.


## 🧠 Concepts clés identifiés

### 🔷 **Classes principales**

| Classe            | Description                                              |
|-------------------|----------------------------------------------------------|
| `Learner`         | Représente un apprenant inscrit dans un programme.       |
| `Instructor`      | Personne responsable d’un cours ou module.              |
| `Course`          | Unité d’enseignement regroupant plusieurs modules.      |
| `Module`          | Partie spécifique d’un cours (ex: Python, Hadoop…).      |
| `Skill`           | Compétence technique ou théorique à acquérir.           |
| `Assessment`      | Évaluation liée à une compétence ou un cours.           |
| `LearningResource`| Ressource pédagogique (vidéo, document, lien, etc.).    |
| `Project`         | Cas pratique ou projet développé par un apprenant.      |
| `Technology`      | Outil, framework ou langage utilisé dans les cours.     |

### 🔸 **Sous-classes proposées**

| Sous-classe        | Super-classe   | Description                                      |
|--------------------|----------------|--------------------------------------------------|
| `BigDataModule`    | `Module`       | Modules axés sur les frameworks Big Data (Hadoop, Spark…) |
| `ProgrammingModule`| `Module`       | Modules de programmation (Python, Scala, etc.)  |
| `Quiz`             | `Assessment`   | Évaluations rapides de type QCM.                |
| `Exam`             | `Assessment`   | Épreuves longues et formelles.                  |
| `PracticalProject` | `Project`      | Projets appliqués à des cas réels ou simulés.   |
## 🔗 Relations entre les concepts (propriétés)

Voici les principales relations définies entre les classes de l’ontologie :

| Propriété          | Domaine → Portée            | Description                                                      |
|--------------------|-----------------------------|------------------------------------------------------------------|
| `teaches`          | `Instructor → Course`        | L’enseignant donne un cours                                      |
| `enrolledIn`       | `Learner → Course`           | L’apprenant est inscrit à un cours                               |
| `includesModule`   | `Course → Module`            | Le cours est composé de plusieurs modules                        |
| `coversSkill`      | `Module → Skill`             | Le module enseigne une ou plusieurs compétences                  |
| `assesses`         | `Assessment → Skill`         | L’évaluation mesure une compétence particulière                  |
| `achievedSkill`    | `Learner → Skill`            | Compétence acquise par l’apprenant                               |
| `producesProject`  | `Learner → Project`          | L’apprenant réalise un projet                                    |
| `usesTechnology`   | `Project → Technology`       | Le projet utilise des technologies spécifiques                   |
| `hasResource`      | `Module → LearningResource`  | Le module est accompagné de ressources pédagogiques              |

## 🌐 Namespaces utilisés

Afin d'assurer la compatibilité avec les standards du Web sémantique, les namespaces suivants seront utilisés dans notre ontologie :

| Préfixe | URI | Utilisation prévue |
|--------|-----|--------------------|
| `rdf:` | `http://www.w3.org/1999/02/22-rdf-syntax-ns#` | Syntaxe RDF de base |
| `rdfs:` | `http://www.w3.org/2000/01/rdf-schema#` | Définition de classes et propriétés |
| `xsd:` | `http://www.w3.org/2001/XMLSchema#` | Types de données (string, int, date...) |
| `owl:` | `http://www.w3.org/2002/07/owl#` | Modélisation OWL pour classes, restrictions |
| `foaf:` | `http://xmlns.com/foaf/0.1/` | Pour les personnes (`Learner`, `Instructor`) |
| `dc:` | `http://purl.org/dc/elements/1.1/` | Métadonnées (titre, créateur, date…) |
| `skos:` | `http://www.w3.org/2004/02/skos/core#` | Vocabulaire hiérarchique ou thématique (ex: catégories de modules) |


## 🖼️ Visualisation de l’ontologie
![Visualisation](img/graph.png)
## 📊 Requêtes SPARQL exécutées avec résultats

### 🔁 Préfixes utilisés dans toutes les requêtes :
```sparql
PREFIX : <http://www.education-ontology.org/education-data-engineering#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
```

---


### ✅ Requête 1 – Apprenants, leurs projets et les technologies utilisées
```sparql
SELECT ?learner ?project ?technology
WHERE {
  ?learner rdf:type :Learner .
  ?learner :producesProject ?project .
  ?project :usesTechnology ?technology .
}
```
| learner  | project               | technology |
|----------|-----------------------|------------|
| Oussema  | Data Analysis Project | Python     |

---

### ✅ Requête 2 – Modules, compétences couvertes et ressources pédagogiques
```sparql
SELECT ?module ?skill ?resource
WHERE {
  ?module :coversSkill ?skill .
  ?module :hasResource ?resource .
  ?module rdf:type :ProgrammingModule .
}
```
| module         | skill         | resource             |
|----------------|---------------|----------------------|
| Python Module  | Python Basics | Intro to Python PDF  |

---

### ✅ Requête 3 – Enseignants, cours enseignés, modules inclus
```sparql
SELECT ?instructor ?course ?module
WHERE {
  ?instructor :teaches ?course .
  ?course :includesModule ?module .
  ?instructor rdf:type :Instructor .
}
```
| instructor   | course                 | module         |
|--------------|------------------------|----------------|
| MrBenSalah   | Data Engineering Course | Spark Module   |
| MrBenSalah   | Data Engineering Course | Python Module  |

---

### ✅ Requête 4 – Apprenants, cours suivis, modules associés
```sparql
SELECT ?learner ?course ?module
WHERE {
  ?learner :enrolledIn ?course .
  ?course :includesModule ?module .
  ?learner rdf:type :Learner .
}
```
| learner   | course                 | module         |
|-----------|------------------------|----------------|
| Oussema   | Data Engineering Course | Spark Module   |
| Oussema   | Data Engineering Course | Python Module  |




