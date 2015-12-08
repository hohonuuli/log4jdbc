# log4jdbc
A more extensive README will be created soon. For now, you can view the usage instructions at the old Google Code hosting site:

https://code.google.com/p/log4jdbc/

You can download the prebuilt jars at:

https://code.google.com/p/log4jdbc/downloads/list

## Features

- Full support for JDBC 3 and JDBC 4!
- Easy to configure, in most cases all you need to do is change the driver class name to net.sf.log4jdbc.DriverSpy and prepend "jdbc:log4" to your existing jdbc url, set up your logging categories and you're ready to go!
- In the logged output, for prepared statements, the bind arguments are automatically inserted into the SQL output. This greatly Improves readability and debugging for many cases.
- SQL timing information can be generated to help identify how long SQL statements take to run, helping to identify statements that are running too slowly and this data can be post processed with an included tool to produce profiling report data for quickly identifying slow SQL in your application..
- SQL connection number information is generated to help identify connection pooling or threading problems.
- Works with any underlying JDBC driver, with JDK 1.4 and above, and SLF4J 1.x.
- Open source software, licensed under the business friendly Apache 2.0 license: http://www.apache.org/licenses/LICENSE-2.0 

## Usage

This version of _log4jdbc_ is compiled for Java 8

__1. Chose the java logging system you will use.__

In many cases, you already know this, because it is dictated by your existing application. log4jdbc uses the Simple Logging Facade for Java (SLF4J) which is a very simple and very flexible little library that lets you pick among many common java logging systems:

- Log4j
- java.util logging in JDK 1.4
- logback
- Jakarta Commons Logging 

SLF4J is designed to de-couple your application from the java logging system so you can choose any one you want. This is the same goal of Jakarta Commons Logging. However many people have had headaches and issues with classloading problems in complex environments using Jakarta Commons Logging. SLF4J solves these problems with it's much simpler design, and you can even integrate SLF4J to use Jakarta Commons Logging, if you really want to (or are required to) use it. 

[Download the latest official SLF4J release](http://www.slf4j.org/) or include it in your project via Maven, SBT, Gradle, Ivy, etc.

You will need two jars: slf4j-api-1.5.0.jar (or the latest available version) and whichever jar you pick depending on the java logging system you choose. 

Place these two .jar files into your application's classpath. 

Please read the documentation at the [SLF4J website](http://www.slf4j.org/). It's really easy to set up! 


__2. Set your JDBC driver class to net.sf.log4jdbc.DriverSpy in your application's configuration.__

The underlying driver that is being spied on in many cases will be loaded automatically without any additional configuration. 

The log4jdbc "spy" driver will try and load the following popular jdbc drivers: 

|Driver Class|Database Type|
|------------|-------------|
|oracle.jdbc.driver.OracleDriver 	      |Older Oracle Driver|
|oracle.jdbc.OracleDriver 	              |Newer Oracle Driver|
|com.sybase.jdbc2.jdbc.SybDriver 	      |Sybase |
|net.sourceforge.jtds.jdbc.Driver 	      |jTDS SQL Server & Sybase driver|
|com.microsoft.jdbc.sqlserver.SQLServerDriver |Microsoft SQL Server 2000 driver|
|com.microsoft.sqlserver.jdbc.SQLServerDriver |Microsoft SQL Server 2005 driver|
|weblogic.jdbc.sqlserver.SQLServerDriver      |Weblogic SQL Server driver|
|com.informix.jdbc.IfxDriver 	              |Informix |
|org.apache.derby.jdbc.ClientDriver  	      |Apache Derby client/server driver, aka the Java DB|
|org.apache.derby.jdbc.EmbeddedDriver 	      |Apache Derby embedded driver, aka the Java DB|
|com.mysql.jdbc.Driver 	MySQL
|org.postgresql.Driver 	PostgresSQL
|org.hsqldb.jdbcDriver 	HSQLDB pure Java database
|org.h2.Driver 	H2 pure Java database 