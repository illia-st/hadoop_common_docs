# Бібліотеки Apache Commons

1. **commons-beanutils**: Інструменти для спрощення маніпуляцій з JavaBeans, зокрема отримання та встановлення значень властивостей об'єктів Java.
   - **Приклад**:
     ```java
     import org.apache.commons.beanutils.BeanUtils;
     
     MyBean bean = new MyBean();
     BeanUtils.setProperty(bean, "name", "ExampleName");
     String name = BeanUtils.getProperty(bean, "name");
     ```

2. **commons-chain**: Фреймворк для реалізації шаблону ["ланцюжок відповідальності" (Chain of Responsibility)](https://refactoring.guru/design-patterns/chain-of-responsibility). Це дозволяє створювати послідовність команд для обробки запитів.

    - **Приклад**:
        ```java
        package org.apache.commons.mailreader;

        import junit.framework.TestCase;
        import org.apache.commons.chain.Command;
        import org.apache.commons.chain.Context;
        import org.apache.commons.chain.mailreader.commands.ProfileCheck;
        import org.apache.commons.chain.mailreader.commands.Profile;
        import org.apache.commons.chain.impl.ContextBase;

        public class ProfileCheckTest extends TestCase {

        public void testProfileCheckNeed() {

            Context context = new ContextBase();
            Command command = new ProfileCheck();
            try {
                command.execute(context);
            } catch (Exception e) {
                fail(e.getMessage());
            }

            Profile profile = (Profile) context.get(Profile.PROFILE_KEY);
            assertNotNull("Missing Profile", profile);

        }
        ```
   
3. **commons-cli**: Бібліотека для роботи з аргументами командного рядка. Вона дозволяє зручно визначати та обробляти опції командного рядка.
   - **Приклад**:
     ```java
     import org.apache.commons.cli.*;

     Options options = new Options();
     options.addOption("h", "help", false, "Show help");

     CommandLineParser parser = new DefaultParser();
     CommandLine cmd = parser.parse(options, args);
     if (cmd.hasOption("h")) {
         System.out.println("Help command triggered");
     }
     ```

4. **commons-codec**: Бібліотека для кодування та декодування даних, зокрема реалізація Base64, хешування та інших алгоритмів.
   - **Приклад**:
     ```java
     import org.apache.commons.codec.binary.Base64;

     byte[] encodedBytes = Base64.encodeBase64("example".getBytes());
     byte[] decodedBytes = Base64.decodeBase64(encodedBytes);
     ```

5. **commons-collections**: Набір додаткових класів колекцій для Java, таких як багатовимірні мапи, декоратори та унікальні структури даних.

    - **Приклад**:
     ```java
    IterableMap map = new HashedMap();
    MapIterator it = map.mapIterator();
    while (it.hasNext()) {
        Object key = it.next();
        Object value = it.getValue();

        it.setValue(newValue);
    }
     ```
   
6. **commons-configuration**: Інструменти для завантаження конфігураційних файлів різних форматів (XML, Properties) та роботи з ними.
- **Приклад**:
     ```java
    Configurations configs = new Configurations();
    try
    {
        Configuration config = configs.properties(new File("config.properties"));
        // access configuration properties
        ...
    }
    catch (ConfigurationException cex)
    {
        // Something went wrong
    }
     ```

7. **commons-daemon**: Засоби для створення та управління системними демонами та сервісами.
- **Приклад**:
    ```java
    import org.apache.commons.daemon.Daemon;
    import org.apache.commons.daemon.DaemonContext;

    public class MyDaemon implements Daemon {
        @Override
        public void init(DaemonContext context) throws Exception {
            // Initialize your daemon here
        }

        @Override
        public void start() throws Exception {
            // Start your daemon here
        }

        @Override
        public void stop() throws Exception {
            // Stop your daemon here
        }

        @Override
        public boolean destroy() {
            // Destroy your daemon here
            return true;
        }
    }
    ```

8. **commons-dbcp**: Пул з'єднань із базою даних, який забезпечує повторне використання з'єднань для підвищення ефективності.
- **Приклад**:
    BasicDataSource Example
    ```java
    BasicDataSource Example
    BasicDataSource ds = new BasicDataSource();
    ds.setDriverClassName("com.mysql.cj.jdbc.Driver");
    ds.setUrl("jdbc:mysql://localhost:3306/mydb");
    ds.setUsername("username");
    ds.setPassword("password");
    ds.setInitialSize(5);
    ds.setMaxActive(10);
    ```
    PoolingDataSource Example    
    ```java
    PoolingDataSource Example
    PoolingDataSource ds = new PoolingDataSource(new BasicDataSource());
    ds.setDriverClassName("com.mysql.cj.jdbc.Driver");
    ds.setUrl("jdbc:mysql://localhost:3306/mydb");
    ds.setUsername("username");
    ds.setPassword("password");
    ds.setInitialSize(5);
    ds.setMaxActive(10);
    ```
    Spring Configuration Example
    ```xml
    <bean id="dataSource" class="org.apache.commons.dbcp2.BasicDataSource">
        <property name="driverClassName" value="com.mysql.cj.jdbc.Driver"/>
        <property name="url" value="jdbc:mysql://localhost:3306/mydb"/>
        <property name="username" value="username"/>
        <property name="password" value="password"/>
        <property name="initialSize" value="5"/>
        <property name="maxActive" value="10"/>
    </bean>
    ```
   
9. **commons-io**: Утиліти для роботи з введенням/виведенням, включаючи прості методи для читання та запису файлів.
   - **Приклад**:
     ```java
     import org.apache.commons.io.FileUtils;
     FileUtils.writeStringToFile(new File("example.txt"), "Hello, world!", "UTF-8");
     ```

10. **commons-lang**: Додаткові утиліти для Java, такі як маніпуляції з рядками, перевірки, випадкові числа.
    - **Приклад**:
      ```java
      import org.apache.commons.lang3.StringUtils;
      
      boolean isBlank = StringUtils.isBlank(" ");
      ```

11. **commons-logging**: Абстракція для логування, що дозволяє використовувати різні бібліотеки логування, наприклад Log4j або JDK Logging.
- **Приклад**:
    ```java
        import org.apache.commons.logging.Log;
        import org.apache.commons.logging.LogFactory;

        public class Example {
            private static Log log = LogFactory.getLog(Example.class);

            public void doSomething() {
                log.debug("Entering method");
                // method implementation
                log.debug("Exiting method");
            }
        }
    ```

12. **commons-math**: Математичні функції та алгоритми, які включають обчислення статистики, алгебру та інше.
- **Приклад**:
    ```java
        import org.apache.commons.math3.stat.descriptive.DescriptiveStatistics;

        public class StatisticsExample {
            public static void main(String[] args) {
                DescriptiveStatistics stats = new DescriptiveStatistics();

                double[] values = {1.2, 3.5, 4.7, 2.8, 3.9};
                for (double value : values) {
                    stats.addValue(value);
                }

                System.out.println("Mean: " + stats.getMean());
                System.out.println("Variance: " + stats.getVariance());
                System.out.println("Standard Deviation: " + stats.getStandardDeviation());
            }
        }

    ```

13. **commons-net**: Бібліотека для роботи з мережевими протоколами, такими як FTP, SMTP, POP3.
- **Приклад**:
    ```java
        import org.apache.commons.net.ftp.FTPClient;
        import java.io.FileOutputStream;
        import java.io.IOException;

        public class FTPExample {
            public static void main(String[] args) {
                FTPClient ftpClient = new FTPClient();
                try {
                    ftpClient.connect("ftp.example.com");
                    ftpClient.login("username", "password");

                    // List files in the root directory
                    String[] files = ftpClient.listNames();
                    for (String file : files) {
                        System.out.println("File: " + file);
                    }

                    // Download a file from the FTP server
                    FileOutputStream outputStream = new FileOutputStream("downloadedFile.txt");
                    boolean success = ftpClient.retrieveFile("/serverDirectory/file.txt", outputStream);
                    outputStream.close();

                    if (success) {
                        System.out.println("File downloaded successfully!");
                    }

                    ftpClient.logout();
                } catch (IOException ex) {
                    ex.printStackTrace();
                } finally {
                    try {
                        ftpClient.disconnect();
                    } catch (IOException ex) {
                        ex.printStackTrace();
                    }
                }
            }
        }

    ```
14. **commons-pool**: Загальний пул об'єктів, який дозволяє повторне використання об'єктів, що часто створюються.
- **Приклад**:
    ```java
        import org.apache.commons.pool.ObjectPool;
        import org.apache.commons.pool.PoolableObjectFactory;

        public class Example {
            public static void main(String[] args) {
                // Create a pool with a maximum size of 10
                ObjectPool pool = new GenericObjectPool(new MyObjectFactory(), 10);

                // Borrow an object from the pool
                Object obj = pool.borrowObject();
                // Use the object...
                pool.returnObject(obj);
            }
        }

        class MyObjectFactory implements PoolableObjectFactory {
            @Override
            public Object makeObject() throws Exception {
                // Create a new object
                return new MyObject();
            }

            @Override
            public void destroyObject(Object obj) throws Exception {
                // Destroy the object
                ((MyObject) obj).destroy();
            }
        }
    ```

15. **commons-validator**: Інструменти для перевірки даних, зокрема валідація email, телефонів, дат тощо.
- **Приклад**:
    Валідаця email
    ```java
    EmailValidator emailValidator = EmailValidator.getInstance();
    boolean isValid = emailValidator.isValid("example@example.com");
    ```

**Примітка**: Це загальні описи, і для повного списку потрібно буде звернутися до [офіційної документації](https://commons.apache.org/) або [репозиторію](https://repository.apache.org/content/repositories/staging/) Apache Commons.
