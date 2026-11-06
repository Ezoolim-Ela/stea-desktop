# STEA — Application de bureau Windows

**STEA** est une application de gestion logistique et de suivi des stocks développée pour
une entreprise de Lomé (Togo), en production depuis août 2026.

Ce dépôt est le **canal de distribution de l'application de bureau** : il héberge les
installeurs Windows dans les [Releases](https://github.com/Ezoolim-Ela/stea-desktop/releases)
et sert les **mises à jour automatiques** (OTA) à tous les postes installés.
Le code source du back-end et de l'interface se trouve dans
[`stea_stock_application`](https://github.com/Ezoolim-Ela/stea_stock_application).

[![Dernière version](https://img.shields.io/github/v/release/Ezoolim-Ela/stea-desktop?label=derni%C3%A8re%20version&color=6D28D9)](https://github.com/Ezoolim-Ela/stea-desktop/releases/latest)
[![Téléchargements](https://img.shields.io/github/downloads/Ezoolim-Ela/stea-desktop/total?label=t%C3%A9l%C3%A9chargements&color=5B21B6)](https://github.com/Ezoolim-Ela/stea-desktop/releases)

---

## Fonctionnalités

- **Stock multi-entrepôts** avec lots, numéros de série et seuils d'alerte.
- **Achats et ventes** : bons de commande, livraisons, bons de livraison, retours et avoirs.
- **Inventaires** et réinitialisations de stock tracées.
- **Réapprovisionnement** : alertes automatiques de stock critique.
- **Comptabilité** et encaissements, statistiques et rapports exportables.
- **8 rôles utilisateurs** (administrateur, opérateur de stock, logisticien, planificateur
  transport, comptable, agents commercial / biomédical / informatique en consultation seule),
  permissions fines et **journal d'audit**.
- Messagerie interne, notifications, guide d'utilisation intégré.

## En chiffres

| 24 | 8 | 173 | 141 | 29+ |
| :---: | :---: | :---: | :---: | :---: |
| modules métier | rôles utilisateurs | endpoints REST | tests automatisés | versions publiées |

---

## Architecture

```
┌──────────────────────────────┐        HTTPS         ┌──────────────────────────────┐
│  Application de bureau       │ ───────────────────▶ │  Serveur STEA                │
│  Electron + electron-updater │                      │  Spring Boot 3 · Java 17     │
│  embarque l'interface React  │ ◀─────────────────── │  API REST sécurisée par JWT  │
└──────────────┬───────────────┘        JSON          │  MySQL                       │
               │ mises à jour automatiques            └──────────────────────────────┘
               ▼
   GitHub Releases de ce dépôt (latest.yml + STEA-Setup-x.y.z.exe)
```

- **Interface** : React, Tailwind CSS, Recharts — embarquée dans le programme Windows.
- **Serveur** : API REST Spring Boot / MySQL, authentification JWT, rôles et permissions.
- **Distribution** : installeur NSIS construit avec `electron-builder` ; à chaque lancement,
  `electron-updater` compare la version installée à la dernière release et se met à jour
  en tâche de fond.
- **Configuration** : le fichier [`config.json`](config.json) de ce dépôt indique l'adresse
  du serveur ; l'application le lit au démarrage, ce qui permet de changer de serveur sans
  republier de version.

---

## Installation

1. Téléchargez `STEA-Setup-x.y.z.exe` depuis la
   [dernière release](https://github.com/Ezoolim-Ela/stea-desktop/releases/latest).
2. Double-cliquez sur l'installeur. L'installeur n'est pas signé numériquement : si Windows
   affiche « Windows a protégé votre ordinateur », cliquez sur **Informations complémentaires**
   puis **Exécuter quand même**.
3. L'application s'installe sans droits administrateur, crée un raccourci sur le bureau et se lance.
4. Connectez-vous avec le compte fourni par l'administrateur de votre entreprise.

Les versions suivantes s'installent **automatiquement** au lancement suivant : aucune
réinstallation n'est nécessaire.

---

## Auteure

**Ago Ezoolim-Ela** — étudiante en Génie Logiciel & Systèmes d'Information à l'IAI-TOGO.
Conception et développement de l'ensemble : back-end, interface, application de bureau et déploiement.

- Portfolio : https://ezoolim-ela.github.io/Portfolio/
- GitHub : https://github.com/Ezoolim-Ela

## Licence

Logiciel propriétaire. Tous droits réservés.
