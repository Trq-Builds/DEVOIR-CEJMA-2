# `💼`・Devoir - 2 ・ BTS SIO SISR 2ᵉ année.

**Thématiques :** Protection des données (DCP) • Identité numérique • Preuve électronique • Sécurité des équipements • Obligations légales.

Ce dépôt regroupe l’intégralité des exercices issus des six documents fournis, entièrement traités et organisés sous forme de documentation technique structurée.
Les analyses et corrections ont été enrichies par des compléments juridiques afin de renforcer la qualité et la conformité du rendu, avec des références au RGPD, à la CNIL, au Code pénal, ainsi qu’aux cadres législatifs pertinents tels que la LCEN.

---

## `🗃️`・Documents de référence : 

L'ensemble des travaux repose sur l'analyse des documents suivants fournis en annexe :

*   `📂`・`Cours 7・CEJMA-ObligationProtectionDonnées`.`pdf`.
*   `📂`・`Cours 8・CEJMA-DisponibilitéIntégritéConfidentialité`.`pdf`.
*   `📂`・`Cours 9・CEJMA-ArchivageProtectionsDonnées`.`pdf`.
*   `📂`・`Cours 10・CEJMA-ObligationsLégales`.`pdf`.
*   `📂`・`Cours 11・CEJMA-PreuvesNumériques`.`pdf`.

---


## `📌`・Table des matières (Cliquez pour être redirigé.)

