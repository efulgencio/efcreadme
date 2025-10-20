### Guía de Comandos de Git

### Índice

-   [Crear un nuevo repositorio en GitHub](#cómo-crear-un-nuevo-repositorio-en-github)
-   [Subir un repositorio local a GitHub (Método Manual)](#cómo-subir-un-repositorio-local-a-github-método-manual)
-   [Subir modificaciones a un repositorio existente](#cómo-subir-modificaciones-a-un-repositorio-existente)
-   [Revertir cambios en Git](#cómo-revertir-cambios-en-git)
-   [Sincronizar con cambios remotos](#cómo-sincronizar-con-cambios-remotos-antes-de-subir-los-tuyos)
-   [Resolver conflictos de fusión (Merge Conflicts)](#cómo-resolver-conflictos-de-fusión-merge-conflicts)
-   [Etiquetar commits con versiones (Tags)](#cómo-etiquetar-commits-con-versiones-tags)
-   [Buscar commits por su mensaje](#cómo-buscar-commits-por-su-mensaje)
-   [Ver el commit de un tag específico](#cómo-ver-el-commit-de-un-tag-específico)
-   [Identificar el repositorio remoto y el usuario local](#cómo-identificar-el-repositorio-remoto-y-el-usuario-local)
-   [Git vs. GitHub CLI: ¿Cuál es la diferencia?](#git-vs-github-cli-gh-cuál-es-la-diferencia)



### Cómo crear un nuevo repositorio en GitHub

Para crear un nuevo repositorio en GitHub desde la línea de comandos, la forma más sencilla es usar la herramienta oficial de GitHub, llamada **GitHub CLI** (`gh`).

### 1. Instalar GitHub CLI

Si no la tienes instalada, primero debes instalarla. Puedes encontrar las instrucciones para tu sistema operativo aquí: [https://cli.github.com/](https://cli.github.com/)

### 2. Autenticación

Una vez instalada, debes autenticarte con tu cuenta de GitHub. Ejecuta el siguiente comando y sigue los pasos:

```bash
gh auth login
```

### 3. Crear el repositorio

Una vez autenticado, puedes crear un nuevo repositorio directamente en tu cuenta (`efulgencio`).

**Opción A: Crear un repositorio nuevo y vacío**

```bash
gh repo create nombre-del-repositorio --public
```

**Opción B: Subir un proyecto local existente a un nuevo repositorio de GitHub con `gh`**

```bash
# Navega a la raíz de tu proyecto local ya inicializado con git
gh repo create nombre-del-repositorio --public --source=. --push
```



### Cómo subir un repositorio local a GitHub (Método Manual)

Si no tienes GitHub CLI (`gh`), este es el proceso tradicional.

### Paso 1: Crea un repositorio nuevo y vacío en la web de GitHub

-   Ve a [https://github.com/new](https://github.com/new).
-   Dale un nombre a tu repositorio (ej: `guia-git`).
-   Asegúrate de que sea **público** o **privado**.
-   **Importante**: NO selecciones "Initialize this repository with a README", ".gitignore" o una licencia. Queremos un repositorio vacío para poder subir el nuestro.
-   Copia la URL del repositorio que te proporciona GitHub. Tendrá un formato como `https://github.com/efulgencio/guia-git.git`.

### Paso 2: Enlaza tu repositorio local con el remoto

Estos comandos se ejecutan en tu terminal, dentro de la carpeta de tu proyecto (`git/` en nuestro caso).

```bash
# Comando para enlazar tu repositorio local con el que creaste en GitHub.
# 'origin' es el nombre estándar que se le da a la conexión remota.
# Reemplaza la URL por la que copiaste en el paso anterior.
git remote add origin https://github.com/efulgencio/guia-git.git
```

### Paso 3: (Opcional pero recomendado) Verifica la conexión

```bash
# Muestra los repositorios remotos que tienes configurados.
# Deberías ver 'origin' con la URL de tu repositorio en GitHub.
git remote -v
```

### Paso 4: (Opcional pero recomendado) Renombra tu rama principal a 'main'

Por defecto, `git init` puede crear la rama `master`, pero el estándar actual en GitHub es `main`.

```bash
# Renombra la rama actual a 'main' para seguir las convenciones de GitHub.
git branch -M main
```

### Paso 5: Sube tus cambios a GitHub

```bash
# Sube ('push') tus commits a la rama 'main' del repositorio remoto 'origin'.
# La opción '-u' (o --set-upstream) enlaza tu rama local 'main' con la remota.
# Solo necesitas usar '-u' la primera vez que subes una rama.
# Las próximas veces, solo necesitarás hacer 'git push'.
git push -u origin main
```
---

## Cómo subir modificaciones a un repositorio existente

Una vez que tu proyecto ya está en GitHub, el flujo para subir cambios es más sencillo.

### Paso 1: (Opcional pero recomendado) Revisa el estado de tus cambios

```bash
# Muestra los ficheros que has modificado, los que has creado y los que no están siendo rastreados por Git.
# Es una buena práctica para saber exactamente qué vas a subir.
git status
```

### Paso 2: Prepara los cambios para ser guardados (Staging)

Puedes añadir todos los ficheros modificados o solo algunos específicos.

```bash
# Opción A: Añade TODOS los ficheros modificados y nuevos al staging.
git add .

# Opción B: Añade solo un fichero específico.
git add nombre-del-fichero.txt
```

### Paso 3: Guarda los cambios en tu repositorio local (Commit)

Crea un "punto de guardado" en el historial de tu repositorio.

```bash
# Guarda los cambios que preparaste en el paso anterior.
# El mensaje ('-m') debe ser descriptivo de los cambios que hiciste.
git commit -m "Describe aquí tus cambios, ej: Actualiza la guía con nuevos comandos"
```

### Paso 4: Sube los cambios a GitHub

Envía los commits de tu repositorio local al remoto (GitHub).

```bash
# Sube los cambios a la rama principal ('main') del repositorio remoto ('origin').
# Si ya usaste 'git push -u origin main' la primera vez, ahora solo necesitas esto.
git push
```

### Crear una rama

```bash

# Crea una rama
git branch nombre-de-la-rama

git branch feature/nueva-funcionalidad

# Cambia a la rama creada

git branch feature/nueva-funcionalidad

# Con las sintaxis moderna

git switch nombre-de-la-rama


```


### Cómo revertir cambios en Git

Equivocarse es normal. Git ofrece maneras seguras de deshacer cambios.

### Escenario A: Revertir un commit que YA ha sido subido a GitHub

Esta es la forma más segura de deshacer cambios en un repositorio compartido, porque no reescribe el historial.

**`git revert`** crea un **nuevo commit** que deshace los cambios del commit que tú le indiques.

#### Paso 1: Encuentra el commit que quieres revertir

```bash
# Muestra el historial de commits. Cada commit tiene un 'hash' único (una larga cadena de letras y números).
# Copia el hash del commit que quieres revertir.
git log
```

#### Paso 2: Crea el commit de reversión

```bash
# Reemplaza 'hash-del-commit-a-revertir' por el que copiaste.
# Git creará un nuevo commit que es el opuesto al commit que quieres deshacer.
# Se abrirá un editor de texto para que confirmes el mensaje del nuevo commit. Simplemente guarda y cierra.
git revert hash-del-commit-a-revertir
```

#### Paso 3: Sube el nuevo commit a GitHub

```bash
# Ahora subes el commit de reversión, igual que subirías cualquier otro cambio.
git push
```

### Escenario B: Deshacer el último commit que AÚN NO ha sido subido

Si te das cuenta del error justo después de hacer `git commit` y **antes** de hacer `git push`, puedes usar `git reset`.

**`git reset`** mueve el puntero de la rama, efectivamente borrando commits. **¡Ten cuidado con este comando!**

#### Opción 1: Deshacer el commit pero mantener los cambios (Recomendado y seguro)

```bash
# Deshace el último commit, pero deja todos los ficheros modificados en tu área de trabajo (working directory).
# Es como si hubieras modificado los ficheros pero nunca hubieras hecho el commit.
# HEAD~1 se refiere al commit anterior al último.
git reset HEAD~1
```
Después de esto, puedes corregir los ficheros y hacer un nuevo commit.

#### Opción 2: Deshacer el commit Y TODOS los cambios (¡PELIGROSO!)

```bash
# ¡¡CUIDADO!! Este comando borrará permanentemente el último commit Y todas las modificaciones
# que contenía. Los cambios se perderán si no los tienes guardados en otro sitio.
git reset --hard HEAD~1
```

### Cómo sincronizar con cambios remotos (antes de subir los tuyos)

Para evitar conflictos, antes de subir tus cambios (`git push`), siempre es buena idea traer los cambios que otros han subido.

### Paso 1: Comprueba si hay cambios en el repositorio remoto (`fetch`)

El comando `git fetch` descarga la información más reciente del remoto (nuevos commits, nuevas ramas, etc.) pero **NO los integra en tus ramas locales**. Es una forma segura de "mirar" lo que hay.

```bash
# Contacta con el remoto 'origin' y descarga toda la información nueva.
# No afectará a tu trabajo local.
git fetch origin
```

### Paso 2: Revisa la diferencia entre tu local y el remoto

Después de hacer `fetch`, tu repositorio local sabe que existen nuevos commits, pero tu rama `main` todavía no los tiene.

```bash
# Compara tu rama local con la versión remota que acabas de descargar.
# Si no hay salida, estáis sincronizados.
# Si hay salida, te mostrará los commits que están en 'origin/main' pero no en tu 'main' local.
git log main..origin/main

# Una forma más rápida es usar 'git status'.
# Si tu rama está desactualizada, te dirá algo como:
# "Your branch is behind 'origin/main' by X commits, and can be fast-forwarded."
git status
```

### Paso 3: Integra los cambios remotos en tu repositorio local (`pull`)

Una vez que sabes que hay cambios, necesitas integrarlos. `git pull` es la forma más común de hacerlo. Es una combinación de `git fetch` y `git merge`.

```bash
# Descarga los cambios de 'origin' y los fusiona ('merge') en tu rama local actual.
# Es importante ejecutar este comando antes de empezar a hacer tus propios cambios
# o justo antes de subir los tuyos.
git pull origin main
```

**Flujo de trabajo recomendado:**

1.  Terminas de hacer tus cambios locales (`git add .`, `git commit -m "..."`).
2.  Antes de subir, sincronizas: `git pull origin main`.
3.  Si hay conflictos de fusión (Git te avisará), los resuelves.
4.  Finalmente, subes tus cambios: `git push origin main`.
---

## Cómo resolver conflictos de fusión (Merge Conflicts)

Un conflicto ocurre cuando haces `git pull` (o `git merge`) y Git no puede fusionar los cambios automáticamente. Esto suele pasar cuando tú y otra persona habéis modificado las **mismas líneas** en el **mismo fichero**.

Git se detendrá y te pedirá que resuelvas el conflicto manualmente.

### Paso 1: Identifica los ficheros en conflicto

Git te dirá exactamente qué ficheros tienen problemas. También puedes usar `git status`.

```bash
# Muestra el estado del repositorio.
# Los ficheros en conflicto aparecerán en la sección "Unmerged paths".
git status
```

### Paso 2: Abre el fichero y busca los marcadores de conflicto

Abre el fichero conflictivo en tu editor de código. Verás unos marcadores especiales que Git ha añadido:

```
<<<<<<< HEAD
// Este es el código que tienes en tu rama local (tus cambios).
console.log("Hola Mundo");
=======
// Este es el código que viene de la rama remota (los cambios de tu compañero).
console.log("Hello World");
>>>>>>> [hash-del-commit-remoto]
```

-   `<<<<<<< HEAD`: El inicio de tus cambios.
-   `=======`: Separa tus cambios de los cambios entrantes.
-   `>>>>>>> ...`: El final de los cambios entrantes.

### Paso 3: Edita el fichero para resolver el conflicto

Tu tarea es decidir cómo debe quedar el código final. Tienes varias opciones:
-   **Quedarte con tus cambios:** Borra los marcadores y el código de tu compañero.
-   **Aceptar los cambios entrantes:** Borra los marcadores y tu código.
-   **Combinar ambos:** Borra los marcadores y edita el código para que contenga una mezcla de ambos cambios.

**Ejemplo de resolución:**

Decides que quieres mantener ambos saludos. Editas el fichero para que quede así:

```
// Mantengo ambos saludos para el ejemplo.
console.log("Hola Mundo");
console.log("Hello World");
```
**Importante:** Asegúrate de borrar las líneas `<<<<<<< HEAD`, `=======` y `>>>>>>>`.

### Paso 4: Marca el conflicto como resuelto

Una vez que has guardado el fichero con la versión final, tienes que decírselo a Git.

```bash
# Añade el fichero al 'staging area', igual que harías con cualquier otro cambio.
# Esto le indica a Git que has resuelto el conflicto en ese fichero.
git add nombre-del-fichero-resuelto.txt
```

### Paso 5: Finaliza la fusión (Merge)

Si el conflicto ocurrió durante un `git pull`, el proceso de fusión está en pausa. Después de añadir todos los ficheros resueltos, solo tienes que completar la fusión.

```bash
# Git ya tiene preparado un mensaje de commit para la fusión.
# Simplemente ejecuta este comando para finalizar el proceso.
git commit
```
Se abrirá un editor de texto con un mensaje de commit por defecto (algo como "Merge branch 'main' of ..."). Simplemente guarda y cierra el editor para confirmar.

### Paso 6: Sube tus cambios (con la fusión resuelta)

Ahora que el conflicto está resuelto y el 'merge commit' está creado en tu repositorio local, puedes subir todo a GitHub.

```bash
git push
```

### Cómo etiquetar commits con versiones (Tags)

Los tags se usan para señalar puntos específicos en el historial de un repositorio, normalmente para marcar lanzamientos de versiones (ej: `v1.0.0`, `v2.1-beta`).

Se recomienda usar **tags anotados** (`-a`) para los lanzamientos, ya que guardan más información (autor, fecha, mensaje) que los tags ligeros.

### Paso 1: Crear un tag anotado en el último commit

Por defecto, el tag se crea sobre el último commit de la rama en la que te encuentras.

```bash
# Crea un tag anotado (-a) llamado 'v1.0.0' con un mensaje (-m).
# Es una convención común empezar los nombres de tags de versión con una 'v'.
git tag -a v1.0.0 -m "Lanzamiento de la versión 1.0.0"
```

### Paso 2 (Opcional): Etiquetar un commit antiguo

Si olvidaste etiquetar un commit en el pasado, puedes hacerlo si tienes su hash.

```bash
# Primero, busca el hash del commit que quieres etiquetar.
git log --oneline

# Luego, crea el tag apuntando a ese hash específico.
git tag -a v1.0.0 HASH_DEL_COMMIT -m "Lanzamiento de la versión 1.0.0"
```

### Paso 3: Sube el tag a GitHub

Por defecto, `git push` **NO** sube los tags. Tienes que hacerlo explícitamente.

```bash
# Opción A: Subir un solo tag específico (Recomendado y más seguro).
git push origin v1.0.0

# Opción B: Subir TODOS tus tags locales a la vez.
git push --tags
```

### Cómo ver y borrar tags

```bash
# Muestra una lista de todos tus tags locales.
git tag

# Borra un tag en tu repositorio local.
git tag -d v1.0.0

# Borra un tag en el repositorio remoto (GitHub).
# Esto requiere una sintaxis especial.
git push --delete origin v1.0.0
```

### Cómo buscar commits por su mensaje

Puedes buscar en el historial de commits por palabras clave en sus mensajes.

### Buscar en tu rama local actual

Este comando busca la palabra 'session' en todos los commits de la rama en la que te encuentras actualmente.

```bash
# La opción '--grep' filtra los commits cuyo mensaje contenga el texto indicado.
# La opción '-i' (opcional) hace que la búsqueda no distinga entre mayúsculas y minúsculas.
git log --grep="session" -i
```

### Buscar en una rama remota específica

Para buscar en una rama que está en `origin` (GitHub), primero asegúrate de tener la información más reciente del remoto.

```bash
# 1. Actualiza tu conocimiento de las ramas remotas.
git fetch

# 2. Busca en la rama 'main' de 'origin'.
git log origin/main --grep="session" -i
```

### Buscar en TODAS las ramas (locales y remotas)

Esta es la forma más completa de buscar, ya que revisa todo el historial conocido por tu repositorio.

```bash
# El flag '--all' le dice a git que busque en todas las ramas.
git log --all --grep="session" -i
```


## Cómo ver el commit de un tag específico

Para inspeccionar la información de un commit asociado a un tag, puedes usar `git show` o `git log`.

### Opción A: Usar `git show` (Recomendado)

Este comando es el más directo. Muestra la información del tag (si es anotado), la información completa del commit (autor, fecha, mensaje) y el `diff` (los cambios exactos que se introdujeron).

```bash
# Muestra toda la información del commit apuntado por el tag 'v1.0.0'.
git show v1.0.0
```

### Opción B: Usar `git log`

Si solo quieres ver la información del commit pero no los cambios del fichero, puedes usar `git log`.

```bash
# El '-1' limita la salida a un solo commit.
git log -1 v1.0.0
```


## Cómo identificar el repositorio remoto y el usuario local

Cuando estás dentro de una carpeta que es un repositorio de Git, puedes averiguar a qué remoto está conectado y qué usuario está configurado para hacer commits.

### 1. Ver el repositorio remoto

Este comando te muestra las URLs de los repositorios remotos a los que está conectado tu repositorio local. Normalmente verás uno llamado `origin`.

```bash
# La opción '-v' (verbose) muestra las URLs para 'fetch' (bajar) y 'push' (subir).
git remote -v
```
La URL te dirá el servidor (ej: `github.com`) y el nombre de usuario/organización y repositorio (ej: `efulgencio/guia-git.git`).

### 2. Ver el usuario configurado para los commits

Esta información es la que se usará como "autor" en los commits que hagas desde este repositorio.

```bash
# Muestra el nombre de usuario configurado.
git config user.name

# Muestra el email configurado.
git config user.email
```

**Importante:** El `user.name` y `user.email` de la configuración de Git **no es lo mismo** que tu cuenta de GitHub. Es simplemente la información de autoría que se guarda con cada commit. La autenticación para subir cambios a GitHub se maneja de forma separada (por ejemplo, con un token de acceso personal o a través de SSH).
---

## Git vs. GitHub CLI (gh): ¿Cuál es la diferencia?

Una pregunta común es: *“¿Cómo creo un repositorio en GitHub solo con Git?”*. La respuesta corta es que **no se puede**. Esta es la diferencia fundamental:

Aunque trabajan juntos, `git` y `gh` son dos herramientas distintas con propósitos diferentes.

### Git: El Sistema de Control de Versiones

-   **Es el motor:** `git` es el software fundamental que rastrea los cambios en tus ficheros.
-   **Funciona localmente:** Su principal responsabilidad es gestionar el historial de tu proyecto en tu propia máquina (crear commits, ramas, fusiones, etc.).
-   **Es universal:** Git es un estándar abierto y puede usarse con cualquier servicio de alojamiento (GitHub, GitLab, Bitbucket) o sin ninguno.
-   **Comandos clave:** `git add`, `git commit`, `git status`, `git branch`, `git merge`, `git push`.

### GitHub CLI (`gh`): Tu Mando a Distancia para GitHub

-   **Es el control remoto:** `gh` es una herramienta para interactuar con la plataforma **GitHub** desde tu terminal.
-   **Gestiona el repositorio remoto:** Te permite hacer cosas que normalmente harías en la página web de GitHub, como crear repositorios, gestionar Pull Requests, revisar Issues, ver workflows de Actions, etc.
-   **Necesita a Git:** A menudo, `gh` ejecuta comandos de `git` por debajo para clonar, subir o bajar cambios.
-   **Comandos clave:** `gh repo create`, `gh pr create`, `gh issue list`, `gh workflow run`.

### Analogía Sencilla

Piensa en **Git** como el motor y la transmisión de un coche. Es la tecnología esencial que gestiona el movimiento y los cambios.

Piensa en **GitHub CLI** como el salpicadero y los botones de ese coche. Te permite interactuar con las funciones del coche (crear un nuevo destino en el GPS, poner música) sin tener que manipular el motor directamente.