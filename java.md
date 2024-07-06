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
Maven
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
Tomcat
```
$ java -version

# Создание группы и учётной записи для Apache Tomcat
$ sudo mkdir /opt/tomcat/
$ sudo groupadd tomcat
$ sudo useradd -s /bin/false -g tomcat -d /opt/tomcat tomcat

# Вставить ссылку на .tar.gz с сайта https://tomcat.apache.org/
$ curl -O https://dlcdn.apache.org/tomcat/tomcat-10/v10.1.25/bin/apache-tomcat-10.1.25.tar.gz
$ sudo tar xzvf apache-tomcat-10.1.25.tar.gz -C /opt/tomcat/ --strip-component=1
$ cd /opt/tomcat/

# Группе и пользователю tomcat предоставьте права на каталог, в который вы произвели установку Tomcat
$ sudo chown -RH tomcat: /opt/tomcat/

# Измените разрешения на sh-скрипты, чтобы предоставить им доступ на исполнение из директории /opt/tomcat/bin/
$ sudo sh -c 'chmod +x /opt/tomcat/bin/*.sh'

$ sudo update-java-alternatives -l

$ cd /etc/systemd/system/
$ sudo nano tomcat.service

[Unit]
Description=Apache Tomcat
After=network.target
[Service]
Type=forking
User=tomcat
Group=tomcat
Environment="JAVA_HOME=/usr/lib/jvm/java-1.11.0-openjdk-amd64"
Environment="JAVA_OPTS=-Djava.security.egd=file:///dev/urandom -Djava.awt.headless=true"
Environment="CATALINA_BASE=/opt/tomcat"
Environment="CATALINA_HOME=/opt/tomcat"
Environment="CATALINA_PID=/opt/tomcat/temp/tomcat.pid"
Environment="CATALINA_OPTS=-Xms512M -Xmx1024M -server -XX:+UseParallelGC"
ExecStart=/opt/tomcat/bin/startup.sh
ExecStop=/opt/tomcat/bin/shutdown.sh
[Install]
WantedBy=multi-user.target

# !!!Обратите внимание, что переменной JAVA_HOME должно соответствовать значение, содержащее путь к одной из версий Java.!!!

# Перечитаются конфигурации всех юнитов
$ sudo systemctl daemon-reload

# Запуск сервиса Tomcat
$ sudo systemctl start tomcat

# Проверка работы
$ sudo systemctl status tomcat

# Добавьте службу в автозагрузку, чтобы Tomcat стартовал вместе с запуском системы
$  sudo systemctl enable tomcat
```
