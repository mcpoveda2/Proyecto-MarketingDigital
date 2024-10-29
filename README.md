# Segmentación de clientes

El objetivo de este proyecto es entender la distribucion de los datos, detectar patrones y valores atipicos 
con el fin de alcanzar un análisis de los datos y poder aplicar un modelo de segmentación óptimo.   


![image](https://github.com/user-attachments/assets/4bce9a86-1cb7-41fd-a7b3-6e49315ae5b9)


![image](https://github.com/user-attachments/assets/65174430-ef59-4fdb-8e11-80dc7e8ec406)


![image](https://github.com/user-attachments/assets/ce895c20-537a-4a8e-bbe6-2527eaf5f49b)


### 1. Información General

Se cargaron los datos y se exploraron las características principales, incluyendo descripciones estadísticas 
y distribución de las variables clave para entender el comportamiento inicial.


![image](https://github.com/user-attachments/assets/003efb47-67b2-4e3b-aa22-6abbd28b821d)


    • El dataset contiene 8950 registros y 18 columnas. 
    • La mayoría de las columnas son numéricas (float64 e int64), excepto la columna CUST_ID, que es de tipo object.
    • La columna CREDIT_LIMIT tiene 1 valor nulo.
    • La columna MINIMUM_PAYMENTS tiene 313 valores nulos.


### Estadísticas Descriptivas:

<img width="1148" alt="image" src="https://github.com/user-attachments/assets/c5d2e6dc-03e1-4e03-8359-99cfaca77708">


#### •BALANCE: 
    Promedio de 1564.47 con un máximo de 19043.14.
#### •PURCHASES: 
    Promedio de 1003.20 con un rango amplio (hasta 49039.57), lo que sugiere que algunos 
    clientes tienen montos de compras elevados.
#### •CREDIT_LIMIT: 
    El promedio de crédito es de 4494.45, y el máximo es 30000.
#### •TENURE: 
    La mayoría de los clientes tiene un periodo de TENURE de 12 meses, lo que indica 
    estabilidad en la muestra de clientes.


El 75% tiene una bajo uso del Oneoff method

<img width="769" alt="Screenshot 2024-10-28 at 9 51 49 PM" src="https://github.com/user-attachments/assets/c07fead5-118e-41a3-986a-c910b1067625">


## Preprocesamiento

Se realizaron transformaciones de datos, como la normalización y la creación de nuevas variables, 
para optimizar el análisis de clustering.
    
    Manejo de Valores Nulos: 
    Se identificaron y gestionaron valores nulos, eliminando o imputando valores según el análisis de cada variable, 
    con el fin de mantener la calidad de los datos sin introducir sesgos.

## Feature Engineering

    Creación de Nuevas Variables: Se generaron nuevas características relevantes para mejorar la separación de clusters. 

<img width="453" alt="image" src="https://github.com/user-attachments/assets/93dbc2df-1691-4073-bf92-6053c7383c6b">

Ejemplos incluyen:
* Ratio de Uso de Crédito: Proporción entre el saldo actual y el límite de crédito, útil para distinguir patrones de gasto.
* Frecuencia de Transacciones: Indicador de la recurrencia de uso de crédito, ayudando a identificar distintos tipos de usuarios.
* Transformación de Variables: Se aplicaron transformaciones como la normalización y estandarización para variables continuas, 
  facilitando el desempeño de algoritmos de clustering sensibles a las escalas de datos, como K-Means y DBSCAN.
      
## Técnicas de Clustering: 
    
Se aplicaron distintos algoritmos, incluyendo K-Means, K-Medoids, DBSCAN y Agglomerative Clustering. 
La selección y el ajuste del número de clusters se optimizaron mediante métodos como el Elbow Method y el Silhouette Score.
    
<img width="879" alt="image" src="https://github.com/user-attachments/assets/73c06393-eca5-41b5-81c9-24f944f5e2ae">


    * Codificación de Variables Categóricas: Las variables categóricas fueron codificadas utilizando técnicas de One-Hot Encoding o 
    Label Encoding, asegurando que la información categórica esté en un formato compatible con los modelos de clustering.

Este desglose proporciona una visión clara de cómo el Feature Engineering contribuyó a mejorar el análisis de clustering 
y la interpretación de resultados. 


## Resultados del Clustering con K-Means
    Selección del Número de Clusters: Utilizando el Elbow Method y el Silhouette Score, se determinó el número óptimo de clusters, 
    asegurando una buena separación entre grupos y minimizando la varianza dentro de cada cluster.
    
## Descripción de Clusters:
    Cada cluster representa un perfil distinto de clientes basado en patrones de uso de crédito, saldos, y otros factores relevantes.
    Algunos clusters mostraron usuarios con saldos altos y baja frecuencia de transacciones, 
    mientras que otros revelaron un uso frecuente de crédito con límites más bajos.

<img width="842" alt="image" src="https://github.com/user-attachments/assets/e5270153-879b-4770-846b-6c4370b09bc0">

### Interpretación Visual:
    Se generaron gráficos, como el análisis de componentes principales (PCA), 
    para visualizar la distribución de los clusters en un espacio reducido de dos dimensiones, 
    facilitando la interpretación de patrones y similitudes entre los grupos.


<img width="919" alt="image" src="https://github.com/user-attachments/assets/a55569cb-8eb3-4f12-9a47-95cc18289f93">


### Evaluación y Visualización: 
    Se compararon las métricas de rendimiento de los modelos y se interpretaron los resultados visualmente, 
    analizando la distribución de clusters y patrones relevantes en los datos.

### Mejora e Interpretabilidad:       
    Se iteraron ajustes de hiperparámetros y se exploró la interpretabilidad mediante SHAP para obtener 
    una comprensión más profunda de los factores que influencian cada cluster.

Con base en la interpretación de los resultados de clustering, parece que el caso de estudio fue exitosamente resuelto 
en términos de segmentación de clientes. Cada cluster revela un perfil financiero y de comportamiento distinto, 
lo que sugiere que el modelo de clustering logró identificar patrones de uso de crédito y 
características financieras significativas para cada grupo de clientes. A continuación, una evaluación de los insights obtenidos:

    Cluster 0: Representa a clientes de ingreso intermedio y bajo gasto. 
    Este grupo hace un uso ocasional de la tarjeta, con baja frecuencia en compras y escasa necesidad de adelantos de efectivo. 
    Esta caracterización permite dirigir servicios financieros de bajo costo y menor frecuencia.
    
    Cluster 1: Agrupa a clientes de bajo ingreso pero alto gasto anual, con frecuencia en las compras y tendencia a realizar pagos mínimos. 
    Este grupo puede ser un objetivo para estrategias que incentiven el pago completo y monitoreo de la deuda, dado su alto gasto.
    
    Cluster 2: Segmenta a clientes de alto valor financiero, con altos ingresos, balances, y un uso frecuente de adelantos de efectivo. 
    Estos clientes presentan un comportamiento de lealtad moderada y tienden a pagar puntualmente, 
    por lo cual podrían ser candidatos para productos premium o incentivos financieros.
    
    Cluster 3: Describe a clientes de ingreso moderado y bajo gasto, con menor lealtad y uso ocasional de adelantos en efectivo. 
    Este grupo podría beneficiarse de estrategias que incrementen la lealtad o incentiven mayor uso de los productos financieros.

# Conclusión

La segmentación obtenida permite personalizar estrategias de marketing y fidelización, además de orientar los servicios según los patrones financieros y de comportamiento de cada cluster. En resumen, el caso de estudio ha sido resuelto de manera efectiva, logrando un análisis de perfiles financieros útiles para tomar decisiones estratégicas.


# Recomendaciones 

Diseñar Estrategias de Marketing Segmentadas
Desarrollar productos específicos para cada cluster, por ejemplo, adelantos de efectivo o líneas de crédito 
ampliadas para el Cluster 2, o una tarjeta con condiciones accesibles para Cluster 1.

Monitorizar y Mejorar la Solvencia:
Clusters 1 y 3 muestran patrones de bajo pago de mínimos y bajo gasto respectivamente, lo cual puede incrementar el riesgo de impago. 
Es recomendable aplicar estrategias de seguimiento proactivo y asistencia financiera para mejorar su solvencia y comportamiento de pago.

Automatizar la Actualización del Modelo:
Implementar un sistema que actualice periódicamente los clusters en función de los cambios en el comportamiento y el mercado. 
Esto asegurará que la segmentación siga siendo relevante con el tiempo.

Evaluar la Efectividad de las Intervenciones:
Tras implementar las recomendaciones, analiza los efectos a través de métricas de lealtad, frecuencia de uso, 
y porcentaje de pago puntual en cada cluster. Esto permitirá ajustar las estrategias basadas en resultados.

Implementando estas recomendaciones, podrás maximizar el impacto de la segmentación de clientes 
y mejorar la alineación de productos y servicios con las necesidades de cada grupo.


# Future Work

Refinamiento de Features:
Continuar desarrollando nuevas variables derivadas que capturen aún mejor el comportamiento del cliente. 
Por ejemplo, indicadores de temporalidad en el gasto (gastos en temporadas altas o bajas) o patrones específicos de uso durante el mes.

Evaluación de Otros Modelos de Clustering:
Probar técnicas de clustering adicionales, como modelos de mezclas gaussianas (GMM) para capturar clusters con distribuciones complejas o 
modelos basados en redes neuronales, como Self-Organizing Maps (SOM), para una segmentación más robusta en datos de alta dimensión.

Análisis Predictivo del Comportamiento del Cliente:
Construir modelos que puedan predecir la transición de clientes entre clusters en función de su comportamiento pasado. 
Esto permitirá identificar clientes que estén en riesgo de moverse hacia segmentos menos rentables y crear intervenciones preventivas.

Implementación de Clustering Dinámico:
Desarrollar un sistema de clustering dinámico, donde los clientes puedan cambiar de cluster en función de su evolución temporal. 
Esto ayudará a capturar cambios en su comportamiento y adaptar las estrategias en tiempo real.




