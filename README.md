# [Pagina web proyecto ISAT](https://ertis-research.github.io/ertis-page/)

El proyecto propone el desarrollo de un Sistema de Alerta Temprana inteligente (iSAT) para mejorar la gestión del agua subterránea en captaciones urbanas durante periodos de sequía. El iSAT integrará un conjunto de sensores de bajo coste para medir parámetros hidrogeológicos en continuo (nivel, caudal, conductividad, temperatura, turbidez y oxígeno disuelto), junto con algoritmos de inteligencia artificial (soft sensors) capaces de anticipar la disponibilidad y calidad del agua e identificar posibles episodios de contaminación. Los datos serán enviados de forma remota mediante comunicaciones multi-protocolo (GPRS, radio y satélite), garantizando la operatividad en entornos remotos. Con este sistema, se busca disponer de una herramienta predictiva y preventiva que apoye la toma de decisiones de gestores y operadores del agua, optimizando el aprovechamiento de acuíferos kársticos y reduciendo riesgos para el abastecimiento urbano.

Esta página web se ha desarrollado utilizando la herramienta de Hugo Blox [Hugo Landing Page Theme](https://github.com/HugoBlox/theme-landing-page)

----

## Personalización de la Plantilla Hugo Blox

Hugo Blox es un constructor de sitios web basado en bloques modulares, lo que permite personalizar páginas de manera flexible sin necesidad de conocimientos avanzados de código. A continuación, se explica cómo modificar la plantilla usando bloques existentes y creando nuevos archivos, basado en la experiencia del proyecto iSAT. Esta guía es reutilizable para cualquier sitio basado en Hugo Blox.

### 1. **Estructura General del Proyecto**
Antes de personalizar, familiarízate con la estructura de archivos:
- **`content/_index.md`**: Archivo principal donde defines las secciones (bloques) de la página de inicio. En este caso es un onepage, pero se pueden añadir nuevas páginas.
- **`layouts/`**: Contiene layouts personalizados (ej. `partials/blox/` para bloques nuevos).
- **`assets/css/`**: Archivos SCSS/CSS para estilos personalizados.
- **`public/css/`**: CSS compilado (no editar directamente). Este es descargado desde un punto remoto cada vez que se lanza el proyecto.
- **`data/`**: Archivos YAML/JSON para datos reutilizables (ej. listas de proyectos).
- **`config/_default/`**: Configuraciones globales (colores, menús, etc.).

### 2. **Usando Bloques Existentes**
Hugo Blox incluye bloques predefinidos como `hero`, `features`, `team`, etc. Para modificarlos:
- Edita `content/_index.md` y agrega o modifica secciones bajo `sections:`.
- Ejemplo para una sección "hero" (cabecera):

  ```yaml
  sections:
    - block: hero
      content:
        title: "Título Principal"
        text: "Descripción breve"
        primary_action:
          text: "Botón Principal"
          url: "#seccion"
      design:
        background:
          color: "bg-primary"  # Usa clases CSS personalizadas (predefinidas en la plantilla, por el momento los colores específicos están añadidos en los css)

### 3. **En caso de querer generar nuevos bloques**

**Paso 1:**
- Crea un layout en layouts/partials/blox/.
**ej:**
            {{ $page := .wcPage }}
            {{ $block := .wcBlock }}

            <section class="py-16 lg:py-24">
            <div class="container mx-auto px-6 lg:px-8">
                <h2>{{ $block.content.title }}</h2>
                ** Lógica personalizada aquí **
                {{ range $item := $block.content.items }}
                <div class="piloto-item">
                    <h3>{{ $item.title }}</h3>
                    <p>{{ $item.description }}</p>
                </div>
                {{ end }}
            </div>
            </section>
    
**Paso 2:**
- Agrega el bloque en el index
        - block: pilotos  <---- Nombre del archivo sin extensión (debe tener el nombre de el archivo)
        content:
            title: "Proyectos Piloto"
            items:
            - title: "Proyecto 1"
                description: "Descripción"


### ** Modificación y Significado de elementos**

### Inicialización de variables de Hugo Blox

    {{ $page := .wcPage }}
    {{ $block := .wcBlock }}

**¿Por qué se usa?**
Permite acceder fácilmente a los datos de la página y del bloque actual usando las variables $page y $block.

**¿Cómo modificar?**
No es necesario modificar esto salvo que quieras cambiar los nombres de las variables por claridad.


### Estructura principal del bloque

    <section class="py-16 lg:py-24">
        <div class="container mx-auto px-6 lg:px-8">
            ...
        </div>
    </section>

**¿Por qué se usa?**
Define el área del bloque con padding vertical (py-16, lg:py-24) y centra el contenido con un contenedor responsive.

**¿Cómo modificar?**
Cambia las clases de padding (py-16, etc.) para ajustar el espacio vertical.
Cambia el ancho del contenedor (max-w-3xl, etc.) si necesitas más o menos ancho.


### Título y subtítulo

    <div class="text-center mb-12">
        <h2 class="text-3xl font-bold ...">
            {{ with $block.content.title }}{{ . | markdownify }}{{ end }}
        </h2>
        {{ with $block.content.subtitle }}
            <p class="text-lg ...">
            {{ . | $page.RenderString | emojify }}
            </p>
        {{ end }}
    </div>

**¿Por qué se usa?**
Muestra el título y subtítulo definidos en el bloque del archivo _index.md.
 * markdownify permite usar Markdown en el título.
 * emojify convierte atajos de emoji en emojis reales.

**¿Cómo modificar?**
Cambia el texto en content/_index.md bajo el bloque objetivos (title y subtitle).
Cambia las clases para modificar el tamaño, color o alineación del texto.


### Lista de objetivos

    <div style="display: flex; justify-content: center;">
    <div class="objetivos-contenedor">
        <ul class="objetivos-lista">
        {{ range $item := $block.content.items }}
            <li class="objetivo-item">
            <span class="objetivo-viñeta">•</span>
            <div class="objetivo-contenido">
                <strong>{{ $item.title }}</strong> {{ $item.description | $page.RenderString | emojify }}
            </div>
            </li>
        {{ end }}
        </ul>
    </div>
    </div>

**¿Por qué se usa?**
Centra la lista de objetivos en la página.
Usa un <ul> para una lista semántica.
Cada objetivo se define en el YAML del bloque (items).
range recorre todos los objetivos definidos.
objetivo-viñeta es la viñeta (puedes cambiar el símbolo o usar un icono).
objetivo-contenido muestra el título y la descripción.

**¿Cómo modificar?**
Añade, quita o edita objetivos en content/_index.md bajo items del bloque objetivos.
Cambia el símbolo de la viñeta en <span class="objetivo-viñeta">•</span>.
Cambia las clases o estructura HTML para modificar el diseño de la lista.


### 4. **Modificar estilos**

Se debe añadir lo siguiente al bloque .html para referenciar los estilos:

    {{ $css := resources.Get "css/ejemplo.css" }} <--- ** Aquí se debe cambiar el nombre y la dirección del archivo**
    <link rel="stylesheet" href="{{ $css.RelPermalink }}">

En el archivo css se puede programar normalmente, ya que afecta directamente al .html.

