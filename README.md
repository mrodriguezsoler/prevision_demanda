### Autoría
Este paquete ha sido desarrollado como parte de la asignatura *Trabajo de Fin de Máster* del Máster Universitario en Ciencia de Datos de la UOC por el alumno Marcos Rodríguez Soler.<br><br>

# **prevision_demanda**

**prevision_demanda** es un paquete que contiene el código fuente para la exploración, limpieza, preprocesamiento, *clustering*, modelado y evaluación económica de los datos que se han empleado como parte del Trabajo de Fin de Máster del Máster Universitario en Ciencia de Datos de la UOC.<br>

Se ha desarrollado un modelo de previsión de la demanda orientado a mejorar cuantitativamente la gestión de *stocks* de una empresa del sector automovilístico. Con este fin, se han comparado varios modelos de *Machine Learning*, y sus resultados se han integrado en una política de reposición *Order-Up-To (R, S)* para evaluar tanto el rendimiento económico como el nivel de servicio de cada uno de ellos.<br>

El código desarrollado se ha implementado en *Jupyter Notebooks* en el lenguaje de programación *Python*, y se ha utilizado la distribución *Anaconda* para la gestión de entornos y dependencias.<br><br>

### Dependencias

El paquete ha sido desarrollado en un entorno virtual de *Anaconda* usando la siguiente versión de *Python*, junto con las siguientes versiones de las principales librerías que se emplean en el proyecto.

 - python == 3.12.3
 - matplotlib == 3.10.8
 - numpy == 2.4.3
 - pandas == 3.0.1
 - seaborn == 0.13.2
 - scikit-learn == 1.7.1
 - xgboost == 3.2.0
 - tensorflow == 2.21.0
 - optuna == 4.6.0<br><br>


### Instalación

Para instalar correctamente el paquete **prevision_demanda**, será necesario abrir una terminal de comandos de *Anaconda*, como *Anaconda Prompt*, y navegar hasta la dirección donde se haya guardado la carpeta del proyecto.  

```bash
cd path_to_prevision_demanda/prevision_demanda
```

A continuación, es necesario crear y activar un entorno virtual para poder instalar todas las dependencias del paquete. El entorno se crea a partir del fichero YAML del paquete.

```bash
conda env create -f env.yml -n venv
conda activate venv
```
<br><br>


### Estructura

El paquete **prevision_demanda** presenta la siguiente estructura.

```bash
prevision_demanda/
├── AED/
│   └── aed.ipynb
├── MODELOS/
│   ├── random_forest.ipynb
│   ├── xgboost.ipynb
│   ├── lstm.ipynb
│   └── naive.ipynb
├── IMPACTO_ECONÓMICO/
│   └── impacto_economico.ipynb
├── DATOS/
│   ├── Datos.xlsx
│   ├── DatosCicloAprovisionamiento.xlsx
│   └── DatosPrecioMedio.xlsx
├── html/
│   ├── aed.html
│   ├── random_forest.html
│   ├── xgboost.html
│   ├── lstm.html
│   ├── naive.html
│   └── impacto_economico.html
├── tfm_mrodriguezsoler.pdf
├── env.yml
├── README.md
└── LICENSE
```

En la carpeta raíz del proyecto, se pueden encontrar los archivos **README.md**, que contiene información importante acerca del contenido del paquete y cómo usarlo, **LICENSE**, que contiene la licencia bajo la cual se puede usar el
paquete, **tfm_mrodriguezsoler.pdf**, que es la memoria escrita del trabajo, y **env.yml**, que incluye las dependencias necesarias para la ejecución del código del paquete.<br>

La carpeta **data** contiene los conjuntos de datos de los productos de la empresa del sector automovilístico con los que se ha trabajado durante el proyecto. Seguidamente se describe brevemente el contenido de estos archivos.

