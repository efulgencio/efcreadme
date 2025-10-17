\# ======================================================================
\# 📘 Podfile — Ejemplo completo y documentado
\# ======================================================================

\# ------------------------------------------------------------
\# Define la versión mínima de iOS compatible con los Pods
\# Si se comenta, CocoaPods usará una versión por defecto (a menudo demasiado baja)
\# ------------------------------------------------------------
platform :ios, '15.0'

\# ------------------------------------------------------------
\# Define el origen del repositorio de especificaciones de pods
\# Por defecto CocoaPods usa el repo central (https://github.com/CocoaPods/Specs)
\# Si quieres usar repos privados o internos, puedes añadirlos aquí
\# ------------------------------------------------------------
source 'https://github.com/CocoaPods/Specs.git'
\# source 'https://github.com/miempresa/SpecsPrivado.git'

\# ------------------------------------------------------------
\# Define el uso de frameworks dinámicos (recomendado para proyectos Swift)
\# Si tus dependencias son puramente Objective-C, podrías omitirlo.
\# use_frameworks! convierte las dependencias en frameworks en vez de librerías estáticas.
\# ------------------------------------------------------------
use_frameworks!

\# ------------------------------------------------------------
\# Alternativa (si tienes dependencias mixtas Swift/Obj-C y hay conflictos):
\# use_frameworks! :linkage => :static
\# o
\# use_modular_headers!
\# Esto indica a CocoaPods cómo enlazar las dependencias
\# ------------------------------------------------------------
\# use_frameworks! :linkage => :static
\# use_modular_headers!

\# ------------------------------------------------------------
\# Define el tipo de instalación: 
\# - :classic → instalación normal
\# - :integrate_targets => false → no modificar el proyecto Xcode
\# - :clean => true → limpia antes de instalar
\# ------------------------------------------------------------
install! 'cocoapods', :clean => true, :warn_for_unused_master_specs_repo => false

\# ------------------------------------------------------------
\# Aquí empieza la definición de un "target"
\# Cada target representa un destino en Xcode (por ejemplo: app, extensión, test, widget, etc.)
\# ------------------------------------------------------------
target 'MyApp' do
  
  \# ------------------------------------------------------------
  \# Si tienes targets adicionales dentro del proyecto, puedes heredar configuraciones
  \# ------------------------------------------------------------
  \# inherit! :search_paths  → hereda los paths de búsqueda de pods del target principal
  \# inherit! :complete      → hereda todas las configuraciones
  \# ------------------------------------------------------------
  \# inherit! :complete
  
  \# ------------------------------------------------------------
  \# Ejemplo de dependencias con diferentes opciones de versión
  \# ------------------------------------------------------------
  
  \# Usa la versión exacta 5.0.1
  pod 'Toast-Swift', '5.0.1'
  
  \# Usa versiones 5.0.x (mayor o igual a 5.0.0 pero menor que 5.1.0)
  pod 'Alamofire', '~> 5.0'
  
  \# Usa siempre la última versión disponible
  pod 'SwiftyJSON'
  
  \# Instala desde una rama específica de un repositorio Git
  pod 'MyPrivateLibrary', :git => 'https://github.com/usuario/privado.git', :branch => 'develop'
  
  \# Instala desde un commit concreto
  pod 'CustomUI', :git => 'https://github.com/usuario/customui.git', :commit => 'a1b2c3d4'
  
  \# Instala desde un tag específico
  pod 'Charts', :git => 'https://github.com/danielgindi/Charts.git', :tag => 'v4.0.0'
  
  \# Instala desde un path local (por ejemplo, un pod en desarrollo)
  pod 'LocalPod', :path => '../LocalPod'

  \# ------------------------------------------------------------
  \# Configuración post-instalación (opcional)
  \# Puedes modificar configuraciones de build después de instalar los pods
  \# ------------------------------------------------------------
  post_install do |installer|
    installer.pods_project.targets.each do |target|
      \# Ejemplo: forzar la versión de compilador Swift para todos los pods
      target.build_configurations.each do |config|
        config.build_settings['SWIFT_VERSION'] = '5.0'
      end
    end
  end
end

\# ------------------------------------------------------------
\# Ejemplo de un segundo target (por ejemplo, pruebas unitarias)
\# ------------------------------------------------------------
target 'MyAppTests' do
  inherit! :search_paths
  pod 'Quick'
  pod 'Nimble'
end

install! 'cocoapods',
  :clean => true,                    \# Elimina archivos temporales antes de instalar
  :warn_for_unused_master_specs_repo => false,  \# Evita avisos innecesarios
  :integrate_targets => true         \# Integra los pods al proyecto Xcode
