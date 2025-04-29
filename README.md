# Detección de Cardiopatías con PTB-XL y Modelos Híbridos CNN-LSTM

Este repositorio contiene el desarrollo de un modelo híbrido **CNN-LSTM** para la clasificación automática de enfermedades cardíacas utilizando el dataset **PTB-XL**. A continuación, se presenta una descripción detallada del proyecto, sus objetivos, antecedentes, metodología y referencias.

---

## Tabla de Contenidos
- [Descripción](#descripción)
- [Palabras Clave](#palabras-clave)
- [Objetivos](#objetivos)
- [Antecedentes](#antecedentes)
- [Modelos Híbridos CNN-LSTM](#modelos-híbridos-cnn-lstm)
- [Desafíos](#desafíos)
- [Referencias](#referencias)

---

## Descripción
El dataset **PTB-XL**, con más de 21,000 registros de **ECG** de 12 derivaciones, es un recurso valioso para la clasificación de condiciones cardíacas mediante técnicas de aprendizaje profundo. Este proyecto se centra en el desarrollo de un modelo híbrido **CNN-LSTM**, que combina la capacidad de las redes convolucionales (**CNN**) para extraer patrones espaciales con la habilidad de las redes de memoria a largo plazo (**LSTM**) para modelar dependencias temporales.

A pesar del éxito de los modelos híbridos **CNN-LSTM** en otras bases de datos como **MIT-BIH**, su aplicación en **PTB-XL** ha sido limitada. La literatura reciente (2023-2024) muestra un uso predominante de modelos individuales como **CNN**, **LSTM** o redes basadas en atención, pero no explora en profundidad combinaciones híbridas para **PTB-XL**. Este proyecto busca llenar este vacío, aprovechando el potencial de los modelos híbridos para mejorar la precisión diagnóstica en aplicaciones clínicas.

---

## Palabras Clave
- **ECG**
- **PTB-XL**
- **Modelos híbridos**
- **Diagnóstico automático**
- **Deep Learning**

---

## Objetivos

### Objetivo General
Desarrollar un modelo híbrido **CNN-LSTM** para la clasificación automática de enfermedades cardíacas utilizando el dataset **PTB-XL**.

### Objetivos Específicos
1. Preprocesar y normalizar las señales **ECG** del dataset **PTB-XL**.
2. Diseñar una arquitectura **CNN-LSTM** para el análisis espacial y temporal de las señales.
3. Evaluar el desempeño del modelo utilizando métricas clínicas como **F1-score**, sensibilidad y especificidad.
4. Comparar el rendimiento del modelo híbrido con arquitecturas tradicionales como **CNN** y **LSTM** individuales.

---

## Antecedentes
A continuación, se resumen estudios relevantes que utilizan el dataset **PTB-XL**, basados en literatura de 2023 y 2024.

### 1. Clasificación de ECG con Representaciones en 1D y 2D [1]
- **Estudio**: "Deep Learning for ECG Classification: A Comparative Study of 1D and 2D Representations and Multimodal Fusion Approaches" (2024, *Biomedical Signal Processing and Control*).
- **Descripción**: Comparó métodos de aprendizaje profundo para la clasificación multietiqueta de cuatro enfermedades cardiovasculares en **PTB-XL**, evaluando representaciones vectoriales y matriciales con modelos como **GRU**, **LSTM** y **CNN**. Exploró estrategias de fusión multimodal (tardía, temprana y conjunta).
- **Resultados**: Los modelos basados en **GRU** lograron una sensibilidad del **79.67%** y una especificidad del **81.04%**. Los enfoques multimodales no mejoraron significativamente el rendimiento respecto a las representaciones 1D. No se implementó un modelo híbrido **CNN-LSTM**.

### 2. ECG-Lense: Evaluación Comparativa de Modelos [2]
- **Estudio**: "ECG-Lense: Benchmarking ML & DL Models on PTB-XL Dataset" (2024, conferencia IEEE).
- **Descripción**: Introdujo **ECG-Lense**, un modelo **CNN** complejo, y comparó algoritmos de aprendizaje automático tradicionales (árbol de decisión, bosque aleatorio, regresión logística) con modelos profundos (**CNN** simple, **LSTM**, **ECG-Lense**) en **PTB-XL**. Utilizó señales **ECG** crudas con técnicas de aumento de datos.
- **Resultados**: Los modelos profundos superaron a los tradicionales, aunque no se reportaron métricas específicas. No se exploró un modelo híbrido **CNN-LSTM**.

### 3. Modelos de Espacio de Estado y Aprendizaje Autosupervisado [3]
- **Estudio**: "Towards Quantitative Precision for ECG Analysis: Leveraging State Space Models, Self-Supervision and Patient Metadata" (2023, preprint en [arXiv](https://arxiv.org/)).
- **Descripción**: Exploró modelos de espacio de estado (**SSM**) combinados con aprendizaje autosupervisado y metadatos de pacientes para mejorar la precisión en **PTB-XL**. Utilizó codificación predictiva contrastiva para robustecer las representaciones.
- **Resultados**: Los **SSM** mostraron un rendimiento comparable o superior a los modelos convolucionales tradicionales.

### 4. Medida Predictiva de Transferibilidad [4]
- **Estudio**: "MELEP: A Novel Predictive Measure of Transferability in Multi-label ECG Diagnosis" (2023, preprint en [arXiv](https://arxiv.org/)).
- **Descripción**: Propuso **MELEP**, una métrica para estimar la transferibilidad del conocimiento en tareas de clasificación multietiqueta en **PTB-XL**. Evaluó modelos preentrenados (**CNN** y **RNN**).
- **Resultados**: **MELEP** mostró una alta correlación con las puntuaciones **F1** promedio (>0.6). No se especificó el uso de modelos híbridos **CNN-LSTM**.

### Cuadro Comparativo
| Estudio                     | Modelo Principal       | Uso de PTB-XL                          | Métricas Clave                              | Referencia |
|-----------------------------|------------------------|----------------------------------------|---------------------------------------------|------------|
| Deep Learning ECG           | **GRU**, **LSTM**, **CNN** | Clasificación multietiqueta            | Sensibilidad: **79.67%**, Especificidad: **81.04%** | [1]        |
| ECG-Lense                   | **CNN**, **LSTM**, **ECG-Lense** | Clasificación de condiciones cardíacas | No especificadas                            | [2]        |
| Quantitative Precision      | **SSM**                | Análisis cuantitativo                  | Comparable a **CNN**                        | [3]        |
| MELEP                       | **CNN**, **RNN**       | Transferibilidad                       | Correlación **F1** > 0.6                   | [4]        |

---

## Modelos Híbridos CNN-LSTM
Los modelos híbridos **CNN-LSTM** han demostrado ser efectivos en la clasificación de **ECG** en bases de datos como **MIT-BIH** Arrhythmia y **PTB** Diagnostic. A continuación, se presentan estudios relevantes que, aunque no utilizan **PTB-XL**, destacan el potencial de estos modelos.

### 1. Diagnóstico Automatizado de Arritmias [5]
- **Estudio**: "Automated Diagnosis of Arrhythmia Using Combination of CNN and LSTM Techniques with Variable Length Heart Beats" (2018).
- **Descripción**: Propuso un modelo híbrido **CNN-LSTM** para diagnosticar ritmos sinusales normales, bloqueos de rama y contracciones prematuras en **MIT-BIH**.
- **Resultados**: Precisión del **98.10%**, sensibilidad del **97.50%** y especificidad del **98.70%** mediante validación cruzada de diez pliegues.

### 2. Clasificación Basada en Secuencias Wavelet [6]
- **Estudio**: "A Novel Wavelet Sequence Based on Deep Bidirectional LSTM Network Model for ECG Signal Classification" (2018, Yildirim).
- **Descripción**: Desarrolló un modelo basado en secuencias wavelet y **LSTM** bidireccional para clasificar señales **ECG** en **MIT-BIH**.
- **Resultados**: Precisión cercana al **99%**, destacando la importancia del preprocesamiento de señales.

### 3. Modelo Ligero para Detección de Arritmias [7]
- **Estudio**: "A lightweight hybrid CNN-LSTM explainable model for ECG-based arrhythmia detection" (2024).
- **Descripción**: Introdujo un modelo híbrido **CNN-LSTM** ligero para detectar ocho tipos de arritmias en **MIT-BIH** y Long-term AF, utilizando técnicas de eliminación de ruido y remuestreo.
- **Resultados**: Precisión promedio del **98.24%**, con valores de Shapley para explicar predicciones.

### Potencial en PTB-XL
El éxito de los modelos híbridos en otras bases de datos sugiere que podrían ser efectivos en **PTB-XL** [5-7]. La estructura de **PTB-XL**, con anotaciones multietiqueta y metadatos ricos, es ideal para entrenar modelos complejos. Técnicas como aumento de datos y transferencia de aprendizaje podrían mejorar el rendimiento, mitigando problemas de sobreajuste.

---

## Desafíos
1. **Complejidad Computacional**: Los modelos híbridos requieren más recursos que los tradicionales, lo que puede limitar su implementación.
2. **Interpretabilidad**: Aunque técnicas como los valores de Shapley [7] mejoran la explicabilidad, garantizar que los modelos sean comprensibles para médicos es crucial.
3. **Estandarización**: La variabilidad en las anotaciones y la necesidad de métricas estandarizadas (**F1-score**, sensibilidad, especificidad) son esenciales para comparar modelos.

---

## Referencias
1. "Deep Learning for ECG Classification: A Comparative Study of 1D and 2D Representations and Multimodal Fusion Approaches." *Biomedical Signal Processing and Control*, 2024.
2. "ECG-Lense: Benchmarking ML & DL Models on PTB-XL Dataset." Conferencia IEEE, 2024.
3. "Towards Quantitative Precision for ECG Analysis: Leveraging State Space Models, Self-Supervision and Patient Metadata." arXiv preprint, 2023.
4. "MELEP: A Novel Predictive Measure of Transferability in Multi-label ECG Diagnosis." arXiv preprint, 2023.
5. "Automated Diagnosis of Arrhythmia Using Combination of CNN and LSTM Techniques with Variable Length Heart Beats." 2018.
6. Yildirim, O. "A Novel Wavelet Sequence Based on Deep Bidirectional LSTM Network Model for ECG Signal Classification." 2018.
7. "A lightweight hybrid CNN-LSTM explainable model for ECG-based arrhythmia detection." *Biomedical Signal Processing and Control*, 2024.

---
