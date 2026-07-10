# 📚 EduDocsAI - Agente RAG con Gemini y LangChain

> Un asistente virtual basado en **Retrieval-Augmented Generation
> (RAG)** desarrollado con **Python**, **LangChain**, **Google Gemini**
> y **ChromaDB**, capaz de responder preguntas utilizando una base de
> conocimiento formada por documentos en múltiples formatos.

------------------------------------------------------------------------

# 📖 Descripción

EduDocsAI implementa un pipeline completo de **Retrieval-Augmented
Generation (RAG)** desde cero.

El proyecto permite:

-   Cargar documentos desde una carpeta local.
-   Procesar múltiples formatos de archivo.
-   Dividir el contenido en fragmentos (chunks).
-   Generar embeddings utilizando Google Gemini.
-   Indexar los embeddings en ChromaDB.
-   Recuperar información mediante búsqueda semántica.
-   Generar respuestas con Gemini utilizando únicamente el contexto
    recuperado.

El objetivo es evitar respuestas inventadas (hallucinations) y
proporcionar información basada exclusivamente en los documentos
disponibles.

------------------------------------------------------------------------

# 🚀 Características

-   ✔ Arquitectura RAG completa
-   ✔ Integración con Google Gemini
-   ✔ Base vectorial con ChromaDB
-   ✔ Recuperación semántica mediante Retriever
-   ✔ Prompt personalizado
-   ✔ Código completamente documentado
-   ✔ Interfaz web con Gradio
-   ✔ Historial de conversación
-   ✔ Retroalimentación del usuario
-   ✔ Fácil de extender

------------------------------------------------------------------------

# 📂 Formatos soportados

Actualmente el proyecto soporta los siguientes formatos:

-   PDF (.pdf)
-   Microsoft Word (.docx)
-   Markdown (.md)
-   CSV (.csv)
-   JSON (.json)
-   HTML (.html)
-   Microsoft Excel (.xlsx)
-   Microsoft PowerPoint (.pptx)

------------------------------------------------------------------------

# 🧠 Arquitectura del proyecto

``` text
                           Usuario
                              │
                              ▼
                  Interfaz Web (Gradio)
                              │
                              ▼
                    Consulta del usuario
                              │
                              ▼
                         Retriever
                              │
                              ▼
              Base Vectorial ChromaDB (chroma_db)
                              ▲
                              │
      Embeddings (Google Gemini Embedding)
                              ▲
                              │
          División en chunks (Chunking)
                              ▲
                              │
         Conversión a objetos Document
                              ▲
                              │
               Carga de documentos
                              ▲
                              │
                Carpeta documents/
────────────────────────────────────────────────────
                              │
                              ▼
                Documentos recuperados
                              │
                              ▼
                   Prompt + Contexto
                              │
                              ▼
               Modelo Gemini 3.5 Flash
                              │
                              ▼
                Generación de la respuesta
                              │
                              ▼
                  Interfaz Web (Gradio)
                              │
                              ▼
                           Usuario
```

------------------------------------------------------------------------

# 📁 Estructura del proyecto

    EduDocsAI/
    │
    ├── documents/
    │   ├── Reglamento_del_Estudiante_6_paginas.pdf
    │   ├── Politica_de_Reembolso_de_Matriculas.docx
    │   ├── Preguntas_Frecuentes_Cursos_y_Certificados.md
    │   ├── Guia_de_Uso_de_la_Plataforma.html
    │   └── Programa_de_Becas_y_Afiliados.xlsx
    │
    ├── notebook/
    │   └── EduDocsAI_RAG_Gemini.ipynb
    ├── README.md
    ├── MANTENIMIENTO.md
    └── requirements.txt

------------------------------------------------------------------------

# ⚙ Preparación del entorno

Antes de ejecutar el notebook es necesario preparar la base de
conocimiento.

## 1. Crear la carpeta `documents`

Dentro del entorno de Google Colab crea una carpeta llamada:

    documents

La estructura debe quedar de la siguiente forma:

    /content
    │
    ├── documents
    │   ├── archivo1.pdf
    │   ├── archivo2.docx
    │   ├── archivo3.md
    │   ├── archivo4.html
    │   └── archivo5.xlsx
    │
    └── EduDocsAI_RAG_Gemini.ipynb

