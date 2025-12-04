# `💼`・Devoir 2 — BTS SIO SISR 2ᵉ année

**Thématiques :** Protection des données (DCP) • Identité numérique • Preuve électronique • Sécurité des équipements • Obligations légales.

Ce dépôt regroupe l’intégralité des exercices issus des six documents fournis, entièrement traités et organisés sous forme de documentation technique structurée.
Les analyses et corrections ont été enrichies par des compléments juridiques afin de renforcer la qualité et la conformité du rendu, avec des références au RGPD, à la CNIL, au Code pénal, ainsi qu’aux cadres législatifs pertinents tels que la LCEN.

Le projet s’appuie également sur les principaux référentiels normatifs en matière de sécurité et de continuité d’activité, notamment ISO 27001 et ISO 22301, afin d’assurer une approche méthodique, rigoureuse et conforme aux bonnes pratiques.

---

## `📂`・Documents de référence

L'ensemble des travaux repose sur l'analyse des documents suivants fournis en annexe :

*   `Cours 7・CEJMA-ObligationProtectionDonnées.pdf`.
*   `Cours 8・CEJMA-DisponibilitéIntégritéConfidentialité.pdf`.
*   `Cours 9・CEJMA-ArchivageProtectionsDonnées.pdf`.
*   `Cours 10・CEJMA-ObligationsLégales.pdf`.
*   `Cours 11・CEJMA-PreuvesNumériques.pdf`.

---


## `📌`・Table des matières exhaustive

1.  [**Dossier 7** — Audit de conformité & Analyse des risques (Cibeco)](#dossier7)
    *   [1.1. Analyse de la confidentialité des archives (Q1)](#d7q1)
    *   [1.2. Analyse du risque d'indisponibilité (Q2)](#d7q2)
    *   [1.3. Classification des risques malveillants (Q4)](#d7q4)
    *   [1.4. Synthèse et plan de remédiation](#d7synthese)
2.  [**Dossier 8** — Rapport d'incident cyber (Ecotri)](#dossier8)
    *   [2.1. Conséquences techniques sur le triptyque DIC (Q1)](#d8q1)
    *   [2.2. Analyse de contagion & Risque systémique (Q2)](#d8q2)
    *   [2.3. Impacts humains, réputationnels et financiers (Q3)](#d8q3)
    *   [2.4. Responsabilité pénale & Identification de l'attaquant (Q4)](#d8q4)
3.  [**Dossier 9** — Archivage & Protection des données (Cibeco)](#dossier9)
    *   [3.1. Audit de la sécurisation physique des archives (Q1)](#d9q1)
    *   [3.2. Conformité de la traçabilité des accès (Q2)](#d9q2)
    *   [3.3. Violations légales sur le serveur critique miRDB (Q3)](#d9q3)
    *   [3.4. Analyse systémique : pourquoi le mot de passe ne suffit pas (Q4)](#d9q4)
4.  [**Dossier 10** — Procédures incidents FRAP (Cibeco)](#dossier10)
    *   [4.1. FRAP n°1 : Confidentialité des accès serveurs (Q1)](#d10q1)
    *   [4.2. FRAP n°2 : Intégrité du transfert des journaux (Q2)](#d10q2)
    *   [4.3. FRAP n°3 : Disponibilité & Respect du SLA (Q3)](#d10q3)
    *   [4.4. Exigences probatoires des autorités judiciaires (Q4)](#d10q4)
5.  [**Dossier 11** — Collecte & Conservation des preuves (Forensic)](#dossier11)
    *   [5.1. Conformité des moyens techniques de collecte (Q1)](#d11q1)
    *   [5.2. Analyse de la complétude des événements (Q2)](#d11q2)
    *   [5.3. Durabilité et viabilité des supports de stockage (Q3)](#d11q3)
    *   [5.4. Résilience et sécurité du site de conservation (Q4)](#d11q4)
6.  [**Annexes** — Références juridiques & techniques](#annexes)

***

<a name="dossier7"></a>
## `📘`・Dossier 7 — Audit de conformité & Analyse des risques (Cibeco)

**Source :** `Cours7-CEJMA-ObligationProtectionDonnées.pdf`
**Contexte :** Audit du système d'archivage de l'entreprise Cibeco.
**Statut global :** 🔴 **Non-conforme** (Risque Critique).

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

*   **[RGPD — Article 32](https://www.cnil.fr/fr/reglement-europeen-protection-donnees/chapitre4#Article32)** : Impose de mettre en œuvre des mesures techniques (telles que le chiffrement ou la pseudonymisation) pour garantir un niveau de sécurité adapté au risque.
*   **[ISO/IEC 27001 — Annexe A.9](https://www.iso.org/standard/27001)** : Exige une gestion formelle des accès utilisateurs et l'application du principe de moindre privilège (ici violé par l'usage d'un compte unique).

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
## `📘`・Dossier 8 — Rapport d'incident cyber (Ecotri)

**Source :** `Cours8-CEJMA-DisponibilitéIntégritéConfidentialité.pdf`
**Contexte :** Analyse post-mortem de l'attaque subie par le site web d'Ecotri le 11 novembre 2019.
**Typologie :** Défiguration (Defacement) et Injection SQL.

<a name="d8q1"></a>
### 2.1. Conséquences techniques sur le triptyque DIC (Q1)

L'analyse forensique de l'incident met en évidence une compromission totale des trois piliers de la sécurité de l'information (DIC).

#### `📊`・Tableau de synthèse des impacts

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

#### `⚖️`・Qualification juridique des faits

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

