### 📝 Guía de Formateo en Markdown

Este documento muestra ejemplos prácticos de **formateo Markdown** que puedes usar en tus propios archivos `.md`.


### 📚 Índice

1. [Títulos y subtítulos](#-títulos-y-subtítulos)
2. [Negrita, cursiva y tachado](#-negrita-cursiva-y-tachado)
3. [Listas](#-listas)
4. [Citas](#-citas)
5. [Enlaces e imágenes](#-enlaces-e-imágenes)
6. [Bloques de código](#-bloques-de-código)
7. [Tablas](#-tablas)
8. [Líneas divisorias](#-líneas-divisorias)
9. [Notas, avisos y tips](#-notas-avisos-y-tips)
10. [Ejemplo completo](#-ejemplo-completo)


### #️⃣ Títulos y subtítulos

Usa `#` para crear títulos y subtítulos.  
Cada `#` adicional baja un nivel jerárquico:

```markdown
# Título nivel 1
## Título nivel 2
### Título nivel 3
#### Título nivel 4
```

# Título nivel 1
## Título nivel 2
### Título nivel 3
#### Título nivel 4


### ✍️ Negrita, cursiva y tachado

```markdown
**Negrita**
*Cursiva*
~~Tachado~~
**_Negrita y cursiva_**
```

**Negrita**  
*Cursiva*  
~~Tachado~~  
**_Negrita y cursiva_**


### 🧾 Listas

### 🔹 Listas no ordenadas
```markdown
- Elemento 1
- Elemento 2
  - Sub-elemento A
  - Sub-elemento B
- Elemento 3
```

- Elemento 1
- Elemento 2
  - Sub-elemento A
  - Sub-elemento B
- Elemento 3

### 🔸 Listas ordenadas
```markdown
1. Paso uno
2. Paso dos
3. Paso tres
```

1. Paso uno
2. Paso dos
3. Paso tres


### 💬 Citas

```markdown
> Esta es una cita simple.
>
> Puedes escribir varias líneas y todas formarán parte de la misma cita.
```

> Esta es una cita simple.  
>  
> Puedes escribir varias líneas y todas formarán parte de la misma cita.


### 🔗 Enlaces e imágenes

### Enlace

```markdown
[Texto del enlace](https://www.google.com)
```

[Texto del enlace](https://www.google.com)

### Imagen

```markdown
![Texto alternativo](https://upload.wikimedia.org/wikipedia/commons/a/a7/React-icon.svg)
```

![Texto alternativo](https://upload.wikimedia.org/wikipedia/commons/a/a7/React-icon.svg)



### 💻 Bloques de código

Usa tres acentos graves ```` ``` ```` para encerrar el código.

### Ejemplo con lenguaje:
```swift
struct Persona {
    let nombre: String
    let edad: Int
}

let usuario = Persona(nombre: "Eduardo", edad: 35)
print(usuario)
```


### 📊 Tablas

```markdown
| Nombre     | Edad | Ciudad       |
|-------------|------|--------------|
| Ana         | 28   | Madrid       |
| Luis        | 34   | Barcelona    |
| Marta       | 22   | Valencia     |
```

| Nombre | Edad | Ciudad |
|--------|------|---------|
| Ana | 28 | Madrid |
| Luis | 34 | Barcelona |
| Marta | 22 | Valencia |



### 🧱 Líneas divisorias

```markdown
---
***
___
```

---
***
___



### 💡 Notas, avisos y tips

```markdown
> ⚠️ **Aviso:** Recuerda guardar tus cambios antes de cerrar.
> 💡 **Consejo:** Usa atajos de teclado para acelerar tu flujo de trabajo.
> ✅ **Hecho:** Configuración completada correctamente.
```

> ⚠️ **Aviso:** Recuerda guardar tus cambios antes de cerrar.  
> 💡 **Consejo:** Usa atajos de teclado para acelerar tu flujo de trabajo.  
> ✅ **Hecho:** Configuración completada correctamente.



### 🧩 Ejemplo completo

```markdown
# Proyecto Demo

## Descripción
Este proyecto demuestra cómo usar Markdown de forma efectiva.

### Características
- Código resaltado
- Tablas claras
- Secciones ordenadas

### Instalación
```bash
git clone https://github.com/usuario/proyecto-demo.git
cd proyecto-demo
```

### Uso
Ejecuta el siguiente comando:
```bash
swift run
```

### Licencia
MIT © 2025 Tu Nombre
```

# Proyecto Demo

## Descripción
Este proyecto demuestra cómo usar Markdown de forma efectiva.

### Características
- Código resaltado
- Tablas claras
- Secciones ordenadas

### Instalación
```bash
git clone https://github.com/usuario/proyecto-demo.git
cd proyecto-demo
```

### Uso
Ejecuta el siguiente comando:
```bash
swift run
```

### Licencia
MIT © 2025 Tu Nombre


📘 *Guía creada para practicar Markdown en archivos README.md*
