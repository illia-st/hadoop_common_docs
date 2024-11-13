# Файлова система в Apache Hadoop Common

Apache Hadoop Common забезпечує підтримку для файлових систем, що дозволяє різним модулям Hadoop працювати з даними, зберігаючи їх у розподіленій файловій системі. Хоча основна система зберігання Hadoop — це **HDFS (Hadoop Distributed File System)**, Hadoop Common також підтримує роботу з іншими файловими системами та надає інтерфейси для їхнього інтегрування.

### Основні компоненти файлової системи Hadoop Common

1. **Абстракція файлової системи**: Hadoop Common надає універсальний інтерфейс `FileSystem`, що абстрагує роботу з різними типами файлових систем. Цей інтерфейс дозволяє виконувати базові операції — створення, читання, запис та видалення файлів і каталогів.

2. **Підтримка різних файлових систем**:
   - **HDFS (Hadoop Distributed File System)**: Основна розподілена файлова система, створена для зберігання великих обсягів даних і оптимізована для високошвидкісного читання.
   - **Local File System**: Hadoop може використовувати локальну файлову систему як файлову систему за замовчуванням або для тестування.
   - **S3 (Amazon Simple Storage Service)**: Hadoop підтримує роботу з S3 для зберігання даних в хмарі AWS.
   - **Azure Blob Storage**: Підтримка зберігання та обробки даних у хмарі Microsoft Azure.
   - **HFTP, WebHDFS**: Протоколи для доступу до даних HDFS через HTTP/HTTPS, що дозволяє взаємодію з даними HDFS віддалено.

3. **Інструменти командного рядка**: Hadoop Common включає утиліти командного рядка для взаємодії з файловими системами. Наприклад:
   - `hadoop fs -ls /path`: Відображає список файлів та каталогів у вказаному шляху.
   - `hadoop fs -put localfile /path`: Копіює файл з локальної файлової системи до файлової системи Hadoop.
   - `hadoop fs -get /path localfile`: Завантажує файл з файлової системи Hadoop до локальної.

4. **Конфігурація та безпека файлової системи**: Файлова система Hadoop Common підтримує конфігурацію через XML-файли, де можна налаштувати різні параметри, такі як шляхи до файлової системи, розміри блоків, рівень реплікації, а також параметри безпеки для захисту даних.

5. **Обробка великих файлів**: Завдяки Hadoop Common, файлові системи можуть оптимізовано працювати з великими файлами, що розділяються на блоки, зберігаються та обробляються паралельно у кластері.

### Приклад роботи з файловою системою Hadoop

Ось приклад коду для завантаження файлу до файлової системи HDFS за допомогою API Hadoop:

```java
import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.fs.FileSystem;
import org.apache.hadoop.fs.Path;

import java.io.IOException;
import java.net.URI;

public class HDFSExample {
    public static void main(String[] args) throws IOException {
        Configuration configuration = new Configuration();
        FileSystem hdfs = FileSystem.get(URI.create("hdfs://namenode:9000"), configuration);
        
        Path localPath = new Path("/local/path/to/file.txt");
        Path hdfsPath = new Path("/hdfs/path/to/file.txt");
        
        hdfs.copyFromLocalFile(localPath, hdfsPath);
        
        System.out.println("Файл успішно завантажено до HDFS!");
    }
}
