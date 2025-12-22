# SailPerformance

Application Android de suivi de performance nautique pour amateurs de voile.

## Description

SailPerformance est une application mobile qui permet aux plaisanciers de :
- Suivre leur position GPS en temps réel
- Visualiser les données de navigation (COG, SOG)
- Mesurer l'attitude du bateau (roulis, tangage) via les capteurs IMU
- Enregistrer et rejouer des traces
- Afficher les données sur une carte

## Fonctionnalités MVP (Phase 1)

- [ ] Collecte GPS temps réel (1 Hz)
- [ ] Collecte IMU (accéléromètre + gyroscope à 100 Hz)
- [ ] Fusion sensorielle (Filtre Complémentaire) → Roll/Pitch
- [ ] Dashboard live : COG, SOG, Roll, Pitch, Position
- [ ] Carte Google Maps temps réel
- [ ] Enregistrement traces SQLite
- [ ] Rejeu des traces
- [ ] Graphiques (COG/SOG/Roll/Pitch vs temps)
- [ ] Paramètres utilisateur

## Stack Technique

| Composant | Technologie |
|-----------|-------------|
| Langage | Kotlin 2.1 |
| UI | Jetpack Compose |
| Navigation | Compose Navigation |
| Base de données | SqlDelight |
| Networking | Ktor Client |
| DI | Koin |
| Cartes | Google Maps Compose |

## Prérequis

- Android Studio Ladybug (2024.2.1) ou plus récent
- JDK 17
- Android SDK 35
- Émulateur ou appareil Android API 26+

## Installation

```bash
# Cloner le projet
git clone <repo-url>
cd SailPerformance

# Ouvrir dans Android Studio
# Ou compiler en ligne de commande :
./gradlew build

# Installer sur émulateur/appareil
./gradlew installDebug
```

## Configuration Google Maps

1. Aller sur [Google Cloud Console](https://console.cloud.google.com/)
2. Créer un projet et activer Maps SDK for Android
3. Générer une API Key
4. Ajouter dans `local.properties` :
   ```
   MAPS_API_KEY=votre_clé_ici
   ```

## Structure du Projet

```
SailPerformance/
├── app/src/main/
│   ├── kotlin/com/sailperformance/
│   │   └── MainActivity.kt          # Point d'entrée
│   ├── res/
│   │   └── values/
│   └── AndroidManifest.xml
├── build.gradle.kts
├── settings.gradle.kts
├── CODING_GUIDELINES.md              # Charte de codage
└── README.md
```

## Licence

Propriétaire - Tous droits réservés

## Auteur

Moi
