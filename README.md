#  Analyse de Sécurité Mobile avec MobSF

---

##  Informations générales

| Champ | Valeur |
|---|---|
| **Application analysée** | PizzaRecipes |
| **Package** | `com.example.pizzarecipes` |
| **Date d'analyse** | 2026-05-02 |
| **Analyste** | sara Essaidi |
| **Outil** | MobSF |
| **Environnement** | VM Mobexler |
| **Hash SHA-256** | `458ac7460ecaa4c8943e1351ae3a53735a9accd519f3c36d8650b81d9aff4f0f` |

---

##  Début de séance

Les prérequis du laboratoire ont été respectés :

- VM Mobexler démarrée et fonctionnelle
  <img width="959" height="548" alt="image" src="https://github.com/user-attachments/assets/9e40d11c-2bfe-46ae-8a59-4ad744d77bf8" />

- APK pédagogique disponible
- Création du dossier de travail dédié à l'analyse :

```bash
mkdir -p ~/apk_analysis/$(date +%Y-%m-%d)
cd ~/apk_analysis/$(date +%Y-%m-%d)
```
<img width="670" height="153" alt="image" src="https://github.com/user-attachments/assets/1b2a9b9d-2087-457b-9884-1d2ba8e6ea56" />

- Copie de l'APK dans le dossier de travail

<img width="680" height="71" alt="image" src="https://github.com/user-attachments/assets/3d90dfff-805a-4710-a3d7-25d9af576eec" />

- Vérification de l'intégrité de l'APK via SHA-256
<img width="648" height="281" alt="image" src="https://github.com/user-attachments/assets/feb2bb0d-2c04-48d1-b6e1-5a41a03b10c9" />

- Création d'un fichier de traçabilité (`analyse_info.txt`)
<img width="634" height="289" alt="image" src="https://github.com/user-attachments/assets/2d41d1fd-4d9e-403c-90c3-ca84aef9c91f" />

<img width="712" height="157" alt="image" src="https://github.com/user-attachments/assets/0f1d4571-c0f1-4360-b236-57ba83600f74" />

- Compréhension des objectifs du laboratoire et du périmètre de sécurité

---

##  Task 1 — Préparation de l'environnement

- Organisation du dossier d'analyse
- Vérification de la taille de l'APK
- Calcul du hash pour garantir l'intégrité
- Documentation des informations dans `analyse_info.txt`

---

##  Task 2 — Lancement de MobSF

- Lancement de MobSF depuis la VM
  <img width="473" height="361" alt="image" src="https://github.com/user-attachments/assets/5824bcab-67d8-4d1f-b85f-bdce449944bb" />

- Accès à l'interface web via navigateur
  <img width="560" height="374" alt="image" src="https://github.com/user-attachments/assets/98d17fca-41ac-42f5-bc5b-392bff08a83b" />

- Vérification du bon fonctionnement de l'outil
<img width="541" height="344" alt="image" src="https://github.com/user-attachments/assets/3ef66412-06a1-4634-b171-14b60c638879" />

---

##  Task 3 — Import et analyse de l'APK

- Upload de l'APK dans MobSF
  <img width="498" height="365" alt="image" src="https://github.com/user-attachments/assets/5300f862-eb41-4421-8dfd-0c19988ea703" />

- Lancement de l'analyse statique
- Génération automatique d'un rapport
<img width="756" height="379" alt="image" src="https://github.com/user-attachments/assets/0c5de515-8efd-4059-96b7-b342ca776049" />

---

##  Task 4 — Analyse du manifest et permissions

###  Observations principales

- Application en mode debug (`debuggable=true`)
- Sauvegarde activée (`allowBackup=true`)
- Composants exportés (`exported=true`)
<img width="742" height="327" alt="image" src="https://github.com/user-attachments/assets/615b09f6-2a4f-4fd9-bd2a-964068def7ad" />
<img width="494" height="300" alt="image" src="https://github.com/user-attachments/assets/6ba328f7-579c-4f19-b483-3a7aec2aabbb" />

###  Permissions

