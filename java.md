#### Java

```bash
# Установка Java
$ sudo apt update
# Установка JRE (последняя версия)
$ sudo apt install default-jre
# Установка JDK (последняя версия)
$ sudo apt install default-jdk

# Проверка установки Java
$ java -version

# Установка Maven
$ sudo apt install maven

# Проверка установки Maven
$ mvn -v
```
```
# Создание проекта my-app
$ mvn archetype:generate -DgroupId=com.example -DartifactId=my-app -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false

# Сборка проекта создаст файл JAR в директории target под именем my-app-1.0-SNAPSHOT.jar
$ mvn clean package

# Запуск скомпилированного приложения
$ java -cp target/my-app-1.0-SNAPSHOT.jar com.example.App
```
Пример pom.xml - Конфигурация Maven проекта
```
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>my-app</artifactId>
    <version>1.0-SNAPSHOT</version>

    <properties>
        <maven.compiler.source>11</maven.compiler.source>
        <maven.compiler.target>11</maven.compiler.target>
    </properties>

    <dependencies>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.11</version>
            <scope>test</scope>
        </dependency>
    </dependencies>
</project>

```

```
# Это создаст файлы mvnw и mvnw.cmd в корне вашего проекта (нужны для Docker)
$ mvn -N io.takari:maven:wrapper
```
