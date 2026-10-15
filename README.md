# ☕ Taller de Cafetería Artesanal

## Ejercicio Avanzado — Accesibilidad Avanzada, WCAG y Componentes Interactivos de UI

### Requisitos previos

Antes de comenzar, es necesario:

* Tener instalado Google Chrome.
* Instalar la extensión **WAVE** en Google Chrome.
* (Opcional recomendado) Tener un lector de pantallas configurado (como NVDA en Windows o VoiceOver en macOS) para pruebas de accesibilidad auditiva y de foco.

---

### 1. Iniciar el proyecto

Antes de comenzar con el ejercicio, preparar una copia propia del repositorio y ejecutar el proyecto de forma local.

1. Realizar un fork del repositorio del taller de cafetería. A partir de este punto, todos los cambios se realizarán sobre la copia creada.
2. Copiar la URL del fork y clonar el repositorio en la computadora:
```bash
git clone URL_DEL_FORK

```


3. Abrir la carpeta del proyecto en Visual Studio Code.
4. Abrir una terminal dentro de Visual Studio Code y ejecutar:
```bash
npm install

```


5. Una vez finalizada la instalación, ejecutar:
```bash
npm run dev

```


6. Abrir en Google Chrome la dirección local que aparece en la terminal.

---

### 2. Auditoría profunda y criterios WCAG (Nivel AA) 🔎

El sitio actual de la cafetería cuenta con múltiples fallas estructurales y de interfaz que no solo afectan las herramientas automáticas, sino también la navegación puramente por teclado y tecnologías de asistencia.

1. **Estructura semántica y Jerarquía de Encabezados (WCAG 1.3.1 y 2.4.6):**
* Inspeccionar el archivo `index.html`. Identificar y corregir saltos en la jerarquía de encabezados (`<h1>` a `<h6>`).
* Asegurar que las secciones principales utilicen elementos semánticos de HTML5 (`<header>`, `<nav>`, `<main>`, `<section>`, `<article>`, `<footer>`) en lugar de contenedores genéricos `<div>` mal rotulados.


2. **Gestión de Foco y Componentes Interactivos Customizados (WCAG 2.1.1 y 2.4.3):**
* El componente de menú desplegable de categorías ("Nuestros Orígenes") está construido de forma personalizada con JavaScript y carece de gestión de foco y atributos ARIA adecuados.
* Implementar la navegación por teclado completa (flechas arriba/abajo, `Escape` para cerrar, `Enter`/`Space` para desplegar) y asegurar el orden lógico del foco (`tabindex`).



---

### 3. Accesibilidad en Formularios Complejos y Modales 📋

El formulario de reservas y el modal de información nutricional presentan barreras críticas de accesibilidad que deben resolverse mediante el estándar WCAG y roles ARIA.

1. **Asociación explícita y Mensajes de Error Dinámicos (WCAG 3.3.1 y 3.3.3):**
* Asegurar que todos los campos del formulario de reservas posean etiquetas asociadas mediante la dupla `for` / `id`.
* Cuando ocurra un error de validación, el mensaje de error no debe mostrarse únicamente por un cambio de color. Debe enlazarse dinámicamente al campo mediante el atributo `aria-describedby` y utilizar `aria-invalid="true"` en los campos erróneos.
* Añadir notificaciones de estado usando regiones en vivo (`aria-live="polite"`).


2. **Trampa de Foco y Accesibilidad en el Modal (WCAG 2.1.2 — No Keyboard Trap / Foco en Modales):**
* El botón "Ver información de alérgenos" abre una ventana modal flotante. Actualmente, al abrir el modal, el foco del teclado no se traslada al interior de este, y el usuario puede tabular hacia elementos del fondo de la página.
* **Requisito:** Al abrir el modal, el foco debe trasladarse obligatoriamente al primer elemento interactivo del modal (el botón de cierre `×`).
* Implementar una **trampa de foco (Focus Trap)** para que al presionar la tecla `Tab` o `Shift + Tab` dentro del modal, el foco no escape de este hasta que se cierre, momento en el cual el foco debe retornar exactamente al botón que lo invocó originalmente.



---

### 4. Contraste de Color Avanzado y Estados de Interfaz 🎨

1. **Verificación de Contraste (WCAG 1.4.3 y 1.4.11):**
* Analizar con la herramienta WAVE y herramientas de color (como Color Contrast Analyser) el texto secundario sobre los fondos de tarjetas de productos y los botones flotantes de redes sociales.
* Modificar las reglas en `src/interface/style.css` para garantizar que la razón de contraste cumpla con el mínimo exigido de **4.5:1** para texto normal y **3:1** para elementos gráficos y componentes de interfaz (botones, bordes de inputs activos).
* Asegurarse de que el enfoque visual (outline o indicador de foco) de los elementos interactivos sea claramente visible y no se haya eliminado con propiedades como `outline: none` sin un reemplazo accesible.



---

### 5. Comprobación y Verificación Final 🚀

Para finalizar, realizar una verificación integral del sistema:

1. Ejecutar **WAVE** nuevamente sobre la página local.
2. Realizar una prueba de **navegación exclusivamente por teclado** (sin usar el mouse en ningún momento): verificar que se puede recorrer todo el sitio, abrir el menú desplegable, interactuar con el formulario y operar la ventana modal sin perder el hilo del foco.
3. Comprobar que los cambios aplicados en la interfaz de usuario no hayan roto la adaptabilidad ni el diseño responsive.

👀 **Resultado esperado:** El sitio web cumple con los estándares WCAG de nivel AA en sus componentes críticos de UI, los modales gestionan correctamente el foco, el formulario comunica errores mediante atributos ARIA y toda la navegación es 100% operable mediante teclado y tecnologías de asistencia.
