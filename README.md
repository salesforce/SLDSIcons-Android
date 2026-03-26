# SLDSIcons

Salesforce Lightning Design System Icons for Android.

## Overview

SLDSIcons provides SLDS icons from the [`@salesforce-ux/icons`](https://www.npmjs.com/package/@salesforce-ux/icons) npm package for Android applications. Icons are stored as Vector Drawables with type-safe Kotlin enum APIs, preserving vector quality at any size.

### Features

- **Dynamic Categories**: All icon categories from the npm package are automatically discovered and included
- **Vector Drawables**: Icons maintain crisp quality at any size
- **Type-Safe API**: Kotlin enums provide compile-time safety for icon access
- **Jetpack Compose Support**: Easy-to-use composables for modern Android UI
- **Flexible Rendering**: Support for custom sizing and tinting

## Installation

### Gradle

Add SLDSIcons to your `build.gradle.kts`:

```kotlin
dependencies {
    implementation("com.salesforce.android.sldsicons:slds-icons:1.0.0")
}
```

Or in Groovy `build.gradle`:

```gradle
dependencies {
    implementation 'com.salesforce.android.sldsicons:slds-icons:1.0.0'
}
```

### Maven

Add SLDSIcons to your `pom.xml`:

```xml
<dependency>
    <groupId>com.salesforce.android.sldsicons</groupId>
    <artifactId>slds-icons</artifactId>
    <version>1.0.0</version>
</dependency>
```

## Usage

### Kotlin

SLDSIcons provides type-safe enums for accessing icons from different categories:

```kotlin
import com.salesforce.android.sldsicons.UtilityIcons
import com.salesforce.android.sldsicons.StandardIcons
import com.salesforce.android.sldsicons.ActionIcons
import com.salesforce.android.sldsicons.CustomIcons

// Using UtilityIcons
val addIcon = UtilityIcons.Add.getDrawable(context, size = 48)

// Using StandardIcons
val accountIcon = StandardIcons.Account.getDrawable(context, size = 64)

// Using ActionIcons
val mapIcon = ActionIcons.Map.getDrawable(context, size = 40)

// Using CustomIcons
val customIcon = CustomIcons.Custom1.getDrawable(context, size = 48)

// With custom color
val coloredIcon = UtilityIcons.Close.getDrawable(
    context = context,
    size = 32,
    color = Color.RED
)
```

### Available Icon APIs

Each icon enum provides these methods:

```kotlin
sealed interface SLDSIcon {
    val resourceName: String

    // Get the vector drawable (original colors)
    fun getVectorDrawable(context: Context): Drawable?

    // Get as Bitmap with default color
    fun getBitmap(context: Context, size: Int): Bitmap

    // Get as Bitmap with custom color
    fun getBitmap(context: Context, size: Int, @ColorInt color: Int): Bitmap

    // Get as Drawable with default color
    fun getDrawable(context: Context, size: Int): Drawable

    // Get as Drawable with custom color
    fun getDrawable(context: Context, size: Int, @ColorInt color: Int): Drawable
}
```

### Jetpack Compose

Use icons in Compose with the provided composable:

```kotlin
import androidx.compose.foundation.Image
import androidx.compose.foundation.layout.size
import androidx.compose.runtime.Composable
import androidx.compose.ui.Modifier
import androidx.compose.ui.graphics.Color
import androidx.compose.ui.graphics.ColorFilter
import androidx.compose.ui.graphics.asImageBitmap
import androidx.compose.ui.platform.LocalContext
import androidx.compose.ui.unit.Dp
import androidx.compose.ui.unit.dp
import androidx.core.graphics.drawable.toBitmap
import com.salesforce.android.sldsicons.SLDSIcon
import com.salesforce.android.sldsicons.UtilityIcons
import com.salesforce.android.sldsicons.StandardIcons

@Composable
fun SLDSIcon(
    icon: SLDSIcon,
    size: Dp,
    modifier: Modifier = Modifier,
    color: Color? = null,
    contentDescription: String? = null
) {
    val drawable = icon.getDrawable(LocalContext.current, size.value.toInt())
    Image(
        bitmap = drawable.toBitmap().asImageBitmap(),
        contentDescription = contentDescription,
        colorFilter = color?.let { ColorFilter.tint(it) },
        modifier = modifier.size(size)
    )
}

// Usage examples:
@Composable
fun IconExamples() {
    // Utility icon
    SLDSIcon(icon = UtilityIcons.Add, size = 24.dp)

    // Standard icon with custom color
    SLDSIcon(
        icon = StandardIcons.Account,
        size = 32.dp,
        color = Color(0xFF0070D2)
    )

    // Action icon with content description
    SLDSIcon(
        icon = ActionIcons.Map,
        size = 40.dp,
        color = Color.White,
        contentDescription = "Map"
    )
}
```

### Android Views (XML)

Icons can also be used in traditional Android Views:

```xml
<ImageView
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:src="@drawable/slds_utility_add"
    android:contentDescription="@string/add_icon" />
```

### Available Categories

| Category | Enum Class | Description | Example Usage |
|----------|-----------|-------------|---------------|
| `action` | `ActionIcons` | Interactive elements like buttons and controls | `ActionIcons.AddContact` |
| `standard` | `StandardIcons` | Object and entity representations | `StandardIcons.Account` |
| `utility` | `UtilityIcons` | General-purpose functional icons | `UtilityIcons.Add` |
| `custom` | `CustomIcons` | Salesforce-specific branded icons | `CustomIcons.Custom1` |

### Icon Naming Convention

Icon enum names follow PascalCase convention:

Examples:
- `UtilityIcons.Add` - Add icon from utility category
- `StandardIcons.Account` - Account icon from standard category
- `ActionIcons.AddContact` - Add Contact icon from action category
- `ActionIcons.NewTask` - New Task icon from action category
- `CustomIcons.Custom1` - Custom icon 1

### Color and Tinting

Icons support custom colors and tinting:

```kotlin
// Default color
val icon = UtilityIcons.Add.getDrawable(context, size = 48)

// Custom color
val redIcon = UtilityIcons.Close.getDrawable(
    context = context,
    size = 48,
    color = 0xFFFF0000.toInt()  // Red
)

// In Compose with Color
SLDSIcon(
    icon = UtilityIcons.Delete,
    size = 32.dp,
    color = Color.Red
)
```

## Finding Available Icons

All icons from the [@salesforce-ux/icons](https://www.npmjs.com/package/@salesforce-ux/icons) npm package are included in this library.

### Browsing Icons

To find available icon names:

1. Visit [@salesforce-ux/icons on npm](https://www.npmjs.com/package/@salesforce-ux/icons)
2. Browse the package contents to see all available icons
3. Icons are organized in folders by category (`action/`, `standard/`, `utility/`, `custom/`, `doctype/`)
4. Convert icon names to PascalCase for the enum (e.g., `add_contact` → `AddContact`)

### Example Icons

Icons can be used as follows:

**Action Icons:**
- `ActionIcons.AddContact` - Add contact action
- `ActionIcons.Approval` - Approval action
- `ActionIcons.NewTask` - New task action
- `ActionIcons.Email` - Email action

**Standard Icons:**
- `StandardIcons.Account` - Account object
- `StandardIcons.Contact` - Contact object
- `StandardIcons.Opportunity` - Opportunity object
- `StandardIcons.Case` - Case object

**Utility Icons:**
- `UtilityIcons.Add` - Add icon
- `UtilityIcons.Close` - Close icon
- `UtilityIcons.Search` - Search icon
- `UtilityIcons.Settings` - Settings icon
- `UtilityIcons.Delete` - Delete icon

**Custom Icons:**
- `CustomIcons.Custom1` through `CustomIcons.Custom113`

## Requirements

- Android API 30+
- Kotlin 1.9+
- Jetpack Compose (optional, for Compose support)

## Troubleshooting

### Icons not loading

1. Ensure the library was properly added to your dependencies
2. Verify you're using the correct API:
   - Use enum-based access: `UtilityIcons.Add.getDrawable(context, size)`
   - Don't access resources directly: `R.drawable.slds_utility_add` ❌
3. Make sure you're importing the correct package: `import com.salesforce.android.sldsicons.*`
4. Clean and rebuild your project:
   ```bash
   ./gradlew clean build
   ```

### Icons appear distorted

Vector drawables preserve quality at any size. If icons appear distorted:

1. Use appropriate size for your use case (24dp-48dp is typical)
2. Set proper ImageView scaleType:
   ```xml
   <ImageView
       android:scaleType="fitCenter"
       android:adjustViewBounds="true" />
   ```

### Resource Not Found Exception

If you get `Resources.NotFoundException` at runtime:

1. Ensure the library is included in your dependencies
2. Check R8/ProGuard rules aren't stripping resources:
   ```proguard
   -keep class com.salesforce.android.sldsicons.** { *; }
   -keepclassmembers class * implements com.salesforce.android.sldsicons.SLDSIcon {
       public *;
   }
   ```

## Contributing

We welcome contributions! Please see [CONTRIBUTING.md](CONTRIBUTING.md) for details on how to get started.

## Code of Conduct

Please follow our [Code of Conduct](CODE_OF_CONDUCT.md).

## License

SLDSIcons is available under the Apache 2.0 license. See the [LICENSE.txt](LICENSE.txt) file for more info.

## Additional Resources

- [SLDS Icons Reference](https://www.lightningdesignsystem.com/icons/) — Browse the full list of available icons
- [`@salesforce-ux/icons` npm package](https://www.npmjs.com/package/@salesforce-ux/icons) — Source icon package
