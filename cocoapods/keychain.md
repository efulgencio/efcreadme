### 🔐 Guía de Tipos de Keychain en iOS

Esta guía explica los principales tipos (`kSecClass`) del Keychain en iOS y macOS, sus usos y ejemplos reales.


### 1️⃣ kSecClassGenericPassword
**Contraseñas o datos genéricos (la más común).**

Representa contraseñas o datos sensibles no vinculados a Internet.
Se usa para guardar tokens, credenciales locales o cualquier dato sensible.

**Ejemplo:**
```swift
let query = [
    kSecClass: kSecClassGenericPassword,
    kSecAttrAccount: "userEmail",
    kSecValueData: "eduardo@example.com".data(using: .utf8)!
] as CFDictionary
SecItemAdd(query, nil)
```

### 2️⃣ kSecClassInternetPassword
**Credenciales de servicios de Internet.**

Diseñada para guardar contraseñas de servidores o sitios web, con atributos específicos.

**Ejemplo:**
```swift
let query = [
    kSecClass: kSecClassInternetPassword,
    kSecAttrAccount: "user123",
    kSecAttrServer: "api.misitio.com",
    kSecAttrProtocol: kSecAttrProtocolHTTPS,
    kSecValueData: "secreto123".data(using: .utf8)!
] as CFDictionary
SecItemAdd(query, nil)
```

### 3️⃣ kSecClassCertificate
**Certificados digitales (solo parte pública).**

Representa un certificado X.509 (.cer, .der) que contiene la parte pública.

**Ejemplo:**
```swift
let certData = try! Data(contentsOf: Bundle.main.url(forResource: "myCert", withExtension: "cer")!)
let certificate = SecCertificateCreateWithData(nil, certData as CFData)!

let query = [
    kSecClass: kSecClassCertificate,
    kSecValueRef: certificate,
    kSecAttrLabel: "myCert"
] as CFDictionary
SecItemAdd(query, nil)
```


### 4️⃣ kSecClassKey
**Claves criptográficas (pública o privada).**

Representa una clave RSA, EC o AES, usada para firmar o cifrar datos.

**Ejemplo:**
```swift
var attributes: [String: Any] = [
    kSecAttrKeyType as String: kSecAttrKeyTypeRSA,
    kSecAttrKeySizeInBits as String: 2048,
    kSecAttrIsPermanent as String: true,
    kSecAttrApplicationTag as String: "com.myapp.privatekey"
]
var error: Unmanaged<CFError>?
if let privateKey = SecKeyCreateRandomKey(attributes as CFDictionary, &error) {
    print("✅ Clave privada generada y guardada en Keychain.")
}
```


### 5️⃣ kSecClassIdentity
**Certificado + clave privada asociada.**

Representa una identidad completa (certificado + clave privada).  
Normalmente se importa desde un archivo .p12 o .pfx.

**Ejemplo:**
```swift
let options = [kSecImportExportPassphrase as String: "1234"]
var items: CFArray?
SecPKCS12Import(p12Data as CFData, options as CFDictionary, &items)

let identity = (items as! [[String: Any]]).first![kSecImportItemIdentity as String] as! SecIdentity

let query = [
    kSecClass: kSecClassIdentity,
    kSecValueRef: identity,
    kSecAttrLabel: "miIdentidad"
] as CFDictionary
SecItemAdd(query, nil)
```


### 📘 Resumen

| Tipo | Qué almacena | Ejemplo de uso |
|------|---------------|----------------|
| kSecClassGenericPassword | Datos genéricos, tokens, contraseñas | Tokens JWT, PIN |
| kSecClassInternetPassword | Credenciales de red | Usuario y password de API o FTP |
| kSecClassCertificate | Certificados X.509 públicos | Guardar .cer |
| kSecClassKey | Claves criptográficas | Firmar o cifrar datos |
| kSecClassIdentity | Certificado + clave privada | Importar .p12 |


## ⚠️ Consejos prácticos
- En la mayoría de las apps iOS se usa `kSecClassGenericPassword`.
- Cada tipo tiene su conjunto de atributos (`kSecAttr...`) válidos.
- Usar un atributo incorrecto produce el error `errSecParam`.
- Los elementos del Keychain están cifrados por el sistema y persistentes.

