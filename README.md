# Mystic Booster - Auto Updater

Sistema de actualización automática para el plugin MysticBooster.

## 📋 Características

- ✅ Verificación automática de versiones
- ✅ Descarga e instalación automática
- ✅ Sistema de backup automático
- ✅ Restauración en caso de error
- ✅ Interfaz de consola con colores
- ✅ Barra de progreso de descarga

## 🚀 Uso

1. Ejecutar `MysticUpdater.exe`
2. El updater verificará si hay actualizaciones
3. Si hay una nueva versión, la descargará automáticamente
4. Reemplazará el DLL antiguo con el nuevo
5. Creará un backup del archivo anterior

## 📦 Estructura

```
test/
├── Updater/
│   ├── Updater.cs          # Código principal del updater
│   └── Updater.csproj      # Configuración del proyecto
├── version-example.json    # Ejemplo de archivo de versión remoto
└── README.md              # Este archivo
```

## 🔧 Configuración

### 1. Archivo de versión remoto (Pastebin/CDN)

Crea un archivo JSON en Pastebin con este formato:

```json
{
  "version": "2.0.1",
  "download_url": "https://your-cdn.com/mysticboosterv2.dll",
  "changelog": "Descripción de cambios",
  "release_date": "2025-01-09"
}
```

### 2. Configurar URLs en Updater.cs

Modifica estas constantes:

```csharp
private const string VERSION_URL = "https://pastebin.com/raw/YOUR_VERSION_FILE";
private const string DLL_DOWNLOAD_URL = "https://your-cdn.com/mysticboosterv2.dll";
```

### 3. Compilar el updater

```bash
cd test/Updater
dotnet build -c Release
```

El ejecutable estará en: `bin/Release/net472/MysticUpdater.exe`

## 📝 Sistema de Versionado

El updater usa **Semantic Versioning** (X.Y.Z):
- **X**: Versión mayor (cambios incompatibles)
- **Y**: Versión menor (nuevas funcionalidades)
- **Z**: Parche (correcciones de bugs)

Ejemplo: `2.0.1` → `2.1.0` → `3.0.0`

## 🔒 Seguridad

- El updater crea backups automáticos antes de actualizar
- Si falla la actualización, restaura el backup
- Usa HTTPS para descargas seguras
- Verifica integridad del archivo descargado

## 💡 Recomendaciones

1. **Hosting del DLL**: Usa servicios como:
   - GitHub Releases
   - Dropbox (con link directo)
   - Google Drive (con link directo)
   - Tu propio CDN/servidor

2. **Pastebin para versiones**: 
   - Usa Pastebin raw URL para el archivo de versión
   - Actualiza el JSON cada vez que liberes una nueva versión

3. **Testing**:
   - Prueba el updater antes de distribuirlo
   - Verifica que las URLs funcionen correctamente

## 🎯 Distribución

Distribuye estos archivos a tus usuarios:
- `MysticUpdater.exe` - El updater compilado
- `version.txt` - Archivo local de versión (opcional, se crea automáticamente)

## 🔄 Flujo de Actualización

```
Usuario ejecuta Updater.exe
         ↓
Lee version.txt local (versión actual)
         ↓
Descarga version.json remoto (versión disponible)
         ↓
Compara versiones
         ↓
Si hay actualización:
  - Crea backup del DLL
  - Descarga nuevo DLL
  - Reemplaza archivo
  - Actualiza version.txt
         ↓
Completado!
```

## 🐛 Troubleshooting

**Error de descarga:**
- Verifica que las URLs estén correctas
- Asegúrate de tener conexión a internet
- Comprueba que el firewall no bloquee el updater

**No detecta actualización:**
- Verifica el formato del JSON de versión
- Asegúrate de que version.txt tenga el formato correcto (X.Y.Z)

**Error al reemplazar archivo:**
- Cierra cualquier proceso que use el DLL
- Ejecuta el updater como administrador si es necesario
