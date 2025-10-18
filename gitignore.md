´´´gitignore
# ============================================
# 🧩 Xcode & macOS
# ============================================

# Archivos temporales de compilación
build/
DerivedData/

# Configuración de usuario
*.pbxuser
!default.pbxuser
*.mode1v3
!default.mode1v3
*.mode2v3
!default.mode2v3
*.perspectivev3
!default.perspectivev3
xcuserdata/

# Archivos de estado
*.moved-aside
*.xccheckout
*.xcscmblueprint

# ============================================
# 🍏 Swift / iOS
# ============================================

# Archivos de cache y logs
*.hmap
*.ipa
*.dSYM.zip
*.dSYM

# Archivos de playgrounds
timeline.xctimeline
playground.xcworkspace

# ============================================
# ☕️ CocoaPods
# ============================================

# Ignorar el directorio de Pods
Pods/

# Si usas la integración de CocoaPods en tu workspace
*.xcworkspace

# ============================================
# 🧠 Swift Package Manager (opcional)
# ============================================

# Ignorar artefactos del SPM
.build/
.swiftpm/

# ============================================
# 💻 macOS específicos
# ============================================

.DS_Store
.AppleDouble
.LSOverride

# Iconos del sistema
Icon
._*

# Archivos temporales
.Spotlight-V100
.Trashes
*.swp
*.lock
*.tmp

# ============================================
# 🔒 Archivos sensibles o locales
# ============================================

# Configuraciones locales
*.env
*.local

# ============================================
# 🧱 Otros (opcional)
# ============================================

# Archivos de logs
*.log

# Backups de editores
*~

´´´

📌 Instrucciones:
Crea el archivo .gitignore en la raíz de tu repositorio (junto al .xcodeproj o .xcworkspace).
Pega este contenido.
Ejecuta en la terminal:

´´´
git rm -r --cached .
git add .
git commit -m "Añadir .gitignore para Xcode + CocoaPods"
´´´

Esto limpia del índice los archivos ignorados previamente subidos (por ejemplo, Pods/ o DerivedData/) y deja solo lo necesario.