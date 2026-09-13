# Blues

App personal (portafolios + gastos/ingresos diarios) empaquetada como Android APK usando Cordova + GitHub Actions. No necesitas Android Studio: GitHub compila el APK por ti en la nube.

## Estructura
- `www/index.html` → la app completa (todo el código vive en un solo archivo).
- `config.xml` → configuración de Cordova (nombre, id, permisos).
- `.github/workflows/build-apk.yml` → workflow que compila el APK automáticamente.

## Paso a paso desde el celular (Android)

**Opción recomendada: crear los archivos directamente en github.com (sin subir el .zip)**
Es más confiable desde el celular porque evita problemas al subir carpetas anidadas como `.github/workflows`.

1. Abre `github.com` en Chrome (inicia sesión).
2. Toca el `+` (arriba a la derecha) → **New repository**. Nómbralo, por ejemplo, `blues` y márcalo como **Privado** (importante, para discreción). Crea el repo.
3. Dentro del repo, toca **Add file → Create new file**.
4. En el campo de nombre, escribe la ruta completa `www/index.html` (GitHub crea la carpeta sola al detectar el `/`). Pega el contenido de ese archivo. Guarda con **Commit changes**.
5. Repite **Add file → Create new file** para:
   - `config.xml`
   - `package.json`
   - `.gitignore`
   - `.github/workflows/build-apk.yml`
   (En cada uno, escribe la ruta completa y pega el contenido correspondiente.)
6. Cuando subas el último archivo (el workflow), GitHub Actions se dispara solo. Ve a la pestaña **Actions** del repo y verás "Build APK" corriendo (tarda unos 5-10 minutos).
7. Cuando termine (check verde ✅), entra a esa ejecución y baja hasta **Artifacts** → descarga `blues-apk` (es un .zip que contiene el `.apk`).
8. Extrae el `.apk` de ese zip con tu gestor de archivos y ábrelo para instalarlo (Android te pedirá permitir "instalar apps de fuentes desconocidas" la primera vez).

**Opción alternativa: subir el .zip que te adjunto**
El .zip que generé tiene toda esta estructura de carpetas ya lista. Si prefieres subirlo tal cual:
1. Extrae el .zip en tu celular con un gestor de archivos (el propio "Archivos" de Android, o ZArchiver) para tener las carpetas sueltas.
2. Crea el repo igual que en el paso 1-2 de arriba.
3. Usa **Add file → Upload files** y selecciona los archivos ya extraídos. Ojo: la app oficial de GitHub y el navegador móvil no siempre preservan subcarpetas ocultas como `.github/workflows` al arrastrar un .zip completo sin extraer — por eso se recomienda extraerlo primero, o usar la Opción 1 si falla.
4. El resto es igual: revisa la pestaña Actions y descarga el APK cuando termine.

## Notas
- Los datos (portafolios, inversiones, gastos/ingresos) se guardan con `localStorage` dentro del propio APK — persisten entre aperturas de la app mientras no borres los datos de la aplicación desde Ajustes de Android.
- El primer build puede tardar más porque descarga el SDK de Android; builds siguientes son más rápidos.
- Si el build falla, revisa el log en la pestaña Actions — normalmente son temas de versión de Gradle/SDK que se resuelven actualizando `cordova-android` en `package.json`.
- El ícono/nombre de la app se ve como "Blues" en el teléfono, sin ninguna referencia a finanzas.
