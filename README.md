LG14 - Investigación y Despliegue de un Repositorio Big Data con Docker

Integrantes del Grupo:Hiber Leandro Veizaga Crespo, Anthony Arévalo Beltrán, Raul Jiménez.

 3. Registro del Repositorio
    Nombre del repositorio: Big-Data-Cluster
    URL: https://github.com/mrugankray/Big-Data-Cluster
    Autor/organización: mrugankray
    Descripción: Clúster local de Big Data dockerizado que incluye procesamiento distribuido con Hadoop y Spark, junto a un ecosistema de streaming con Kafka.

4. Información general y Tecnologías
   Objetivo del proyecto: Proporcionar un entorno local unificado en contenedores que integre procesamiento batch (Hadoop), en memoria (Spark) y streaming (Kafka) para desarrollo.
   Tecnología principal: Apache Hadoop (HDFS/YARN), Apache Spark y Apache Kafka.
   Uso de Docker/Compose: Sí.
   Bases de datos y Frameworks: Postgres, Cassandra, Zookeeper, Airflow, Zeppelin, Hive, Hue.
   Lenguajes: Shell, Dockerfile, Python, Java/Scala.

5. Análisis de la Arquitectura
El clúster base levanta 5 contenedores (y hasta 18 en su versión completa).
   namenode: Contenedor maestro que agrupa HDFS NameNode, Spark Master/Slave, Zeppelin, Airflow y Flume.
   datanode: HDFS DataNode y Python.
   resourcemanager: Gestor YARN.
   nodemanager: Nodo de trabajo YARN.
   historyserver: Seguimiento de trabajos Hadoop.
   Redes y Volúmenes: Se conectan mediante una red Bridge interna. Utilizan volúmenes Docker para persistir los datos de HDFS. Se configuró mapeo de puertos locales (ej. 8085:8080 para Spark).


 7. Implementación Práctica y Ejecución
Se ejecutaron los siguientes comandos para el despliegue:
1. `git clone https://github.com/mrugankray/Big-Data-Cluster.git`
2. `cd Big-Data-Cluster`
3. `docker compose -f basic-hadoop-docker-compose.yaml up -d`
4. `docker ps` (Se adjunta captura en la carpeta `/evidencias`).

Prueba Funcional Obligatoria (Hadoop / HDFS)
Se ingresó al contenedor maestro (`docker exec -it namenode bash`) y se ejecutó un script para crear un directorio, cargar un archivo de texto local hacia el HDFS y consultar su contenido exitosamente mediante `hdfs dfs -cat`. 

## 8. Comparación con docker-hadoop (Big Data Europe)
| Característica | docker-hadoop (BDE) | Big-Data-Cluster (Seleccionado) |
| :--- | :--- | :--- |
| **Tecnología principal** | Hadoop. | Ecosistema mixto: Hadoop, Spark, Kafka, Airflow. |
| **Contenedores** | 5 contenedores fijos. | 5 a 18 contenedores. |
| **Procesamiento** | MapReduce (YARN). | YARN y Apache Spark (en memoria). |
| **Complejidad** | Baja. | Media/Alta. Demanda más recursos de RAM/CPU. |
| **Caso de uso** | Análisis de datos Batch clásico. | Entorno Data Engineering completo (Batch, Streaming, Orquestación). |
