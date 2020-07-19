# guest-config-server
Spring cloud config-server

#Config Server

In order to externalize the micro service configuration, the config server provides a centrol place to store all property files for all the micro services. Instead of hodling 
the property by the service itself, the service ask the config server to get back the property file.

The property files are commited in a git repository, and the config server observes on its changes. Once it is modified, the configuration can be picked up and broadcasted to clients.

