# 📦 EfcFramework — Distribución binaria (.xcframework) mediante CocoaPods

Este documento explica cómo empaquetar tu **EfcFramework** como un binario (`.xcframework`) y distribuirlo en otros proyectos mediante **CocoaPods**, sin exponer el código fuente.

---

## 🧱 1. Requisitos previos

- Tu framework debe estar compilado en formato `.xcframework`  
  Por ejemplo:
  ```
  /Users/eofc/Documents/AppshelperMe/EfcFramework/EfcFramework.xcframework
  ```

---

## ⚙️ 2. Estructura recomendada

```
EfcFramework/
├── EfcFramework.podspec
├── EfcFramework.xcframework/
│   ├── ios-arm64/
│   ├── ios-arm64_x86_64-simulator/
│   └── Info.plist
└── README.md
```

---

## 🧩 3. Archivo `.podspec` para binarios

Crea o edita el archivo **EfcFramework.podspec** con este contenido:

```ruby
Pod::Spec.new do |s|
  s.name             = "EfcFramework"
  s.version          = "1.0.0"
  s.summary          = "Framework binario de utilidades creado por Eduardo Fulgencio"
  s.description      = <<-DESC
    EfcFramework contiene funciones y utilidades comunes compiladas en un framework binario (.xcframework).
  DESC
  s.homepage         = "https://github.com/eduardofulgencio/EfcFramework"
  s.license          = { :type => "MIT" }
  s.author           = { "Eduardo Fulgencio" => "eduardofulgenciocomendeiro@gmail.com" }

  s.platform         = :ios, "15.0"
  s.swift_version    = "5.9"

  # Ruta local del repositorio o del framework
  s.source           = { :git => "file:///Users/eofc/Projects/EfcFramework", :tag => s.version.to_s }

  # Enlace al binario compilado
  s.vendored_frameworks = "EfcFramework.xcframework"

  s.framework        = "Foundation"
end
```

> 🔹 Usa `vendored_frameworks` para indicar que se trata de un framework binario precompilado.

---

## 🗂️ 4. Crear o actualizar el repositorio local de pods

Desde **Terminal**:

```bash
cd ~/Projects
pod repo add repo-local ~/Projects/repo-local
pod repo push repo-local EfcFramework.podspec --allow-warnings
```

Esto actualizará tu repositorio local de especificaciones de CocoaPods.

---

## 🚀 5. Usar el framework binario en otro proyecto

1. Crea o edita tu **Podfile** en el proyecto cliente:

```ruby
source 'file:///Users/eofc/Projects/repo-local'
source 'https://cdn.cocoapods.org/'

platform :ios, '15.0'
use_frameworks!

target 'MiAppQueUsaElFramework' do
  pod 'EfcFramework', '1.0.0'
end
```

2. Instala los pods:

```bash
pod install
```

3. Abre el `.xcworkspace` y utiliza el framework:

```swift
import EfcFramework

print(EfcHelper.greet(name: "Eduardo"))
```

---

## ☁️ 6. (Opcional) Distribuir mediante un ZIP remoto

Si deseas distribuir el `.xcframework` alojado en GitHub (por ejemplo, en *Releases*), cambia en el `.podspec`:

```ruby
s.source = { :http => "https://github.com/eduardofulgencio/EfcFramework/releases/download/1.0.0/EfcFramework.xcframework.zip" }
```

De esta forma CocoaPods descargará el binario directamente desde la URL.

---

## 🧠 Notas finales

- Actualiza el número de versión (`s.version`) y etiqueta (`git tag`) en cada release.  
- Puedes validar el podspec antes de publicarlo con:
  ```bash
  pod lib lint EfcFramework.podspec --allow-warnings
  ```
- El archivo `.xcframework` puede comprimirse en `.zip` para subirlo a GitHub o a un servidor privado.

---

© 2025 Eduardo Fulgencio Comendeiro
