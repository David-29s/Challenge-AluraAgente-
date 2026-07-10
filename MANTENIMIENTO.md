# MANTENIMIENTO.md

# Mantenimiento del Agente RAG EduDocsAI

Este documento describe las tareas recomendadas para mantener
actualizado y confiable el agente RAG desarrollado con LangChain,
ChromaDB y Google Gemini.

------------------------------------------------------------------------

# 1. Actualización de documentos

Los documentos utilizados por el agente se almacenan en la carpeta
`documents`.

Cuando un documento sea:

-   Agregado.
-   Modificado.
-   Eliminado.

se recomienda volver a ejecutar el proceso de indexación para actualizar
la base vectorial.

Flujo recomendado:

1.  Actualizar el contenido de la carpeta `documents`.
2.  Eliminar la carpeta `chroma_db` (si se desea reconstruir
    completamente el índice).
3.  Ejecutar nuevamente el notebook.
4.  Verificar que la base vectorial se haya creado correctamente.

------------------------------------------------------------------------

# 2. Curaduría del contenido

Los documentos deben revisarse periódicamente para asegurar que:

-   Corresponden a la versión oficial.
-   No existen documentos duplicados.
-   La información continúa siendo vigente.
-   Los archivos obsoletos sean eliminados.

------------------------------------------------------------------------

# 3. Monitoreo de calidad

Después de desplegar el agente es recomendable revisar:

-   Preguntas que el agente no pudo responder.
-   Respuestas con retroalimentación negativa.
-   Tiempo promedio de respuesta.
-   Calidad de las respuestas generadas.

Estos indicadores permiten identificar oportunidades de mejora.

------------------------------------------------------------------------

# 4. Ciclo de mejora

Cuando los usuarios realicen preguntas que el agente no pueda responder
correctamente se recomienda:

-   Agregar nuevos documentos relacionados con el tema.
-   Mejorar los documentos existentes.
-   Ajustar el Prompt del sistema.
-   Revisar la estrategia de recuperación (Retriever).
-   Reconstruir la base vectorial.

------------------------------------------------------------------------

# 5. Actualización del modelo

Periódicamente es recomendable evaluar nuevas versiones del modelo
Gemini.

Antes de cambiar de modelo se recomienda:

-   Ejecutar pruebas con preguntas conocidas.
-   Comparar la calidad de las respuestas.
-   Verificar tiempos de respuesta.
-   Confirmar compatibilidad con LangChain.

------------------------------------------------------------------------

# 6. Mantenimiento de la base vectorial

La carpeta `chroma_db` contiene el índice vectorial del proyecto.

Se recomienda reconstruirla cuando:

-   Se agreguen documentos nuevos.
-   Se modifiquen documentos existentes.
-   Se eliminen documentos.
-   Se cambie el modelo de embeddings.

------------------------------------------------------------------------

# 7. Buenas prácticas

-   Mantener organizados los documentos dentro de `documents`.
-   Utilizar nombres descriptivos para los archivos.
-   Evitar indexar documentos duplicados.
-   Verificar periódicamente el funcionamiento del agente.
-   Mantener actualizadas las dependencias del proyecto.

------------------------------------------------------------------------

# Resumen

El mantenimiento del agente consiste en mantener actualizados los
documentos, reconstruir la base vectorial cuando sea necesario,
supervisar la calidad de las respuestas y evaluar periódicamente nuevas
versiones del modelo para garantizar un sistema confiable y actualizado.
