# 🧰 Guía Práctica de JFrog CLI (para desarrolladores en macOS)

## 📘 Introducción

**JFrog CLI** es una herramienta de línea de comandos que permite interactuar con **JFrog Artifactory**, **Xray**, y otros servicios JFrog directamente desde el terminal.

Permite automatizar tareas como:
- Subir y descargar artefactos
- Buscar dependencias
- Gestionar builds
- Limpiar artefactos antiguos
- Trabajar con configuraciones seguras sin abrir la interfaz web

Ideal para desarrolladores que quieren optimizar flujos de trabajo desde macOS.



## ⚙️ Instalación en macOS

### 1. Instalar con Homebrew

```bash
brew install jfrog-cli
```

### 2. Verificar la instalación

```bash
jfrog --version
```

Deberías ver algo como:

```
jfrog version 2.59.0
```


## 🔐 Configuración inicial

Antes de usar el CLI, debes registrar tu servidor Artifactory:

```bash
jfrog config add artifactory-server   --url=https://artifactory.miempresa.com   --user=admin   --password=MiPasswordSeguro
```

🔸 Puedes usar un **token de acceso** en lugar de contraseña:
```bash
jfrog config add artifactory-server   --url=https://artifactory.miempresa.com   --access-token=<TOKEN>
```

Para listar las configuraciones guardadas:
```bash
jfrog config show
```


## 🧱 Comandos Básicos

### 📤 Subir artefactos

Sube archivos o carpetas a un repositorio de Artifactory:

```bash
jfrog rt upload "build/*.zip" mi-repo-local/
```

Ejemplo práctico:
```bash
jfrog rt upload "dist/app-release.apk" mobile-repo/
```

👉 Puedes usar comodines (`*`, `**`) y rutas relativas.



### 📥 Descargar artefactos

Descarga artefactos desde un repositorio remoto o local:

```bash
jfrog rt download mi-repo-local/app-release.apk ./downloads/
```

O con comodines:

```bash
jfrog rt download "mi-repo-local/*.zip" ./builds/
```


### 🧹 Borrar artefactos

Para eliminar archivos antiguos o versiones obsoletas:

```bash
jfrog rt del "mi-repo-local/*.zip"
```

Con filtro de fecha:
```bash
jfrog rt del "mi-repo-local/*.zip" --older-than=30d
```


### 🔍 Buscar artefactos

Puedes buscar artefactos por nombre, propiedad o patrón:

```bash
jfrog rt s "mi-repo-local/*.ipa"
```

También puedes añadir filtros:

```bash
jfrog rt s "libs-release-local/*.jar" --props "version=1.0.0"
```


## 🧩 Propiedades de Artefactos

Artifactory permite añadir **propiedades personalizadas** a tus archivos:

```bash
jfrog rt sp "mi-repo-local/*.zip" "entorno=prod;version=1.0.0"
```

Consultar propiedades:

```bash
jfrog rt gp "mi-repo-local/app.zip"
```


## 🧱 Gestión de Builds

JFrog CLI permite definir y publicar builds completos (útil para trazabilidad).

### Crear y publicar un build

```bash
jfrog rt bce miBuild 1
jfrog rt upload "build/*.zip" repo-local/ --build-name=miBuild --build-number=1
jfrog rt bp miBuild 1
```

- `bce`: build create env  
- `bp`: build publish  

Consultar builds en Artifactory → pestaña **Builds**.

---

## 🧰 Limpieza y Mantenimiento

Eliminar versiones antiguas o artefactos no usados:

```bash
jfrog rt del "repo-local/*.zip" --older-than=60d --quiet
```

Listar repositorios existentes:

```bash
jfrog rt repo-list
```

Borrar configuración del CLI:

```bash
jfrog config remove artifactory-server
```

## 🚀 Automatizaciones Útiles (macOS Terminal)

### Subir automáticamente el build actual

```bash
#!/bin/zsh
VERSION="1.0.0"
BUILD_DIR="./dist"

jfrog rt upload "$BUILD_DIR/*.zip" "ios-repo/"   --props "version=$VERSION;platform=ios"
```

Guarda este script como `upload_build.sh`, dale permisos y ejecútalo:

```bash
chmod +x upload_build.sh
./upload_build.sh
```



## 🔒 Seguridad

- Usa **tokens de acceso** en lugar de contraseñas.
- Evita subir credenciales a Git.
- Configura variables de entorno:
  ```bash
  export JFROG_CLI_LOG_LEVEL=ERROR
  export JFROG_CLI_HOME_DIR=~/.jfrog
  ```



## 📚 Recursos Oficiales

- 🏠 Sitio oficial: [https://jfrog.com](https://jfrog.com)
- 📘 Documentación CLI: [https://jfrog.com/getcli/](https://jfrog.com/getcli/)
- 🧪 Ejemplos CLI: [https://github.com/jfrog/jfrog-cli](https://github.com/jfrog/jfrog-cli)
- 🧱 Documentación Artifactory: [https://jfrog.com/artifactory/](https://jfrog.com/artifactory/)



## 🧾 Resumen rápido de comandos

| Comando | Descripción |
|----------|--------------|
| `jfrog config add` | Configura un servidor Artifactory. |
| `jfrog rt upload` | Sube artefactos. |
| `jfrog rt download` | Descarga artefactos. |
| `jfrog rt s` | Busca artefactos. |
| `jfrog rt del` | Borra artefactos. |
| `jfrog rt sp` | Asigna propiedades a artefactos. |
| `jfrog rt bp` | Publica un build. |
| `jfrog rt repo-list` | Lista repositorios. |



**Autor:** Guía generada por ChatGPT (Eduardo Fulgencio Comendeiro)  
**Fecha:** Octubre 2025  
**Versión:** 1.0.0  
