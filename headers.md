### 📘 Guía de Parámetros de Cabecera en una Petición HTTP

Este documento explica los **parámetros de cabecera (headers)** utilizados en una petición HTTP, sus funciones más comunes y ejemplos prácticos.


### 🧠 ¿Qué son las cabeceras HTTP?

Las **cabeceras HTTP** (o *HTTP headers*) son pares clave-valor que se envían junto con una petición o respuesta HTTP.  
Sirven para **transmitir metadatos** sobre la comunicación, como el tipo de contenido, autenticación, idioma, caché, y más.


### ⚙️ Estructura básica de una petición HTTP

```http
GET /api/usuarios HTTP/1.1
Host: api.ejemplo.com
Authorization: Bearer 123abcTOKEN
Content-Type: application/json
Accept: application/json
User-Agent: MiApp/1.0
```

### 🔑 Cabeceras comunes en las peticiones HTTP

| Cabecera | Descripción | Ejemplo |
|-----------|--------------|---------|
| **Authorization** | Envía credenciales de autenticación (token, Basic Auth, etc.). | `Authorization: Bearer eyJhbGciOiJIUzI1NiIs...` |
| **Content-Type** | Indica el formato del cuerpo de la petición. | `Content-Type: application/json` |
| **Accept** | Especifica qué formato de respuesta acepta el cliente. | `Accept: application/json` |
| **User-Agent** | Identifica al cliente que realiza la petición. | `User-Agent: MiApp/1.0 (iOS)` |
| **Cache-Control** | Controla el almacenamiento en caché. | `Cache-Control: no-cache` |
| **Accept-Language** | Indica el idioma preferido para la respuesta. | `Accept-Language: es-ES` |
| **Host** | Indica el dominio al que se hace la petición. | `Host: api.ejemplo.com` |
| **Referer** | Indica la URL de origen desde la que se realizó la solicitud. | `Referer: https://ejemplo.com/login` |
| **Origin** | Indica el origen de la solicitud, usada en CORS. | `Origin: https://miapp.com` |


### 🧩 Ejemplo práctico con `fetch` en JavaScript

```js
fetch("https://api.ejemplo.com/usuarios", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
    "Authorization": "Bearer 123abcTOKEN",
    "Accept": "application/json",
  },
  body: JSON.stringify({ nombre: "Eduardo", edad: 30 }),
})
  .then((res) => res.json())
  .then((data) => console.log(data))
  .catch((err) => console.error(err));
```


### 🐍 Ejemplo práctico con `requests` en Python

```python
import requests

url = "https://api.ejemplo.com/usuarios"
headers = {
    "Content-Type": "application/json",
    "Authorization": "Bearer 123abcTOKEN",
    "Accept": "application/json"
}
data = {"nombre": "Eduardo", "edad": 30}

response = requests.post(url, headers=headers, json=data)

print(response.status_code)
print(response.json())
```


### 🧱 Ejemplo de respuesta HTTP con cabeceras

```http
HTTP/1.1 200 OK
Content-Type: application/json
Date: Sat, 18 Oct 2025 08:00:00 GMT
Server: Apache/2.4.41 (Ubuntu)
Cache-Control: no-store
```

**Cuerpo de respuesta:**
```json
{
  "status": "ok",
  "mensaje": "Usuario creado correctamente"
}
```


### 🧭 Cabeceras personalizadas

Puedes definir tus propias cabeceras, siempre que empiecen con el prefijo `X-`:

```http
X-App-Version: 1.5.3
X-Device-ID: 9f2c-abc-34d
```

**Ejemplo:**
```js
fetch("https://api.ejemplo.com/datos", {
  headers: {
    "X-App-Version": "1.5.3",
    "X-Device-ID": "9f2c-abc-34d"
  }
})
```


### 🧩 Resumen rápido

- Las cabeceras **aportan contexto** a la comunicación HTTP.  
- Se pueden usar para **autenticación, caché, idioma, seguridad o formato de datos**.  
- Son clave-valor y pueden ser tanto estándar como personalizadas.

---

📄 **Autor:** Eduardo Fulgencio Comendeiro  
📅 **Última actualización:** Octubre 2025  
🔗 **Licencia:** MIT
