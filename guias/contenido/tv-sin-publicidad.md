Limpia la pantalla de inicio de tu Android TV desde el PC, por WiFi. Sin root, gratis y reversible: las apps de fábrica se desactivan, no se borran.

> **Paquete de archivos:** el paso 5 y los siguientes usan un paquete (.zip, 15 KB) con el parche, los scripts, el tema y las listas de ejemplo. Descárgalo desde la [versión original de esta guía](https://claude.ai/artifact/SwoYVpdLhj8njKFN3TF7Yu).

## Qué cambia y qué no

| Cambia | No cambia |
| --- | --- |
| La pantalla de inicio: reloj, saludo, dock compacto con tus apps y fondo a pantalla completa. | No se hace root ni se toca el firmware. |
| Las apps de fábrica de tu lista se desactivan y dejan de mostrar anuncios. | No se borran apps ni datos: puedes reactivarlas. |
| Los fondos rotan solos por horario (día, tarde, noche) con fundido suave. | Tus cuentas y sesiones (Netflix, YouTube…) siguen igual. |
| Botones redondos arriba: Entradas, WiFi, Energía, Ajustes. | Nada se envía a servidores: todo va entre tu PC y tu TV. |
| Se activa la depuración ADB, que apagas al terminar. | Una actualización del sistema puede reactivar apps o devolver el inicio de fábrica; se repite el proceso. |

El botón Input del control no abre de forma fiable el menú propio y el botón Energía no está verificado en todas las TV. Hazlo solo en TV propias.

## Antes de empezar

- Una TV con **Android o Google TV** y un PC con **Windows** en la misma red WiFi.
- **Python 3** y **Git**.
- **JDK 17 a 22** completo. Con JDK 23 o más nuevo, Gradle falla.
- **Android SDK** con plataforma 34 y build-tools 34.x (se instala desde el SDK Manager de Android Studio).
- Unos 40 minutos la primera vez. La segunda TV toma unos 10.

> **Atención:** desactivar el paquete equivocado puede dejar la TV sin pantalla de inicio. Por eso no se desactiva el asistente de fábrica hasta confirmar que el launcher nuevo funciona. Las listas de ejemplo son de una TCL 55C6K: en otra marca revisa cada paquete.

## Paso a paso

Reemplaza `<IP_DE_TU_TV>` por la IP de tu TV. Ejecuta todo en PowerShell, siempre desde la carpeta raíz **tv-vibehack**, salvo que se indique otra.

### 1. Activa el modo desarrollador en la TV

*En la TV, con el control.*

Ve a Ajustes, Sistema, Acerca de. Pulsa OK siete veces sobre «Compilación» hasta ver «Ya eres desarrollador». Luego entra a Opciones de desarrollador y activa **Depuración USB** y, si aparece, **Depuración ADB por red**. Anota la IP en Ajustes, Red, tu WiFi, Detalles.

### 2. Instala las herramientas en el PC

*En el PC.*

Instala Python 3, Git, un JDK entre 17 y 22 y Android Studio. Desde su SDK Manager instala «Android SDK Platform 34» y «Build-Tools 34.x». El adb oficial solo hace falta si tu TV pide código de emparejamiento.

```
python --version
git --version
java -version
```

### 3. Descarga el proyecto

*En el PC · PowerShell.*

```
git clone https://github.com/Gathin23/tv-vibehack
cd tv-vibehack
```

> **Atención:** esta es la carpeta raíz. Casi todos los errores vienen de ejecutar un script desde otra carpeta.

### 4. Prepara las herramientas del proyecto y conecta

*En el PC · carpeta raíz.*

```
python -m venv tools\venv
tools\venv\Scripts\python.exe -m pip install -r tools\requirements.txt
$env:TV_HOST = "<IP_DE_TU_TV>"
tools\venv\Scripts\python.exe -I tools\tv.py --probe
```

La TV mostrará «¿Permitir depuración?». Elige **Permitir siempre**. Si la prueba muestra el modelo y la versión de Android, estás conectado.

### 5. Aplica el parche

*En el PC · carpeta raíz.*

Descomprime el paquete y copia `launcher-compacto.patch` dentro de la carpeta **tv-vibehack**.

```
git apply --ignore-whitespace launcher-compacto.patch
```

Cambia 11 archivos: dock compacto, fondos por horario, botones redondos, botón de energía y servicio de la tecla Input.

### 6. Elige las apps de tu dock

*En el PC.*

Lista los paquetes de las apps que instalaste tú y copia los que quieras al archivo `launcher\app\src\main\res\values\config.xml`, en `dock_apps`. En `hidden_apps` pon las que no quieres ver.

```
tools\venv\Scripts\python.exe -I tools\tv.py "pm list packages -3"
```

### 7. Desactiva lo que sobra (debloat)

*En el PC · carpeta raíz.*

Copia `ejemplos\debloat.txt` del paquete a `examples\mi-tv\debloat.txt` (crea la carpeta). Es una lista de una TCL 55C6K: quita o comenta con `#` todo lo que no reconozcas. Guarda una copia. Nada se desinstala.

```
powershell -ExecutionPolicy Bypass -File tools\disable.ps1 -TvHost <IP_DE_TU_TV> examples\mi-tv\debloat.txt
```

> **Atención:** no desactives paquetes de WiFi, entradas HDMI (`com.tcl.tv`, `com.tcl.tvinput`), ni nada `com.mediatek.*` o Dolby. La lista de ejemplo explica cuáles se conservan a propósito.

### 8. Compila e instala el launcher

*En el PC · carpeta raíz.*

```
powershell -ExecutionPolicy Bypass -File launcher\build-and-install.ps1 -TvHost <IP_DE_TU_TV>
```

Compila, instala y lo deja como inicio. Si no queda como inicio, se revierte solo. Si dice *classes.dex en uso*, ejecuta `launcher\gradlew.bat --stop` y repite.

### 9. Desactiva el asistente de fábrica

*En el PC · solo si el paso 8 funcionó.*

Confirma que al pulsar Inicio abre tu launcher. Entonces aplica la segunda lista del paquete (`despues-del-launcher.txt`) igual que en el paso 7.

### 10. Instala el tema y los fondos

*En el PC · carpeta raíz.*

Crea la carpeta `themes\mi-tv` y copia ahí `config.json`, `instalar-tema.ps1`, `activar-input.ps1` y `limpiar-cache.ps1`. Dentro crea `fondos` con tus fotos JPG de 1920x1080 o más. El final del nombre decide cuándo se muestra: `-dia` (6 a 17 h), `-tarde` (17 a 19 h), `-noche` (el resto). Sin sufijo, todo el día.

```
powershell -ExecutionPolicy Bypass -File themes\mi-tv\instalar-tema.ps1 -TvHost <IP_DE_TU_TV>
```

En `config.json` ajusta `dock_apps`, `wallpaper_minutes` (1 a 1440) y `compact_ui`.

### 11. Opcional: tecla Input y limpieza

*En el PC · carpeta raíz.*

```
powershell -ExecutionPolicy Bypass -File themes\mi-tv\activar-input.ps1 -TvHost <IP_DE_TU_TV>
powershell -ExecutionPolicy Bypass -File themes\mi-tv\limpiar-cache.ps1 -TvHost <IP_DE_TU_TV>
```

La primera activa el servicio de la tecla Input (puede no funcionar con todos los controles). La segunda libera caché sin borrar datos.

### 12. Cierra y reinicia

*En la TV.*

Apaga la depuración ADB en Opciones de desarrollador, reinicia la TV y comprueba que abre tu inicio nuevo. Guarda la carpeta del proyecto y el paquete por si una actualización lo revierte.

## Si algo falla

| Síntoma | Causa | Solución |
| --- | --- | --- |
| `unauthorized` | No aceptaste el permiso en la TV | Reconecta y elige «Permitir siempre» |
| `class file major version 69` o Gradle falla | JDK 23 o más nuevo | Instala un JDK entre 17 y 22 y apunta `JAVA_HOME` a él |
| Script o archivo no encontrado | Carpeta equivocada | Haz `cd` a la raíz **tv-vibehack** primero |
| Scripts bloqueados por Windows | Política de ejecución | Usa `powershell -ExecutionPolicy Bypass -File …` |
| `classes.dex` en uso | Gradle tiene el archivo bloqueado | `launcher\gradlew.bat --stop` y repite |
| `git apply` falla | Saltos de línea o parche en otra carpeta | Usa `--ignore-whitespace` en la carpeta raíz, sobre una copia limpia |
| Se abre el asistente de configuración al pulsar Inicio | El asistente de fábrica sigue activo | Aplica la lista del paso 9 |
| Fondos borrosos o con bandas | Imágenes pequeñas o muy comprimidas | 1920x1080 o más, JPG con calidad alta |
| Aparecen apps extra en el dock | `columns` mal configurado | Usa `"columns": 4` en `config.json` |

## Cómo deshacerlo

```
powershell -ExecutionPolicy Bypass -File themes\mi-tv\instalar-tema.ps1 -TvHost <IP_DE_TU_TV> -Reset
powershell -ExecutionPolicy Bypass -File tools\restore.ps1 -TvHost <IP_DE_TU_TV> examples\mi-tv\debloat.txt -Stock com.google.android.apps.tv.launcherx
```

La primera quita el tema y los fondos. La segunda reactiva las apps de tu lista y el inicio de Google TV. En Android TV sin Google TV, omite `-Stock`. Último recurso: restablecimiento de fábrica, que borra cuentas.

## Créditos

Proyecto base: [tv-vibehack](https://github.com/Gathin23/tv-vibehack), de Gathin23 (licencia MIT). El parche, los scripts de tema y esta guía son trabajo derivado. Hazlo solo en TV que sean tuyas y bajo tu responsabilidad: el método no modifica el firmware, pero cada TV reacciona distinto.
