# Análisis de Sentimientos con ML y MLOps

## Resumen del Proyecto
Este proyecto se centra en analizar el sentimiento de textos (positivo, negativo o neutral) utilizando técnicas de procesamiento ML y un enfoque MLOps para asegurar una integración y despliegue continuo en ambientes productivos.

## Motivación y Objetivos
- **Motivación:**  
  Se toma importancia a la necesidad de contar con una herramienta que interprete automáticamente el tono de los textos, facilitando la toma de decisiones en áreas como atención al cliente, análisis de opiniones en redes sociales, etc.
- **Objetivos:**  
  - Desarrollar un modelo robusto de análisis de sentimientos.
  - Integrar una API que permita el consumo del modelo en tiempo real.
  - Implementar buenas prácticas de MLOps para asegurar escalabilidad y mantenimiento.

### Diagrama de Arquitectura Model Building
![Diagrama de Arquitectura](architecture_model.png)  
_Descripción:_  
El diagrama muestra cómo se recibe los datos de web scraping, se procesa mediante técnicas de NLP, se analiza el sentimiento y se devuelve una respuesta.

### Pipeline de Procesamiento
1. **Recepción de Datos:**  
   El sistema recibe las reseñas a traves de Scrapy con web scraping.
2. **Preprocesamiento:**  
   Se aplican técnicas de limpieza de texto con regex y stop words de NLTK.
3. **Análisis del Sentimiento:**  
   El modelo, entrenado con datos etiquetados, evalúa el texto y genera una clasificación (por ejemplo, positivo, negativo, neutral).
4. **Respuesta:**  
   Se devuelve un JSON con el resultado del análisis y métricas asociadas.

#### Diagarama de Arquitecutra Model Inference
![Pipeline de Procesamiento](inference.png)  
_Esta imagen detalla el proceso de Model Inference._

### Pipeline de API 
1. **Uso del modelo creado por el equipo model building:**  
   Se carga el modelo con torch.jit.load().
2. **Preprocesamiento:**  
   Se aplican técnicas vectorizacion al texto, para aplicar predicciones de sentimiento.
3. **Análisis del Sentimiento:**  
   El modelo, entrenado con datos etiquetados, evalúa el texto y genera una clasificación (positivo, negativo, neutral).
4. **Respuesta:**  
   Se devuelve un JSON con el resultado del análisis y métricas asociadas.

#### CI/CD GITHUB Actions
Tanto en model building y model inference se implemento el archivo yaml, para esto.

#### Docker
![Dockerfile](docker.png)  
Despues de que el equipo de model inference, haya creado la API, esta se usa para crear la imagen docker.
Dando paso a usar multi satge builds para reducir el peso de la imagen, he evitar tiempos altos de ejecucion en CI/CD CON GITHUB Actions.


#### Google Clodu Run
  ![Artifact Regisrty](gcloud_3.png) 
Dando Uso a la imagen docker creada, haciendo deploy de esta en la nube de google.

## Demostraciones Visuales

- **Dashboard de Monitorización:**  
  ![Dashboard](gcloud.png)  
  ![Dashboard](gcloud_2.png)  
  _Descripción:_ Visualización en tiempo real de las solicitudes y respuestas procesadas por la API a traves de Google Cloud Run.

- **Ejemplo de Respuesta de la API:**  
  ![Respuesta API](sentiments_responses.png)  
  _Descripción:_ Ejemplo del JSON devuelto que muestra la clasificación del sentimiento y el score correspondiente.

## Tecnologías y Herramientas Utilizadas
- **Lenguaje:** Python
- **Framework de API:** Flask
- **Bibliotecas de NLP:** NLTK
- **Modelo de Machine Learning:** PyTorch
- **MLOps:** Docker, integración con CI/CD (GitHub Actions)
- **Despliegue en la Nube:** GCR

## Conclusiones y Futuras Mejoras
- **Conclusiones:**  
  Resumen de los logros y la efectividad del modelo.
- **Futuras Mejoras:**  
  Ampliar el proyecto, como mejorar la precisión del modelo, soporte para múltiples idiomas o integración de nuevas fuentes de datos.

