# 📦 EfcFramework — Distribución mediante CocoaPods

Este documento explica cómo empaquetar y utilizar tu framework `EfcFramework` en otros proyectos de Xcode mediante **CocoaPods**.

---

## 🧱 1. Estructura recomendada

Organiza tus carpetas así:

```
~/Projects/
├── EfcFramework/
│   ├── EfcFramework.podspec
│   ├── Sources/
│   │   └── EfcHelper.swift
│   └── README.md
└── MiAppQueUsaElFramework/
    └── Podfile
```

---

## ⚙️ 2. Crear el archivo `.podspec`

Dentro de `EfcFramework/`, crea un archivo llamado **EfcFramework.podspec**:

```ruby
Pod::Spec.new do |s|
  s.name             = "EfcFramework"
  s.version          = "1.0.0"
  s.summary          = "Framework de utilidades creado por Eduardo Fulgencio"
  s.description      = <<-DESC
    EfcFramework contiene funciones y extensiones comunes utilizadas en proyectos iOS.
  DESC
  s.homepage         = "https://github.com/eduardofulgencio/EfcFramework"
  s.license          = { :type => "MIT" }
  s.author           = { "Eduardo Fulgencio" => "eduardofulgenciocomendeiro@gmail.com" }

  s.platform         = :ios, "15.0"
  s.swift_version    = "5.9"

  # Fuente local o remota del framework
  s.source           = { :git => "file:///Users/eofc/Projects/EfcFramework", :tag => s.version.to_s }

  # Archivos fuente
  s.source_files     = "Sources/**/*.{swift}"

  s.framework        = "Foundation"
end
```

> 🔹 Asegúrate de que el código del framework esté dentro de `Sources/` y marcado como `public` donde sea necesario.

---

## 🗂️ 3. Crear un repositorio local de pods

1. Abre **Terminal** y ejecuta:

```bash
cd ~/Projects
pod repo add repo-local ~/Projects/repo-local
```

2. Luego añade tu framework al índice local:

```bash
pod repo push repo-local EfcFramework.podspec --allow-warnings
```

Esto crea un repositorio local que CocoaPods puede usar como fuente.

---

## 🚀 4. Usar el framework en otro proyecto

1. En tu proyecto cliente, crea o edita el **Podfile**:

```ruby
source 'file:///Users/eofc/Projects/repo-local'
source 'https://cdn.cocoapods.org/'

platform :ios, '15.0'
use_frameworks!

target 'MiAppQueUsaElFramework' do
  pod 'EfcFramework', '1.0.0'
end
```

2. Instala las dependencias:

```bash
pod install
```

3. Abre el `.xcworkspace` generado y usa tu framework:

```swift
import EfcFramework

print(EfcHelper.greet(name: "Eduardo"))
```

---

## 🧪 5. (Opcional) Publicar en GitHub

Si subes tu framework a GitHub, cambia el origen en el `.podspec`:

```ruby
s.source = { :git => "https://github.com/eduardofulgencio/EfcFramework.git", :tag => s.version.to_s }
```

Y podrás usarlo directamente sin necesidad de `repo-local`.

---

## 💡 Consejos adicionales

- Asegúrate de compilar y etiquetar tu versión (`git tag 1.0.0 && git push origin 1.0.0`)
- Mantén actualizado el archivo `.podspec` con cada versión nueva
- Usa `pod lib lint` para validar el `.podspec` antes de publicarlo

---

© 2025 Eduardo Fulgencio Comendeiro
