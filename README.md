vaadin-multimodule-wildfly
==============

Template for a full-blown Vaadin application that only requires a Servlet 3.0 container to run (no other JEE dependencies).

In addition to the default Vaadin template, this also has preconfigured the wildfly maven plugin.

To get it running do:
1. Download Wildfly to your machine and install to a folder
1. Point the jbossHome configuration in vaadin-multimodule-wildfly-ui/pom.xml to the folder of your Wildfly.
1. In vaadin-multimodule-wildfly-ui project run 'mvn package wildfly:run -DskipTests=true' to get
it running quickly and your application deployed.
1. Browse to http://localhost:8080/vaadin-multimodule-wildfly

Project Structure
=================

The project consists of the following three modules:

- parent project: common metadata and configuration
- vaadin-multimodule-wildfly-addon: addon module, custom server and client side code
- vaadin-multimodule-wildfly-ui: main application module
- vaadin-multimodule-wildfly-backend: backend module, contains any server side java code and dependencies

Workflow
========

To compile the entire project, run "mvn install" in the parent project.

Other basic workflow steps:

- getting started
- compiling the whole project
  - run "mvn install" in parent project
- developing the application
  - edit code in the ui module
  - run "mvn jetty:run" in ui module
  - open http://localhost:8080/
- adding add-ons to the project
  - edit POM in ui module, add add-ons as dependencies
- client side changes
  - edit code in addon module
  - run "mvn install" in addon module
  - if a new add-on has an embedded theme, run "mvn vaadin:update-theme" in the ui module
- debugging client side code
  - run "mvn vaadin:run-codeserver" in ui module
  - activate Super Dev Mode in the debug window of the application
- enabling production mode
  - set vaadin.productionMode=true system property in the production server

Developing a theme using the runtime compiler
-------------------------

When developing the theme, Vaadin can be configured to compile the SASS based
theme at runtime in the server. This way you can just modify the scss files in
your IDE and reload the browser to see changes.

To use on the runtime compilation, open pom.xml of your UI project and comment
out the compile-theme goal from vaadin-maven-plugin configuration. To remove
an existing pre-compiled theme, remove the styles.css file in the theme directory.

When using the runtime compiler, running the application in the "run" mode
(rather than in "debug" mode) can speed up consecutive theme compilations
significantly.

The production module always automatically precompiles the theme for the production WAR.

Using Vaadin pre-releases
-------------------------

If Vaadin pre-releases are not enabled by default, use the Maven parameter
"-P vaadin-prerelease" or change the activation default value of the profile in pom.xml .
