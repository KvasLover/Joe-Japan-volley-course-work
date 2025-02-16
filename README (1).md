[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/V-2uIfVx)
[![Open in Codespaces](https://classroom.github.com/assets/launch-codespace-2972f46106e565e64193e422d61a12cf1da4916b45550586e14ef0a7c637dd04.svg)](https://classroom.github.com/open-in-codespaces?assignment_repo_id=17999740)
# Отчёт по выполнению лабораторной работы №1
--------------------------------------------
Выполнила: Вальмус У.М. гр. 210901
Проверил: Прудник А.М.
---------------------------------------------
📝  Для данной лабораторной работы я буду использовать GitHub CodeSpace.
В качестве задания я выбрала следующее: преобразование данных.

Для работы программы пришлось установить pyspark:
![alt text](pyspark.png)

1 задание:

Отфильтруйте строки, где возраст больше 30 лет.

Решение:

```
from pyspark.sql import SparkSession
spark = SparkSession.builder.appName("DataFiltering").getOrCreate()
data = [("John", 25), ("Alice", 30), ("Bob", 35)]
df = spark.createDataFrame(data, ["Name", "Age"])
filtered_df = df.filter(df["Age"] > 30)
filtered_df.show()
```

Результат:
![alt text](task1.png)


2 задание:

Преобразуйте DataFrame, чтобы добавить новый столбец "Age_Group", который разделяет людей на группы "Молодые" и "Взрослые" по возрасту (меньше 30 - "Молодые", 30 и больше - "Взрослые").

Решение:

```
from pyspark.sql.functions import when
df_with_age_group = df.withColumn("Age_Group", when(df["Age"] < 30, "Молодые").otherwise("Взрослые"))
df_with_age_group.show()
```

Результат:
![alt text](task2.png)



3 задание:

Рассчитайте средний возраст для каждой возрастной группы ("Молодые" и "Взрослые").

Решение:

```
from pyspark.sql.functions import avg
average_age_df = df_with_age_group.groupBy("Age_Group").agg(avg("Age").alias("Average_Age"))
average_age_df.show()
```

Результат:
![alt text](task3.png)

Ответы на вопросы из анкеты для самопроверки.
Вопрос 1:
Объясните назначение Hadoop в экосистеме Больших данных и его связь с распределенными системами хранения, такими как HDFS.

Ответ: Hadoop - это платформа для распределенной обработки и хранения больших данных. Главная цель Hadoop - эффективно обрабатывать и анализировать огромные объемы данных, которые не могут быть обработаны традиционными реляционными базами данных. Hadoop использует HDFS (Hadoop Distributed File System) для распределенного хранения данных. HDFS разбивает данные на небольшие блоки и распределяет их по кластеру, что обеспечивает надежность и доступность данных даже в случае отказа отдельных узлов.

Вопрос 2:
Опишите ключевые компоненты экосистемы Hadoop и их роли в обработке и анализе данных.

Ответ: Экосистема Hadoop включает несколько ключевых компонентов:
HDFS (Hadoop Distributed File System): Распределенная система хранения, обеспечивающая надежность и масштабируемость.
YARN (Yet Another Resource Negotiator): Менеджер ресурсов, который распределяет ресурсы кластера между различными приложениями.
MapReduce: Модель программирования для обработки больших объемов данных путем разбиения задач на подзадачи, которые обрабатываются параллельно.
HBase: Распределенная, масштабируемая база данных, предназначенная для работы с большими объемами данных.
Hive: Инструмент для запросов и анализа данных с использованием языка запросов, похожего на SQL.
Pig: Платформа для анализа больших данных с использованием процедурного языка сценариев.
Spark: Инструмент для быстрой обработки больших объемов данных, поддерживающий как пакетную, так и потоковую обработку.

Вопрос 3:
Обсудите шаги по настройке среды Hadoop и Spark, выделяя важные параметры конфигурации и возможные проблемы.

Ответ:
Установка Java: Hadoop и Spark требуют установки Java. Убедитесь, что переменные окружения JAVA_HOME и PATH настроены правильно.
Скачивание и установка Hadoop: Загрузите и распакуйте дистрибутив Hadoop. Настройте конфигурационные файлы core-site.xml, hdfs-site.xmlи mapred-site.xml.
Форматирование HDFS: Выполните команду для форматирования HDFS перед первым запуском.
Запуск демонов Hadoop: Запустите демоны NameNode, DataNode, ResourceManager и NodeManager.
Скачивание и установка Spark: Загрузите и распакуйте дистрибутив Spark. Настройте переменные окружения SPARK_HOME и PATH.
Конфигурация Spark: Обновите файл spark-defaults.confдля настройки параметров Spark.
Запуск Spark: Запустите Spark на локальном режиме или кластере.

Вопрос 4:
Определите общие методы устранения неполадок при установке и настройке Hadoop и Spark.

Ответ:
Проверка журналов: Изучите журналы Hadoop и Spark для обнаружения ошибок.
Проверка конфигурации: Убедитесь, что все конфигурационные файлы настроены правильно и содержат корректные пути и параметры.
Проверка переменных окружения: Убедитесь, что переменные окружения JAVA_HOME, HADOOP_HOME и SPARK_HOME настроены верно.
Проверка сетевых настроек: Убедитесь, что все узлы кластера могут обмениваться данными и имеют корректные настройки сети.
Повторный запуск служб: Перезапустите демоны Hadoop и Spark после внесения изменений в конфигурацию.

Вопрос 5:
Объясните значение локализации данных в обработке Hadoop и Spark и как это способствует оптимизации производительности.
Ответ: Локализация данных (data locality) играет важную роль в производительности Hadoop и Spark. Принцип локализации данных заключается в том, чтобы обработка данных происходила как можно ближе к месту их хранения. Это минимизирует необходимость передачи данных по сети, что сокращает задержки и повышает общую производительность системы. В Hadoop и Spark узлы обработки выполняют задачи непосредственно на тех узлах, где хранятся данные, что позволяет эффективно использовать ресурсы кластера и ускоряет выполнение задач.
---

## 🎯 Lab 1: Hadoop and Spark - Big Data Environment Setup

### 📚 Objective
This lab aims to establish a Big Data environment using Hadoop and Spark, fundamental tools in the Big Data ecosystem. Students will learn to set up these tools, configure them, and execute basic operations to ensure a functional environment for future data processing tasks.

### 📝 Tasks

#### 📌 Task 1: Joining the Classroom
- Join the classroom using the invitation link provided by your instructor after creating your GitHub account.
- Follow the instructions to join the classroom, granting access to course materials and assignment submissions.

#### 📌 Task 2: Joining the Course
- Once in the classroom, join the specific course related to this lab.
- Navigate to the course page within the classroom interface and follow the instructions to join.
- This step provides access to the course syllabus, schedule, and assignments.

#### 📌 Task 3: Setting Up the Environment
- Install and configure Hadoop and Spark on your local machine or use GitHub Codespaces for development.
- Ensure your machine meets the necessary system requirements for Hadoop and Spark.
- If using GitHub Codespaces:
  - Launch a virtual development environment in your browser by opening the repository and selecting "Open with Codespaces."
- For local setup:
  - Download Hadoop and Spark from their official pages.
  - Follow the installation instructions provided by the documentation.
- Verify correct installation by running basic commands:
  - `hadoop version`: Checks the installed version of Hadoop.
  - `spark-shell`: Launches the Spark shell for Scala.
  - `pyspark`: Launches the Spark shell for Python.
  - `spark-shell --master local[2]`: Launches Spark shell with two local worker threads.

#### 📌 Task 4: Software Installation and Configuration
- **Downloading Required Software:**
  - Download the appropriate versions of Hadoop and Spark compatible with your system and course requirements.
  - Obtain Hadoop from the [Apache Hadoop official page](https://hadoop.apache.org/releases.html) and Spark from the [Apache Spark official page](https://spark.apache.org/downloads.html).
- **Configuring the Software:**
  - After downloading, extract the software files.
  - Configure Hadoop and Spark to work in your environment:
    - Edit XML configuration files located in the `etc/hadoop` and `conf` directories for Hadoop and Spark, respectively.
    - Adjust configurations based on your specific setup and course requirements.
- **Verifying Installation:**
  - Confirm correct installation by running basic commands:
    - `hadoop version`: Checks the installed version of Hadoop.
    - `hadoop fs -ls /`: Lists the contents of the root directory in Hadoop's distributed file system.

#### 📌 Task 5: Running Simple Spark Programs
- Write and execute Spark programs to validate setup and execution in your environment. Explore various use cases for Spark programs, such as:
  - **Data Transformation:** Perform data transformations like filtering, mapping, and aggregating on large datasets.
  - **Machine Learning:** Implement machine learning algorithms for tasks like classification, regression, and clustering.
  - **Graph Processing:** Analyze graph data structures for applications such as social network analysis and recommendation systems.
  - **Real-time Streaming:** Process real-time data streams from sources like sensors, logs, or social media feeds.
  - **Text Analysis:** Conduct text mining and natural language processing tasks like sentiment analysis, topic modeling, and entity recognition.
  - **Geospatial Analysis:** Analyze spatial data for applications in GIS, location-based services, and urban planning.
  - **Image Processing:** Apply image processing techniques for tasks like object detection, image classification, and image segmentation.
  - **Time Series Analysis:** Analyze time series data for forecasting, anomaly detection, and trend analysis.
  - **Joining Datasets:** Perform join operations on multiple datasets to combine and analyze related information.

Two examples are provided below:

  - **Simple Data Analysis Program (Python):**
    ```python
    from pyspark.sql import SparkSession
    
    # Create SparkSession
    spark = SparkSession.builder.appName("SimpleDataAnalysis").getOrCreate()
    
    # Create DataFrame
    data = [("John", 25), ("Alice", 30), ("Bob", 35)]
    df = spark.createDataFrame(data, ["Name", "Age"])
    
    # Perform transformations and actions
    df.show()
    df.filter(df["Age"] > 30).show()
    ```

  - **Simple Data Analysis Program (Scala):**
    ```scala
    import org.apache.spark.sql.SparkSession
    
    // Create SparkSession
    val spark = SparkSession.builder().appName("SimpleDataAnalysis").getOrCreate()
    
    // Create DataFrame
    import spark.implicits._
    val data = Seq(("John", 25), ("Alice", 30), ("Bob", 35))
    val df = data.toDF("Name", "Age")
    
    // Perform transformations and actions
    df.show()
    df.filter($"Age" > 30).show()
    ```

  - **Pi Estimation Program (Python):**
    ```python
    from pyspark.sql import SparkSession
    import random
    
    # Create SparkSession
    spark = SparkSession.builder.appName("PiEstimation").getOrCreate()
    
    # Number of points to generate
    num_points = 1000000
    
    # Generate random points and count those inside the unit circle
    inside_circle = spark.sparkContext.parallelize(range(0, num_points)) \
                    .filter(lambda _: random.random()**2 + random.random()**2 < 1).count()
    
    # Estimate Pi
    pi_estimate = 4 * inside_circle / num_points
    print("Estimated Pi:", pi_estimate)
    ```

  - **Pi Estimation Program (Scala):**
    ```scala
    import org.apache.spark.sql.SparkSession
    
    // Create SparkSession
    val spark = SparkSession.builder().appName("PiEstimation").getOrCreate()
    
    // Number of points to generate
    val num_points = 1000000
    
    // Generate random points and count those inside the unit circle
    val inside_circle = spark.sparkContext.parallelize(0 until num_points)
                        .filter { _ =>
                          val x = math.random()
                          val y = math.random()
                          x * x + y * y < 1
                        }.count()
    
    // Estimate Pi
    val pi_estimate = 4.0 * inside_circle / num_points
    println(s"Estimated Pi: $pi_estimate")
    ```

- Submit your programs as `.py` or `.scala` files, depending on the language used.

---

## 🧠 Self-Check Questionnaire

### 🔍 Question 1:
Explain the purpose of Hadoop in the Big Data ecosystem and its relationship with distributed storage systems like HDFS.

### 🔍 Question 2:
Describe the key components of the Hadoop ecosystem and their respective roles in data processing and analysis.

### 🔍 Question 3:
Discuss the steps involved in setting up a Hadoop and Spark environment, highlighting important configuration parameters and potential challenges.

### 🔍 Question 4:
Identify common troubleshooting techniques for resolving issues during Hadoop and Spark installation and configuration.

### 🔍 Question 5:
Explain the significance of data locality in Hadoop and Spark processing and how it contributes to performance optimization.
