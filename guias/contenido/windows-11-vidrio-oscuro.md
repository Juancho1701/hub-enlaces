Guía paso a paso para dejar tu escritorio como el de la imagen: fondo negro de seda, barra tipo dock, menú Inicio translúcido y widgets a la derecha.

## Qué vamos a lograr

| Parte | Herramienta | Dificultad |
| --- | --- | --- |
| Fondo y modo oscuro | Configuración de Windows | Fácil |
| Barra de tareas flotante | Windhawk + TranslucentTB | Media |
| Menú Inicio de vidrio | Windhawk (Start Menu Styler) | Media |
| Reloj, clima, CPU/RAM/SSD y música | Rainmeter | Media-alta |
| Iconos del escritorio | Pack de iconos gris/glass | Fácil |

> **Nota honesta:** la imagen parece un render conceptual. Con estas herramientas se logra cerca de un 85-90% del look. Algunos detalles, como el desenfoque exacto del vidrio, pueden variar según tu versión de Windows 11.

## Paso 1. Crea un punto de restauración

Antes de tocar nada, guarda un respaldo del sistema. Si algo se ve mal, vuelves atrás en un minuto.

1. Abre Inicio y escribe **Crear un punto de restauración**.
2. Selecciona la unidad C: y pulsa **Configurar**.
3. Activa **Habilitar protección del sistema** y acepta.
4. Pulsa **Crear**, ponle un nombre (por ejemplo, *Antes del tema*) y espera a que termine.

> **Consejo:** este paso se hace una sola vez, pero repítelo antes de instalar mods nuevos.

## Paso 2. Activa el modo oscuro y pon el fondo

La base visual del diseño es un fondo negro con ondas de seda y todo el sistema en oscuro.

1. Ve a **Configuración > Personalización > Colores**.
2. Cambia el modo a **Oscuro** y activa **Efectos de transparencia**.
3. Ve a **Personalización > Fondo** y elige una imagen propia.
4. Busca un wallpaper 4K con la frase *black silk abstract wallpaper 4K*, o genera uno con IA pidiendo ondas de seda negra con brillos blancos suaves.

> **Consejo:** elige un fondo oscuro y sin mucho detalle en el lado derecho, porque ahí irán los widgets y se leen mejor.

## Paso 3. Instala Windhawk

Windhawk es un gestor de mods para Windows. Permite cambiar el aspecto de la barra de tareas y del menú Inicio sin reemplazar archivos del sistema, y cada mod se puede apagar con un clic.

1. Descárgalo desde [windhawk.net](https://windhawk.net) e instálalo en modo normal.
2. Ábrelo y ve a la pestaña **Explore**: ahí se buscan e instalan los mods.
3. Cada mod tiene un botón **Install** y, después, **Settings** para ajustarlo.

## Paso 4. Barra de tareas tipo dock flotante

En Windows 11 los iconos ya van centrados. Lo que falta es que la barra parezca una cápsula de vidrio separada del borde.

1. En Windhawk busca **Windows 11 Taskbar Styler** e instálalo.
2. En sus ajustes elige un tema translúcido tipo dock.
3. Opcional: instala **Taskbar height and icon size** para agrandar un poco los iconos.
4. Para más transparencia, instala **TranslucentTB** desde Microsoft Store y elige el estilo *Clear* o *Acrylic*.
5. Quita los widgets nativos: clic derecho en la barra, Configuración de la barra de tareas, y desactiva Widgets y Vista de tareas.

> **Consejo:** si el tema se ve raro, desactiva el mod en Windhawk y prueba otro. No pasa nada.

## Paso 5. Menú Inicio de vidrio

El menú de la imagen tiene buscador arriba, apps ancladas y una zona de Recomendadas con archivos recientes, todo sobre vidrio oscuro.

1. En Windhawk instala **Windows 11 Start Menu Styler**.
2. En sus ajustes elige un tema oscuro translúcido o acrílico.
3. Ve a **Configuración > Personalización > Inicio** y activa **Mostrar elementos recientes**.
4. Ancla tus apps: clic derecho sobre una app y **Anclar a Inicio** (Edge, VS Code, Figma, GitHub, etc.).

## Paso 6. Widgets con Rainmeter

Rainmeter pone pequeños paneles sobre el escritorio. Con él se replican el reloj, el clima, los tres medidores circulares y el reproductor de música.

1. Instala Rainmeter desde [rainmeter.net](https://www.rainmeter.net).
2. Busca skins tipo *glass dashboard* o *modern system monitor* (DeviantArt o r/Rainmeter). Se instalan abriendo el archivo `.rmskin`.
3. **Reloj y fecha:** viene incluido en casi todos los skins.
4. **Clima:** necesita una clave gratuita de un servicio de clima; el skin te indica cómo ponerla y tu ciudad.
5. **CPU / RAM / SSD:** medidores circulares que se leen directo del sistema, sin configuración.
6. **Música:** usa el plugin NowPlaying para mostrar lo que suena en Spotify.
7. Clic derecho en cada widget: activa **Click through** y **Keep on screen**, y arrástralos al lado derecho.

> **Consejo:** si quieres el diseño exacto de la imagen, se puede crear un skin personalizado con colores y bordes iguales.

## Paso 7. Iconos del escritorio

La imagen usa iconos grises con efecto de vidrio, a la izquierda: Este equipo, Proyectos, Assets, Descargas y Papelera.

1. Descarga un pack de iconos gris/glass monocromo (DeviantArt o icon-icons.com).
2. Para tus carpetas: clic derecho, **Propiedades > Personalizar > Cambiar icono**.
3. Para Este equipo y Papelera: **Personalización > Temas > Configuración de iconos del escritorio > Cambiar icono**.
4. Alinéalos en una columna a la izquierda: clic derecho en el escritorio, Ver, desactiva *Organizar iconos automáticamente* y arrástralos.

## Paso 8. Ajustes finales

Con todo instalado, falta pulir para que se vea cohesionado.

1. Reinicia el Explorador: Administrador de tareas, Explorador de Windows, clic derecho y **Reiniciar**.
2. Revisa que los widgets no tapen iconos y que haya aire entre ellos.
3. Ajusta la opacidad de cada skin de Rainmeter (clic derecho, Opacity).
4. Reinicia el equipo una vez para confirmar que todo se carga al arrancar.

## Si algo sale mal

| Problema | Solución |
| --- | --- |
| Un mod de Windhawk se ve mal | Ábrelo en Windhawk y pulsa **Disable**. Se revierte al instante. |
| El Explorador se cierra o se congela | Reinícialo desde el Administrador de tareas. |
| Algo grave | Usa el punto de restauración del paso 1 (Inicio, Recuperación, Abrir Restaurar sistema). |
| Tras una actualización grande de Windows un mod deja de funcionar | Espera a que Windhawk lo actualice. |