> **Importante:** La carpeta debe llamarse exactamente **`documents`**,
> ya que el notebook carga automáticamente todos los archivos mediante:

``` python
documents = cargar_documentos("documents")
```

------------------------------------------------------------------------

## 2. Agregar los documentos

Copia dentro de la carpeta `documents` todos los archivos que formarán
parte de la base de conocimiento.

Todos los documentos encontrados serán procesados automáticamente.

------------------------------------------------------------------------

# 🔑 Configuración de la API de Gemini

Este proyecto utiliza la API de Google Gemini.

En Google Colab crea un **Secret** con el nombre:

    GOOGLE_API_KEY

Posteriormente el notebook recupera la clave mediante:

``` python
GOOGLE_API_KEY = userdata.get("GOOGLE_API_KEY")
```

> **Nunca almacenes tu API Key directamente dentro del código ni la
> publiques en GitHub.**

------------------------------------------------------------------------

# 📦 Instalación

Instala las dependencias del proyecto:

``` bash
pip install -r requirements.txt
```

O instala manualmente:

``` bash
pip install \
langchain \
langchain-community \
langchain-text-splitters \
langchain-google-genai \
chromadb \
pypdf \
unstructured \
python-docx \
docx2txt \
openpyxl \
beautifulsoup4 \
python-pptx
```

------------------------------------------------------------------------

# 🔄 Pipeline RAG

El proyecto implementa las siguientes etapas:

## 1. Recolección y organización

Carga automáticamente todos los documentos ubicados dentro de la carpeta
`documents`.

------------------------------------------------------------------------

## 2. Procesamiento y extracción

Cada documento es convertido en texto utilizando el loader
correspondiente.

------------------------------------------------------------------------

## 3. Chunking

Los documentos se dividen en fragmentos utilizando:

``` python
RecursiveCharacterTextSplitter
```

Configuración:

    chunk_size = 800
    chunk_overlap = 100

------------------------------------------------------------------------

## 4. Embeddings

Cada chunk se convierte en un embedding utilizando:

    GoogleGenerativeAIEmbeddings

Modelo:

    gemini-embedding-2

------------------------------------------------------------------------

## 5. Base de datos vectorial

Los embeddings son almacenados en ChromaDB.

------------------------------------------------------------------------

## 6. Recuperación

El Retriever localiza los fragmentos más relevantes mediante búsqueda
semántica.

``` python
retriever = vector_db.as_retriever(
    search_kwargs={"k":3}
)
```

------------------------------------------------------------------------

## 7. Generación de respuestas

Gemini recibe:

-   La pregunta del usuario.
-   El contexto recuperado.

y genera una respuesta basada únicamente en dicho contexto.

------------------------------------------------------------------------

# 💬 Ejemplo de consulta

Pregunta:

    ¿Cómo obtengo mi certificado?

Respuesta esperada:

    Debes completar el 100 % del curso y aprobar la evaluación final utilizando la información recuperada desde la base de conocimiento.

------------------------------------------------------------------------

# 🛠 Tecnologías utilizadas

-   Python
-   Google Colab
-   LangChain
-   Google Gemini API
-   ChromaDB
-   PyPDF
-   BeautifulSoup
-   OpenPyXL
-   python-docx
-   python-pptx

------------------------------------------------------------------------

# 📈 Posibles mejoras

-   Persistencia de ChromaDB.
-   Historial de conversación.
-   Memoria del agente.
-   Filtrado por metadatos.
-   Reranking.
-   Citación automática de fuentes.
-   Interfaz con Gradio.
-   FastAPI.
-   LangGraph.
-   LangSmith.

------------------------------------------------------------------------

# 👨‍💻 Autor

**David Sanchez**

Proyecto desarrollado con fines educativos para comprender el
funcionamiento interno de un sistema **Retrieval-Augmented Generation
(RAG)** utilizando LangChain, Google Gemini y ChromaDB.

------------------------------------------------------------------------

# 📄 Licencia

Este proyecto se distribuye únicamente con fines educativos.
