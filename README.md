# AHORA SÍ, ACEPTO 
Creado por Víctor Calabró - Proyecto final curso AI Engineering - Nucba

## Descripción del Proyecto

"AHORA SÍ, ACEPTO" es una aplicación web interactiva que aborda la problemática común de la incomprensión de documentos legales en línea, como Términos y Condiciones (T&C) o políticas de privacidad. En un entorno digital donde los usuarios frecuentemente aceptan acuerdos sin una lectura exhaustiva, esta herramienta actúa como un "Abogado de Fair Play" impulsado por Inteligencia Artificial. Su propósito es desglosar estos textos complejos, ofreciendo un resumen digerible, identificando riesgos potenciales y facilitando la creación de consultas informadas.

La aplicación busca democratizar el acceso a una comprensión clara de los compromisos legales, empoderando a usuarios individuales, consumidores digitales y pequeñas empresas para que tomen decisiones más informadas.

## Funcionalidades Clave

"AHORA SÍ, ACEPTO" ofrece una suite de herramientas impulsadas por IA para simplificar el análisis de documentos legales:

1.  **Resumen "ELI5" (Explícamelo como si tuviera 5 años):**
    *   Genera un resumen conciso y fácil de entender de los puntos más relevantes del documento.
    *   Cada punto incluye un "Ejemplo Práctico" que ilustra cómo esa cláusula podría afectar al usuario en una situación real.

2.  **Semáforo de Peligros (Análisis de Riesgos):**
    *   Identifica y clasifica las cláusulas de alto impacto en tres niveles de riesgo visuales:
        *   **Rojo:** Riesgos críticos o financieros significativos.
        *   **Amarillo:** Cláusulas que requieren precaución, a menudo relacionadas con la privacidad o el uso de datos.
        *   **Verde:** Cláusulas estándar o neutrales con bajo impacto.
    *   Los riesgos se etiquetan con categorías claras como "Dinero", "Privacidad", "Permanencia" (ej. facilidad de cancelación) o "Responsabilidad", acompañadas de explicaciones detalladas.

3.  **Consulta Inteligente (Borrador de Comunicación):**
    *   Genera automáticamente un borrador de correo electrónico formal.
    *   Este borrador está diseñado para ser enviado al equipo de soporte de la empresa, formulando preguntas específicas sobre las cláusulas más ambiguas, potencialmente injustas o que generen mayor preocupación en el documento analizado. Incluye un botón para copiar el texto directamente al portapapeles.

## Tecnología y Arquitectura

La aplicación está construida como una Single Page Application (SPA) y utiliza las siguientes tecnologías clave:

*   **Frontend:**
    *   **React & TypeScript:** Para una interfaz de usuario dinámica, robusta y escalable.
    *   **Tailwind CSS:** Para un diseño responsivo y altamente personalizable que garantiza una excelente experiencia de usuario en cualquier dispositivo.
*   **Inteligencia Artificial:**
    *   **Google Gemini API (`@google/genai` SDK):** El corazón del análisis, permitiendo la integración directa con los modelos de IA de Google.
    *   **Modelo `gemini-3-flash-preview`:** Seleccionado por su eficiencia y capacidad para comprender y procesar textos complejos y generar respuestas estructuradas.
    *   **Ingeniería de Prompts:** Los prompts están diseñados meticulosamente con `systemInstruction` y `responseSchema` (JSON) para asegurar una salida consistente, relevante y en español, manteniendo el rol de un "Abogado de Fair Play" imparcial.
*   **Gestión de Estado y Persistencia:**
    *   **Hooks de React (useState, useEffect, useCallback, useMemo, useRef):** Para una gestión eficiente del estado y el ciclo de vida de los componentes.
    *   **`localStorage`:** Utilizado para persistir el estado de la limitación de solicitudes (rate limiting) del usuario, garantizando un uso responsable de la API.

## Instrucciones de Uso

1.  **Acceso:** Abrí la aplicación en tu navegador web. (El enlace funcional se proporcionará en la sección de Entregables).
2.  **Entrada de Texto:** En el área de texto principal, pega los Términos y Condiciones, una política de privacidad, o cualquier documento legal que necesites comprender.
    *   Puedes utilizar el botón "Texto de ejemplo" para cargar contenido predefinido y familiarizarte con las funcionalidades.
3.  **Análisis:** Haz clic en el botón "Analizar Contrato". La IA procesará el texto, lo cual puede tomar unos segundos. Durante este proceso, se mostrará un indicador de carga.
4.  **Explora los Resultados:** Una vez finalizado el análisis, la aplicación presentará los resultados en tres secciones distintas:
    *   **"Muy largo, acá un resumen":** Muestra los puntos clave de forma sencilla.
    *   **"Semáforo de Peligros":** Detalla los riesgos identificados, clasificados por gravedad.
    *   **"Consulta inteligente":** Proporciona un borrador de correo electrónico listo para usar.
    *   Todas estas secciones son colapsables para una mejor navegación, especialmente en dispositivos móviles.
5.  **Copia el Borrador:** Si el borrador de consulta te es útil, haz clic en "Copiar al portapapeles" para guardarlo y usarlo en tu cliente de correo.

**Consideraciones importantes:**
*   La aplicación está diseñada para manejar textos de hasta `200.000` caracteres y requiere un mínimo de `100` palabras para un análisis efectivo.
*   Se ha implementado un sistema de `rate limiting`: un `cooldown` de 10 segundos entre análisis y un límite de 3 análisis por cada 24 horas para gestionar el uso de la API de forma equitativa.
*   Si el texto proporcionado no parece ser un documento legal válido, la IA te informará al respecto.

## Proceso de Desarrollo

El desarrollo de "AHORA SÍ, ACEPTO" ha sido una experiencia enriquecedora en la aplicación práctica de la ingeniería de IA para resolver un problema de la vida real. Los puntos clave y aprendizajes incluyen:

*   **Dominio de la Ingeniería de Prompts:** La calidad del análisis depende directamente de la calidad de las instrucciones dadas a la IA. El uso estratégico de `systemInstruction` para definir el rol y `responseSchema` para controlar el formato de salida JSON ha sido fundamental para obtener respuestas estructuradas, precisas y relevantes.
*   **Abordaje de la Ambigüedad Legal:** Se ha puesto especial atención en guiar al modelo para manejar la ambigüedad inherente en los textos legales. El sistema está diseñado para indicar explícitamente cuando una información no se encuentra en el documento, en lugar de inferirla o inventarla.
*   **Diseño Centrado en el Usuario (UX/UI):** Una parte crucial del proyecto fue asegurar que la compleja salida de la IA se presentara de manera comprensible y accesible. La implementación de indicadores de carga, mensajes de error claros, manejo de `rate limiting` y componentes colapsables (como las secciones de resultados) ha sido vital para una experiencia de usuario fluida e intuitiva, particularmente en dispositivos móviles.
*   **Integración Robusta de API:** La conexión con la API de Google Gemini a través de su SDK requirió atención a la gestión segura de las claves (`process.env.API_KEY`) y una sólida estrategia de manejo de errores para garantizar la estabilidad de la aplicación.
*   **Desarrollo Frontend con React/TypeScript:** La elección de React y TypeScript permitió construir una interfaz reactiva con código mantenible y escalable, facilitando la implementación de lógicas complejas y la interacción con la IA.

Este proyecto demuestra el gran potencial de la IA generativa para desmitificar información especializada y empoderar a los usuarios al brindarles claridad y control sobre los acuerdos digitales.

## Entregables

*   **Enlace a la aplicación desplegada:** `https://ahora-s-acepto-958162232752.us-west1.run.app/`
---
