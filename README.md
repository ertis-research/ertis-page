# ERTIS Research Group Website

[![Deploy Status](https://img.shields.io/badge/deploy-success-brightgreen)](https://ertis-research.github.io/ertis-page/)
[![Hugo](https://img.shields.io/badge/Hugo-0.112+-blue.svg)](https://gohugo.io/)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE.md)

[🌐 Visita el sitio web oficial](https://ertis-research.github.io/ertis-page/)

Sitio web oficial del grupo de investigación **ERTIS (Embedded Real-Time Systems)** de la Universidad de Málaga, perteneciente al Instituto del Software ITIS.

## 🔬 Sobre ERTIS

ERTIS centra su actividad investigadora en mejorar la gestión, accesibilidad e integración de dispositivos embebidos en el contexto del Internet de las Cosas (IoT). Nuestras principales líneas de investigación incluyen:

- **Gemelos Digitales**: Desarrollo de frameworks componibles, interoperables y cognitivos
- **Deep Learning Distribuido**: Edge AI, Fog Computing y redes neuronales distribuidas
- **IoT, Edge y Fog Computing**: Middleware y arquitecturas distribuidas para dispositivos heterogéneos
- **Sistemas de Tiempo Real y Críticos**: Métodos que garantizan predictibilidad, seguridad funcional y ciberseguridad

## 🏗️ Tecnología

Este sitio está construido con [Hugo Blox Builder](https://hugoblox.com/), un constructor modular basado en bloques que permite personalizar páginas de forma flexible sin necesidad de conocimientos avanzados de código.

### Estructura del Proyecto

```
ertis-research.github.io/
├── content/              # Contenido de las páginas
│   ├── _index.md        # Página principal con secciones
│   ├── members.md       # Página de miembros del equipo
│   ├── projects.md      # Página de proyectos
│   ├── publications.md  # Publicaciones científicas
│   ├── news/            # Artículos de noticias
│   └── gallery/         # Galería de imágenes
├── layouts/             # Plantillas Hugo personalizadas
│   ├── _default/        # Layouts por defecto
│   └── partials/blox/   # Bloques personalizados
├── assets/
│   └── css/             # Estilos personalizados (SCSS/CSS)
├── data/                # Datos estructurados (JSON)
│   ├── members.json     # Información de miembros
│   ├── projects.json    # Información de proyectos
│   ├── publications.json # Publicaciones
│   └── visits.json      # Visitas y eventos
├── config/              # Configuración del sitio
│   └── _default/
│       ├── hugo.yaml    # Configuración principal de Hugo
│       ├── params.yaml  # Parámetros del sitio
│       └── menus.yaml   # Estructura de menús
└── public/              # Sitio compilado (generado automáticamente)
```

## 🚀 Inicio Rápido

### Prerrequisitos

- [Hugo Extended](https://gohugo.io/installation/) (v0.112.0 o superior)
- [Node.js](https://nodejs.org/) y pnpm (opcional, para procesamiento de assets)
- [Go](https://go.dev/) (v1.20+)

### Instalación

1. **Clonar el repositorio**
   ```bash
   git clone https://github.com/ertis-research/ertis-research.github.io.git
   cd ertis-research.github.io
   ```

2. **Instalar dependencias** (opcional)
   ```bash
   pnpm install
   ```

3. **Ejecutar el servidor de desarrollo**
   ```bash
   hugo server
   ```

4. **Acceder al sitio**
   Abre tu navegador en [http://localhost:1313](http://localhost:1313)

### Despliegue

El sitio se despliega automáticamente en GitHub Pages mediante GitHub Actions cuando se hace push a la rama principal.

## 📝 Guía de Personalización

### 1. Estructura General

El sitio utiliza un sistema de bloques modulares donde cada sección es un componente independiente:

- **`content/_index.md`**: Archivo principal que define las secciones de la página de inicio
- **`layouts/`**: Contiene layouts personalizados y bloques reutilizables
- **`assets/css/`**: Estilos personalizados que extienden Hugo Blox
- **`data/`**: Archivos JSON con datos estructurados (miembros, proyectos, etc.)
- **`config/_default/`**: Configuraciones globales (colores, menús, idiomas)

### 2. Usando Bloques Existentes

Hugo Blox incluye bloques predefinidos como `hero`, `features`, `team`, etc. Para usarlos:

**Edita `content/_index.md`** y agrega o modifica secciones bajo `sections:`

**Ejemplo de bloque Hero:**

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
        color: "bg-primary"  # Clases CSS personalizadas
```

### 3. Creando Bloques Personalizados

#### Paso 1: Crear el Layout

Crea un archivo en `layouts/partials/blox/mi_bloque.html`:

```html
{{ $page := .wcPage }}
{{ $block := .wcBlock }}

<section class="py-16 lg:py-24">
  <div class="container mx-auto px-6 lg:px-8">
    <h2>{{ $block.content.title }}</h2>
    {{ range $item := $block.content.items }}
      <div class="item">
        <h3>{{ $item.title }}</h3>
        <p>{{ $item.description }}</p>
      </div>
    {{ end }}
  </div>
</section>
```

#### Paso 2: Agregar el Bloque al Contenido

En `content/_index.md`:

```yaml
- block: mi_bloque  # Nombre del archivo sin extensión
  content:
    title: "Mi Sección"
    items:
      - title: "Item 1"
        description: "Descripción del item"
```

### 4. Componentes de un Bloque

#### Variables de Hugo Blox

```html
{{ $page := .wcPage }}
{{ $block := .wcBlock }}
```

**Propósito:** Acceso a los datos de la página y del bloque actual

#### Estructura del Contenedor

```html
<section class="py-16 lg:py-24">
  <div class="container mx-auto px-6 lg:px-8">
    ...
  </div>
</section>
```

**Propósito:** Define el área del bloque con padding vertical y contenedor responsive

**Personalización:**
- `py-16`, `lg:py-24`: Ajusta el espacio vertical
- `max-w-3xl`, etc.: Cambia el ancho máximo del contenedor

#### Título y Subtítulo

```html
<div class="text-center mb-12">
  <h2 class="text-3xl font-bold">
    {{ with $block.content.title }}{{ . | markdownify }}{{ end }}
  </h2>
  {{ with $block.content.subtitle }}
    <p class="text-lg">
      {{ . | $page.RenderString | emojify }}
    </p>
  {{ end }}
</div>
```

**Funciones:**
- `markdownify`: Permite usar Markdown en el título
- `emojify`: Convierte atajos de emoji en emojis reales

#### Iteración de Items

```html
{{ range $item := $block.content.items }}
  <li class="item">
    <span class="bullet">•</span>
    <div class="content">
      <strong>{{ $item.title }}</strong>
      {{ $item.description | $page.RenderString | emojify }}
    </div>
  </li>
{{ end }}
```

**Propósito:** Recorre y muestra todos los items definidos en el YAML

### 5. Estilos Personalizados

#### Referenciar Estilos en Bloques

Agrega al inicio del archivo HTML del bloque:

```html
{{ $css := resources.Get "css/mi_estilo.css" }}
<link rel="stylesheet" href="{{ $css.RelPermalink }}">
```

#### Crear Archivo CSS

Crea `assets/css/mi_estilo.css`:

```css
.mi-clase {
  color: #333;
  padding: 1rem;
}
```

## 📚 Recursos Adicionales

- [Documentación de Hugo](https://gohugo.io/documentation/)
- [Hugo Blox Docs](https://hugoblox.com/docs/)
- [Tailwind CSS](https://tailwindcss.com/docs) (usado en los estilos)

## 🤝 Contribuir

Las contribuciones son bienvenidas. Para cambios importantes:

1. Fork el proyecto
2. Crea una rama para tu feature (`git checkout -b feature/AmazingFeature`)
3. Commit tus cambios (`git commit -m 'Add some AmazingFeature'`)
4. Push a la rama (`git push origin feature/AmazingFeature`)
5. Abre un Pull Request

## 📄 Licencia

Este proyecto está bajo la Licencia MIT. Ver el archivo [LICENSE.md](LICENSE.md) para más detalles.

## 📧 Contacto

**ERTIS Research Group**
- Web: [https://ertis-research.github.io/ertis-page/](https://ertis-research.github.io/ertis-page/)
- Institución: Universidad de Málaga - ITIS Software Institute

---

Desarrollado con ❤️ por el equipo ERTIS

