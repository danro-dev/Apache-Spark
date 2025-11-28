# Apache Spark Study Repository

![Apache Spark](img/Apache_spark.png)

Este repositorio está diseñado para aprender y practicar Apache Spark utilizando Python (PySpark).

## Estructura del Proyecto

- **notebooks/**: Espacio para guardar tus Jupyter Notebooks (`.ipynb`). Aquí es donde realizarás la mayoría de tus experimentos interactivos.
- **data/**: Carpeta para almacenar datasets (CSV, JSON, Parquet, etc.). Esta carpeta está montada en los contenedores, por lo que los datos son accesibles desde Spark.
- **apps/**: Para scripts de Python independientes (`.py`) o aplicaciones Spark completas que se envían con `spark-submit`.
- **docker-compose.yml**: Definición de la infraestructura local de Spark.

## Cómo Iniciar

### Prerrequisitos
- Docker
- Docker Compose

### Levantar el entorno

Ejecuta el siguiente comando en la raíz del proyecto:

```bash
docker-compose up -d
```

Esto iniciará los siguientes servicios:

1.  **Spark Master**: El nodo maestro del cluster.
    - Dashboard: [http://localhost:8080](http://localhost:8080)
    - URL interna: `spark://spark-master:7077`
2.  **Spark Worker**: Un nodo trabajador para ejecutar tareas.
3.  **Jupyter Notebook**: Entorno interactivo con PySpark preinstalado.
    - Interfaz: [http://localhost:8888](http://localhost:8888)
    - Spark UI (para el contexto actual del notebook): [http://localhost:4040](http://localhost:4040)

### Acceder a Jupyter

Después de ejecutar `docker-compose up`, revisa los logs para obtener el token de acceso si es necesario (aunque la configuración intenta deshabilitarlo o fijarlo, por seguridad por defecto Jupyter pide token).

```bash
docker-compose logs jupyter
```

Busca una URL como `http://127.0.0.1:8888/lab?token=...`

## Ejemplo de Uso en Notebook

Para conectar al cluster desde un notebook, puedes usar:

```python
from pyspark.sql import SparkSession

spark = SparkSession.builder \
    .appName("MiPrimerApp") \
    .master("spark://spark-master:7077") \
    .getOrCreate()

spark
```

## Recursos Útiles

- [Documentación Oficial de PySpark](https://spark.apache.org/docs/latest/api/python/)
- [Spark SQL Guide](https://spark.apache.org/docs/latest/sql-programming-guide.html)
