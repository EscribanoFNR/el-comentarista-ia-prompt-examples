# "El Comentarista" - Arquitectura de Prompts y Ejemplos Conceptuales

Este repositorio ofrece una visión sobre la arquitectura de prompts y la metodología de *prompt engineering* que hay detrás de **"El Comentarista"**, la Inteligencia Artificial de análisis y comentarios de [NoticiasResumidas.com](https://noticiasresumidas.com).

El sistema no se basa en prompts estáticos, sino en un **motor de prompts dinámico** gestionado desde una base de datos. Esto nos permite experimentar, versionar y asignar diferentes "personalidades" a la IA de forma flexible y escalable.

---

### 🧠 Anatomía de Nuestro Sistema de Prompts Dinámico

Cada tarea de la IA se ejecuta a través de un "prompt maestro" que se construye dinámicamente combinando varios elementos clave almacenados en nuestra base de datos:

1.  **System Prompt (La Personalidad Base de la IA):**
    Es la instrucción de más alto nivel que define el rol, los principios y las reglas innegociables de la IA. Actúa como su "constitución". En nuestro caso, define a la IA como un "analista de noticias de élite" y le impone mandatos como la búsqueda de la máxima densidad informativa, la priorización de datos sobre opiniones y la adherencia estricta a un formato de salida JSON.

2.  **User Prompt (La Tarea Específica):**
    Este es el núcleo de la instrucción. Es una plantilla detallada que guía a la IA paso a paso para realizar una tarea concreta (resumir una noticia, generar un comentario, etc.). Utilizamos marcadores de posición (ej: `qq_titulo_qq`, `qq_contenido_qq`) que el sistema reemplaza en tiempo de ejecución con los datos de la noticia.

3.  **Parámetros de Inferencia:**
    Cada prompt tiene asociados parámetros como la `temperatura` (creatividad) o el `max_tokens` (longitud de la respuesta), lo que nos permite ajustar el comportamiento de la IA para cada tarea específica.

4.  **Motor de Personas (Para Comentarios):**
    Para generar comentarios, hemos creado una base de datos de **arquetipos de comunicación**. Cada arquetipo tiene definidos:
    *   **Mentalidad (El QUÉ piensa):** Sus valores, su visión del mundo, sus ideas recurrentes.
    *   **Forma de Hablar (El CÓMO lo dice):** Su tono, vocabulario, muletillas y estilo de escritura.

Estos arquetipos se inyectan en prompts específicos para que la IA pueda "actuar" como diferentes perfiles de usuario, creando un ecosistema de comentarios dinámico y realista.

---

### 📝 Ejemplos de Flujos de Trabajo y Prompts Conceptuales

A continuación se muestran ejemplos simplificados de cómo funciona nuestro sistema.

#### Ejemplo 1: El Prompt Maestro de Resumen de Noticias

Para resumir una noticia, no pedimos simplemente un "resumen". Utilizamos un prompt de múltiples pasos que obliga a la IA a pensar de forma estructurada y a devolver un objeto JSON con varios campos de análisis.

**Fragmento Conceptual del User Prompt (`resume_ini`):**
```
Analiza este artículo periodístico:
TÍTULO: qq_titulo_qq
CONTENIDO: qq_contenido_qq

Sigue estos pasos rigurosamente:

1. Expectativa del lector (basado SOLO en el título):
   ¿Qué información concreta espera encontrar el lector? Responde con 2-5 palabras máximo.

2. Resumen (EXACTAMENTE 300 palabras):
   - Reescribe el artículo con lenguaje periodístico directo.
   - Incluye TODOS los datos relevantes: cifras, fechas, nombres.

3. Respuesta concreta:
   Frase específica (3-7 palabras) que satisface DIRECTAMENTE la expectativa del lector.

[...] // Otros pasos como clasificación, prompts para imágenes, etc.

7. Crítica del artículo:
   Análisis mordaz (2 frases máximo) evaluando si el contenido cumple con las expectativas del título.

RESPONDER EXCLUSIVAMENTE en JSON con esta estructura exacta:
{
  "expectativa_lector": "...",
  "resumen": "...",
  "respuesta_concreta": "...",
  "conceptos_principales_resumen": [...],
  "tema_clasificacion": "...",
  "prompt_DALLY_llm": "...",
  "critica_del_articulo": "..."
}
```
Este enfoque nos permite obtener datos estructurados y de alta calidad en una sola llamada, optimizando el proceso.

#### Ejemplo 2: El Flujo de Generación de Comentarios con Personas

Generar un comentario es un proceso de dos pasos:

**Paso 1: Seleccionar un Arquetipo.**
El sistema elige un perfil de la base de datos, por ejemplo, "El Hater Nostálgico":
*   **Mentalidad:** `Cree que cualquier tiempo pasado fue mejor y que ahora todo es comercial y sin alma.`
*   **Forma de Hablar:** `Tono cínico y resentido. Empieza con "Esto antes no pasaba...". Desprecia sistemáticamente lo nuevo.`

**Paso 2: Inyectar el Arquetipo en un Prompt de Comentario.**
Estos datos se insertan en una plantilla de prompt (`comentario_simple`) que instruye a la IA para que actúe como esa persona.

**Fragmento Conceptual del User Prompt (`comentario_simple`):**
```
### 1. DATOS DEL PERFIL
- Nombre: qq_nombre_qq
- Mentalidad (QUÉ piensa): "Cree que cualquier tiempo pasado fue mejor..."
- Forma de Hablar (CÓMO habla): "Tono cínico y resentido..."

### 2. DATOS DE LA NOTICIA
- Título: "Anuncian el remake de la película clásica de los 80"
- Contenido: "..."

### 3. TU TAREA
Escribe un comentario CORTO (2 frases como máximo) reaccionando a la noticia desde la perspectiva y el estilo del perfil proporcionado.
```
El resultado es un comentario coherente con el arquetipo, que enriquece la conversación de forma autónoma.

#### Ejemplo 3: Workflow de Múltiples IA (Texto a Imagen)

Nuestro sistema utiliza un flujo encadenado. El prompt de resumen (Ejemplo 1) genera un campo `"prompt_DALLY_llm"` con una descripción visual de la noticia. Luego, este texto se pasa a un segundo sistema que lo combina con un estilo predefinido (ej: "3D Animation", "Pop Art") para generar la imagen final.

---

**⚠️ Disclaimer:** Estos son ejemplos conceptuales para ilustrar la metodología. El sistema real de `NoticiasResumidas.com` utiliza prompts más complejos y una cadena de validaciones para asegurar la calidad y coherencia de todas las generaciones de la IA.

**Para ver a "El Comentarista" en acción, visita [NoticiasResumidas.com](https://noticiasresumidas.com).**
```
