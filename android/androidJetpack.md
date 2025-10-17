# Proyecto Android con Arquitectura Limpia

Este es un proyecto Android de ejemplo creado desde cero, diseñado para demostrar una arquitectura de software moderna y robusta, siguiendo las mejores prácticas recomendadas por Google.

## Resumen del Proyecto

*   **Proyecto Completo:** Se ha generado un proyecto Android funcional.
*   **Arquitectura Limpia (Clean Architecture):** El código está estrictamente separado en tres capas principales:
    *   **Capa de Datos (`data`):** Responsable de la obtención de datos. Incluye DTOs, Mappers, la interfaz de `ApiService` para Retrofit y la implementación del `Repository`.
    *   **Capa de Dominio (`domain`):** Contiene la lógica de negocio central y los modelos de datos limpios de la aplicación. Los `UseCases` (casos de uso) orquestan el flujo de datos desde los repositorios.
    *   **Capa de UI (`ui`):** Responsable de la presentación. Utiliza Jetpack Compose para construir la interfaz de usuario de forma declarativa. El `ViewModel` se encarga de gestionar el estado de la UI y comunicarse con la capa de dominio.
*   **Inyección de Dependencias:** Se utiliza **Hilt** para gestionar y proveer todas las dependencias de la aplicación, facilitando el desacoplamiento y las pruebas.
*   **UI Moderna:** La interfaz está construida íntegramente con **Jetpack Compose**, el framework de UI declarativo y moderno de Google.
*   **Funcionalidad:** La aplicación muestra una pantalla de carga mientras simula una llamada de red. Al completarse, muestra un mensaje de bienvenida. También está preparada para gestionar y mostrar estados de error.

## Stack Tecnológico

*   **Lenguaje:** Kotlin
*   **UI:** Jetpack Compose
*   **Arquitectura:** MVVM con Clean Architecture
*   **Inyección de Dependencias:** Hilt
*   **Networking:** Retrofit (simulado en este ejemplo)
*   **Asincronía:** Corrutinas de Kotlin

## Próximos Pasos

Para compilar y ejecutar este proyecto:
1.  Abre la carpeta del proyecto con una versión reciente de Android Studio.
2.  Android Studio sincronizará el proyecto con los ficheros de Gradle y descargará todas las dependencias definidas.
3.  Ejecuta la aplicación en un emulador o en un dispositivo físico.
