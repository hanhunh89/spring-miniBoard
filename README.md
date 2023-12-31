# spring-miniBoard

Spring으로 작은 게시판을 만들어보자. 

## 개발환경
```
OS google cloud platform E2 (Debian 5.10.197-1 (2023-09-29) x86_64) 
JAVA 11
Apache Tomcat x.x
Spring 3.1.1 RELEASE
Spring Security 3.1.7.RELEASE
eclipse 2020-09 (4.17.0)
Spring Tools 3.9.14 RELEASE
```
 현재 진행중이 서비스가 regacy spring을 사용하고 있으므로 Spring 3.1.1을 쓰도록 한다. <br>
 사실 Spring 3 버전은 크게 어려울 것 없다. 하지만... Spring Security가 지옥문을 열었다. <br>
 10년 전의 블로그를 찾아 헤메는 고고학자가 된 느낌이었다. 

## POM.XML
```
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/maven-v4_0_0.xsd">
	<modelVersion>4.0.0</modelVersion>
	<groupId>com.springmvc</groupId>
	<artifactId>miniboard</artifactId>
	<name>spring-project</name>
	<packaging>war</packaging>
	<version>1.0.0-BUILD-SNAPSHOT</version>
	<properties>
		<java-version>11</java-version>
		<org.springframework-version>3.1.1.RELEASE</org.springframework-version>
		<org.aspectj-version>1.6.10</org.aspectj-version>
		<org.slf4j-version>1.6.6</org.slf4j-version>
		<commons-fileupload-version>1.4</commons-fileupload-version>
		<commons.io-version>2.11.0</commons.io-version>
	</properties>
	<dependencies>
		<!-- Spring -->
		<dependency>
			<groupId>org.springframework</groupId>
			<artifactId>spring-context</artifactId>
			<version>${org.springframework-version}</version>
			<exclusions>
				<!-- Exclude Commons Logging in favor of SLF4j -->
				<exclusion>
					<groupId>commons-logging</groupId>
					<artifactId>commons-logging</artifactId>
				 </exclusion>
			</exclusions>
		</dependency>
		<dependency>
			<groupId>org.springframework</groupId>
			<artifactId>spring-webmvc</artifactId>
			<version>${org.springframework-version}</version>
		</dependency>
				
		<!-- AspectJ -->
		<dependency>
			<groupId>org.aspectj</groupId>
			<artifactId>aspectjrt</artifactId>
			<version>${org.aspectj-version}</version>
		</dependency>	
		
		<!-- Logging -->
		<dependency>
			<groupId>org.slf4j</groupId>
			<artifactId>slf4j-api</artifactId>
			<version>${org.slf4j-version}</version>
		</dependency>
		<dependency>
			<groupId>org.slf4j</groupId>
			<artifactId>jcl-over-slf4j</artifactId>
			<version>${org.slf4j-version}</version>
			<scope>runtime</scope>
		</dependency>
		<dependency>
			<groupId>org.slf4j</groupId>
			<artifactId>slf4j-log4j12</artifactId>
			<version>${org.slf4j-version}</version>
			<scope>runtime</scope>
		</dependency>
		<dependency>
			<groupId>log4j</groupId>
			<artifactId>log4j</artifactId>
			<version>1.2.15</version>
			<exclusions>
				<exclusion>
					<groupId>javax.mail</groupId>
					<artifactId>mail</artifactId>
				</exclusion>
				<exclusion>
					<groupId>javax.jms</groupId>
					<artifactId>jms</artifactId>
				</exclusion>
				<exclusion>
					<groupId>com.sun.jdmk</groupId>
					<artifactId>jmxtools</artifactId>
				</exclusion>
				<exclusion>
					<groupId>com.sun.jmx</groupId>
					<artifactId>jmxri</artifactId>
				</exclusion>
			</exclusions>
			<scope>runtime</scope>
		</dependency>

		<!-- @Inject -->
		<dependency>
			<groupId>javax.inject</groupId>
			<artifactId>javax.inject</artifactId>
			<version>1</version>
		</dependency>
				
		<!-- Servlet -->
		<dependency>
			<groupId>javax.servlet</groupId>
			<artifactId>servlet-api</artifactId>
			<version>2.5</version>
			<scope>provided</scope>
		</dependency>
		<dependency>
			<groupId>javax.servlet.jsp</groupId>
			<artifactId>jsp-api</artifactId>
			<version>2.1</version>
			<scope>provided</scope>
		</dependency>
		<dependency>
			<groupId>javax.servlet</groupId>
			<artifactId>jstl</artifactId>
			<version>1.2</version>
		</dependency>
	
		<!-- Test -->
		<dependency>
			<groupId>junit</groupId>
			<artifactId>junit</artifactId>
			<version>4.7</version>
			<scope>test</scope>
		</dependency>        
		

		<!-- security -->
		<dependency>
		    <groupId>org.springframework.security</groupId>
    		<artifactId>spring-security-web</artifactId>
    		<version>3.1.7.RELEASE</version>
		</dependency>
		<dependency>
    		<groupId>org.springframework.security</groupId>
    		<artifactId>spring-security-config</artifactId>
    		<version>3.1.7.RELEASE</version>
		</dependency>
		<dependency>
		    <groupId>org.springframework.security</groupId>
    		<artifactId>spring-security-taglibs</artifactId>
    		<version>3.1.7.RELEASE</version>
		</dependency>
		
		
		<!-- CGLib -->
		<dependency>
     		<groupId>cglib</groupId>
     		<artifactId>cglib</artifactId>
     		<version>3.1</version>
    		 <type>jar</type>
     		<scope>compile</scope>
		</dependency>
		
		
		<!-- File Upload -->
		<dependency>
			<groupId>commons-fileupload</groupId>
			<artifactId>commons-fileupload</artifactId>
			<version>${commons-fileupload-version}</version>
		</dependency>
		<dependency>
			<groupId>commons-io</groupId>
			<artifactId>commons-io</artifactId>
			<version>${commons.io-version}</version>
		</dependency>
		
		<!--  mysql -->
		<dependency>
			<groupId>org.springframework</groupId>
			<artifactId>spring-jdbc</artifactId>
			<version>${org.springframework-version}</version>
		</dependency>
		<dependency>
			<groupId>org.apache.commons</groupId>
			<artifactId>commons-dbcp2</artifactId>
			<version>2.5.0</version>
		</dependency>
		<dependency>
			<groupId>mysql</groupId>
			<artifactId>mysql-connector-java</artifactId>
			<version>8.0.24</version>
		</dependency>
		
    	<!--  junit -->
    	<dependency>
        	<groupId>junit</groupId>
        	<artifactId>junit</artifactId>
        	<version>4.12</version> <!-- 또는 4.13.2 등 최신 버전으로 수정 -->
    	</dependency>
		
		<dependency>
        	<groupId>org.springframework</groupId>
        	<artifactId>spring-test</artifactId>
        	<version>3.1.1.RELEASE</version> <!-- Replace with your Spring version -->


    </dependency>
			
		
	</dependencies>
    <build>
        <plugins>
            <plugin>
                <artifactId>maven-eclipse-plugin</artifactId>
                <version>2.9</version>
                <configuration>
                    <additionalProjectnatures>
                        <projectnature>org.springframework.ide.eclipse.core.springnature</projectnature>
                    </additionalProjectnatures>
                    <additionalBuildcommands>
                        <buildcommand>org.springframework.ide.eclipse.core.springbuilder</buildcommand>
                    </additionalBuildcommands>
                    <downloadSources>true</downloadSources>
                    <downloadJavadocs>true</downloadJavadocs>
                </configuration>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>2.5.1</version>
                <configuration>
                    <source>1.6</source>
                    <target>1.6</target>
                    <compilerArgument>-Xlint:all</compilerArgument>
                    <showWarnings>true</showWarnings>
                    <showDeprecation>true</showDeprecation>
                </configuration>
            </plugin>
            <plugin>
                <groupId>org.codehaus.mojo</groupId>
                <artifactId>exec-maven-plugin</artifactId>
                <version>1.2.1</version>
                <configuration>
                    <mainClass>org.test.int1.Main</mainClass>
                </configuration>
            </plugin>
        </plugins>
    </build>
</project>

```

