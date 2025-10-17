# 🧩 Ejemplo Práctico: CocoaPods con Repo Local + Pod Local

Este ejemplo muestra cómo configurar un **repositorio de especificaciones local** y un **pod local** para desarrollo con CocoaPods.

---

## 📂 Estructura de carpetas

```
CocoaPodsLocalExample/
│
├── repo-local/
│   └── Specs/
│       └── MiFramework/
│           └── 1.0.0/
│               └── MiFramework.podspec
│
├── MiFramework/
│   ├── MiFramework.podspec
│   ├── Sources/
│   │   └── MiFramework.swift
│   └── LICENSE
│
└── MiApp/
    ├── Podfile
    └── (Proyecto Xcode)
```

---

## ⚙️ 1. Crear el repo local

```bash
pod repo add repo-local /Users/eduardo/Projects/repo-local
```

Esto crea un índice local donde se registrarán tus librerías.

---

## 📘 2. Registrar el pod local

Copia el `.podspec` dentro del repo local:

```bash
mkdir -p /Users/eduardo/Projects/repo-local/Specs/MiFramework/1.0.0
cp /Users/eduardo/Projects/MiFramework/MiFramework.podspec /Users/eduardo/Projects/repo-local/Specs/MiFramework/1.0.0/
pod repo update repo-local
```

---

## 🧱 3. Configurar el Podfile

```ruby
source '/Users/eduardo/Projects/repo-local'
source 'https://github.com/CocoaPods/Specs.git'

platform :ios, '15.0'
use_frameworks!

target 'MiApp' do
  pod 'MiFramework', '1.0.0'
end
```

---

## 📦 4. Instalar los pods

```bash
cd MiApp
pod install --repo-update
```

---

## 🧠 5. Usar el framework

```swift
import MiFramework

print(MiFramework.saluda()) // "Hola desde MiFramework 👋"
```

---

## ✅ Verificar

```bash
pod list
```

Deberías ver:

```
-> MiFramework (1.0.0)
   Un framework local de ejemplo.
```

---

## 💡 Recomendaciones

- Usa `:path => '../MiFramework'` durante desarrollo.
- Usa `pod repo update repo-local` para refrescar el índice.
- Versiona tus librerías con `1.0.0`, `1.1.0`, etc.
- Incluye un `LICENSE` y `README` en tus pods.

---

© 2025 — Ejemplo educativo para desarrolladores iOS que trabajan con CocoaPods locales.
