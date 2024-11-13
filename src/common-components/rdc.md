# Модуль RPC (Remote Procedure Call) в Apache Hadoop Common

**Apache Hadoop Common** включає модуль **RPC (Remote Procedure Call)**, який забезпечує ефективну та масштабовану комунікацію між різними компонентами Hadoop у розподіленому середовищі. Цей модуль дозволяє клієнтам викликати методи на віддалених серверах так, ніби вони є локальними, спрощуючи взаємодію між процесами.

## Основні особливості модуля RPC в Hadoop

1. **Інтерфейси та проксі**

   Hadoop використовує загальний механізм RPC, де клієнт і сервер спільно використовують визначений інтерфейс. Клієнт створює проксі для цього інтерфейсу, що дозволяє викликати віддалені методи через локальні виклики.

   **Приклад визначення інтерфейсу:**

   ```java
   import org.apache.hadoop.ipc.VersionedProtocol;

   public interface MyProtocol extends VersionedProtocol {
       long versionID = 1L;

       String ping(String message);
   }
   ```
2. **Серверна реалізація**

    Сервер реалізує визначений інтерфейс та обробляє запити від клієнтів.

    **Приклад реалізації сервера:**
    ```java
    import org.apache.hadoop.ipc.RPC;
    import org.apache.hadoop.ipc.Server;
    import org.apache.hadoop.conf.Configuration;

    public class MyServer implements MyProtocol {
        @Override
        public String ping(String message) {
            return "Received: " + message;
        }

        public static void main(String[] args) throws Exception {
            Server server = new RPC.Builder(new Configuration())
                .setProtocol(MyProtocol.class)
                .setInstance(new MyServer())
                .setBindAddress("localhost")
                .setPort(12345)
                .build();
            server.start();
        }
    }
    ```
3. **Клієнтська реалізація**

    Клієнт створює проксі для віддаленого інтерфейсу та викликає методи, які передаються на сервер через RPC.

    **Приклад реалізації клієнта:**
    ```java
    import org.apache.hadoop.ipc.RPC;
    import org.apache.hadoop.conf.Configuration;

    public class MyClient {
        public static void main(String[] args) throws Exception {
            MyProtocol proxy = RPC.getProxy(
                MyProtocol.class,
                MyProtocol.versionID,
                new InetSocketAddress("localhost", 12345),
                new Configuration()
            );
            String response = proxy.ping("Hello, Hadoop RPC!");
            System.out.println(response);
            RPC.stopProxy(proxy);
        }
    }

    ```
4. **Версіонування протоколів**

Для забезпечення зворотної сумісності Hadoop підтримує версіонування протоколів. Кожен інтерфейс RPC має унікальне ім'я та версію, що дозволяє клієнтам і серверам узгоджувати підтримувані версії.

5. **Безпека**

Модуль RPC підтримує автентифікацію та авторизацію, забезпечуючи безпечну комунікацію між компонентами. Hadoop може бути налаштований для використання Kerberos для автентифікації RPC-з'єднань.

## Додаткові ресурси

[Hadoop RPC - Apache Software Foundation](https://cwiki.apache.org/confluence/display/HADOOP2/HadoopRpc)
