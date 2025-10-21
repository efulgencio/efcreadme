### 🧭 Schemes en Xcode --- Guía práctica

Un **Scheme** en Xcode define **qué se construye, ejecuta, prueba o
archiva**, y **cómo** se hace.\
Es un plan de ejecución que organiza el flujo completo de trabajo de tu
app o framework.

------------------------------------------------------------------------

### 🚀 ¿Qué es un Scheme?

Un **Scheme** le dice a Xcode: - Qué **target** (app, framework, test)
debe ejecutar. - Qué **configuración de compilación** usar (`Debug` o
`Release`). - Qué **acciones** realizar antes o después de compilar. -
Qué **entorno** usar al ejecutar o probar.

Cada proyecto puede tener varios schemes, por ejemplo: -
`UseCocoaPodsLocal` → tu app principal. - `MiFramework` → un framework
local. - `App-Staging` y `App-Production` → entornos diferentes.

------------------------------------------------------------------------

### ⚙️ Editar un Scheme

Haz clic en el menú de schemes junto al botón ▶️ en Xcode y selecciona
**Edit Scheme...**.

Verás varias secciones en la barra lateral:

### 🔹 1. Build

Define qué targets se deben compilar y en qué orden.\
Puedes decidir si tu framework o librería se construye junto con tu app,
o si se omite.

**Ejemplo:** Si tienes un pod local o framework, puedes decidir que solo
se compile al archivar, no en ejecución normal.

------------------------------------------------------------------------

### 🔹 2. Run

Configura cómo se ejecuta tu app cuando presionas **Run (⌘ + R)**: - El
**build configuration**: normalmente "Debug". - **Variables de
entorno.** - **Argumentos** que se pasan a la app al ejecutar. - Si se
abre la consola o un debugger.

**Ejemplo práctico:** Puedes probar diferentes comportamientos sin
cambiar el código:

``` bash
-enableFeatureX YES
API_URL=https://dev.server.com
```

------------------------------------------------------------------------

### 🔹 3. Test

Define qué tests se ejecutan y con qué configuración.\
Puedes activar o desactivar conjuntos de tests o cambiar la
configuración solo para pruebas.

------------------------------------------------------------------------

### 🔹 4. Profile

Se usa para ejecutar con **Instruments** y medir rendimiento.\
Puedes definir si el build es tipo `Release` o `Debug`.

------------------------------------------------------------------------

### 🔹 5. Analyze y Archive

-   **Analyze** → ejecuta el analizador estático de código.
-   **Archive** → define cómo se compila tu app para distribución (.ipa
    o App Store).

------------------------------------------------------------------------

### 🧩 Ejemplo práctico de varios Schemes

Imagina que tienes dos entornos: - **Desarrollo (staging)** → usa API de
pruebas. - **Producción (release)** → usa la API real.

Puedes crear dos schemes:

-   `App-Staging`
-   `App-Production`

Cada uno con su variable de entorno:

``` bash
API_ENV=staging
```

o

``` bash
API_ENV=production
```

Y luego, en tu código Swift:

``` swift
let env = ProcessInfo.processInfo.environment["API_ENV"] ?? "production"
print("Running in \(env) environment")
```

Así puedes ejecutar o depurar la app con configuraciones distintas sin
modificar el código.

------------------------------------------------------------------------

### ✅ Resumen

  Sección       Propósito principal          Ejemplo
  ------------- ---------------------------- ---------------------
  **Build**     Qué targets se construyen    App + Framework
  **Run**       Cómo se ejecuta              Debug con variables
  **Test**      Qué tests se ejecutan        Unit tests
  **Profile**   Optimizar rendimiento        Instruments
  **Archive**   Crear versión distribuible   .ipa o App Store

------------------------------------------------------------------------

**Consejo:** puedes duplicar un scheme existente desde **Manage
Schemes... → Duplicate**, renombrarlo y modificar solo las variables o
configuración que necesites.

------------------------------------------------------------------------

📘 **Autor:** Eduardo Fulgencio Comendeiro\
🧩 **Tema:** Xcode Schemes --- Entornos y configuración avanzada