- **DatosCicloAprovisionamiento.xlsx** -> Contiene los datos referentes al ciclo de aprovisionamiento de cada producto. Se incluyen campos como el tiempo de revisión de inventario y el *lead time*.
- **DatosPrecioMedio.xlsx** -> Presenta los precios medios de venta de los distintos productos de la empresa.
- **Datos.xslx** -> Contiene cuatro hojas de datos.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; - Venta -> Contiene las secuencias de la demanda histórica de cada producto.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; - Calendario -> Incluye fechas relevantes dentro del contexto operativo de la empresa, como las festividades y el estado de apertura de la tienda en cada fecha dada.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; - Promociones -> Contiene los periodos temporales en los que se ofertaron los distintos productos.<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; - *Stock* -> Presenta el inventario disponible de cada artículo en cada fecha de los históricos de la demanda.

Por otro lado, el código del proyecto se ha estructurado en tres etapas bien diferenciadas: el análisis exploratorio de los datos, el entrenamiento de los modelos de *machine learning*, y la evaluación del rendimiento económico de los algoritmos. Para cada una de estas fases se ha creado una carpeta específica, las cuales se describen a continuación.

- Carpeta **AED/** -> Incluye el *notebook aed.ipynb* en donde se cargan e integran los datos, se desarrolla el análisis exploratorio, y también se realiza un procedimiento de *clustering* para agrupar productos similares. Tras la ejecución de dicho archivo, se genera un fichero de nombre **dataset_preprocesado.csv**, que contiene los datos tratados listos para prepararlos para el entrenamiento de los modelos de aprendizaje automático.
- Carpeta **MODELOS/** -> Contiene los *notebooks* en donde se preprocesan los datos para el entrenamiento de los modelos de *machine learning*, dando lugar a los archivos **random_forest.ipynb**, **xgboost.ipynb**, y **lstm.ipynb**. Adicionalmente se ha entrenado un modelo ingenuo que se usa como objeto de comparación durante la evaluación del rendimiento económico, por lo que también se ha añadido un archivo **naive.ipynb** en donde se entrena este modelo. La ejecución de cada uno de estos *notebooks* produce 5 archivos de nombre *res_modelo_dataset.csv*, donde modelo hace referencia al nombre del algoritmo (*Random Forest*, *XGBoost*, LSTM o *naive*), y *dataset* corresponde al nombre del conjunto de datos empleado (global, *top_ventas*, *residual*, *estandar* o *alta_rotacion*. Los últimos cuatro conjuntos surgen tras el proceso de *clustering* del análisis exploratorio de los datos). Estos ficheros contienen las predicciones de los modelos en los conjuntos de prueba de los *datasets* en cuestión. Adicionalmente, también se generan otros 5 ficheros por algoritmo, de nombre *rmses_modelo_dataset*, que contienen los RMSE para cada horizonte de predicción del conjunto de prueba del *dataset* en cuestión. Estos archivos se emplean durante la evaluación del impacto económico para aproximar la incertidumbre de las predicciones.
- Carpeta **IMPACTO_ECONÓMICO/** -> Incluye el *notebook impacto_economico.ipynb* en donde se determinan los mejores modelos y se realiza una simulación de inventario para estimar los costes asociados a cada modelo entrenado.

Finalmente, la carpeta **html/** contiene los archivos de cada *notebook* en versión HTML. Estos ficheros presentan el contenido de estos archivos tras su ejecución total.
<br><br>


### Uso
Para ejecutar los distintos *notebooks* que componen el paquete, tan solo es necesario abrir *jupyter notebook* en un servidor local y ejecutarlos como se desee. Para ello, una vez se ha activado el entorno virtual del paquete, se debe ejecutar el siguiente comando.

```bash
jupyter notebook
```

Una vez se haya inicializado el servidor local con *jupyter notebook*, se podrá acceder al contenido de cada *notebook*. El orden de ejecución del código fuente debe ser **aed.ipynb** -> **random_forest.ipynb / xgboost.ipynb / lstm.ipynb / naive.ipynb** -> **impacto_economico.ipynb**. Esto permite que se generen los conjuntos de datos intermedios adecuados para la ejecución de cada *notebook*.
<br><br>


### Licencia **prevision_demanda**

Dado el contexto en el que se ha desarrollado el código, y los datos que se manejan, se ha decidido otorgar la licencia de tipo **MIT** al paquete **prevision_demanda**, de manera que se permite el uso, modificación y distribución del código a todo el dominio público.

[MIT](https://choosealicense.com/licenses/mit/)