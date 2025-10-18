### 📦 Guía de Ficheros `.podspec` en CocoaPods

### 🧩 ¿Qué es un `.podspec`?

Un fichero **`.podspec`** (abreviatura de *Pod Specification*) es el **archivo de definición** que describe una librería o framework en CocoaPods.  
Contiene la **información necesaria para instalar, compilar y distribuir** un pod, tanto en proyectos locales como en repositorios públicos o privados.

En resumen:  
> El `.podspec` es el "contrato" que dice a CocoaPods **qué es tu librería, dónde está su código y cómo debe integrarse.**



### 🗂️ Estructura básica de un `.podspec`

Un `.podspec` es un fichero Ruby que define un objeto `Pod::Spec`.  
Ejemplo mínimo:

```ruby
Pod::Spec.new do |s|
  s.name             = 'MiFramework'
  s.version          = '1.0.0'
  s.summary          = 'Una librería que muestra un mensaje personalizado.'
  s.description      = 'Este framework contiene una vista personalizada para mostrar mensajes con estilo.'
  s.homepage         = 'https://github.com/miusuario/MiFramework'
  s.license          = { :type => 'MIT', :file => 'LICENSE' }
  s.author           = { 'Eduardo Fulgencio' => 'eduardo@ejemplo.com' }
  s.source           = { :git => 'https://github.com/miusuario/MiFramework.git', :tag => s.version.to_s }

  s.ios.deployment_target = '15.0'
  s.swift_versions   = ['5.0', '5.9']

  s.source_files     = 'Sources/**/*.{swift,h,m}'
  s.resources        = 'Resources/**/*'
  s.frameworks       = 'UIKit'
end
```

### 🔍 Descripción de los principales campos

| Campo | Descripción |
|-------|--------------|
| **name** | Nombre del pod tal como se usará en el `Podfile`. |
| **version** | Versión actual del pod (usa [Semantic Versioning](https://semver.org/): `MAJOR.MINOR.PATCH`). |
| **summary** | Breve descripción visible en el catálogo de CocoaPods. |
| **description** | Descripción extendida del proyecto (puede incluir varias líneas). |
| **homepage** | URL del repositorio o página del proyecto. |
| **license** | Tipo de licencia (MIT, Apache, GPL, etc.). |
| **author** | Autor o autores del pod. |
| **source** | Ubicación del código fuente (Git, local, etc.). |
| **platform / deployment_target** | Plataforma mínima compatible (iOS, macOS, etc.). |
| **swift_versions** | Versiones de Swift soportadas. |
| **source_files** | Rutas a los archivos fuente que deben compilarse. |
| **resources** | Archivos no código: imágenes, xibs, JSON, etc. |
| **frameworks / libraries** | Frameworks o librerías del sistema requeridas. |
| **dependencies** | Otras dependencias CocoaPods. |

Ejemplo:

```ruby
s.dependency 'Alamofire', '~> 5.6'
```


### 🧠 Ejemplo completo con dependencias

```ruby
Pod::Spec.new do |s|
  s.name             = 'AwesomeKit'
  s.version          = '1.2.0'
  s.summary          = 'Colección de utilidades para iOS.'
  s.description      = <<-DESC
  AwesomeKit ofrece extensiones y utilidades comunes para el desarrollo de apps iOS:
  - Extensiones de UIKit
  - Manejo de colores y tipografías
  - Controladores base reutilizables
  DESC

  s.homepage         = 'https://github.com/miempresa/AwesomeKit'
  s.license          = { :type => 'MIT', :file => 'LICENSE' }
  s.author           = { 'Equipo iOS' => 'ios@miempresa.com' }
  s.source           = { :git => 'https://github.com/miempresa/AwesomeKit.git', :tag => s.version }

  s.ios.deployment_target = '15.0'
  s.swift_versions   = ['5.9']

  s.source_files     = 'Sources/**/*.{swift}'
  s.resources        = 'Assets/**/*.{xcassets,json,png}'

  s.frameworks       = 'UIKit'
  s.dependency       'Alamofire', '~> 5.6'
  s.dependency       'Kingfisher', '~> 7.0'
end
```


### ⚙️ Validar un `.podspec`

Antes de publicarlo o usarlo localmente, es recomendable validar su sintaxis y metadatos:

```bash
pod lib lint MiFramework.podspec
```

Si lo estás usando en local y no quieres validaciones online:
```bash
pod lib lint MiFramework.podspec --allow-warnings --sources='https://github.com/CocoaPods/Specs.git'
```


### 📦 Publicar un `.podspec`

### 1️⃣ Registrar el repositorio de especificaciones (solo si es privado)
```bash
pod repo add mi-repo-specs https://github.com/miempresa/pods-specs.git
```

### 2️⃣ Subir el podspec a ese repo
```bash
pod repo push mi-repo-specs MiFramework.podspec
```

### 3️⃣ O publicarlo en el trunk oficial (público)
```bash
pod trunk push MiFramework.podspec
```


### 🧰 Usarlo desde un proyecto

En el `Podfile`:
```ruby
pod 'MiFramework', '~> 1.0.0'
```

O si estás desarrollando en local:
```ruby
pod 'MiFramework', :path => '../MiFramework'
```


### 💡 Buenas prácticas

- Sigue **Semantic Versioning (1.0.0)** para versiones.
- Usa `swift_versions` para evitar incompatibilidades.
- Incluye un archivo `LICENSE`.
- Mantén la ruta `source_files` limpia y genérica.
- Valida siempre antes de publicar (`pod lib lint`).
- Si usas un repo privado, documenta su `source`.


### 🔗 Recursos oficiales

- 📘 [Guía oficial de `.podspec` — CocoaPods Docs](https://guides.cocoapods.org/syntax/podspec.html)
- 🧱 [Publicar tus propios Pods](https://guides.cocoapods.org/making/making-a-cocoapod.html)
- 🧩 [CocoaPods Specs Repo](https://github.com/CocoaPods/Specs)


© 2025 — Guía creada para desarrolladores iOS que deseen crear, mantener y distribuir sus propias librerías CocoaPods.
