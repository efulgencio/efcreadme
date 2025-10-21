# 📦 EfcFramework — Guía de creación y uso en Xcode

Este documento explica cómo crear, compilar y utilizar un **framework iOS** en Xcode llamado `EfcFramework`.

---

## 🧱 1. Crear el proyecto del framework

1. Abre **Xcode**  
2. Ve a **File > New > Project…**  
3. Selecciona: **iOS → Framework & Library → Framework**  
4. Pulsa **Next**

### Configuración inicial

| Campo | Valor |
|-------|--------|
| **Product Name** | `EfcFramework` |
| **Team** | (Tu equipo o “None”) |
| **Organization Identifier** | `com.tuempresa` |
| **Language** | Swift |
| **Include Tests** | ✅ (opcional) |

---

## 📁 2. Estructura inicial del framework

```
EfcFramework/
├── EfcFramework.xcodeproj
├── EfcFramework/
│   ├── EfcFramework.h
│   └── Info.plist
└── EfcFrameworkTests/
```

---

## 🧩 3. Añadir código Swift

Crea un archivo `EfcHelper.swift` dentro de la carpeta `EfcFramework` con este contenido:

```swift
import Foundation

public struct EfcHelper {
    public static func greet(name: String) -> String {
        return "Hola \(name)! Bienvenido a EfcFramework 👋"
    }
}
```

> Usa `public` para que sea accesible desde fuera del framework.

---

## 🧪 4. Probar el framework

1. Crea un nuevo proyecto **iOS App**  
2. Ve a **General > Frameworks, Libraries, and Embedded Content**  
3. Pulsa ➕ → **Add Other > Add Files…** y selecciona `EfcFramework.xcodeproj`  
4. Marca el framework como **Embed & Sign**

Luego importa y usa el framework en tu código:

```swift
import EfcFramework

print(EfcHelper.greet(name: "Eduardo"))
```

Ejecuta la app y verás el mensaje en la consola ✅

---

## 📦 5. Empaquetar como `.xcframework` (opcional)

Si quieres distribuirlo o compartirlo:

```bash
xcodebuild -create-xcframework \
  -framework path/to/Debug-iphoneos/EfcFramework.framework \
  -framework path/to/Debug-iphonesimulator/EfcFramework.framework \
  -output EfcFramework.xcframework
```

Esto generará un archivo **EfcFramework.xcframework** universal, listo para compartir o subir a un repositorio.

---

## ✨ Notas finales

- Usa `public` o `open` para exponer funciones y tipos.  
- Mantén la estructura limpia con carpetas como `Sources/` y `Tests/`.  
- Añade un `README.md` y licencia si lo distribuyes.

---

© 2025 Eduardo Fulgencio Comendeiro
