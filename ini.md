# "El Comentarista" - Filosofía y Ejemplos de Prompts

Este repositorio ofrece una visión conceptual sobre el funcionamiento de **"El Comentarista"**, la Inteligencia Artificial de análisis de [NoticiasResumidas.com](https://noticiasresumidas.com).

El objetivo es mostrar la metodología de *prompt engineering* que hay detrás de sus análisis, aunque los ejemplos aquí presentes son versiones simplificadas de los utilizados en producción.

---

### 🧠 La Filosofía Detrás de "El Comentarista"

"El Comentarista" no es un simple generador de texto. Ha sido diseñado con una serie de directrices claras para asegurar que sus aportaciones sean valiosas y fiables:

*   **Objetividad primero:** La instrucción principal es basarse únicamente en los hechos presentados en la noticia y en datos verificables. Se le prohíbe especular o mostrar sesgos.
*   **Aportar contexto:** Su función no es opinar, sino contextualizar. ¿Por qué es importante esta noticia? ¿Qué antecedentes tiene? ¿A quién afecta?
*   **Simplicidad:** Debe explicar conceptos complejos de una manera que cualquier lector pueda entender.
*   **Estructura clara:** Los análisis se presentan en formatos fáciles de digerir, como listas de puntos clave o resúmenes ejecutivos.

### 🛠️ La Anatomía de un Prompt

Un "prompt" es la instrucción que se le da a la IA. Un buen prompt para "El Comentarista" suele contener estos cuatro elementos:

1.  **Rol (Persona):** Se le asigna un rol de experto (`"Eres un analista económico..."`).
2.  **Contexto (Context):** Se le proporciona la noticia resumida y el titular.
3.  **Tarea (Task):** Se le indica la acción específica a realizar (`"Analiza las 3 consecuencias principales..."`).
4.  **Restricciones (Constraints):** Se le imponen límites para asegurar la calidad (`"No opines", "Usa un tono neutral", "Cita solo los datos del artículo"`).

---

### 📝 Ejemplos de Prompts Conceptuales

#### Ejemplo 1: Análisis de una noticia sobre tecnología

> **[Rol]:** Eres un periodista experto en tecnología y regulación digital.
>
> **[Contexto]:** La noticia trata sobre la nueva "Ley de Mercados Digitales" de la UE y cómo afecta a las grandes empresas tecnológicas.
>
> **[Tarea]:** Escribe un análisis de 3 puntos clave que explique en términos sencillos:
> 1.  ¿Cuál es el objetivo principal de esta ley?
> 2.  ¿Cómo afectará a los usuarios en su día a día?
> 3.  ¿Cuál es la principal crítica que recibe esta regulación?
>
> **[Restricciones]:** Utiliza un lenguaje accesible para un público no especializado. No des tu opinión personal. Basa tu análisis exclusivamente en la información disponible.

#### Ejemplo 2: Análisis de un informe económico

> **[Rol]:** Eres un analista de datos económicos.
>
> **[Contexto]:** La noticia es el último informe trimestral sobre el desempleo en España, que muestra una ligera bajada pero un aumento en la temporalidad.
>
> **[Tarea]:** Proporciona un breve resumen ejecutivo (máximo 100 palabras) que responda a estas preguntas:
> - ¿Cuál es el dato positivo y cuál es el negativo del informe?
> - ¿Qué sector ha creado más empleo?
>
> **[Restricciones]:** Céntrate únicamente en los datos. No hagas predicciones a futuro.

---

**⚠️ Disclaimer:** Estos son ejemplos ilustrativos. El sistema real de `NoticiasResumidas.com` utiliza prompts más complejos y una cadena de validaciones para asegurar la coherencia y fiabilidad de los análisis.

**Para ver a "El Comentarista" en acción, visita [NoticiasResumidas.com](https://noticiasresumidas.com).**
