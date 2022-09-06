

When you are creating business rules, you sometimes need to perform operations that are not built natively into Corticon. For example, you may need to apply a complex mathematical formula or to retrieve data from an external web service. Corticon provides the ability to add custom extensions for just such purposes.

Extensions are written as custom Java code that you package into one or more JAR files. You simply add extension jar files to your rule project to have them bundled into the EDS file for your Decision Service. This ease of adding extensions makes it easier to develop extensions yourself or to use open source extensions that you download from the Corticon community. By bundling extensions with EDS files, the EDS file becomes self-contained. You can deploy it to a Corticon Server without modifying the server’s classpath. It also allows you to have different Decision Services, or versions of Decisions Services, running that use different versions of an extension.

When developing an extension, it needs to implement one or more Java interfaces that Corticon has defined. The Corticon Extensions API provides for Java annotations to describe the extension, thereby eliminating the need for additional configuration files.

When developing a project in Corticon Studio you can add extensions to your project through the project's Properties dialog box, so that they are available for development and running rule tests. The Package and Deploy wizard in Corticon Studio will include any extensions used by the project into the EDS file it generates or deploys. If you want to script the building of your EDS files, you can also use the Corticon ANT scripts to package extensions into EDS files.

For compatibility with previous releases you can still place extension JAR files on the Corticon classpath so that they are available to all Decision Services.

Extensions can be created in the Java development environment included in Corticon Studio, or you can use another IDE.

There are two types of Corticon extensions:

- [**Extended operators**](extended-operators.md) are used when defining conditions and actions in a Rulesheet. While Corticon has a large built-in set of operators, you can expand this set by adding custom operators. Operators can operate on individual attributes, collections or sequences. For example:
     -    Financial functions, such as net present value, and loan amortization
     -    Statistical functions, such as standard deviation, and permutations
     -  Engineering functions, such as pi, sine, and cosine
  
-  [**Service callouts**](service-callouts.md) can be used in a ruleflow to retrieve, modify, or store data that is being processed by the rules. The most common use is to access data in a database or external web service. For example, if your Ruleflow needs to look up an applicant's credit rating, the service callout can have a step in the Ruleflow processing that calls out to a trusted realtime ratings provider, and then adds the response back into the decision processing.

