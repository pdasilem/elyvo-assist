# Elyvo Assist — Guía del usuario

> 🌐 Esta guía también está disponible en: [English](USER_GUIDE.md) · [Беларуская](USER_GUIDE.be.md) · [Deutsch](USER_GUIDE.de.md) · **Español** · [Français](USER_GUIDE.fr.md) · [Italiano](USER_GUIDE.it.md) · [Português](USER_GUIDE.pt.md) · [Русский](USER_GUIDE.ru.md) · [Українська](USER_GUIDE.uk.md)

Elyvo Assist es un asistente de IA de escritorio para reuniones, investigación y lluvias de ideas. Vive como una superposición translúcida sobre cualquier ventana, invocada con una tecla de acceso rápido. Puede escuchar tu micrófono y el audio del sistema, transcribir en tiempo real, ver tu pantalla y responder preguntas según el contexto, mientras permanece oculto para la compartición y grabación de pantalla.

Esta guía cubre la instalación y un resumen de las principales funciones.

- [Instalación](#instalación)
- [Primer inicio](#primer-inicio)
- [Permisos](#permisos)
- [La superposición y las teclas de acceso rápido](#la-superposición-y-las-teclas-de-acceso-rápido)
- [Resumen de funciones](#resumen-de-funciones)
- [Configuración](#configuración)
- [Actualización](#actualización)
- [Desinstalación](#desinstalación)
- [Solución de problemas](#solución-de-problemas)

---

## Instalación

Los instaladores y binarios se publican a través de [GitHub Releases](https://github.com/pdasilem/elyvo-assist/releases). Descarga el archivo correspondiente a tu plataforma desde la última versión. Todas las compilaciones son de 64 bits (`x86_64` / Apple Silicon).

Cada versión contiene, para la versión `X.Y.Z`:

| Plataforma | Archivo |
|----------|------|
| Windows | `elyvo-assist-X.Y.Z-windows-x64-setup.exe` |
| macOS (Intel) | `elyvo-assist-X.Y.Z-macos-x64.dmg` |
| macOS (Apple Silicon) | `elyvo-assist-X.Y.Z-macos-arm64.dmg` |
| Debian / Ubuntu | `elyvo-assist-X.Y.Z-linux-x86_64.deb` |
| Arch / Manjaro | `elyvo-assist-X.Y.Z-1-x86_64.pkg.tar.zst` (+ `install.sh`) |

### Windows

1. Descarga el instalador `...-setup.exe` (NSIS).
2. Ejecútalo y sigue las indicaciones. La aplicación se instala en `Program Files\Elyvo Assist`.
3. Inicia **Elyvo Assist** desde el menú Inicio.

### macOS

1. Descarga el `.dmg` correspondiente a tu chip: `macos-x64` para Intel, `macos-arm64` para Apple Silicon (M1/M2/M3 y posteriores).
2. Abre la imagen de disco y arrastra **Elyvo Assist** a **Aplicaciones**.
3. En el primer inicio, macOS puede advertir que la aplicación proviene de un desarrollador no identificado. Haz clic derecho en la aplicación → **Abrir** → **Abrir** para permitirla.

> **Requisitos en Linux.** Elyvo Assist está diseñado para el escritorio **KDE Plasma** sobre **Wayland**. La protección de captura de pantalla de la superposición se implementa mediante KWin (el compositor de KDE), por lo que el comportamiento de ocultación frente a la compartición de pantalla solo funciona en KDE/KWin. Otros entornos de escritorio (GNOME, etc.) pueden ejecutar la aplicación, pero las garantías de protección de captura no se aplican. También necesitas una sesión de **PipeWire** en ejecución para la captura del micrófono y del audio del sistema.

### Linux — Debian / Ubuntu

```bash
sudo apt install ./elyvo-assist-X.Y.Z-linux-x86_64.deb
```

`apt` resuelve las dependencias de tiempo de ejecución (WebKitGTK 4.1, OpenSSL 3, PipeWire). En versiones más antiguas de `apt`, usa `sudo dpkg -i ...` seguido de `sudo apt -f install` para incorporar las dependencias faltantes.

### Linux — Arch / Manjaro

La forma más rápida es el script de instalación publicado, que descarga el paquete, instala las bibliotecas del sistema necesarias y ejecuta `pacman` por ti:

```bash
curl -fsSL https://github.com/pdasilem/elyvo-assist/releases/latest/download/install.sh -o install.sh
bash install.sh
```

El script solo es compatible con sistemas basados en `pacman` e instalará los paquetes de tiempo de ejecución que falten (GTK3, WebKit2GTK 4.1, PipeWire, libayatana-appindicator, entre otros).

¿Prefieres hacerlo manualmente? Descarga el `.pkg.tar.zst` e instálalo directamente:

```bash
sudo pacman -U elyvo-assist-X.Y.Z-1-x86_64.pkg.tar.zst
```

---

## Primer inicio

1. **Inicia sesión.** Inicia sesión con **correo electrónico y contraseña**, un **código de un solo uso por correo electrónico** o **Google**. Las cuentas nuevas se crean desde la misma pantalla (correo electrónico → código de verificación → establecer una contraseña).
2. **Incorporación.** Un breve asistente de configuración te guía a través de algunos pasos, incluidos los **permisos** y la **creación de tu primer proyecto**, y termina con un paso **Sobre ti** en el que puedes adjuntar opcionalmente un archivo (`.pdf`, `.doc`, `.docx`, `.md`, `.txt`) para darle al asistente más contexto sobre ti. Puedes editar esto más tarde desde tu **Perfil**.
3. **Comienza a usarlo.** Después de la incorporación se abre el **Panel de control**. Invoca la superposición de chat en cualquier momento con la tecla de acceso rápido de alternancia (por defecto `Ctrl+\`).

---

## Permisos

Para escuchar y ver tu pantalla, Elyvo Assist necesita dos permisos a nivel del sistema operativo, solicitados durante la incorporación (onboarding):

- **Micrófono** — para capturar lo que dices.
- **Captura de pantalla** — para que *Preguntar sobre mi pantalla* pueda ver la ventana activa.

En **Windows** y **macOS**, esto se gestiona mediante los avisos habituales del sistema operativo. En **Linux**, concédelos cuando se soliciten; si niegas alguno por error, concédelo desde la configuración de privacidad de tu sistema operativo.

La configuración de audio y micrófono no se puede ajustar dentro de la app — Elyvo siempre usa el **dispositivo predeterminado** de tu sistema.

> En Linux, la captura del micrófono y del audio del sistema utiliza PipeWire y el portal de escritorio. Asegúrate de que PipeWire esté en ejecución (es el valor predeterminado en las versiones actuales de Manjaro y Ubuntu).

---

## La superposición y las teclas de acceso rápido

Elyvo Assist se maneja casi por completo con el teclado para que puedas usarlo sin salir de tu reunión. La superposición de chat flota sobre otras ventanas, se puede arrastrar y está **oculta de la compartición y grabación de pantalla** (consulta [protección de ventana](../README.md#window-protection-from-screen-sharing)).

Teclas de acceso rápido predeterminadas (todas reasignables en **Configuración → Combinaciones de teclas**):

| Acción | Predeterminada | Qué hace |
|--------|---------|--------------|
| Alternar visibilidad | `Ctrl+\` | Mostrar / ocultar la superposición de Elyvo |
| Preguntar a Elyvo | `Ctrl+Enter` | Preguntar sobre tu pantalla o el audio actual |
| Borrar chat | `Ctrl+R` | Borrar la conversación actual |
| Iniciar / detener sesión | `Ctrl+Shift+\` | Comenzar o finalizar una sesión de escucha |
| Mover superposición | `Ctrl+↑ / ↓ / ← / →` | Reposicionar la ventana en la pantalla |
| Desplazar respuesta | `Ctrl+Shift+↑ / ↓` | Desplazar la respuesta hacia arriba / abajo |

Para reasignar, abre **Configuración → Combinaciones de teclas**, haz clic en un atajo y presiona la nueva combinación.

---

## Resumen de funciones

### Sesiones

Una **sesión** es cuando Elyvo está escuchando activamente y manteniendo el contexto. Inicia o detén una sesión con `Ctrl+Shift+\`. Durante una sesión, Elyvo captura tu micrófono y el audio del sistema, lo transcribe en tiempo real y conserva la transcripción en curso como contexto para tus preguntas. Elyvo utiliza el dispositivo de entrada **predeterminado** de tu sistema (no puedes cambiarlo dentro de la aplicación); en Configuración puedes ver el dispositivo detectado y probar los niveles de tu micrófono y del audio del sistema con medidores en vivo.

### Preguntar sobre tu pantalla o audio

Presiona **Preguntar a Elyvo** (`Ctrl+Enter`) y Elyvo responde utilizando lo que actualmente se muestra en tu pantalla y el audio/transcripción reciente como contexto; útil para "resume lo que se acaba de decir", "qué es este error" o "redacta una respuesta a esto". También puedes escribir un mensaje normal en el cuadro de chat en cualquier momento.

### Acciones rápidas

Durante una sesión, el chat ofrece cinco acciones de un clic. Son **conscientes del rol**: cada una toma su significado de la situación y el objetivo del modo activo, así que el mismo botón ayuda de forma distinta según estés respondiendo, evaluando, negociando o aprendiendo.

- **Assist** — la sustancia que pide el momento: la respuesta a lo que te acaban de preguntar; una respuesta de referencia o una evaluación rápida cuando el que evalúa eres *tú*; la solución completa cuando la captura contiene una tarea. Es material para pensar, no palabras para decir en voz alta.
- **What should I say?** — la siguiente frase que deberías decir en voz alta, con tu voz, lista para usar tal cual.
- **Follow-up questions** — un conjunto de 3–4 preguntas que podrías hacer a continuación para avanzar hacia tu objetivo: un menú para elegir, no una sola línea.
- **What did they mean?** — descifra la última intervención de la otra parte: su idea, su intención y cualquier preocupación implícita no dicha.
- **Recap** — hasta tres puntos sobre lo que cambió, se decidió o se preguntó desde la última vez que consultaste.

Cómo funciona la rotación: en un modo de candidato, Assist responde la pregunta dirigida a ti; en un modo de evaluador, te da la respuesta de referencia con la que juzgar lo que oyes; en un modo de negociación, Follow-up questions se convierten en preguntas de sondeo. En un modo de clase o webinar, donde sobre todo escuchas, Assist explica en términos más sencillos el punto que se acaba de exponer, Follow-up questions pasan a ser preguntas para el ponente o comprobaciones de tu propia comprensión, y Recap te pone al día tras una distracción. Todo esto lo dirige el prompt de sistema del modo activo — los botones no cambian (ver **Modos de IA** más abajo).

### Modos de IA

Los **modos** te permiten adaptar el comportamiento del asistente a diferentes situaciones. Cada modo tiene su propio mensaje de sistema (system prompt) y una plantilla de notas opcional. Gestiónalos en **Modos**:

- Comienza desde la **Galería de plantillas** — sus plantillas las proporciona el servidor y cambian con el tiempo — o crea un modo desde cero.
- Edita el mensaje de sistema para establecer el tono, el rol y las reglas de esa situación.
- Adjunta **archivos de modo**: material de referencia que el asistente debe tener en cuenta para ese modo.
- Marca un modo como activo; siempre hay disponible un modo general/predeterminado.

### Chat ambiental de IA

El chat ambiental es un chat ligero y siempre disponible que te sigue a través de la aplicación y que puede acotarse a un proyecto. Forma parte del plan de pago (consulta **Configuración → Facturación**).

### Qué incluye tu plan

Elyvo funciona con cualquier plan; una suscripción ampliada eleva los límites y desbloquea el trabajo en equipo. A grandes rasgos, un plan superior te da:

- sesiones más largas y más frecuentes;
- margen para más proyectos y más documentos;
- la posibilidad de compartir un proyecto con otras personas — aceptar una invitación y trabajar en el proyecto de otra persona es posible en cualquier plan;
- usar la app en más de un dispositivo a la vez;
- el autoaprendizaje del asistente, para que mejore con tus sesiones.

Qué incluye tu plan actual y cómo cambiarlo está en **Configuración → Facturación**. Donde se aplica un límite, la app te lo indica en el momento en que lo alcanzas en lugar de fallar en silencio.

### Proyectos

Los **proyectos** agrupan sesiones relacionadas y le dan al asistente un contexto compartido y persistente. Dentro de un proyecto puedes gestionar:

- **Miembros** — ve quién está en el proyecto e invita a otros por correo electrónico (cada invitado aparece como *pendiente* hasta que acepta). Enviar invitaciones requiere un plan que incluya compartir; aceptar una invitación y trabajar en el proyecto de otra persona, no.
- **Memoria** — hechos y contexto que el asistente debe recordar en todas las sesiones de ese proyecto.
- **Reglas** — pautas que el asistente sigue para ese proyecto.
- **Configuración** — un **modo**, un **idioma de salida** y un **idioma de transcripción** por proyecto, además de **Enriquecer contexto**, un interruptor (desactivado por defecto) que permite al asistente extraer contexto relevante de tus *otras* sesiones dentro del mismo proyecto (recuperación entre sesiones).

Cuando alguien te invita a su proyecto, la invitación aparece en la parte superior de **Proyectos** con botones de **Aceptar** / **Rechazar**. El chat ambiental puede acotarse a un proyecto para que las respuestas se basen en la memoria y las reglas de ese proyecto.

Si el plan del propietario deja de incluir la función de compartir, el proyecto compartido pasa a ser de **solo lectura** para todos hasta que se eliminen sus miembros. No se borra nada, y el acceso completo vuelve en cuanto el proyecto deja de estar compartido — o el plan vuelve a incluir la función.

### Documentos

Elyvo puede mantener una biblioteca personal de documentos de referencia que puedes abrir como su propia superposición mientras trabajas, útil para tener a mano notas, un resumen o una lista de verificación durante una llamada.

- **Gestiona tus documentos.** En **Configuración → Recursos**, agrega archivos Markdown (`.md`) —de hasta **1 MB** cada uno— en *Tus documentos*, o elimina los que ya no necesites. Los documentos son privados para tu cuenta. Cuántos documentos puedes conservar depende de tu plan.
- **Habilita por proyecto.** Para el proyecto activo, marca los documentos que quieras tener listos a mano. Los documentos habilitados **se abren automáticamente como pestañas** en el visor de Documentos cada vez que lo abres para ese proyecto. Habilitar un documento controla lo que muestra el visor para ese proyecto; no introduce el contenido del archivo en las respuestas del asistente.
- **Abre el visor.** Desde el menú de sesión de la superposición de chat (el botón `···`), elige **Documentos**. Se abre como su propia ventana arrastrable que, al igual que la superposición principal, está **oculta de la compartición y grabación de pantalla**. El mismo elemento del menú la cierra.
- **Lee y cambia.** Cada documento se abre en su propia pestaña. Usa la pestaña **+** para abrir cualquiera de tus documentos, haz clic en una pestaña para cambiar y en **×** para cerrarla. El contenido se renderiza como Markdown con formato y sigue el tema y el tamaño de fuente de tu chat.

### Calendario y reuniones

Conecta **Google Calendar** (desde **Configuración → General**) para ver tus próximas reuniones dentro de Elyvo. En la tarjeta de una reunión, **«Unirse a la reunión →»** solo abre el enlace de la llamada (Zoom/Meet/Teams) en tu navegador, mientras que **«Tomar notas»** inicia una sesión de escucha. Poco antes de una reunión, Elyvo también muestra un recordatorio dentro de la app con su propio botón **«Tomar notas»**, que hace ambas cosas a la vez —inicia la sesión y abre el enlace de la llamada—, de modo que el asistente esté escuchando desde el momento en que te unes.

### Panel de control e historial

El **Panel de control** es tu base principal: enumera las sesiones anteriores en una lista con búsqueda agrupada por fecha (el cuadro de búsqueda está en la cabecera de la app) y te permite abrir el detalle de una sesión, que tiene tres pestañas: **Resumen** (el resumen de la reunión), **Transcripción** (la transcripción capturada) y **Uso** (las preguntas que le hiciste a Elyvo durante la sesión y sus respuestas). Úsalo para revisar o hacer seguimiento después de una reunión. En la pestaña **Resumen**, el botón de copiar copia todo el resumen de una vez.

### Memoria y autoaprendizaje

Elyvo mejora con el uso. En tu **Perfil** puedes revisar y editar:

- **Memoria del usuario** — hechos duraderos sobre ti y tus preferencias que el asistente aplica en todas partes.
- **Desambiguaciones** — aclaraciones que el asistente ha aprendido (por ejemplo, a qué "Juan" o a qué proyecto te refieres) para que deje de adivinar mal.

El autoaprendizaje depende de tu plan. Sin él, el asistente sigue usando todo lo que añadas tú — simplemente deja de recopilar hechos nuevos por su cuenta.

### Protección de ventana frente a la compartición de pantalla

La superposición es intencionalmente invisible a la captura para que puedas usarla durante una llamada compartida sin que aparezca en la transmisión. La cobertura varía según la plataforma; el [README principal](../README.md#window-protection-from-screen-sharing) es la matriz de referencia. En resumen:

- **Windows 11** — oculta de todos los tipos de captura de forma predeterminada.
- **Windows 10** — misma protección, pero **no garantizada**: una limitación conocida del sistema operativo puede mostrar la superposición como un rectángulo negro en la captura en lugar de ocultarla por completo.
- **Linux (KDE / KWin)** — oculta de la *grabación y compartición* de pantalla de forma predeterminada. En **KWin 6.7.0+ (Plasma 6.7+)** las *capturas de pantalla* estáticas también quedan ocultas de forma predeterminada — no se necesita parche. En KWin más antiguos (≤ 6.6.x), ocultarla de las *capturas de pantalla* estáticas (Spectacle/PrintScreen) requiere un parche de KWin de una sola vez, que debe volver a aplicarse tras las actualizaciones de KWin.
- **macOS** — utiliza el mismo mecanismo nativo de protección de contenido. Fiable en **macOS 14 y anteriores**; en **macOS 15 y posteriores** la indetectabilidad **no está garantizada** y la superposición puede aparecer en las capturas.

---

## Configuración

Abre Configuración desde el menú de usuario. Las pestañas son:

- **General** — preferencias principales, el dispositivo de entrada de audio detectado y los medidores de prueba de micrófono / audio del sistema, conexión con Google Calendar, opciones de captura de pantalla y **Buscar actualizaciones**.
- **Combinaciones de teclas** — ver y reasignar todas las teclas de acceso rápido.
- **Perfil** — tus respuestas de incorporación, la memoria del usuario y las desambiguaciones.
- **Seguridad** — opciones de seguridad de la cuenta, incluidos los dispositivos con sesión iniciada. En planes limitados a un solo dispositivo, iniciar sesión en otro sitio cierra la sesión aquí.
- **Idioma** — idioma de la interfaz / de las respuestas.
- **Recursos** — sube y gestiona tus documentos Markdown, y elige cuáles están habilitados para el proyecto activo (consulta [Documentos](#documentos)).
- **Facturación** — tu suscripción y plan: qué incluye y cómo cambiarlo. Tu plan controla el acceso a funciones de pago como el chat ambiental de IA, la función de compartir y los límites de proyectos y documentos.

---

## Actualización

Elyvo Assist **no** se actualiza a sí mismo, pero la comprobación de versión sí es automática: el servidor consulta GitHub periódicamente (aproximadamente cada 8 horas, más una vez al iniciar el servidor) en busca de nuevas versiones y, si encuentra una más reciente, envía a tu Panel de control un aviso descartable **«New version!»** (el título queda en inglés) con un enlace de descarga. También puedes activar manualmente **Buscar actualizaciones** en **Configuración → General** en cualquier momento para abrir directamente la página de [Releases](https://github.com/pdasilem/elyvo-assist/releases) en tu navegador.

Para actualizar, descarga el instalador más reciente para tu plataforma desde [Releases](https://github.com/pdasilem/elyvo-assist/releases) y ejecútalo sobre tu instalación existente: la configuración y el inicio de sesión se conservan.

- **Arch / Manjaro:** vuelve a ejecutar el `install.sh` de la última versión, o usa `sudo pacman -U` con el nuevo `.pkg.tar.zst`.
- **Debian / Ubuntu:** `sudo apt install ./elyvo-assist-<nueva-versión>-linux-x86_64.deb`.
- **Windows / macOS:** ejecuta el nuevo instalador / abre el nuevo DMG.

> Usuarios de Linux KDE con KWin anterior a 6.7.0: vuelve a aplicar el parche de captura de pantalla de KWin después de una actualización del sistema KWin si dependes de la protección de capturas de pantalla. Si la actualización te lleva a KWin 6.7.0 o posterior, el parche ya no es necesario — la protección está integrada.

---

## Desinstalación

- **Windows** — *Configuración → Aplicaciones → Aplicaciones instaladas → Elyvo Assist → Desinstalar*.
- **macOS** — arrastra **Elyvo Assist** desde *Aplicaciones* a la Papelera.
- **Debian / Ubuntu** — `sudo apt remove elyvo-assist`.
- **Arch / Manjaro** — `sudo pacman -R elyvo-assist`.

---

## Solución de problemas

**La superposición no aparece.** Asegúrate de que la aplicación esté en ejecución (comprueba la bandeja del sistema/la barra de menú) y presiona la tecla de acceso rápido de alternancia (`Ctrl+\`). En macOS, confirma que el permiso de Accesibilidad esté concedido; de lo contrario, las teclas de acceso rápido globales no se activarán.

**No se captura audio.** Comprueba el acceso al micrófono y a la captura de pantalla en la configuración de privacidad de tu sistema operativo, y luego usa la prueba de micrófono / audio del sistema en **Configuración → General** para confirmar los niveles. Elyvo utiliza el dispositivo de entrada predeterminado de tu sistema, así que configura el dispositivo correcto como predeterminado en los ajustes de sonido de tu sistema operativo. En Linux, confirma que PipeWire esté en ejecución.

**La superposición sigue apareciendo en las capturas de pantalla en Linux.** La *grabación/compartición* de pantalla está oculta de forma predeterminada. En KWin 6.7.0+ (Plasma 6.7+) las capturas de pantalla quedan ocultas de forma predeterminada; en KWin más antiguos, las capturas de pantalla estáticas requieren el parche de KWin de una sola vez descrito en el [README](../README.md#window-protection-from-screen-sharing) — vuelve a aplicarlo después de las actualizaciones de KWin.

**Problemas de inicio de sesión.** Prueba el método alternativo (correo electrónico/contraseña frente a Google) y asegúrate de que el reloj de tu sistema esté correcto; la validación de OAuth y de tokens es sensible al tiempo.

**Se cerró tu sesión de forma inesperada.** En planes limitados a un solo dispositivo, iniciar sesión en otro dispositivo cierra la sesión aquí: vuelve a iniciar sesión para continuar. Puedes revisar los dispositivos de tu cuenta en **Configuración → Seguridad**.

Para cualquier otro problema, abre un issue en el [repositorio de releases](https://github.com/pdasilem/elyvo-assist/issues).
