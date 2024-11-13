# Конфігураційні файли в Apache Hadoop Common

**Apache Hadoop Common** використовує набір конфігураційних файлів у форматі XML для налаштування різних параметрів системи. Ці файли визначають поведінку та взаємодію компонентів Hadoop, забезпечуючи гнучкість та адаптивність системи до різних середовищ та вимог.

## Основні конфігураційні файли

1. **core-site.xml**

   Містить загальні налаштування для всіх компонентів Hadoop, такі як:

   - Шлях до файлової системи за замовчуванням (`fs.defaultFS`).
   - Налаштування безпеки та автентифікації.
   - Параметри вводу/виводу та стиснення даних.

   **Приклад:**

   ```xml
   <configuration>
       <property>
           <name>fs.defaultFS</name>
           <value>hdfs://namenode:9000</value>
       </property>
       <property>
           <name>hadoop.security.authentication</name>
           <value>kerberos</value>
       </property>
   </configuration>
   '''
2. **hdfs-site.xml**

    Визначає налаштування для Hadoop Distributed File System (HDFS), зокрема:
    - Розмір блоків (`dfs.blocksize`).
    - Кількість реплік для кожного блоку (`dfs.replication`).
    - Шляхи до директорій зберігання даних на NameNode та DataNode.
    **Приклад:**

   ```xml
   <configuration>
        <property>
            <name>dfs.replication</name>
            <value>3</value>
        </property>
        <property>
            <name>dfs.blocksize</name>
            <value>134217728</value> <!-- 128 MB -->
        </property>
    </configuration>
   '''
3. **mapred-site.xml**

    Містить налаштування для MapReduce, такі як:
    - Тип фреймворку для виконання завдань (`mapreduce.framework.name`).
    - Розмір пам'яті для маперів та ред'юсерів.
    - Шляхи до директорій для зберігання проміжних даних.
    **Приклад:**

    ```xml
   <configuration>
        <property>
            <name>mapreduce.framework.name</name>
            <value>yarn</value>
        </property>
        <property>
            <name>mapreduce.map.memory.mb</name>
            <value>1024</value>
        </property>
    </configuration>
   '''
4. **yarn-site.xml**
    Визначає налаштування для YARN (Yet Another Resource Negotiator), зокрема:
    - Ресурси, доступні для контейнерів (yarn.nodemanager.resource.memory-mb).
    - Адреси та порти для ResourceManager та NodeManager.
    - Параметри безпеки та ізоляції ресурсів.
     **Приклад:**
    
    ```xml
   <configuration>
        <property>
            <name>yarn.nodemanager.resource.memory-mb</name>
            <value>8192</value>
        </property>
        <property>
            <name>yarn.resourcemanager.address</name>
            <value>resourcemanager:8032</value>
        </property>
    </configuration>
   '''

## Рекомендації щодо налаштування

- **Резервне копіювання**: Перед внесенням змін до конфігураційних файлів рекомендується створювати резервні копії оригінальних файлів.

- **Валідація**: Після змін перевірте синтаксис XML-файлів, щоб уникнути помилок при запуску системи.

- **Документація**: Детальні описи параметрів та їх можливих значень доступні в офіційній документації Apache Hadoop.

## Додаткові ресурси
[Apache Hadoop Configuration Documentation](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-common/core-default.xml)
    

