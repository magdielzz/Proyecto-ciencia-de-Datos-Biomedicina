# Análisis de Estancias Hospitalarias Prolongadas para México con Ciencia de Datos

## Resumen del Proyecto

Este proyecto, desarrollado como parte del curso *Introducción a la Ciencia de Datos* en la Facultad de Ciencias de la UNAM, analiza las estancias hospitalarias prolongadas (Length of Stay, LOS) en México utilizando técnicas de ciencia de datos y aprendizaje automático. El objetivo principal es identificar factores que contribuyen a estancias hospitalarias prolongadas (>10 días) en pacientes, con un enfoque en optimizar la gestión hospitalaria en instituciones como el Instituto Mexicano del Seguro Social (IMSS), que enfrenta problemas de sobresaturación y tiempos de espera prolongados.

El análisis se basa en el conjunto de datos `train_data.csv` de Kaggle, que contiene 318,438 registros de admisiones hospitalarias. Se implementó un flujo de trabajo estructurado que incluye preprocesamiento, análisis exploratorio de datos (EDA), modelado con Random Forest Classifier, y análisis de interpretabilidad con SHAP. El modelo logró una exactitud del 90.23%, con una sensibilidad del 98.72% y un F1-Score del 94.81%. Los resultados destacan la importancia de factores logísticos (como el número de visitantes y el depósito de admisión) sobre los factores clínicos, y se identificaron patrones mediante técnicas como K-Means y la paradoja de Simpson para evitar conclusiones erróneas.

El proyecto propone recomendaciones para mejorar la gestión hospitalaria, como optimizar la asignación de recursos, agilizar admisiones de emergencia y trauma, y explorar factores socioeconómicos. El código es completamente reproducible y está alojado en este repositorio, con visualizaciones y documentación detallada.

## ¿Cómo Funciona?

El proyecto sigue un flujo de trabajo de ciencia de datos modular y reproducible:

1. **Adquisición de Datos**: Se utiliza el conjunto de datos `train_data.csv` de Kaggle, cargado mediante `kagglehub` para garantizar acceso público y reproducible.
2. **Preprocesamiento**: 
   - Eliminación de identificadores únicos (`case_id`, `Hospital_code`, `patientid`).
   - Manejo de valores faltantes con `SimpleImputer` (mediana para numéricas, moda para categóricas).
   - Estandarización de variables numéricas con `StandardScaler` y codificación one-hot para categóricas.
   - Creación de una variable binaria `Prolonged_Stay` para clasificar estancias >10 días.
3. **Análisis Exploratorio (EDA)**:
   - Análisis univariado: histogramas y estadísticas descriptivas.
   - Análisis bivariado: boxplots y correlaciones, con atención a la paradoja de Simpson.
   - Análisis multivariado: clustering con K-Means y visualizaciones como heatmaps y diagramas de Sankey.
4. **Modelado**:
   - Uso de un `Random Forest Classifier` con hiperparámetros `n_estimators=100` y `class_weight='balanced'`.
   - División de datos: 70% entrenamiento, 15% validación, 15% prueba.
   - Validación cruzada de 5 pliegues para asegurar robustez.
   - Evaluación con métricas: precisión (91.21%), sensibilidad (98.72%), F1-Score (94.81%).
5. **Interpretación**:
   - Análisis SHAP para identificar la importancia de variables como `Visitors with Patient` y `Admission_Deposit`.
   - Recomendaciones para optimizar la gestión hospitalaria basadas en los hallazgos.
6. **Documentación**: Código, visualizaciones y decisiones metodológicas documentadas en un Jupyter Notebook y un informe en PDF.

## Estructura de Archivos

- **`Tiempo de Espera y Diagnóstico Tardío en Pacientes con Enfermedades Crónicas 2.ipynb`**: Jupyter Notebook con el código completo, incluyendo adquisición de datos, preprocesamiento, EDA, modelado y análisis SHAP.
- **`Análisis_de_Estancias_Hospitalarias_Prolongadas_para_México_con_Ciencia_de_Datos.pdf`**: Informe detallado del proyecto, con objetivos, metodología, resultados y referencias.
- **`imagenes/`**: Carpeta con visualizaciones generadas (histogramas, boxplots, gráficos SHAP, etc.).
- **`requirements.txt`**: Lista de librerías Python necesarias para ejecutar el proyecto.
- **`README.md`**: Este archivo, con la descripción del proyecto y las instrucciones de configuración.

