### 🧩 Guía Práctica de JFrog Artifactory

### 📘 Introducción

**JFrog Artifactory** es un repositorio universal de artefactos que centraliza y gestiona los binarios generados durante el desarrollo de software.

Permite almacenar, versionar y distribuir **dependencias internas** (frameworks, librerías, paquetes, contenedores, etc.) de forma segura y reproducible.

JFrog es la empresa creadora de esta herramienta, junto con otras soluciones como:
- **JFrog Xray** → análisis de vulnerabilidades y licencias  
- **JFrog Pipelines** → CI/CD  
- **JFrog Distribution** → distribución segura de binarios  
- **JFrog Mission Control** → gestión centralizada de múltiples instancias


### 🏗️ Conceptos Clave

| Tipo de Repositorio | Descripción |
|----------------------|-------------|
| **Local** | Repositorio interno donde se publican artefactos creados por tu equipo o empresa. |
| **Remoto** | Proxy o caché de repositorios externos (ej. npmjs, Maven Central, CocoaPods, etc.). |
| **Virtual** | Agrupa varios repositorios (locales y remotos) bajo una misma URL de acceso. |


### ⚙️ Instalación (Local con Docker)

Si quieres una instalación rápida de **Artifactory OSS (Open Source)**:

```bash
docker run --name artifactory -d -p 8081:8081 -p 8082:8082   -v artifactory-data:/var/opt/jfrog/artifactory   docker.bintray.io/jfrog/artifactory-oss:latest
```

- Accede desde tu navegador: [http://localhost:8082/ui/](http://localhost:8082/ui/)
- Usuario y contraseña por defecto:
  ```
  Username: admin
  Password: password
  ```


### 🌍 Versiones Disponibles

| Tipo | Descripción |
|------|--------------|
| **Community Edition (CE)** | Gratuita, ideal para entornos de prueba o pequeños equipos. |
| **Pro / Enterprise** | Incluye seguridad avanzada, replicación, y soporte para más tipos de repositorio. |
| **Cloud (SaaS)** | Servicio gestionado por JFrog. |
| **On-Premise** | Instalación en servidores propios. |



### 🧱 Ejemplo de Uso con npm

### 1. Configurar el archivo `.npmrc`

```bash
registry=https://artifactory.miempresa.com/artifactory/api/npm/npm-virtual/
_auth = <TOKEN>
always-auth=true
```

### 2. Publicar un paquete

```bash
npm publish
```

### 3. Descargar paquetes desde Artifactory

```bash
npm install mi-paquete
```



### 🍎 Ejemplo de Uso con CocoaPods

En tu `Podfile` puedes configurar el repositorio:

```ruby
source 'https://artifactory.miempresa.com/artifactory/api/pods/cocoapods-virtual'
use_frameworks!
platform :ios, '15.0'

target 'MyApp' do
  pod 'MiFramework', '~> 1.0.0'
end
```

Luego instala los pods:

```bash
pod install
```


### 🔄 Integración con CI/CD

Artifactory se integra fácilmente con:

- **Jenkins** (plugin oficial)
- **GitHub Actions**
- **GitLab CI**
- **Azure DevOps**
- **CircleCI**

### Ejemplo básico (GitHub Actions)

```yaml
name: Build and Publish
on: [push]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Build Package
        run: npm run build

      - name: Publish to Artifactory
        run: |
          npm config set registry https://artifactory.miempresa.com/artifactory/api/npm/npm-local/
          npm publish
```


### 🧩 Ventajas de Usar Artifactory

- Centralización de binarios y dependencias.
- Repositorios cacheados para mayor velocidad.
- Control de acceso y permisos.
- Integración CI/CD nativa.
- Versionado y trazabilidad de artefactos.
- Compatibilidad con más de 30 tipos de paquetes (npm, Maven, Docker, NuGet, CocoaPods, Swift, etc).



### 🧰 Limpieza y Mantenimiento

Para limpiar versiones antiguas o artefactos no usados:
- Usa políticas de limpieza (Retention Policies).
- Automatiza con **JFrog CLI**.

### Ejemplo de JFrog CLI

```bash
# Instalar JFrog CLI
brew install jfrog-cli

# Configurar servidor
jfrog config add artifactory-server --url=https://artifactory.miempresa.com --user=admin --password=xxxx

# Subir artefacto
jfrog rt upload "build/*.zip" repo-local/

# Descargar artefacto
jfrog rt download repo-local/myartifact.zip .
```

---

### 🔐 Seguridad

- Control de acceso por usuario/grupo.
- Tokens de acceso.
- Escaneo de vulnerabilidades con **JFrog Xray**.
- Integración LDAP y SSO.



### 📚 Recursos Oficiales

- 🏠 Sitio oficial: [https://jfrog.com](https://jfrog.com)
- 📘 Documentación de Artifactory: [https://jfrog.com/artifactory/](https://jfrog.com/artifactory/)
- 🧰 JFrog CLI: [https://jfrog.com/getcli/](https://jfrog.com/getcli/)
- 🧪 Ejemplos de integración: [https://github.com/jfrog](https://github.com/jfrog)



### 🧾 Resumen Rápido

| Comando / Acción | Descripción |
|------------------|--------------|
| `docker run ... artifactory-oss` | Inicia Artifactory local. |
| `.npmrc` o `Podfile` | Configura acceso desde npm o CocoaPods. |
| `jfrog rt upload` | Sube artefactos. |
| `jfrog rt download` | Descarga artefactos. |
| `jfrog rt del` | Borra artefactos antiguos. |
| `jfrog rt bce` / `jfrog rt bp` | Maneja builds completos. |



**Autor:** Guía generada por ChatGPT (Eduardo Fulgencio Comendeiro)  
**Fecha:** Octubre 2025  
**Versión:** 1.0.0  
