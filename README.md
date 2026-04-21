# LAB 8 — Analyse de posture et exposition d'applications mobiles (BeVigil & Yaazhini)

## Objectif
Ce laboratoire vise à analyser la surface d’attaque d’une application mobile Android en combinant :
- une analyse externe (OSINT) avec BeVigil
- une analyse interne (statique) avec Yaazhini

L’objectif est d’identifier les éléments exposés, les vulnérabilités potentielles et de les corréler avec les standards OWASP.

---

## Application analysée
- Nom: InsecureBankv2
- Package: com.android.insecurebankv2
- Type: APK pédagogique

---

## Structure du projet

lab-mobile-security/

├── 00-scope/  
│   └── scope.md  
├── 01-bevigil/  
│   ├── bevigil_export.json  
│   ├── bevigil_summary.txt  
│   └── bevigil_notes.md  
├── 02-yaazhini/  
│   └── yaazhini_notes.txt  
├── 03-triage/  
│   └── triage.md  
├── 04-report/  
├── analyse_info.txt  
└── commands.log  

---
<img width="1662" height="591" alt="Screenshot 2026-04-21 170708" src="https://github.com/user-attachments/assets/6be204e7-9a21-41a5-bc6c-ab802eeb5dc7" />

## Étapes réalisées

### 1. Définition du périmètre
- Cible: APK pédagogique autorisé
- Aucune exploitation ni test intrusif

---

### 2. Analyse BeVigil (externe)

#### Résultats
- Score sécurité: 7.4 (Average)
- Vulnérabilités détectées:
  - Stockage de données sensibles (SharedPreferences)
  - Données sensibles dans les logs
  - Activité exportée
  - Secret potentiel détecté
  - Client HTTP non sécurisé
<img width="1884" height="867" alt="Screenshot 2026-04-21 172340" src="https://github.com/user-attachments/assets/c866784a-3cb6-4793-8c30-9d0b7a247216" />

#### Analyse
BeVigil met en évidence des faiblesses liées à l’exposition externe et à la mauvaise gestion des données.

---

### 3. Analyse Yaazhini (interne)

#### Informations
- Min SDK: 15 (obsolète)
- Target SDK: 22 (obsolète)

#### Vulnérabilités
- Données sensibles stockées localement
- Logs exposant des informations
- Présence possible de secrets
- Utilisation de HTTP non sécurisé
- Composants Android exportés

#### Analyse
Yaazhini confirme les problèmes internes liés à :
- la sécurité du stockage
- la configuration Android
- la communication réseau

---
<img width="1901" height="968" alt="Screenshot 2026-04-21 174028" src="https://github.com/user-attachments/assets/a3e84c02-482e-4c34-8dc9-907378c78e30" />

### 4. Triage des résultats

#### Vulnérabilités confirmées
- Stockage de données sensibles
- Logs contenant informations sensibles
- HTTP non sécurisé
- Activités exportées

#### Vulnérabilités potentielles
- Secrets dans le code
- Endpoints exposés

#### Conclusion
Les résultats des deux outils sont cohérents et confirment une mauvaise posture de sécurité globale.

---

## Mapping OWASP Mobile Top 10

- M2: Insecure Data Storage → SharedPreferences
- M3: Insecure Communication → HTTP non sécurisé
- M4: Insecure Authentication → possible (selon endpoints)
- M5: Insufficient Cryptography → absence de chiffrement
- M6: Insecure Authorization → activités exportées
- M9: Reverse Engineering → code facilement analysable

---

## Conclusion générale

L’application InsecureBankv2 présente plusieurs faiblesses critiques :

- mauvaise gestion des données sensibles
- utilisation de technologies obsolètes
- communication non sécurisée
- exposition de composants internes

Ces vulnérabilités peuvent entraîner :
- fuite de données utilisateur
- accès non autorisé
- interception des communications

---
<img width="593" height="699" alt="image" src="https://github.com/user-attachments/assets/3538e6fa-a368-44f9-903c-2270b117eced" />

## Task 8 — Corrélation OWASP

### Objectif
Associer les vulnérabilités identifiées avec les catégories OWASP Mobile Top 10 afin de standardiser l’analyse.

### Fichier généré
03-triage/owasp_mapping.md

### Résultats

#### M2 - Insecure Data Storage
- Stockage de données sensibles (SharedPreferences)
- Données non chiffrées

#### M3 - Insecure Communication
- Utilisation de HTTP non sécurisé
- Risque d’interception (MITM)

#### M5 - Insufficient Cryptography
- Absence de chiffrement des données sensibles

#### M6 - Insecure Authorization
- Activités Android exportées
- Accès non contrôlé

#### M9 - Reverse Engineering
- Application facilement analysable
- Présence potentielle de secrets dans le code

### Conclusion OWASP
L’application présente plusieurs vulnérabilités critiques alignées avec OWASP Mobile Top 10, indiquant une posture de sécurité faible.

---
<img width="995" height="623" alt="Screenshot 2026-04-21 174953" src="https://github.com/user-attachments/assets/37448dda-35c0-41a9-96f9-40ab8bbcd535" />

## Task 9 — Rapport final

### Objectif
Produire un rapport structuré résumant toute l’analyse réalisée.

### Fichier généré
04-report/final_report.md

### Contenu du rapport

#### 1. Introduction
Présentation de l’analyse et des outils utilisés.

#### 2. Informations générales
- Application: InsecureBankv2
- Package: com.android.insecurebankv2

#### 3. Méthodologie
- Analyse externe (BeVigil)
- Analyse interne (Yaazhini)
- Triage des résultats

#### 4. Résultats BeVigil
- Score: 7.4
- Vulnérabilités liées à l’exposition externe

#### 5. Résultats Yaazhini
- SDK obsolètes
- Vulnérabilités internes

#### 6. Triage
- Vulnérabilités confirmées
- Vulnérabilités potentielles

#### 7. Mapping OWASP
- Correspondance avec OWASP Mobile Top 10

#### 8. Analyse des risques
- Fuite de données
- MITM
- Accès non autorisé

#### 9. Recommandations
- Chiffrement des données
- Utilisation HTTPS
- Sécurisation des composants
- Mise à jour SDK

#### 10. Conclusion
Posture de sécurité faible avec plusieurs risques critiques.

---

## Résultat final attendu

lab-mobile-security/

├── 03-triage/
│   ├── triage.csv
│   └── owasp_mapping.md
│
├── 04-report/
│   └── final_report.md

---
## Outils utilisés

- BeVigil (analyse OSINT)
- Yaazhini (analyse statique APK)
- PowerShell (gestion et traçabilité)

---

## Auteur

LAHDIRI Youness  
LAB 8 — Sécurité des applications mobiles
