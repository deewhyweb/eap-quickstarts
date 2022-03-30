# EAP Kitchen sink application using external MySQL database.

To run, first start a mysql database using docker-compose

`docker-compose up`

Run wildfly, from the EAP_HOME folder, run:

`./bin/standalone.sh`

Copy the contents of the modules folder to the EAP_HOME/modules folder.

deploy the Kitchen sink application, from the repo location run:


`mvn clean install wildfly:deploy`

Add the driver and datasource, from the EAP_HOME folder, run:


```

jboss-cli.sh

/subsystem=datasources/jdbc-driver=mysql:add(driver-name=mysql,driver-module-name=com.mysql)

data-source add --name=mysql --jndi-name=java:/jdbc/mysql --driver-name=mysql --connection-url=jdbc:mysql://127.0.0.1:3306/books --user-name=root --password=root
```

Test the kitchen sink app at url:  http://127.0.0.1:8080/kitchensink/index.jsf