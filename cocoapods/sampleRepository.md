### 🧩 Ejemplo Práctico: CocoaPods con Repo Local + Pod Local

Este ejemplo muestra cómo configurar un **repositorio de especificaciones local** y un **pod local** para desarrollo con CocoaPods.



### 📂 Estructura de carpetas

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


### ⚙️ 1. Crear el repo local

```bash
pod repo add repo-local /Users/eduardo/Projects/repo-local
```

Esto crea un índice local donde se registrarán tus librerías.


### 📘 2. Registrar el pod local

Copia el `.podspec` dentro del repo local:

```bash
mkdir -p /Users/eduardo/Projects/repo-local/Specs/MiFramework/1.0.0
cp /Users/eduardo/Projects/MiFramework/MiFramework.podspec /Users/eduardo/Projects/repo-local/Specs/MiFramework/1.0.0/
pod repo update repo-local
```


### 🧱 3. Configurar el Podfile

```ruby
source '/Users/eduardo/Projects/repo-local'
source 'https://github.com/CocoaPods/Specs.git'

platform :ios, '15.0'
use_frameworks!

target 'MiApp' do
  pod 'MiFramework', '1.0.0'
end
```


### 📦 4. Instalar los pods

```bash
cd MiApp
pod install --repo-update
```


### 🧠 5. Usar el framework

```swift
import MiFramework

print(MiFramework.saluda()) // "Hola desde MiFramework 👋"
```


### ✅ Verificar

```bash
pod list
```

Deberías ver:

```
-> MiFramework (1.0.0)
   Un framework local de ejemplo.
```


### 💡 Recomendaciones

- Usa `:path => '../MiFramework'` durante desarrollo.
- Usa `pod repo update repo-local` para refrescar el índice.
- Versiona tus librerías con `1.0.0`, `1.1.0`, etc.
- Incluye un `LICENSE` y `README` en tus pods.


### A veces CocoaPods cachea los resultados. Puedes forzar una limpieza:

 ´´´
pod cache clean --all
pod repo update
pod search MiFramework
 ´´´

 ### Este es el pod que me ha funcionado para MiFramework

 ´´´
 platform :ios, '15.0'
use_frameworks!

target 'UseCocoaPodsLocal' do
  # Comment the next line if you don't want to use dynamic frameworks
  pod 'MiFramework', :path => '/Users/eofc/Projects/MiFramework'
  # Pods for UseCocoaPodsLocal

end
´´´

### El contenido de MiFramework.podspec

´´´
Pod::Spec.new do |s|
  s.name             = 'MiFramework'
  s.version          = '1.0.0'
  s.summary          = 'Un framework local de ejemplo.'
  s.description      = 'Ejemplo de cómo usar un pod local con un repo local.'
  s.homepage         = 'https://github.com/eduardo/MiFramework'
  s.license          = { :type => 'MIT', :file => 'LICENSE' }
  s.author           = { 'Eduardo Fulgencio' => 'eduardo@ejemplo.com' }
  s.source           = { :path => '.' }
  s.ios.deployment_target = '15.0'
  s.swift_versions   = ['5.9']
  s.source_files     = 'Sources/**/*.{swift}'
end

´´´

© 2025 — Ejemplo educativo para desarrolladores iOS que trabajan con CocoaPods locales.
