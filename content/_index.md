---
title: 'Home'
date: 2023-10-24
type: landing

design:
  # Default section spacing
  spacing: "6rem"

sections:
  # Section 1: Header
  - block: hero
    content:
      title: "ERTIS Research group"
      text: "ERTIS focuses its research activity on improving the management, accessibility and integration of embedded devices in the context of the Internet of Things. ERTIS is part of the <span style='color: rgb(var(--color-primary-orange));'>ITIS Software institute.</span>"
      primary_action:
        id: btn-more-info
        text: "More Info..."
        url: "research/"
      background_image: ../assets/media/Comida_2025.jpg
    design:
      spacing:
        padding: [0, 0, 0, 0]
        margin: [0, 0, 0, 0]
      css_class: "dark"

  # Section 2: Areas
  - block: research
    id: areas
    content:
      title: Research Areas
      text: ERTIS focuses on several research lines that address the challenges of embedded and distributed systems in real-time and critical domains. Our work is organized into the following areas
      items:
        - name: Digital Twins and Open Platforms
          icon: puzzle-piece
          description: Architectures for modeling, simulation, and monitoring of physical processes, applied to domains such as agriculture, energy, and infrastructures.
          image_one: 
            path: ../assets/media/logo_OpenTwins.svg
            name: Open Twins
            link: https://ertis-research.github.io/opentwins/
        - name: Streaming Deep and Distributed Neural Networks over the IoT/Edge/Fog/Cloud
          icon: cloud
          description: ERTIS investiga cómo integrar redes neuronales profundas con sistemas de mensajería para desplegarlas en entornos IoT, Edge, Fog y Cloud, ejemplificado en su framework **Kafka-ML**, que gestiona todo el ciclo de vida de modelos de IA mediante flujos de datos.
          image_one: 
            path: ../assets/media/logo_Kafka.svg
            name: Kafka-ML
            link: https://github.com/ertis-research/kafka-ml
        - name: IoT, Edge, and Fog Computing
          icon: globe
          description: Middleware and distributed architectures that enable efficient data processing across heterogeneous devices and networks.
        - name: Real-Time and Critical Systems
          icon: shield
          description: Methods and tools to ensure predictability, functional safety, and cybersecurity in systems where failures are not acceptable.

  # Section 3: Publications and Projects
  - block: publications_projects
    id: publications_projects
    content:
      title: "Publications and Projects"
      text: "Explore our latest research projects and publications in embedded systems and IoT."

  # Section 4: Visits
  - block: visits
    id: visits
    content:
      title: "Visits"
      text: "Some of the distinguished researchers and collaborators who have visited us recently. We value these exchanges as opportunities to foster innovation and collaboration in embedded systems and IoT."
      images:
        name_1: Eduardo_Canete.jpg
        name_2: Gwanggil_Jeon.jpeg
        name_3: Nauman_Aslam.jpeg
        name_4: Nigel_Shofield.jpg
        name_5: Qasim_Ahmed.jpg
        name_6: Roufaida.jpeg

# Nueva estructura de la sección Sobre nosotros (versión landing institucional)

# Projects, Publications & Collaborations → un bloque conjunto que muestre la actividad científica y de transferencia.

# Our Team → destacar investigadores principales + link al listado completo.

# Location → un mapa simple con la ubicación en la UMA + datos de contacto básicos.
---
