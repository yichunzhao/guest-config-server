
# Spring cloud config-server

In order to externalize the microservice configuration, the config server provides a control place to store all property files for all the microservices. Instead of holding 
the property by the service itself, the service asks the config server to get back the property file.

After committing property files to a git repository, the config server will keep observing its changes. 
Once it finds a new change on the property files, and then it will inform those config clients.

# Setup cloud config-server

* @EnableConfigServer
* Adding spring-could-config-server dependency
* Define server port number
* Input git url pointing to the property file location 
* Set git.force-pull to be true, making sure to refresh config server when making a change.  