## git 설치
```
sudo apt update
sudo apt install git
```

## tomcat 설치
```
sudo apt-get update
sudo apt-get install tomcat9
sudo systemctl enable tomcat9   // 시스템 부팅시 자동 실행
sudo systemctl start tomcat9
```

## war 파일 배포
```
cd /var/lib/tomcat9/webapps
sudo git clone https://github.com/hanhunh89/spring-miniBoard ./my
cd my
sudo mv ./miniboard.war ../miniboard.war
cd ..
sudo rm -rf my
```

## tomcat 재시작
```
sudo service tomcat9 restart
```

## DB(mariaDB) 설치
```
sudo apt install mariadb-server
```

## DB user 및 table 생성
```
sudo mysql -u root  // db 접속
CREATE DATABASE myDB;   // myDB database 생성
USE myDB;		// database 사용

CREATE TABLE post (      //post table 생성
    postId INT AUTO_INCREMENT PRIMARY KEY,
    title VARCHAR(30),
    content TEXT,
    view INT DEFAULT 0,
    writer VARCHAR(30),
    imageName VARCHAR(50)
);

CREATE TABLE user (    // user table 생성
    userId VARCHAR(50) NOT NULL PRIMARY KEY,
    password VARCHAR(100) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    auth VARCHAR(20) DEFAULT 'ROLE_USER'
);


CREATE USER 'myuser'@'localhost' IDENTIFIED BY '1234';  //myuser 계정 생성

GRANT ALL PRIVILEGES ON myDB.* TO 'myuser'@'localhost' WITH GRANT OPTION;  //myuser에 권한 부여

FLUSH PRIVILEGES;   // 적용

```

