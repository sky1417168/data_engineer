Java 是一种广泛使用的面向对象的编程语言，由 Sun Microsystems（现在属于 Oracle）于 1995 年推出。Java 以其“一次编写，到处运行”的理念而闻名，这得益于其跨平台的特性。Java 适用于多种应用场景，包括企业级应用、Web 开发、Android 应用开发、大数据处理等。

### 1. Java 基本概念

#### 1.1 **特点**
- **跨平台**：Java 代码编译成字节码（. class 文件），可以在任何安装了 Java 虚拟机（JVM）的平台上运行。
- **面向对象**：Java 是一种纯面向对象的语言，支持封装、继承和多态。
- **强类型**：Java 是一种强类型语言，变量必须先声明类型再使用。
- **垃圾回收**：Java 自动管理内存，通过垃圾回收机制回收不再使用的对象。
- **安全性**：Java 提供了多种安全机制，如沙箱环境和类加载器。
- **多线程**：Java 内置了多线程支持，便于开发并发应用程序。

### 2. Java 语法

#### 2.1 **变量声明**
- **基本类型**：
  ```java
  int a = 10;
  double b = 3.14;
  boolean c = true;
  char d = 'A';
  ```
- **引用类型**：
  ```java
  String str = "Hello";
  ```

#### 2.2 **数据类型**
- **基本类型**：
  - **整型**：`byte`, `short`, `int`, `long`
  - **浮点型**：`float`, `double`
  - **字符型**：`char`
  - **布尔型**：`boolean`
- **引用类型**：
  - **类**：`String`, `ArrayList`, `HashMap` 等
  - **数组**：`int[]`, `String[]` 等

#### 2.3 **控制结构**
- **条件语句**：
  ```java
  if (x > 0) {
      System.out.println("Positive");
  } else if (x < 0) {
      System.out.println("Negative");
  } else {
      System.out.println("Zero");
  }
  ```
- **循环语句**：
  ```java
  for (int i = 0; i < 5; i++) {
      System.out.println(i);
  }

  while (x > 0) {
      System.out.println(x);
      x--;
  }

  do {
      System.out.println(x);
      x--;
  } while (x > 0);
  ```

#### 2.4 **函数（方法）**
- **定义方法**：
  ```java
  public int add(int a, int b) {
      return a + b;
  }
  ```
- **可变参数方法**：
  ```java
  public int sum(int... numbers) {
      int total = 0;
      for (int number : numbers) {
          total += number;
      }
      return total;
  }
  ```

#### 2.5 **类和对象**
- **定义类**：
  ```java
  public class Person {
      private String name;
      private int age;

      public Person(String name, int age) {
          this.name = name;
          this.age = age;
      }

      public String getName() {
          return name;
      }

      public void setName(String name) {
          this.name = name;
      }

      public int getAge() {
          return age;
      }

      public void setAge(int age) {
          this.age = age;
      }

      public void sayHello() {
          System.out.println("Hello, my name is " + name + " and I am " + age + " years old.");
      }
  }
  ```
- **创建对象**：
  ```java
  Person person = new Person("John Doe", 30);
  person.sayHello();
  ```

### 3. 面向对象编程

#### 3.1 **封装**
- **私有属性**：使用 `private` 关键字将属性设为私有。
- **公共方法**：提供公共方法（getter 和 setter）来访问私有属性。

#### 3.2 **继承**
- **定义子类**：
  ```java
  public class Student extends Person {
      private String studentId;

      public Student(String name, int age, String studentId) {
          super(name, age);
          this.studentId = studentId;
      }

      public String getStudentId() {
          return studentId;
      }

      public void setStudentId(String studentId) {
          this.studentId = studentId;
      }

      @Override
      public void sayHello() {
          System.out.println("Hello, my name is " + getName() + ", I am " + getAge() + " years old, and my student ID is " + studentId);
      }
  }
  ```

#### 3.3 **多态**
- **方法重写**：子类可以重写父类的方法。
- **动态绑定**：方法调用在运行时确定。
  ```java
  Person person = new Student("John Doe", 30, "12345");
  person.sayHello();  // 调用 Student 类的 sayHello 方法
  ```

### 4. 异常处理

- **抛出异常**：
  ```java
  public void divide(int a, int b) throws ArithmeticException {
      if (b == 0) {
          throw new ArithmeticException("Division by zero");
      }
      System.out.println(a / b);
  }
  ```
- **捕获异常**：
  ```java
  try {
      divide(10, 0);
  } catch (ArithmeticException e) {
      System.out.println("Error: " + e.getMessage());
  } finally {
      System.out.println("Finally block executed");
  }
  ```

### 5. 集合框架

- **常用集合**：
  - **List**：`ArrayList`, `LinkedList`
  - **Set**：`HashSet`, `TreeSet`
  - **Map**：`HashMap`, `TreeMap`
  ```java
  List<String> list = new ArrayList<>();
  list.add("Apple");
  list.add("Banana");

  Set<String> set = new HashSet<>();
  set.add("Apple");
  set.add("Banana");

  Map<String, Integer> map = new HashMap<>();
  map.put("Apple", 1);
  map.put("Banana", 2);
  ```

