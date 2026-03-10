# [UIC-2.0] Modelos de lenguaje

---

## Qué es ChatGPT?

- Es un asistente o **AI chatbot** que mantiene conversaciones (chats).
 
- No es un **modelo de lenguaje** (LLM), sino una interfaz de usuario basada en un modelo de lenguaje.

- Chatbot arena: ChatGPT (OpenAI), Claude (Anthropic), Gemini (Google), Grok (X AI), Copilot (Microsoft), Coral (Cohere), Le Chat (Mistral AI), DeepSeek (High-Flyer), Qwen (Alibaba), Kimi (Moonshot AI).

---

## Críticas tempranas a ChatGPT 

- No es fáctico.

- Limitado por su período de entrenamiento.

- Limitado a datos públicos, sin accesso a información confidencial.

- Sin capacidad de razonamiento.

- Flojo en matemáticas.

- Alucinaciones.

---

## Estado del arte

-  Ingeniería de prompts:

    + Instruccciones detalladas.

    + Ejemplos.

    + Chain-of-Thought (CoT) reasoning.

- Herramientas:

    + Búsqueda en la web.

    + Intérprete de Python.

---

## Taxonomía LLM (1)

- **Modelos de generación de texto**: generan nuevo texto a partir de un texto propuesto por el usuario, el llamado **prompt**. Ejemplos: Google Gemini 3.0 Flash, OpenAi GPT-5.

    + General-purpose.

    + **Code**.
    
    + **Reasoning/Thinking**.

    + **Deep research**.

- **Modelos de embedding**: generan representaciones vectoriales. Exemplos: Google gemini-embedding-001, OpenAI text-embedding-3-small.

---

## Taxonomía LLM (2)

- Modelos cerrados: sólo por acceso remoto, normalmente en modo pay-per-use. Ejemplo: Google Gemini 3, OpenAi gpt-5.2, Anthropic Claude Opus 4.6.

- Modelos abiertos: open-source u open-weight. Examples: OpenAI gpt-oss-20b (open-weight), Google's Gemma 3n E4B (open-weight), DeepSeek R1 (open-source), Alibaba's Qwen3 14B (open-source).

    + Instalación local: LMStudio, Ollama, Hugging Face, ModelScope.

    + Instalación remota: Cerebras, Groq, OpenRouter.

---

## Tokens

- Las **tokens** son los "átomos" en los que el texto es descompuesto por el modelo de lenguaje. 

- Típicamente palabras, trozos de palabras o puntuación. También hay tokens para el inicio y el final de un texto.

- El primer componente de un modelo de languaje es un **tokenizer**. El tokenizer descompone el prompt de acuerdo con un **vocabulario** de tokens. Para cada token, hay un **embedding vector**. 

---

## ¿Qué es la generación de texto?

- El modelo produce una continuación razonable del prompt, basada en lo gente ha escrito en millones de páginas web (training data).

- Efectúa unas operaciones matemáticas con los vectores de entrada, usando una arquitectura de **red neuronal** cuyos parámetros se han calculado durante el entrenamiento del modelo. la arquitectura de red usada por los modelos de languaje se llama **transformer**.

- El vector resultante es un conjunto de **probabilidades** para el token de salida, que se escoge de acuerdo a esas probabilidades.

---

## Continuación

- La token de salida se añade a las de entrada. A continuación se genera otra token de salida, y así sucesivamente, hasta la token final. El conjunto de tokens generadas es la respuesta del modelo.

- **Ventana de contexto**: el máximo número de tokens que el modelo puede manejar para responder a un prompt. Para los modelos de razonamiento, éste es un parámetro relevante.

---

## Cómo interaccionamos con un modelo de languaje?

- Chat app/web: ChatGPT, Gemini, Kimi, Perplexity, LM Studio.

- Programa:

    + Cliente-servidor (API): OpenAI, Gemini, Claude, OpenRouter, Cerebras.
    
    + Modelo local: Ollama, Hugging Face.
