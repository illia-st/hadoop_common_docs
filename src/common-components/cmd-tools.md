# Інструменти командного рядка в Apache Hadoop Common

**Apache Hadoop Common** надає набір інструментів командного рядка, які спрощують взаємодію з різними компонентами Hadoop. Ці утиліти дозволяють користувачам та адміністраторам ефективно керувати файловими системами, запускати завдання та виконувати інші адміністративні операції.

## Основні інструменти командного рядка

1. **hadoop fs**

   Утиліта для роботи з файловими системами, підтримуваними Hadoop, зокрема HDFS. Вона надає команди для управління файлами та каталогами.

   **Приклади використання:**

   - Перегляд вмісту каталогу:

     ```bash
     hadoop fs -ls /user/hadoop/
     ```

   - Копіювання файлу з локальної файлової системи до HDFS:

     ```bash
     hadoop fs -put localfile.txt /user/hadoop/
     ```

   - Завантаження файлу з HDFS до локальної файлової системи:

     ```bash
     hadoop fs -get /user/hadoop/file.txt localfile.txt
     ```

2. **hadoop jar**

   Дозволяє запускати Java-додатки, упаковані у форматі JAR, на кластері Hadoop. Це корисно для виконання MapReduce-завдань.

   **Приклад використання:**

   ```bash
   hadoop jar myapp.jar com.example.MyApp input output