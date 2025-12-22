# Charte de Codage - SailPerformance

Ce document définit les conventions de codage pour le projet SailPerformance.

---

## 1. Conventions de Nommage

### Fichiers
- Classes : `PascalCase.kt` (ex: `MainActivity.kt`, `SensorFusion.kt`)
- Ressources : `snake_case.xml` (ex: `strings.xml`, `ic_launcher.png`)

### Code Kotlin
| Type | Convention | Exemple |
|------|------------|---------|
| Classes | PascalCase | `DashboardViewModel` |
| Fonctions | camelCase | `calculateSpeed()` |
| Variables | camelCase | `currentPosition` |
| Constantes | SCREAMING_SNAKE_CASE | `GPS_UPDATE_INTERVAL` |
| Packages | lowercase | `com.sailperformance.ui` |

### Composables
- Préfixe fonction : PascalCase (car retourne du contenu UI)
- Pattern : `NomScreen`, `NomCard`, `NomButton`

```kotlin
@Composable
fun DashboardScreen() { ... }

@Composable
fun MetricCard(value: String) { ... }
```

---

## 2. Structure des Fichiers

### Organisation d'un fichier Kotlin
```kotlin
// 1. Package
package com.sailperformance.ui

// 2. Imports (groupés par type)
import android.* 
import androidx.*
import com.sailperformance.*
import kotlinx.*

// 3. Constantes top-level (si nécessaire)
private const val TAG = "DashboardScreen"

// 4. Classes / Fonctions
class MyClass { ... }
```

### Longueur
- Ligne max : **120 caractères**
- Fonction max : **50 lignes** (sinon découper)
- Fichier max : **500 lignes** (sinon découper en modules)

---

## 3. Documentation

### KDoc pour les fonctions publiques
```kotlin
/**
 * Calcule la vitesse fond (SOG) à partir des données GPS.
 *
 * @param previousPoint Point GPS précédent
 * @param currentPoint Point GPS actuel
 * @return Vitesse en nœuds
 */
fun calculateSOG(previousPoint: GeoPoint, currentPoint: GeoPoint): Double {
    // ...
}
```

### Commentaires
- Anglais pour le code
- Français OK pour les commentaires explicatifs si nécessaire
- Éviter les commentaires évidents (`// incrémente i` ❌)

---

## 4. Architecture

### Layers (à implémenter progressivement)
```
presentation/  → UI Compose, ViewModels
domain/        → Modèles, interfaces repository
data/          → Implémentations, DB, capteurs
```

### Règles de dépendance
- `presentation` → peut dépendre de `domain`
- `data` → peut dépendre de `domain`
- `domain` → **ne dépend de rien** (cœur isolé)

---

## 5. Gestion des Erreurs

### Pattern Result
```kotlin
sealed class Result<out T> {
    data class Success<T>(val data: T) : Result<T>()
    data class Error(val exception: Throwable) : Result<Nothing>()
}
```

### Logging
- Utiliser Timber (ou Log avec TAG)
- Pas de `println()` en production

---

## 6. Tests

### Nommage des tests
```kotlin
@Test
fun `calculateSOG returns zero when points are identical`() {
    // ...
}
```

### Structure AAA
```kotlin
@Test
fun exampleTest() {
    // Arrange
    val input = ...
    
    // Act
    val result = function(input)
    
    // Assert
    assertEquals(expected, result)
}
```

---

## 7. Git

### Branches
- `main` : production stable
- `develop` : intégration
- `feature/xxx` : nouvelles fonctionnalités
- `fix/xxx` : corrections

### Commits
Format : `type: description courte`

Types :
- `feat:` nouvelle fonctionnalité
- `fix:` correction de bug
- `refactor:` refactoring sans changement fonctionnel
- `docs:` documentation
- `test:` ajout/modification de tests

Exemple :
```
feat: add GPS location provider
fix: correct roll calculation overflow
```

---

## 8. TODO

À compléter au fur et à mesure du développement :
- [ ] Règles Detekt/Ktlint
- [ ] CI/CD pipeline
- [ ] Règles ProGuard