### 6. 输入输出

- **读取文件**：
  ```java
  import java.io.BufferedReader;
  import java.io.FileReader;
  import java.io.IOException;

  public class FileReadExample {
      public static void main(String[] args) {
          try (BufferedReader reader = new BufferedReader(new FileReader("file.txt"))) {
              String line;
              while ((line = reader.readLine()) != null) {
                  System.out.println(line);
              }
          } catch (IOException e) {
              e.printStackTrace();
          }
      }
  }
  ```
- **写入文件**：
  ```java
  import java.io.BufferedWriter;
  import java.io.FileWriter;
  import java.io.IOException;

  public class FileWriteExample {
      public static void main(String[] args) {
          try (BufferedWriter writer = new BufferedWriter(new FileWriter("file.txt"))) {
              writer.write("Hello, World!");
          } catch (IOException e) {
              e.printStackTrace();
          }
      }
  }
  ```

### 7. 网络编程

- **TCP 服务器**：
  ```java
  import java.io.*;
  import java.net.*;

  public class TCPServer {
      public static void main(String[] args) throws IOException {
          ServerSocket serverSocket = new ServerSocket(8080);
          System.out.println("Server started on port 8080");

          while (true) {
              Socket socket = serverSocket.accept();
              new Thread(new ClientHandler(socket)).start();
          }
      }

      static class ClientHandler implements Runnable {
          private Socket socket;

          public ClientHandler(Socket socket) {
              this.socket = socket;
          }

          @Override
          public void run() {
              try (BufferedReader in = new BufferedReader(new InputStreamReader(socket.getInputStream()));
                   PrintWriter out = new PrintWriter(socket.getOutputStream(), true)) {

                  String inputLine;
                  while ((inputLine = in.readLine()) != null) {
                      System.out.println("Received: " + inputLine);
                      out.println("Echo: " + inputLine);
                  }
              } catch (IOException e) {
                  e.printStackTrace();
              }
          }
      }
  }
  ```
- **TCP 客户端**：
  ```java
  import java.io.*;
  import java.net.*;

  public class TCPClient {
      public static void main(String[] args) throws IOException {
          Socket socket = new Socket("localhost", 8080);
          try (BufferedReader in = new BufferedReader(new InputStreamReader(socket.getInputStream()));
               PrintWriter out = new PrintWriter(socket.getOutputStream(), true);
               BufferedReader stdIn = new BufferedReader(new InputStreamReader(System.in))) {

              String userInput;
              while ((userInput = stdIn.readLine()) != null) {
                  out.println(userInput);
                  System.out.println("Echo: " + in.readLine());
              }
          }
      }
  }
  ```

### 8. 并发编程

- **线程**：
  ```java
  public class MyThread extends Thread {
      @Override
      public void run() {
          System.out.println("Thread running");
      }

      public static void main(String[] args) {
          MyThread thread = new MyThread();
          thread.start();
      }
  }
  ```
- **Runnable**：
  ```java
  public class MyRunnable implements Runnable {
      @Override
      public void run() {
          System.out.println("Runnable running");
      }

      public static void main(String[] args) {
          Thread thread = new Thread(new MyRunnable());
          thread.start();
      }
  }
  ```
- **同步**：
  ```java
  public class Counter {
      private int count = 0;

      public synchronized void increment() {
          count++;
      }

      public synchronized int getCount() {
          return count;
      }

      public static void main(String[] args) {
          Counter counter = new Counter();

          Thread t1 = new Thread(() -> {
              for (int i = 0; i < 1000; i++) {
                  counter.increment();
              }
          });

          Thread t2 = new Thread(() -> {
              for (int i = 0; i < 1000; i++) {
                  counter.increment();
              }
          });

          t1.start();
          t2.start();

          try {
              t1.join();
              t2.join();
          } catch (InterruptedException e) {
              e.printStackTrace();
          }

          System.out.println("Final count: " + counter.getCount());
      }
  }
  ```

### 9. 最佳实践

- **代码组织**：将相关的代码组织成包，提高代码的可维护性和复用性。
- **异常处理**：合理使用异常处理机制，避免捕获过于宽泛的异常。
- **性能优化**：使用合适的数据结构和算法，避免不必要的对象创建。
- **测试**：编写单元测试和集成测试，确保代码的正确性和可靠性。

### 10. 工具和框架

- **开发工具**：
  - **IntelliJ IDEA**：功能强大的 IDE，支持多种编程语言。
  - **Eclipse**：流行的 Java 开发 IDE。
  - **NetBeans**：轻量级的 Java 开发 IDE。
- **构建工具**：
  - **Maven**：项目管理和构建工具。
  - **Gradle**：自动化构建工具。
- **框架**：
  - **Spring**：企业级应用开发框架。
  - **Hibernate**：ORM 框架。
  - **Struts**：Web 应用开发框架。
  - **Vaadin**：Web 应用开发框架，支持 Java 和 Web 组件。
