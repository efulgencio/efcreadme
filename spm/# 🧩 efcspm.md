### 🧩 efcspm

**efcspm** es un paquete de utilidades comunes para proyectos **SwiftUI** y **SwiftData**, que proporciona *helpers*, *extensiones* y *servicios reutilizables* para acelerar el desarrollo de aplicaciones iOS.


### 📦 Instalación

### Swift Package Manager (SPM)

En Xcode:

1. Ve a **File > Add Packages...**
2. Introduce la URL:
   ```
   https://github.com/eduardofulgencio/efcspm.git
   ```
3. Selecciona la versión y añade el paquete a tu target.


### 🧩 Ejemplo de uso

```swift
import efcspm

let message = EFCSPM.hello()
print(message)
```

O en SwiftUI:

```swift
Text(EFCSPM.hello())
```


## 📱 Demo iOS

En la carpeta `Example/` encontrarás un proyecto Xcode con una pequeña app SwiftUI que importa y muestra funciones del paquete.


## 👤 Autor

**Eduardo Fulgencio Comendeiro**  
📧 [eduardofulgenciocomendeiro@gmail.com](mailto:eduardofulgenciocomendeiro@gmail.com)  
💼 [LinkedIn](https://www.linkedin.com/in/eduardofulgenciocomendeiro)  
📦 [GitHub](https://github.com/eduardofulgencio)



## 📜 Licencia

MIT License

´´´
Explicación del contenido
Package.swift

// swift-tools-version: 5.9
import PackageDescription

let package = Package(
    name: "efcspm",
    platforms: [
        .iOS(.v17)
    ],
    products: [
        .library(
            name: "efcspm",
            targets: ["efcspm"]
        ),
    ],
    targets: [
        .target(
            name: "efcspm",
            dependencies: []
        ),
        .testTarget(
            name: "efcspmTests",
            dependencies: ["efcspm"]
        ),
    ]
)

// swift-tools-version: 5.9

Versión mínima de las herramientas Swift necesarias para compilar este paquete.
Esto le dice a Xcode o a swift build qué versión de swift-tools debe usar.
Si usas Xcode 15 o posterior (que soporta Swift 5.9), está perfecto.

import PackageDescription

Importa el módulo que permite describir el paquete.
Gracias a él, puedes definir dependencias, targets, plataformas, productos, etc.

let package = Package(

Aquí comienza la definición del paquete.
Todo lo que se configure dentro de este bloque define la estructura y comportamiento del paquete.

name: "efcspm",

Nombre interno del paquete (y del módulo principal).
Este será el nombre que usarás con import efcspm.


platforms: [
    .iOS(.v17)
],

Define para qué plataformas se puede usar el paquete y a partir de qué versión mínima.

En este caso:
Solo es compatible con iOS 17 o superior.

Puedes añadir más si quisieras soportar varios sistemas:

platforms: [
    .iOS(.v17),
    .macOS(.v14),
    .watchOS(.v10)
]

Products

products: [
    .library(
        name: "efcspm",
        targets: ["efcspm"]
    ),
],

Define qué genera el paquete para otros proyectos.

En este caso, se produce una librería Swift llamada efcspm.

targets: ["efcspm"] indica qué parte del código fuente se compila en esa librería.

Si tu paquete tuviera varias librerías o ejecutables, aquí se declararían todas.

Ejemplo con dos productos:

products: [
    .library(name: "efcspmCore", targets: ["Core"]),
    .library(name: "efcspmUI", targets: ["UI"])
]

targets

targets: [
    .target(
        name: "efcspm",
        dependencies: []
    ),
    .testTarget(
        name: "efcspmTests",
        dependencies: ["efcspm"]
    ),
]

Los targets son los módulos internos del paquete:

🔹 .target

Representa el código fuente principal del paquete (Sources/efcspm/).

dependencies: [] indica que este módulo no depende de otros paquetes externos.

Si dependieras de otro paquete, por ejemplo Alamofire, sería:


.target(
    name: "efcspm",
    dependencies: ["Alamofire"]
)

.testTarget

Representa el módulo de pruebas unitarias (Tests/efcspmTests/).

dependencies: ["efcspm"] significa que los tests usarán la librería principal para probar su comportamiento.

Ejemplo: cómo se usa

Una vez que este Package.swift está en GitHub, puedes añadirlo a cualquier proyecto con:

dependencies: [
    .package(url: "https://github.com/eduardofulgencio/efcspm.git", from: "1.0.0")
]

Y luego usarlo así en tu app:


import efcspm

print(EFCSPM.hello())


Resumen

| Sección               | Función                                               |
| --------------------- | ----------------------------------------------------- |
| `swift-tools-version` | Versión mínima de las herramientas Swift              |
| `name`                | Nombre del paquete y módulo principal                 |
| `platforms`           | Plataformas y versiones mínimas soportadas            |
| `products`            | Qué produce el paquete (librerías, ejecutables, etc.) |
| `targets`             | Módulos internos: código fuente y tests               |


´´´