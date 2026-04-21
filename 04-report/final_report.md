\# Rapport d'analyse de sécurité mobile  

\## LAB 8 — BeVigil \& Yaazhini



\### 1. Introduction

Dans le cadre de ce laboratoire, une analyse de la posture de sécurité d'une application mobile Android a été réalisée en utilisant deux outils complémentaires :

\- BeVigil (analyse externe / OSINT)

\- Yaazhini (analyse interne statique)



L’objectif est d’identifier les éléments exposés et les vulnérabilités potentielles.



\---



\### 2. Informations générales



\- Application: InsecureBankv2  

\- Package: com.android.insecurebankv2  

\- Type: APK pédagogique  

\- Analyste: LAHDIRI Youness  



\---



\### 3. Méthodologie



L’analyse a été réalisée en trois phases :



\#### 3.1 Analyse externe (BeVigil)

Identification des assets exposés :

\- endpoints

\- domaines

\- technologies

\- indicateurs de fuite



\#### 3.2 Analyse interne (Yaazhini)

Analyse du contenu APK :

\- code source

\- configuration Android

\- stockage des données

\- permissions



\#### 3.3 Triage

\- fusion des résultats

\- suppression des doublons

\- classification des vulnérabilités



\---



\### 4. Résultats BeVigil



\- Score sécurité: 7.4 / 10 (Average)



\#### Vulnérabilités identifiées

\- Stockage de données sensibles

\- Données sensibles dans les logs

\- Activités exportées

\- Secret potentiel détecté

\- Communication HTTP non sécurisée



\---



\### 5. Résultats Yaazhini



\#### Informations techniques

\- Min SDK: 15 (obsolète)

\- Target SDK: 22 (obsolète)



\#### Vulnérabilités internes

\- Données sensibles stockées localement

\- Logs contenant informations sensibles

\- Présence possible de secrets dans le code

\- Utilisation de HTTP non sécurisé

\- Composants Android exportés



\---



\### 6. Triage des résultats



\#### Vulnérabilités confirmées

\- Stockage de données sensibles

\- Logs exposant des informations

\- Communication HTTP non sécurisée

\- Activités exportées



\#### Vulnérabilités potentielles

\- Présence de secrets dans le code

\- Exposition d’endpoints API



\---



\### 7. Mapping OWASP Mobile Top 10



\- M2: Insecure Data Storage  

\- M3: Insecure Communication  

\- M5: Insufficient Cryptography  

\- M6: Insecure Authorization  

\- M9: Reverse Engineering  



\---



\### 8. Analyse des risques



Les vulnérabilités identifiées peuvent entraîner :

\- fuite de données sensibles

\- interception des communications (attaque MITM)

\- accès non autorisé aux composants internes

\- exploitation via reverse engineering



\---



\### 9. Recommandations



\- Chiffrer les données sensibles stockées localement

\- Supprimer toute information sensible des logs

\- Utiliser HTTPS pour toutes les communications

\- Restreindre les composants exportés

\- Mettre à jour les versions SDK

\- Protéger les clés API et secrets



\---



\### 10. Conclusion



L’application InsecureBankv2 présente une posture de sécurité faible caractérisée par :

\- une mauvaise gestion des données sensibles

\- une communication non sécurisée

\- une configuration Android obsolète



Ces faiblesses augmentent significativement le risque de compromission.



\---



\### 11. Outils utilisés



\- BeVigil  

\- Yaazhini  

\- PowerShell  



\---



\### 12. Traçabilité



Toutes les commandes et étapes ont été enregistrées dans :

\- commands.log  

\- analyse\_info.txt  