1.  [**Dossier 7** ・ Audit de conformité & Analyse des risques (Cibeco)](#dossier7)
    *   [1.1. Analyse de la confidentialité des archives (Q1)](#d7q1)
    *   [1.2. Analyse du risque d'indisponibilité (Q2)](#d7q2)
    *   [1.3. Classification des risques malveillants (Q4)](#d7q4)
    *   [1.4. Synthèse et plan de remédiation](#d7synthese)
2.  [**Dossier 8** ・ Rapport d'incident cyber (Ecotri)](#dossier8)
    *   [2.1. Conséquences techniques sur le triptyque DIC (Q1)](#d8q1)
    *   [2.2. Analyse de contagion & Risque systémique (Q2)](#d8q2)
    *   [2.3. Impacts humains, réputationnels et financiers (Q3)](#d8q3)
    *   [2.4. Responsabilité pénale & Identification de l'attaquant (Q4)](#d8q4)
3.  [**Dossier 9** ・ Archivage & Protection des données (Cibeco)](#dossier9)
    *   [3.1. Audit de la sécurisation physique des archives (Q1)](#d9q1)
    *   [3.2. Conformité de la traçabilité des accès (Q2)](#d9q2)
    *   [3.3. Violations légales sur le serveur critique miRDB (Q3)](#d9q3)
    *   [3.4. Analyse systémique : pourquoi le mot de passe ne suffit pas (Q4)](#d9q4)
4.  [**Dossier 10** ・ Procédures incidents FRAP (Cibeco)](#dossier10)
    *   [4.1. FRAP n°1 : Confidentialité des accès serveurs (Q1)](#d10q1)
    *   [4.2. FRAP n°2 : Intégrité du transfert des journaux (Q2)](#d10q2)
    *   [4.3. FRAP n°3 : Disponibilité & Respect du SLA (Q3)](#d10q3)
    *   [4.4. Exigences probatoires des autorités judiciaires (Q4)](#d10q4)
5.  [**Dossier 11** ・ Collecte & Conservation des preuves (Forensic)](#dossier11)
    *   [5.1. Conformité des moyens techniques de collecte (Q1)](#d11q1)
    *   [5.2. Analyse de la complétude des événements (Q2)](#d11q2)
    *   [5.3. Durabilité et viabilité des supports de stockage (Q3)](#d11q3)
    *   [5.4. Résilience et sécurité du site de conservation (Q4)](#d11q4)
6.  [**Annexes** ・ Références juridiques & techniques](#annexes)

***

<a name="dossier7"></a>
## `📘`・Dossier 7 ・ Audit de conformité & Analyse des risques (Cibeco)

* **Source :** `Cours7-CEJMA-ObligationProtectionDonnées.pdf`
* **Contexte :** Audit du système d'archivage de l'entreprise Cibeco.
* **Statut global :** 🔴 **Non-conforme** (Risque Critique).

<a name="d7q1"></a>
### 1.1. Analyse de la confidentialité (Q1)

L'analyse de la procédure d'archivage actuelle met en évidence une absence totale de garantie de confidentialité. Les données sont exposées à plusieurs niveaux de l'architecture.

#### `🧠`・Diagnostic technique

| Vecteur de risque | Description de la faille | Conséquence technique |
| :--- | :--- | :--- |
| **Stockage** | Absence de chiffrement au repos. | Les données sont lisibles en clair sur le disque en cas d'extraction. |
| **Authentification** | Mot de passe simple, compte unique. | Risque élevé de compromission par force brute. |
| **Processus** | Transfert manuel via clé USB non sécurisée. | Risque de perte ou vol du support amovible. |
| **Architecture** | Réseau plat (pas de segmentation). | Mouvement latéral possible entre les environnements clients. |

#### `⚖️`・Références juridiques et normatives

*   **[RGPD ・ Article 32](https://www.cnil.fr/fr/reglement-europeen-protection-donnees/chapitre4#Article32)** : Impose de mettre en œuvre des mesures techniques (telles que le chiffrement ou la pseudonymisation) pour garantir un niveau de sécurité adapté au risque.
*   **[ISO/IEC 27001 ・ Annexe A.9](https://www.iso.org/standard/27001)** : Exige une gestion formelle des accès utilisateurs et l'application du principe de moindre privilège (ici violé par l'usage d'un compte unique).

---

<a name="d7q2"></a>
### 1.2. Analyse de la disponibilité (Q2)

Le système d'archivage actuel présente un **Point Unique de Défaillance (SPOF)**. Aucune mesure de redondance n'est en place.

#### `⚠️`・Facteurs de risques d'indisponibilité

1.  **Défaillance matérielle :** Panne du disque dur unique ou corruption de la clé USB de transfert.
2.  **Dépendance humaine :** Le processus repose intégralement sur une personne (M. Darmon). Une absence entraîne un arrêt du service.
3.  **Sinistre physique :** La salle serveur unique n'offre aucune protection contre les risques environnementaux (incendie, dégât des eaux).

#### `⚖️`・Références juridiques

*   **[Loi LCEN (2004-575)](https://www.legifrance.gouv.fr/loda/id/JORFTEXT000000801164/)** : Obligation pour les hébergeurs de conserver les données de connexion (logs) pendant 1 an. Une indisponibilité des archives constitue une infraction pénale.
*   **[ISO 22301](https://www.iso.org/standard/75106.html)** : Norme relative à la continuité d'activité, non respectée ici (absence de PCA/PRA).

---

<a name="d7q4"></a>
### 1.3. Classification des risques malveillants (Q4)

L'analyse de risques met en avant deux scénarios malveillants majeurs nécessitant une qualification juridique précise.

#### Risque A : Accès illégitime aux données
*   **Type :** Atteinte à la confidentialité.
*   **Gravité :** **Critique**.
*   **Justification :** L'accès non autorisé à des données personnelles (DCP) ou sensibles (logs de trafic) constitue une violation au sens de l'**[Article 33 du RGPD](https://www.cnil.fr/fr/reglement-europeen-protection-donnees/chapitre4#Article33)**, entraînant une obligation de notification à la CNIL sous 72h.

#### Risque B : Altération des archives
*   **Type :** Atteinte à l'intégrité.
*   **Gravité :** **Critique**.
*   **Justification :** La modification de journaux systèmes (logs) relève de l'infraction d'introduction frauduleuse de données dans un STAD (**[Article 323-3 du Code Pénal](https://www.legifrance.gouv.fr/codes/article_lc/LEGIARTI000006418319)**). Elle rend les preuves juridiquement irrecevables.

---

<a name="d7synthese"></a>
### 1.4. Plan de remédiation

Pour mettre le système en conformité, les actions suivantes sont recommandées :

*   **Immédiat :** Chiffrement des disques (BitLocker/LUKS) et mise en place de mots de passe forts.
*   **Court terme :** Automatisation des sauvegardes (suppression de la clé USB) et réplication sur un site secondaire (règle 3-2-1).
*   **Gouvernance :** Rédaction d'une Politique de Sécurité des Systèmes d'Information (PSSI) et formation du personnel.

---

<a name="dossier8"></a>
## `📘`・Dossier 8 ・ Rapport d'incident cyber (Ecotri)

* **Source :** `Cours8-CEJMA-DisponibilitéIntégritéConfidentialité.pdf`
* **Contexte :** Analyse post-mortem de l'attaque subie par le site web d'Ecotri le 11 novembre 2019.
* **Typologie :** Défiguration (Defacement) et Injection SQL.

<a name="d8q1"></a>
### 2.1. Conséquences techniques sur le triptyque DIC (Q1)

L'analyse forensique de l'incident met en évidence une compromission totale des trois piliers de la sécurité de l'information (DIC).

#### `📊`・Tableau de synthèse des impacts : 

| Critère | État | Description de l'incident | Impact métier |
| :--- | :--- | :--- | :--- |
| **Disponibilité** | 🔴 **Interrompue** | Le service de valorisation des déchets est inaccessible. Le forum est dégradé (lecture seule ou contenu altéré). | Arrêt de la production, impossibilité pour les clients d'utiliser le service. |
| **Intégrité** | 🔴 **Compromise** | Modification de la page d'accueil (`new_msg`) et remplacement d'images (`valider.ok.jpeg`). Injection de code malveillant en base de données. | Perte de confiance, diffusion de fausses informations, corruption des données. |
| **Confidentialité** | 🟠 **Menacée** | L'injection SQL a potentiellement permis l'exfiltration de la table `membres` (noms, adresses, téléphones). | Violation de données personnelles (DCP) nécessitant une notification CNIL. |

#### `🧠`・Analyse technique
La vulnérabilité exploitée est une **Injection SQL** (CWE-89). Le code source PHP (lignes 9-10 du document fourni) ne filtre pas les entrées utilisateurs et n'utilise pas de requêtes préparées (`INSERT INTO ... VALUES ...`).

---

<a name="d8q2"></a>
### 2.2. Analyse de contagion & Risque systémique (Q2)

Le risque ne se limite pas au seul client Ecotri. L'incident révèle une faille structurelle dans les processus de développement de l'hébergeur Cibeco.

#### Diagnostic de contagion
*   **Réutilisation de code :** Cibeco semble utiliser le même moteur de site ou les mêmes procédures d'authentification pour l'ensemble de ses clients.
*   **Vecteur de propagation :** Si la faille réside dans un module commun (ex: `connexion.php` ou `forum.php`), **tous les clients hébergés par Cibeco sont vulnérables** à la même attaque.
*   **Absence de cloisonnement :** Si l'architecture ne prévoit pas une isolation stricte (VLAN, conteneurs, bases de données séparées), un attaquant ayant compromis Ecotri pourrait pivoter vers d'autres clients (Mouvement latéral).

---

<a name="d8q3"></a>
### 2.3. Impacts humains, réputationnels et financiers (Q3)

L'attaque engendre des conséquences dépassant le cadre purement technique.

#### `👥`・Impacts Humains
*   **Clients (ex: Jean Dupont, Audrey Rabanov) :** Frustration, perte de confiance, sentiment d'insécurité quant à leurs données personnelles.
*   **Personnel (M. Legendre) :** Stress intense, risque psychosociaux (burnout), surcharge de travail pour la gestion de crise.

#### `💶`・Impacts Financiers
1.  **Perte de Chiffre d'Affaires :** Résiliation de contrats (churn), comme menacé par le client Hubert Garand ("C'est fini Ecotri").
2.  **Coûts de remédiation :** Intervention d'experts cyber, reconstruction du site, audit de code.
3.  **Sanctions juridiques :** Risque d'amende administrative par la CNIL pouvant atteindre **4% du chiffre d'affaires mondial** ou 20 millions d'euros en cas de défaut de sécurité avéré ([Art. 83 RGPD](https://www.cnil.fr/fr/reglement-europeen-protection-donnees/chapitre8#Article83)).

---

<a name="d8q4"></a>
### 2.4. Responsabilité pénale & Identification de l'attaquant (Q4)

L'attaque constitue une série d'infractions pénales caractérisées.

#### `⚖️`・Qualification juridique des faits : 

| Acte malveillant | Qualification pénale | Article Code Pénal | Peine encourue |
| :--- | :--- | :--- | :--- |
| Intrusion sur le serveur | Accès frauduleux dans un STAD | **[Art. 323-1](https://www.legifrance.gouv.fr/codes/article_lc/LEGIARTI000006418316)** | 3 ans, 100 000 € |
| Modification du site | Introduction ou modification frauduleuse de données | **[Art. 323-3](https://www.legifrance.gouv.fr/codes/article_lc/LEGIARTI000006418319)** | 5 ans, 150 000 € |
| Vol de la base clients | Extraction de données | **[Art. 323-3](https://www.legifrance.gouv.fr/codes/article_lc/LEGIARTI000006418319)** | 5 ans, 150 000 € |

#### `🔍`・Identification de l'attaquant
*   **Élément technique :** L'adresse IP `82.89.34.7` a été relevée dans les logs du serveur web au moment de l'attaque.
*   **Procédure légale :**
    1.  Dépôt de plainte par Ecotri auprès des services de police ou gendarmerie (C3N/OCLCTIC).
    2.  Le procureur ou le juge d'instruction délivre une réquisition judiciaire.
    3.  Le Fournisseur d'Accès Internet (FAI) détenteur de l'IP est contraint de fournir l'identité de l'abonné associé à cette IP à l'heure de l'attaque (**[Loi LCEN Art. 6](https://www.legifrance.gouv.fr/loda/article_lc/LEGIARTI000042038969/)**).

---

<a name="dossier9"></a>
## `📘`・Dossier 9 ・ Archivage & Protection des données (Cibeco)

* **Source :** `Cours9-CEJMA-ArchivageProtectionsDonnées.pdf`
* **Contexte :** Analyse approfondie de la sécurisation physique et logique de l'infrastructure d'hébergement de Cibeco.
* **Objet :** Mise en conformité des locaux et des serveurs critiques.

<a name="d9q1"></a>
### 3.1. Audit de la sécurisation physique des archives (Q1)

L'audit des locaux révèle de graves manquements aux obligations légales de sécurité physique, compromettant l'intégrité et la disponibilité des données hébergées.

#### `📋`・Tableau des non-conformités physiques : 

| Élément de sécurité | Constat sur site (Doc 1) | Obligation violée | Risque induit |
| :--- | :--- | :--- | :--- |
| **Protection Incendie** | Absence de détecteurs automatiques et d'extinction gaz. Présence d'extincteurs manuels inadaptés. | **[APSAD R4](https://cnpp.com/Boutique/Editions/Referentiels-APSAD/Incendie/Referentiel-APSAD-R4)** / Code du Travail | Destruction totale des données par le feu avant intervention humaine. |
| **Climatisation** | Climatisation centralisée standard (type bureau). | **ISO 27001 (A.11.2)** | Surchauffe serveur, arrêt de production, réduction durée de vie matériel. |
| **Contrôle d'accès** | Digicode unique partagé, pas de vidéosurveillance. | **[RGPD Art. 32](https://www.cnil.fr/fr/reglement-europeen-protection-donnees/chapitre4#Article32)** | Accès non tracé, intrusion, vol de matériel (serveur tour non racké). |
| **Alimentation** | Serveur tour simple alimentation. | **ISO 22301** | Arrêt brutal en cas de coupure électrique (perte de données en cache). |

---

<a name="d9q2"></a>
### 3.2. Conformité de la traçabilité des accès (Q2)

La procédure actuelle de gestion des accès est obsolète et juridiquement irrecevable.

#### Diagnostic
*   **Méthode actuelle :** Formulaire papier (Doc 2) rempli manuellement.
*   **Problème majeur :** Ce système ne garantit ni l'**intégrité** (le papier peut être détruit ou modifié), ni la **non-répudiation** (signature facile à falsifier), ni la **disponibilité** (recherche d'information lente et complexe).

#### Exigence légale
L'**[Article 32 du RGPD](https://www.cnil.fr/fr/reglement-europeen-protection-donnees/chapitre4#Article32)** impose la capacité de rétablir la disponibilité et l'accès aux données. De plus, l'obligation de reddition de comptes (Accountability) nécessite une journalisation informatique inaltérable (logs) pour prouver qui a accédé à quelle donnée et à quel moment.

---

<a name="d9q3"></a>
### 3.3. Violations légales sur le serveur critique miRDB (Q3)

L'analyse de la configuration du serveur de base de données `miRDB` (Doc 3) met en évidence des violations directes de la loi.

#### 1. Absence de chiffrement (Confidentialité)
*   **Constat :** L'interface d'administration est accessible en HTTP (non sécurisé) et les données semblent stockées en clair.
*   **Violation :** Non-respect de l'obligation de sécurité des moyens de traitement (**RGPD Art. 32**). En cas d'interception réseau (Man-in-the-Middle), les données sont compromises.

#### 2. Désactivation des journaux (Traçabilité)
*   **Constat :** Les logs sont désactivés pour "économiser de l'espace disque".
*   **Violation :**
    *   **[Code de Commerce Art. L123-22](https://www.legifrance.gouv.fr/codes/article_lc/LEGIARTI000006221311)** : Obligation de conserver les documents comptables et pièces justificatives pendant 10 ans. Sans logs, impossible de prouver l'intégrité des transactions.
    *   **Droit pénal :** L'absence de logs empêche l'identification des auteurs en cas d'infraction, ce qui peut être qualifié de négligence ou de complicité par fourniture de moyens.

---

<a name="d9q4"></a>
### 3.4. Analyse systémique : pourquoi le mot de passe ne suffit pas (Q4)

La mise en place d'un mot de passe robuste pour l'administrateur, bien que nécessaire, est **insuffisante** pour garantir la conformité globale.

#### Justification structurée

1.  **Périmètre limité :** Le mot de passe ne protège que l'accès logique (Authentification). Il ne couvre pas :
    *   La **sécurité physique** (vol du serveur).
    *   L'**interception réseau** (connexion HTTP non chiffrée).
    *   La **disponibilité** (panne matérielle, incendie).
2.  **Facteur Humain :** Un mot de passe unique partagé (comme c'est le cas ici) empêche l'imputabilité des actions. Si une erreur est commise, on ne peut savoir quel administrateur en est responsable.
3.  **Défense en profondeur :** La sécurité doit être multicouche. Un mot de passe fort ne sert à rien si la base de données est accessible publiquement sans pare-feu ou si les sauvegardes sont inexistantes.

---

<a name="dossier10"></a>
## `📘`・Dossier 10 ・ Procédures incidents FRAP (Cibeco)

* **Source :** `Cours10-CEJMA-ObligationsLégales.pdf`
* **Contexte :** Audit des Fiches de Réponse à Incident (FRAP) de Cibeco.
* **Objectif :** Identifier les non-conformités juridiques et opérationnelles des procédures de secours.

<a name="d10q1"></a>
### 4.1. FRAP n°1 : Confidentialité des accès serveurs (Q1)

La procédure actuelle de gestion des accès de secours (génération de clés SSH) présente des failles critiques de sécurité.

#### `🛑`・Analyse des non-conformités : 

| Étape Procédure | Faille identifiée | Risque Juridique / Normatif |
| :--- | :--- | :--- |
| **Génération** | Clés générées manuellement par une stagiaire (Sarah) sans supervision. | Violation du principe de compétence et de responsabilité (**ISO 27001 A.7**). |
| **Stockage** | Clé privée stockée sur une clé USB non chiffrée, laissée sur un bureau ("Post-it"). | Négligence caractérisée (**[Code Pénal Art. 226-17](https://www.legifrance.gouv.fr/codes/article_lc/LEGIARTI000006417978)** : manquement à l'obligation de sécurité). |
| **Traçabilité** | Aucune journalisation de la création ou de l'usage de la clé. | Impossibilité d'imputer une action malveillante (Non-répudiation). |
| **Cycle de vie** | Pas de date d'expiration ni de procédure de révocation. | Risque d'accès persistant non autorisé. |

**Sanction potentielle :** Jusqu'à 5 ans d'emprisonnement et 300 000 € d'amende pour défaut de sécurisation des données personnelles.

---

<a name="d10q2"></a>
### 4.2. FRAP n°2 : Intégrité du transfert des journaux (Q2)

Le transfert des journaux systèmes (logs) vers le serveur d'archivage ne garantit pas leur valeur probante.

#### `⚠️`・Problèmes d'intégrité
1.  **Absence de scellement :** Les logs sont transférés sans calcul d'empreinte numérique (Hash SHA-256). En cas de modification durant le transfert (Attaque *Man-in-the-Middle*), l'altération est indétectable.
2.  **Canal non sécurisé :** Le protocole de transfert n'est pas spécifié comme chiffré (SFTP/TLS), exposant les données à une interception.

#### Conséquence juridique
Selon l'**[Article 1366 du Code Civil](https://www.legifrance.gouv.fr/codes/article_lc/LEGIARTI000032042341)**, l'écrit électronique n'a la même force probante que l'écrit papier qu'à la condition que « puisse être dûment identifiée la personne dont il émane et qu'il soit établi et conservé dans des conditions de nature à en garantir l'intégrité ».
**Conclusion :** Les logs collectés via cette FRAP seraient rejetés comme preuve par un tribunal.

---

<a name="d10q3"></a>
### 4.3. FRAP n°3 : Disponibilité & Respect du SLA (Q3)

La procédure de restauration des services clients est incompatible avec les engagements contractuels de Cibeco.

#### `📉`・Analyse de l'écart RTO/RPO
*   **Engagement (SLA) :** Disponibilité de 99,9% (soit < 9h d'arrêt par an).
*   **Réalité Procédure :** La sauvegarde est trimestrielle (tous les 3 mois).
*   **Calcul du risque :**
    *   **RPO (Perte de données maximale) :** 90 jours.
    *   **Impact :** Perte massive de données clients.

#### Violation Contractuelle & Légale
*   **Droit des contrats :** Manquement à l'obligation de résultat sur la sauvegarde. Cibeco s'expose à des dommages et intérêts pour perte d'exploitation de ses clients.
*   **RGPD Art. 32 :** L'incapacité à restaurer la disponibilité des données "dans des délais appropriés" constitue une infraction administrative passible d'amende.

---

<a name="d10q4"></a>
### 4.4. Exigences probatoires des autorités judiciaires (Q4)

Pour que les preuves numériques collectées (logs, images disques) soient acceptées par les services d'enquête (OCLCTIC, C3N) ou les tribunaux, les procédures FRAP doivent garantir :

1.  **L'Intégrité :** Usage de fonctions de hachage (SHA-256) avant et après toute copie pour prouver que la donnée n'a pas été altérée.
2.  **La Traçabilité (Chain of Custody) :** Chaque action sur la preuve doit être documentée (qui, quand, quoi, comment) dans un procès-verbal ou un journal sécurisé.
3.  **La Préservation :** Les supports originaux doivent être mis sous scellés (Write-Blocker) et une copie de travail doit être utilisée pour l'analyse.

**Référence :** Norme **ISO/IEC 27037** (Lignes directrices pour l'identification, la collecte, l'acquisition et la préservation de preuves numériques).

---

<a name="dossier11"></a>
## `📘`・Dossier 11 ・ Collecte & Conservation des preuves (Forensic)

* **Source :** `Cours11-CEJMA-PreuvesNumériques.pdf`
* **Contexte :** Évaluation des capacités de Cibeco à collecter et conserver des preuves numériques recevables en justice.

<a name="d11q1"></a>
### 5.1. Conformité des moyens techniques de collecte (Q1)

L'analyse de l'infrastructure de journalisation (Syslog) révèle des points forts mais aussi des lacunes critiques pour la conformité forensique.

#### `✅`・Points de conformité (Bonnes pratiques) : 
*   **Centralisation :** Utilisation d'un serveur Syslog dédié (Kiwi) évitant le stockage local volatil.
*   **Redondance :** Existence de deux serveurs de logs.
*   **Synchronisation :** Utilisation du protocole NTP (Network Time Protocol) garantissant un horodatage cohérent, essentiel pour la corrélation d'événements.

#### `❌`・Non-conformités critiques : 
*   **Absence de Chiffrement :** Les logs transitent et sont stockés en clair.
    *   *Violation :* **[RGPD Art. 32](https://www.cnil.fr/fr/reglement-europeen-protection-donnees/chapitre4#Article32)** (Sécurité du traitement).
*   **Absence de Signature :** Aucune garantie d'intégrité (pas de Hachage/Signature électronique).
    *   *Violation :* **[Code de Procédure Pénale Art. 803](https://www.legifrance.gouv.fr/codes/article_lc/LEGIARTI000006578342)** (Recevabilité de la preuve).

---

<a name="d11q2"></a>
### 5.2. Analyse de la complétude des événements (Q2)

La liste des événements collectés par le serveur Kiwi (Doc 3) est insuffisante pour mener une investigation complète.

#### `📉`・Événements manquants (Gap Analysis)

Selon les recommandations de l'**ANSSI** et la norme **ISO 27037**, une journalisation efficace doit inclure :

1.  **Gestion des identités :** Création/Suppression de comptes, modifications de droits (Manquant).
2.  **Élévation de privilèges :** Usage de commandes `sudo` ou accès `root` (Manquant - Critique pour détecter un *insider*).
3.  **Accès aux fichiers sensibles :** Lecture/Écriture sur des fichiers de configuration ou des bases de données (Manquant).
4.  **Activité périphérique :** Connexion de clés USB ou disques externes (Manquant - Vecteur d'exfiltration).

---

<a name="d11q3"></a>
### 5.3. Durabilité et viabilité des supports de stockage (Q3)

La politique de rotation des sauvegardes est juridiquement dangereuse.

#### `🛑`・Analyse de la rotation hebdomadaire
Cibeco pratique une rotation des supports (bandes ou disques) sur une période d'une semaine. Cela signifie que les preuves sont écrasées tous les 7 jours.

*   **Problème Juridique :** L'**[Article L123-22 du Code de Commerce](https://www.legifrance.gouv.fr/codes/article_lc/LEGIARTI000006221311)** impose une conservation des documents comptables et pièces justificatives (dont les logs de transactions) pendant **10 ans**.
*   **Risque Pénal :** La destruction volontaire ou par négligence de preuves peut être qualifiée d'entrave à la justice ou de destruction de preuves (**[Code Pénal Art. 434-4](https://www.legifrance.gouv.fr/codes/article_lc/LEGIARTI000006418587)**).

**Recommandation :** Passer à un archivage long terme (WORM - *Write Once Read Many*) pour garantir l'immuabilité sur la durée légale.

---

<a name="d11q4"></a>
### 5.4. Résilience et sécurité du site de conservation (Q4)

L'audit du site de conservation (Doc 6) montre une vulnérabilité physique inacceptable pour un hébergeur.

#### `🏗️`・Audit de robustesse
*   **Localisation :** Salle unique (S02), pas de site de repli distant. En cas de sinistre majeur (incendie, inondation), toutes les preuves sont perdues.
*   **Normes non respectées :**
    *   **ISO 22301 (Continuité) :** Exige une redondance géographique (> 10 km) pour les données critiques.
    *   **SecNumCloud (ANSSI) :** Recommande des datacenters de niveau Tier III ou IV (redondance électrique et climatique totale).

---

<a name="annexes"></a>
## `📎`・ Annexes ・ Références juridiques & techniques

Cette section regroupe les textes réglementaires et normatifs cités tout au long du dossier.

### `⚖️`・Textes de Loi (France & UE)
*   **[Règlement (UE) 2016/679 (RGPD)](https://eur-lex.europa.eu/legal-content/FR/TXT/?uri=CELEX%3A32016R0679)** : Règlement Général sur la Protection des Données.
*   **[Loi n° 2004-575 (LCEN)](https://www.legifrance.gouv.fr/loda/id/JORFTEXT000000801164/)** : Loi pour la Confiance dans l'Économie Numérique (Obligations des hébergeurs).
*   **[Code Pénal - Art. 323-1 à 323-7](https://www.legifrance.gouv.fr/codes/section_lc/LEGITEXT000006070719/LEGISCTA000006165323)** : Atteintes aux Systèmes de Traitement Automatisé de Données (STAD).
*   **[Code Pénal - Art. 226-16 à 226-24](https://www.legifrance.gouv.fr/codes/section_lc/LEGITEXT000006070719/LEGISCTA000006165315)** : Atteintes aux droits de la personne résultant des fichiers ou des traitements informatiques.
*   **[Code de Commerce - Art. L123-22](https://www.legifrance.gouv.fr/codes/article_lc/LEGIARTI000006221311)** : Obligations comptables et conservation des documents (10 ans).

### `🛠️`・Normes & Référentiels
*   **ISO/IEC 27001:2022** : Systèmes de management de la sécurité de l'information (SMSI).
*   **ISO/IEC 27037:2012** : Directives pour l'identification, la collecte, l'acquisition et la préservation de preuves numériques.
*   **ISO 22301:2019** : Sécurité et résilience ・ Systèmes de management de la continuité d'activité.
*   **[ANSSI - Guide d'hygiène informatique](https://www.ssi.gouv.fr/guide/guide-dhygiene-informatique/)** : Bonnes pratiques essentielles pour la sécurité des SI.

---

