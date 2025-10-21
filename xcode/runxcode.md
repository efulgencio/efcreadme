
Cuando tengo dos XCode en el mac

```
XCode_26
XCode_16
```

**Primero activarlo en el terminal:**

```bash
sudo xcode-select -s /Applications/Xcode_16.app
```

**Comprobar la ruta activa del Developer Directory**

```bash
xcode-select -p
```

**Comprobar la versión del compilador**

```bash
clang --version
```

**Resultado del Terminal**

```bash
eofc@ESPC028208 ~ % xcode-select -p
/Applications/Xcode_16.app/Contents/Developer
eofc@ESPC028208 ~ % clang --version
Apple clang version 17.0.0 (clang-1700.0.13.5)
Target: arm64-apple-darwin24.6.0
Thread model: posix
InstalledDir: /Applications/Xcode_16.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/bin
eofc@ESPC028208 ~ %
```