## Requisitos

Para ejecutar el proyecto, necesitas instalar las siguientes dependencias de Python, listadas en `requirements.txt`:

- Python 3.9
- pandas
- numpy
- scikit-learn
- matplotlib
- seaborn
- kagglehub
- shap

## Instrucciones de Configuración

Sigue estos pasos para clonar y configurar el proyecto en tu máquina local:

1. **Clonar el Repositorio**:
   ```bash
   git clone https://github.com/magdielzz/Proyecto-ciencia-de-Datos-Biomedicina.git
   cd Proyecto-ciencia-de-Datos-Biomedicina
   ```

2. **Crear un Entorno Virtual** (opcional, pero recomendado):
   ```bash
   python -m venv venv
   source venv/bin/activate  # En Windows: .\venv\Scripts\activate
   ```

3. **Instalar Dependencias**:
   ```bash
   pip install -r requirements.txt
   ```

4. **Configurar Kaggle API** (para descargar el dataset):
   - Instala `kagglehub` si no está incluido en `requirements.txt`:
     ```bash
     pip install kagglehub[pandas-datasets]
     ```
   - Configura tu clave de API de Kaggle:
     - Ve a tu cuenta de Kaggle, genera una API token en `Settings > API`.
     - Coloca el archivo `kaggle.json` en `~/.kaggle/` (Linux/Mac) o `%USERPROFILE%\.kaggle\` (Windows).
     - Asegúrate de que el dataset `nehaprabhavalkar/av-healthcare-analytics-ii` esté accesible.

5. **Ejecutar el Notebook**:
   - Abre el archivo `Tiempo de Espera y Diagnóstico Tardío en Pacientes con Enfermedades Crónicas 2.ipynb` en Jupyter Notebook o JupyterLab:
     ```bash
     jupyter notebook
     ```
   - Ejecuta las celdas en orden para reproducir el análisis.

6. **Acceder a Visualizaciones**:
   - Las visualizaciones generadas (histogramas, boxplots, gráficos SHAP) se guardan en la carpeta `imagenes/`.

## Referencias

1. Prabhavalkar, N. (2019). *AV: Healthcare Analytics II*. Kaggle. Disponible en: https://www.kaggle.com/datasets/nehaprabhavalkar/av-healthcare-analytics-ii
2. ENSANUT: Encuesta Nacional de Salud y Nutrición, México.
3. IMSS: Reportes del Instituto Mexicano del Seguro Social.
4. *Aplicación de machine learning en la gestión de personas con enfermedades crónicas*. https://www.mhealthecare.com/
5. Centro de Investigación en Inteligencia Artificial (CIIIA). *Machine learning para diagnóstico temprano de enfermedades*. https://www.ciiia.mx/noticiasciiia/machinelearning-diagnostico-temprano-enfermedades
6. Villagrán, V., Rivas, H., & Vera, J. (2022). *Machine learning para el diagnóstico temprano de enfermedades: Una revisión sistemática*. Revista Médica de Chile, 150(12), 1655-1664. https://doi.org/10.1016/j.rmcl.2022.12.005
7. Fliguer, F. *SHAP*. GitHub Pages. https://fedefliguer.github.io/AAI/shap.html
8. Scikit-learn Documentation: *K-Means Clustering and Cross-Validation*. https://scikit-learn.org/stable/modules/clustering.html
9. Simpson, E. H. (1951). *The Interpretation of Interaction in Contingency Tables*. Journal of the Royal Statistical Society, Series B, 13(2), 238-241.

## Notas Adicionales

- El código está diseñado para ser modular y adaptable a nuevos conjuntos de datos hospitalarios.
- Se recomienda validar los resultados con datos adicionales del IMSS o ENSANUT para mejorar la generalización.
- Para contribuir al proyecto, crea un *pull request* con tus mejoras o correcciones.