- Aucune permission dangereuse détectée
- Présence d'une permission custom sécurisée
<img width="765" height="311" alt="image" src="https://github.com/user-attachments/assets/77e665a4-dffc-4bdd-afa3-fc38c69961e9" />

###  Conclusion

- Mauvaises configurations de sécurité identifiées
- Surface d'attaque augmentée

---

##  Task 5 — Analyse de la configuration réseau

- Absence de `network_security_config.xml`
- Paramètre `usesCleartextTraffic` non défini
- Aucun endpoint détecté


> **Conclusion :** configuration réseau par défaut, potentiellement non sécurisée.

---

##  Task 6 — Analyse du code et des ressources

- Aucune vulnérabilité détectée dans le code
  <img width="491" height="356" alt="image" src="https://github.com/user-attachments/assets/595aba48-e397-470e-9bb1-abbcb3f82e79" />

- Aucun secret hardcodé
- Aucun endpoint exposé
<img width="739" height="349" alt="image" src="https://github.com/user-attachments/assets/68f00ac8-ab4d-4dfa-9b4d-281d7aa2274d" />

> **Conclusion :** code propre, mais problèmes de configuration.

---

##  Task 7 — Corrélation OWASP MASVS

| Vulnérabilité | Référence MASVS |
|---|---|
| Debug activé | `MSTG-RESILIENCE-1` |
| Backup activé | `MSTG-STORAGE-1` |
| Composants exportés | `MSTG-PLATFORM-1` |
<img width="464" height="265" alt="image" src="https://github.com/user-attachments/assets/85b0770f-3be8-4d10-a49a-fe9a787e31f2" />

<img width="802" height="213" alt="image" src="https://github.com/user-attachments/assets/95369f31-00af-47e6-8a5a-52d140f20f8b" />

<img width="821" height="242" alt="image" src="https://github.com/user-attachments/assets/2016b5e3-d47e-4033-8f34-fe33034c606e" />
<img width="796" height="286" alt="image" src="https://github.com/user-attachments/assets/55a33239-49b6-4b74-ad11-cf7d485f4e06" />

---

##  Task 8 — Export du rapport

- Génération du rapport PDF via MobSF
- Sauvegarde dans le dossier d'analyse
- Utilisation pour identifier les vulnérabilités critiques
<img width="1069" height="511" alt="image" src="https://github.com/user-attachments/assets/0619a21a-553d-47d0-bb12-51dde1efa600" />

<img width="1126" height="255" alt="image" src="https://github.com/user-attachments/assets/a970c5b5-4cf0-478e-b82b-7021c8d8f35f" />

---

##  Task 9 — Synthèse et rapport final

###  Résumé exécutif

L'analyse révèle un **niveau de risque global élevé**. Les vulnérabilités identifiées concernent principalement des erreurs de configuration.

###  Vulnérabilités principales

####  Mode debug activé
- **Sévérité :** Élevée
- **Impact :** Facilite le reverse engineering

####  Support Android vulnérable
- **Sévérité :** Élevée
- **Impact :** Exploitation de vulnérabilités connues

####  Sauvegarde activée
- **Sévérité :** Moyenne
- **Impact :** Fuite de données

####  Composants exportés
- **Sévérité :** Moyenne
- **Impact :** Accès externe non contrôlé
<img width="597" height="381" alt="image" src="https://github.com/user-attachments/assets/44d77b0c-a7ca-4c07-b3df-68358c4f8397" />

###  Recommandations

1. Désactiver le mode debug en production
2. Désactiver la sauvegarde des données
3. Restreindre les composants exportés
4. Augmenter la version minimale Android
5. Implémenter une configuration réseau sécurisée

---

##  Annexes

### Permissions

- Aucune permission dangereuse

### Composants exportés

- `SplashActivity`
- `ProfileInstallReceiver`

### Endpoints

- Aucun

---

---

##  Conclusion

L'application présente des vulnérabilités liées à la **configuration**. Une correction de ces éléments permettrait d'améliorer significativement la sécurité globale.
