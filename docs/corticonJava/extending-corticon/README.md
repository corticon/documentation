# Extending Corticon

Extensions are written as custom Java code that you package into one or more JAR files. You simply add extension jar files to your rule project to have them bundled into the EDS file for your Decision Service. This ease of adding extensions makes it easier to develop extensions yourself or to use open source extensions that you download from the Corticon community. By bundling extensions with EDS files, the EDS file becomes _self-contained_. You can deploy it to a Corticon Server without modifying the server’s classpath. It also allows you to have different Decision Services, or versions of Decisions Services, running that use different versions of an extension.

When developing an extension, it needs to implement one or more Java interfaces that Corticon has defined. The [Corticon Extensions API](https://documentation.progress.com/output/Corticon/6.2.0/javadoc/Extensions/com/corticon/services/extensions/package-summary.html) provides for Java annotations to describe the extension, thereby eliminating the need for additional configuration files.

When developing a project in Corticon Studio you can add extensions to your project through the project's **Properties** dialog box, so that they are available for development and running rule tests. The **Package and Deploy** wizard in Corticon Studio will include any extensions used by the project into the EDS file it generates or deploys. If you want to script the building of your EDS files, you can also use the Corticon ANT scripts to package extensions into EDS files.

For compatibility with previous releases you can still place extension JAR files on the Corticon classpath so that they are available to all Decision Services.

Extensions can be created in the Java development environment included in Corticon Studio, or you can use another IDE.

There are two types of Corticon extensions: Extended Operators and Service Callouts.&#x20;
