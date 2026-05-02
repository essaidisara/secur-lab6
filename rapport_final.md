# Rapport d'analyse statique - PizzaRecipes

## Informations générales
- **Date d'analyse :** 2026-05-02
- **Analyste :** sara Essaidi
- **APK analysé :** app-debug.apk (SHA-256: 458ac7460ecaa4c8943e1351ae3a53735a9accd519f3c36d8650b81d9aff4f0f)
- **Version :** 1.0
- **Outils utilisés :** MobSF dans VM Mobexler

---

## Résumé exécutif
L'analyse statique de l'application PizzaRecipes révèle un niveau de risque global **élevé**.  
Les principales vulnérabilités concernent le mode debug activé, la sauvegarde des données et l'exposition de composants exportés.  
Aucune vulnérabilité critique n'a été détectée dans le code, mais plusieurs erreurs de configuration peuvent exposer l'application à des attaques.

---

## Vulnérabilités critiques

### 1. Mode debug activé
- **Sévérité :** Élevée
- **Catégorie MASVS :** MSTG-RESILIENCE-1
- **Description :** L'application est déboguable en production.
- **Preuve :** android:debuggable=true dans AndroidManifest.xml
- **Impact :** Facilite le reverse engineering et l'analyse par un attaquant.
- **Remédiation :** Désactiver le mode debug en production.

---

### 2. Support des versions Android vulnérables
- **Sévérité :** Élevée
- **Catégorie MASVS :** MSTG-PLATFORM-1
- **Description :** L'application supporte des versions Android anciennes (minSdk=24).
- **Preuve :** android:minSdkVersion=24
- **Impact :** Exposition à des vulnérabilités connues non corrigées.
- **Remédiation :** Augmenter la version minimale Android (API ≥ 29).

---

### 3. Sauvegarde des données activée
- **Sévérité :** Moyenne
- **Catégorie MASVS :** MSTG-STORAGE-1
- **Description :** Les données peuvent être sauvegardées via ADB.
- **Preuve :** android:allowBackup=true
- **Impact :** Risque de fuite de données utilisateur.
- **Remédiation :** Désactiver allowBackup.

---

### 4. Composants exportés accessibles
- **Sévérité :** Moyenne
- **Catégorie MASVS :** MSTG-PLATFORM-1
- **Description :** Certains composants sont accessibles par d'autres applications.
- **Preuve :** android:exported=true (SplashActivity, Receiver)
- **Impact :** Accès externe non autorisé possible.
- **Remédiation :** Restreindre l'accès ou ajouter des permissions.

---

## Autres observations
- Aucune vulnérabilité détectée dans le code source
- Aucun secret hardcodé identifié
- Aucune permission dangereuse détectée
- Aucune configuration réseau spécifique définie

---

## Recommandations prioritaires
1. Désactiver android:debuggable en production
2. Désactiver android:allowBackup
3. Restreindre les composants exportés
4. Augmenter minSdkVersion
5. Mettre en place une configuration réseau sécurisée

---

## Annexes

### Permissions dangereuses
- Aucune

### Composants exportés
- SplashActivity
- ProfileInstallReceiver

### Endpoints identifiés
- Aucun
