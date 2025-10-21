# 🧩 Validación de Podspec en CocoaPods  
### Diferencias entre `pod spec lint` y `pod lib lint`

Cuando creas un **framework** o **librería CocoaPods**, es fundamental validar tu archivo `.podspec` antes de distribuirlo o integrarlo en otros proyectos.  
Para ello, CocoaPods ofrece dos comandos similares pero con propósitos distintos:

---

## ⚙️ `pod spec lint`
Valida el `.podspec` **como si ya estuviera publicado** en un repositorio (por ejemplo, GitHub o un spec repo privado).

### 🔍 Qué hace
- Descarga el código desde la fuente definida en `s.source` (`:git`, `:http`, etc.).
- Intenta compilarlo en un proyecto temporal.
- Verifica compatibilidad de plataformas, frameworks, dependencias y arquitectura.
- Detecta errores de linking, firmas o configuraciones faltantes.

### 🧠 Cuándo usarlo
- **Antes de publicar** tu Pod (por ejemplo, antes de subirlo a un repo remoto o GitHub).
- **Para validar distribución**, asegurando que otros puedan instalarlo.

### 💻 Ejemplo:
```bash
cd /Users/eofc/Projects/EfcFramework
pod spec lint EfcFramework.podspec --allow-warnings --verbose
```

### ✅ Resultado esperado
```
-> EfcFramework (1.0.0)
   - WARN  | license: Unable to find a license file
   EfcFramework.podspec passed validation.
```

---

## ⚙️ `pod lib lint`
Valida el `.podspec` **usando tu código local**, sin necesidad de tener un tag o repo remoto.

### 🔍 Qué hace
- Usa los archivos que tienes en tu disco (`s.source = { :path => "." }`).
- Compila localmente sin requerir un repositorio remoto.
- Ideal para desarrollo activo o pruebas internas.

### 🧠 Cuándo usarlo
- **Durante el desarrollo** del Pod, antes de subirlo a GitHub.
- Para probar que el `.podspec` compila bien localmente con los archivos actuales.

### 💻 Ejemplo:
```bash
pod lib lint EfcFramework.podspec --allow-warnings --skip-tests
```

El flag `--skip-tests` acelera el proceso evitando que CocoaPods cree proyectos de prueba innecesarios.

---

## 🧾 Diferencias clave

| Aspecto | `pod lib lint` | `pod spec lint` |
|----------|----------------|----------------|
| Fuente del código | Local (`:path => "."`) | Remota (`:git`, `:http`, etc.) |
| Requiere tag remoto | ❌ No | ✅ Sí (si usas `:tag`) |
| Uso típico | Desarrollo / pruebas locales | Validación antes de publicar |
| Tiempo de ejecución | Más rápido | Más completo |
| Verifica integridad de distribución | ❌ No | ✅ Sí |

---

## 💡 Recomendación práctica

1. Durante el desarrollo del framework:
   ```bash
   pod lib lint EfcFramework.podspec --allow-warnings --skip-tests
   ```
2. Antes de publicar o compartir:
   ```bash
   pod spec lint EfcFramework.podspec --allow-warnings --verbose
   ```

---

## 🚀 Ejemplo completo de flujo

```bash
# 1️⃣ Validar localmente (en desarrollo)
pod lib lint EfcFramework.podspec --allow-warnings --skip-tests

# 2️⃣ Subir cambios al repositorio remoto (GitHub)
git add .
git commit -m "Versión 1.0.0 estable"
git push origin main

# 3️⃣ Crear tag
git tag 1.0.0
git push origin 1.0.0

# 4️⃣ Validar distribución remota
pod spec lint EfcFramework.podspec --allow-warnings --verbose
```

---

✅ **Resultado final:**
Tu `.podspec` validado correctamente para uso local y remoto, garantizando que tu framework pueda instalarse sin errores desde CocoaPods.

```
EfcFramework.podspec passed validation.
```