## spring security 설정 변경
security-context.xml과 servlet-context.xml의 db정보를 변경한다. 
```
sudo nano /var/lib/tomcat9/webapps/miniboard/WEB-INF/spring/security-context.xml

        <!--  mysql -->
        <beans:bean id="dataSource" class="org.springframework.jdbc.datasource.DriverManagerDataSource">
                <beans:property name="driverClassName" value="com.mysql.cj.jdbc.Driver"/>
		<!-- database name을 myDB로 변경 -->
                <beans:property name="url" value="jdbc:mysql://localhost:3306/myDB?serverTimezone=UTC"/>
		<!-- username을 myuser로 변경 -->
                <beans:property name="username" value="myuser"/>
                <beans:property name="password" value="1234"/>
        </beans:bean>

        <beans:bean id="jdbcTemplate" class="org.springframework.jdbc.core.JdbcTemplate">
                <beans:property name="dataSource" ref="dataSource"/>
        </beans:bean>

sudo nano /var/lib/tomcat9/webapps/miniboard/WEB-INF/spring/appServlet/servlet-context.xml
        <!--  mysql -->
        <beans:bean id="dataSource" class="org.springframework.jdbc.datasource.DriverManagerDataSource">
                <beans:property name="driverClassName" value="com.mysql.cj.jdbc.Driver"/>
		<!-- database name을 myDB로 변경 -->
                <beans:property name="url" value="jdbc:mysql://localhost:3306/myDB?serverTimezone=UTC"/>
		<!-- username을 myuser로 변경 -->
                <beans:property name="username" value="myuser"/>
                <beans:property name="password" value="1234"/>
        </beans:bean>

        <beans:bean id="jdbcTemplate" class="org.springframework.jdbc.core.JdbcTemplate">
                <beans:property name="dataSource" ref="dataSource"/>
        </beans:bean>
```

## tomcat 재시작
```
sudo service tomcat9 restart
```


# 끗
이제 http://serverIp:8080/miniboard/ 로 접속하면 miniborad 사용 가능합니다.

이어서 apache를 이용하여 tomcat을 이중화하겠습니다. 
