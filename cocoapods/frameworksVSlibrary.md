### 📘 Guía completa de CocoaPods para iOS

CocoaPods es un **gestor de dependencias** para proyectos iOS y macOS.  
Permite integrar librerías de terceros fácilmente en tus proyectos Xcode.



### ⚙️ Instalación e inicialización

### 🔹 1. Instalar CocoaPods

```bash
sudo gem install cocoapods
```

Verifica la instalación:

```bash
pod --version
```


### 🔹 2. Configurar CocoaPods

```bash
pod setup --verbose
```

🧩 **Significado:**  
- Descarga y configura el **repositorio maestro de especificaciones (Specs repo)**.  
- `--verbose` muestra salida detallada.  
- Solo se ejecuta una vez (o para forzar la actualización del repo).



### 🔹 3. Crear el Podfile

```bash
pod init
```

🧩 Crea un archivo `Podfile` donde defines las dependencias de tu proyecto.



### 📄 Estructura del Podfile

```ruby
# platform :ios, '9.0'

target 'LearnDevice' do
  use_frameworks!
  pod 'Toast-Swift', '~> 5.0.1'
end
```

### 🔍 Secciones explicadas:

#### 🔸 `platform :ios, '9.0'`
Define la versión mínima de iOS compatible.

#### 🔸 `use_frameworks!`
Compila los Pods como **frameworks dinámicos**, necesarios para Swift.

#### 🔸 `pod 'Nombre', 'Versión'`
Declara la dependencia y su versión.



### ⚙️ Frameworks dinámicos vs Librerías estáticas en CocoaPods

Cuando usas CocoaPods, puedes decidir **cómo integrar las dependencias** dentro de tu proyecto Xcode:  
como **frameworks dinámicos** (`use_frameworks!`) o como **librerías estáticas** (sin usar esa directiva).



### 🧩 Diferencias principales

| Característica | 🧱 **Framework dinámico** (`use_frameworks!`) | 📦 **Librería estática** (sin `use_frameworks!`) |
|----------------|-----------------------------------------------|--------------------------------------------------|
| **Definición** | Se compila como un módulo `.framework` que se carga al ejecutar la app. | Su código se inserta directamente en el binario final durante la compilación. |
| **Extensión de archivo** | `.framework` | `.a` |
| **Momento de enlace** | En tiempo de ejecución. | En tiempo de compilación. |
| **Compatibilidad con Swift** | ✅ Obligatorio si usas librerías escritas en Swift. | ⚠️ Solo compatible con Objective-C. |
| **Tamaño del binario** | Menor, ya que los frameworks se cargan aparte. | Mayor, porque todo se incrusta en el ejecutable. |
| **Tiempo de arranque de la app** | Ligeramente más lento (debe cargar frameworks). | Más rápido (todo ya está enlazado). |
| **Mantenimiento y modularidad** | Más flexible: permite actualizar módulos o frameworks. | Requiere recompilar todo si cambias una librería. |
| **Ejemplo CocoaPods** | `use_frameworks!` → instala como frameworks dinámicos. | Sin `use_frameworks!` → instala como librerías estáticas. |



### ⚙️ Ejemplo visual

#### ✅ Con `use_frameworks!`
CocoaPods genera frameworks dinámicos:

```
Pods/
 └── Alamofire.framework
 └── Toast_Swift.framework
```

El binario de tu app **no contiene directamente** el código de los pods, sino referencias dinámicas a ellos.



#### 📦 Sin `use_frameworks!`
CocoaPods genera librerías estáticas:

```
Pods/
 └── libAFNetworking.a
```

El código de cada librería se **incrusta dentro del binario final** de la aplicación.



### 🧠 En resumen

| Situación | Recomendado |
|------------|-------------|
| Proyecto moderno 100% Swift | `use_frameworks! :linkage => :static` |
| Proyecto mixto (Swift + Objective-C) | `use_frameworks!` |
| Proyecto antiguo solo Objective-C | Sin `use_frameworks!` (usa librerías estáticas) |



### 💬 Nota adicional (CocoaPods ≥ 1.5.0)

Desde CocoaPods 1.5.0 puedes usar:

```ruby
use_frameworks! :linkage => :static
```

Esto permite que los **Pods se compilen como frameworks estáticos**, combinando:
- compatibilidad con Swift ✅  
- rendimiento y carga rápida de librerías estáticas ⚡️  



### 🎯 Recomendación práctica

- Si tu app usa **librerías Swift**, **activa `use_frameworks!`**.  
- Si tu app es **Objective-C pura**, puedes omitirlo.  
- Para **máximo rendimiento en apps modernas**, usa:  
  ```ruby
  use_frameworks! :linkage => :static
  ```



### 🔄 Instalar y actualizar dependencias

### `pod install`
Instala las librerías declaradas en el `Podfile` y genera `Podfile.lock`.

### `pod update`
Actualiza las dependencias existentes a las versiones más recientes compatibles.



### 🧹 Limpieza de dependencias

```bash
rm -rf Pods
rm Podfile.lock
pod install
```



### 🧮 Versionado Semántico (Semantic Versioning)

Formato: `MAJOR.MINOR.PATCH` → `1.0.0`

| Parte | Significado | Ejemplo |
|-------|--------------|---------|
| MAJOR | Cambios incompatibles | 1.x.x → 2.0.0 |
| MINOR | Nuevas funciones | 1.0.0 → 1.1.0 |
| PATCH | Corrección de errores | 1.0.0 → 1.0.1 |

Ejemplo:  
`pod 'Toast-Swift', '~> 5.0.1'` → instala cualquier versión >= 5.0.1 pero < 6.0.0.



### 🌐 Documentación oficial

📚 [Guía oficial de CocoaPods](https://guides.cocoapods.org/using/getting-started.html)



### ✅ Comandos útiles

| Comando | Descripción |
|----------|--------------|
| `pod setup --verbose` | Inicializa el repositorio local |
| `pod init` | Crea el `Podfile` |
| `pod install` | Instala los pods |
| `pod update` | Actualiza pods existentes |
| `pod repo update` | Actualiza el repositorio de especificaciones |
| `pod deintegrate` | Elimina CocoaPods del proyecto |
| `pod list` | Lista los pods instalados |
| `pod outdated` | Muestra versiones nuevas disponibles |



### 🧪 Ejemplo práctico: Integrar Toast-Swift con UIKit

### 1️⃣ Crear el proyecto Xcode
- Abre Xcode → “Create a new iOS project” → App → UIKit.

### 2️⃣ Inicializa CocoaPods

```bash
cd ruta/del/proyecto
pod init
```

### 3️⃣ Edita el Podfile

```ruby
platform :ios, '15.0'

target 'LearnDevice' do
  use_frameworks!
  pod 'Toast-Swift', '~> 5.0.1'
end
```

### 4️⃣ Instala los pods

```bash
pod install
```

Abre el archivo `.xcworkspace` generado.

### 5️⃣ Usa la librería en tu ViewController

```swift
import UIKit
import Toast_Swift

class ViewController: UIViewController {
    override func viewDidLoad() {
        super.viewDidLoad()
        self.view.makeToast("¡Hola CocoaPods! 🎉")
    }
}
```

Ejecuta la app en el simulador y verás un mensaje Toast.



🎯 **Resumen final:**
- `pod init` → crea Podfile  
- `pod install` → instala dependencias  
- `pod update` → actualiza versiones  
- `use_frameworks!` → habilita Swift  
- `Podfile.lock` → controla versiones instaladas  
- Abrir siempre el proyecto desde `.xcworkspace`



© 2025 Guía CocoaPods — por Eduardo Fulgencio Comendeiro
