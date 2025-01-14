# Flujo de Trabajo en n8n: Integración de Chatbot con Google Gemini y Qdrant

Este flujo de trabajo en n8n permite integrar un chatbot impulsado por los modelos de Google Gemini (PaLM) para procesar entradas de texto y almacenar embeddings en una base de datos vectorial (Qdrant). Soporta la carga de documentos, tokenización y respuestas de IA conversacional en tiempo real.

---

## Características

1. **Disparador de Mensajes de Chat**:
   - Detecta mensajes de chat entrantes y activa la ejecución del flujo de trabajo.
   - Basado en webhooks para la integración.

2. **Creación de Embeddings**:
   - Utiliza el modelo de embeddings de Google Gemini para procesar texto o contenido de archivos y generar embeddings.
   - Soporta la división de texto en fragmentos óptimos para el procesamiento.

3. **Manejo de Documentos**:
   - Procesa archivos binarios cargados durante una sesión.
   - Convierte el contenido del archivo en texto para su análisis.

4. **Base de Datos Vectorial Qdrant**:
   - Guarda los embeddings generados en Qdrant, una base de datos vectorial, para almacenamiento y recuperación.
   - Crea dinámicamente colecciones para diferentes sesiones de chat.

5. **IA Conversacional**:
   - Implementa un agente de IA conversacional utilizando el modelo de chat de Google Gemini para respuestas en tiempo real.
   - Permite la interacción con un chatbot entrenado en embeddings almacenados.

6. **Integración de Herramientas**:
   - Facilita la búsqueda vectorial y la recuperación de embeddings utilizando los datos de Qdrant.

---

## Detalles del Flujo de Trabajo

### Nodos

1. **When Chat Message Received**:
   - Activa el flujo de trabajo al recibir un nuevo mensaje de chat.
   - Entrada: Contenido del mensaje de chat.

2. **Embeddings Google Gemini**:
   - Genera embeddings utilizando el modelo `embedding-001`.
   - Entrada: Datos de texto o contenido de archivo.

3. **Default Data Loader**:
   - Procesa archivos binarios cargados durante la sesión.
   - Salida: Contenido en texto para tokenización.

4. **Token Splitter**:
   - Divide el texto en fragmentos más pequeños para generar embeddings.
   - Parámetros:
     - Tamaño de fragmento: 500 tokens.
     - Superposición: 50 tokens.

5. **Qdrant Vector Store**:
   - Almacena embeddings en Qdrant, asociándolos con un ID de sesión específico.

6. **Google Gemini Chat Model**:
   - Procesa entradas conversacionales y genera respuestas.
   - Modelo: `gemini-1.5-flash`.

7. **Vector Store Tool**:
   - Recupera embeddings de Qdrant para generar respuestas contextuales.

---

## Requisitos

1. **Configuración de n8n**:
   - Instalar n8n localmente o desplegarlo en un servidor.
   - Importar el archivo json a n8n en un nuevo workflow.

2. **Credenciales de API**:
   - Google Gemini (PaLM) API:
     - Requerido para los modelos de embeddings e IA conversacional.
   - Qdrant API:
     - Requerido para el almacenamiento vectorial.

3. **Variables de Entorno**:
   - Configura las claves de API y los ajustes de conexión para Qdrant y Google Gemini en tu entorno.

---

## Uso

1. **Inicia el Flujo de Trabajo**:
   - Comienza enviando un mensaje de chat o cargando un documento.
   - El flujo procesa la entrada y genera embeddings.

2. **Procesamiento de Datos**:
   - Los archivos cargados se tokenizan y se convierten en embeddings utilizando Google Gemini.

3. **Almacenamiento Vectorial**:
   - Los embeddings se almacenan en Qdrant para su recuperación durante las conversaciones con el chatbot.

4. **Interacción con el Chatbot**:
   - Usa el agente de IA conversacional para consultar los embeddings almacenados o continuar con la interacción.

---

## Personalización

1. **Ajusta los Modelos**:
   - Cambia los modelos de Google Gemini para embeddings o respuestas de chat según sea necesario.

2. **Modifica la Tokenización**:
   - Personaliza el tamaño de los fragmentos o la superposición para optimizar casos específicos.

3. **Amplía Funcionalidades**:
   - Añade más nodos para manejar fuentes de datos adicionales o mejorar las capacidades del chatbot.

---

## Solución de Problemas

- **Errores de API**:
  - Asegúrate de que las credenciales de API estén correctamente configuradas en n8n.
- **Conectividad con Qdrant**:
  - Verifica que la instancia de Qdrant esté en ejecución y sea accesible.

---

## Licencia

Este flujo de trabajo se distribuye bajo la Licencia MIT. Siéntete libre de modificarlo y usarlo según tus necesidades.

