Spring cloud is a framework for building cloud applications.
Spring cloud config-server facilitates the     

## Spring cloud config-server

In order to externalize the microservice configuration, the config server provides a control place to store all property
files for all the microservices. Instead of holding the property file by the service itself, the service asks the 
config server to get it.

After committing property files to a git repository, the config server will keep observing its changes. 
Once it finds a new change on the property files, and then it will inform those config clients.

## Setup cloud config-server

*@EnableConfigServer* 

at the application main class, designating this application as a Config server.

*Adding spring-could-config-server dependency in the pom*
````
		<dependency>
			<groupId>org.springframework.cloud</groupId>
			<artifactId>spring-cloud-config-server</artifactId>
		</dependency>
````

Adding Spring cloud dependency management.
````
	<properties>
		<java.version>1.8</java.version>
		<spring-cloud.version>Hoxton.SR6</spring-cloud.version>
	</properties>

	<dependencyManagement>
		<dependencies>
			<dependency>
				<groupId>org.springframework.cloud</groupId>
				<artifactId>spring-cloud-dependencies</artifactId>
				<version>${spring-cloud.version}</version>
				<type>pom</type>
				<scope>import</scope>
			</dependency>
		</dependencies>
	</dependencyManagement>
````

*Properties*

````
server.port=9000
spring.cloud.config.server.git.uri=${user.home}\\IdeaProjects\\config
spring.cloud.config.server.git.force-pull=true
```` 

*Input git url pointing to the property file location*

storing all property files in the folder git.uri; it is pointing to remote git repository.  

*Set git.force-pull to be true, making sure to refresh config server when making a change*

*Bootstrapping configuration*  

For subsequent servers, we want they may use this config server to manage their properties.  To do that, we need to 
configure each application so that they make know this server and talk back to it. 

It is a bootstrap process, and each application is going to have a file called **bootstrap.properties**.
A parent Spring ApplicationContext loads bootstrap.properties first. This is critical so that config server can start
managing in the properties in application.properties. It is special ApplicationContext that will also decrypt any
encrypted application properties.

For an application that consume the property files stored externally in the config server. 

Bootstrap.properties File 
````
spring.application.name=reservationservices
spring.cloud.config.uri=http://localhost:9000
````  

It uses config server uri to locate the config server, and application name to fetch its own application.properties