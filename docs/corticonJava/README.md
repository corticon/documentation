# Server-Based Decision Services

## Overview

Corticon Server processes the rules modeled, verified and tested in Corticon Studio. Corticon Server is a natural fit for today's deployment architectures, supporting on-premise and cloud deployment, web service deployment in popular application servers, in-process deployment for real-time applications, and application containers.

Corticon Server takes advantage of industry standards to provide flexible options for integration with applications running on [Java ](how-would-you-like-your-corticon-server/java-server/)or .[NET ](how-would-you-like-your-corticon-server/.net-server.md)platforms. You can embed Corticon Server in any layer of an application’s architecture, from the presentation layer on the desktop to the shared-service layer distributed across back-end servers. By design, Corticon Server integrates easily with composite or packaged applications through service-oriented architecture (SOA) or business process management (BPM) systems.

The Corticon Server for Java provides the necessary components to deploy Corticon as a REST or SOAP service on a Java application server or to deploy Corticon in-process in your custom Java application. Corticon Server provides installers for both Windows and Linux. The actual deployment artifacts - the JAR and WAR files - are platform independent. See the Web Services and In-Process guides for more information. See the Corticon 6.2 - Supported Platforms Matrix for a list of supported application servers.

Corticon Server and Web Console install a standard Tomcat distribution to help you quickly get started. This is a standard Tomcat distribution at the time of Corticon release. It may not have the latest security patches or other security configuration changes recommended for production use.When moving to production, it is recommended to deploy Corticon Server and Web Console to a supported application server that you have supplied and secured. If you choose to use the bundled Tomcat in production, you assume responsibility for applying Tomcat security patches and performing security configuration

The Corticon Server for .NET provides the necessary components to deploy Corticon as a REST or SOAP service to Microsoft Internet Information Services (IIS) or to deploy Corticon in-process in your custom .NET application. Corticon Server .NET install is only available on Windows. Corticon uses a high performance bridging technology to call from .NET languages such as C# to Corticon Server. See the Web Services and In-Process guides for more information. See the Corticon 6.2 - Supported Platforms Matrix for a list of supported platforms.

### Invoking Corticon Server

Client applications invoke Corticon Server, sending a data payload as part of a request message.The invocation of Corticon Server can be either indirect (such as when using REST) or direct (such as when making in-process Java calls). This request contains the name of the Corticon Decision Service (the Decision Service Name assigned in the Deployment Descriptor file that should process the payload.) Corticon Server matches the payload to the Decision Service and then commences execution of that Decision Service. One Corticon Server can manage multiple, different Decision Services, each of which might reference a different Vocabulary.

### Working Memory

When a Reactor (an instance of a Decision Service) processes rules, it accesses the data resident in “working memory”. Working memory is populated by any of the following methods:

1. The payload of the Corticon Request- The payload – whether a REST or XML document, or a reference to Java business objects – is inserted into working memory when the client’s request (invocation) is received. When running a Studio Test, the Studio itself is acting as the client, and it inserts the data from the Input Ruletest into working memory.
2. The results of rules- During rule processing, some rules may create new data, modify existing data, or even delete data. These updates are maintained in working memory until the Decision Service completes execution.
3. An external Datasource- If, during the course of rule execution, some data is required that is not already in working memory, then the Reactor asks Corticon Server to query and retrieve it from an external Datasource. For Datasource access to occur, Corticon Server or Studio Tester must be configured correctly and the Vocabulary must be mapped to the datasource's schema.

### Server Properties

The Corticon Server is configured by default to fit the majority of use cases. Recognizing that this configuration may not be optimal for all situations, Corticon provides numerous properties for altering the behavior of Corticon Server. These properties are set via the Corticon brms.properties file in your CORTICON\_WORK directory. When deploying Corticon in-process, you can also set these properties when instantiating a Corticon Server. Where properties are referenced, this guide presents how to set them via brms.properties. See the topic "Properties in context" and Corticon Server API JavaDoc for more information.

### Multi-threaded execution

Multiple Decision Services place their requests in a queue for processing. Server-level thread pooling is implemented by default, using built-in Java concurrent pooling mechanisms to control the number of concurrent executions. This design allows the server to determine how many concurrent requests are to be processed at any one time.

#### Execution queue

Each thread coming into the Server gets an available Reactor from the Decision Service, and then the thread is added to the Server's Execution Thread Pooling Queue, or, simply put, the Execution Queue.The Execution Queue guarantees that threads do not overload the cores of the machine by allowing a specified number of threads in the Execution Queue to start executing, while holding back the other threads. Once an executing thread completes, the next thread in the Execution Queue starts executing.&#x20;

The Server will discover the number of cores on a machine and, by default, limit the number of concurrent executions to that many cores, but a property can be set to specify the number of concurrent executions. Most use cases will not need to set this property. However, if you have multiple applications running on the same machine as Corticon Server, you might want to set this property lower to limit the system resources Corticon uses. While this tactic might slow down Corticon processing when there is a heavy load of incoming threads, it will help ensure Corticon does not monopolize the system. Conversely, if you have Decision Services which make calls to external services (such as connection to a Datasource) you may want to set this property higher so that a core is not idle while a thread is waiting for a response.

#### Memory management

Allocation means that you could allocate hundreds of execution threads for one Decision Service. The way Reactors are maintained in each Decision Service, the Server can re-use cached processing data (not including payload data) across all Reactors for the Decision Service. Runtime performance should reveal only modest differences in memory utilization between a Decision Service that contains just one Reactor and another that contains hundreds of Reactors. Because each Reactor reuses cached processing data, the Server can dynamically create a new Reactor per execution thread (rather than creating Reactors and holding them in memory.) Even when an allocation is set to 100, the Server only creates a new Reactor (with cached data) for every incoming execution thread, up to 100. If there are only 25 execution threads against Decision Service 1, then there are just 25 Reactors in memory. Large request payloads are more of a concern than the number of concurrent executions or the number of Reactors.

#### Related Server Properties

The following Server properties let you adjust Server executions:

* Determines how many concurrent executions can occur across the Server. Ideally, this value is set to the number of Cores on the machine. By default, this value is set to 0, which means the Server will auto-detect the number of Cores on the server.&#x20;

`com.corticon.server.execution.processors.available=0`&#x20;

* This is the timeout setting for how long an execution thread can be inside the Execution Queue. The time starts when the execution thread enters the Execution Queue and ends when it completes executing against a Decision Service. A CcServerTimeoutException will be thrown if the execution thread fails to complete in the allotted time. The value is in milliseconds. Default value is 180000 (180000ms = 3 minutes)&#x20;

`com.corticon.server.execution.queue.timeout=180000`

### Reactor state

A Reactor is an executable instance of a deployed Decision Service. Corticon Server acts as the broker to one or more Reactors for each deployed Decision Service. During Decision Service execution, the Reactor is a stateless component, so all data state must be maintained in the message payloads flowing to and from the Reactor.

If a deployed Ruleflow contains multiple Rulesheets, state is preserved across those Rulesheets as the Rulesheets successively execute within the Ruleflow. However, no interaction with the client application occurs between or within Rulesheets. After the last Rulesheet within the Ruleflow is executed, the results are returned back to the client as a CorticonResponse message. Upon sending the CorticonResponse message, the Reactor is deleted from memory. A new Reactor will be created for the next incoming CorticonRequest. As an integrator, you must keep in mind that there are only two ways for you to retain state upon completion of a Decision Service execution:

1. Receive and process the data from within the CorticonResponse message.
2. Persist the results of a Decision Service execution to an external database. Once a Decision Service execution has completed, the Reactor itself does not remember anything about the data it just processed.

### Server state

Although data state is not maintained by Reactors from transaction-to-transaction, the names and deployment settings of Decision Services deployed to Corticon Server are maintained.The file `ServerState.xml`, located in `[CORTICON_WORK_DIR]{INP|SER}\CcServerSandbox\DoNotDelete`, maintains a record of the Ruleflows and deployment settings currently loaded on Corticon Server for each Decision Service. If Corticon Server inadvertently shuts down, or the container crashes, then this file is read upon restart and the prior Server state is re-established automatically.

#### How to turn off server state persistence

By default, Corticon Server automatically creates and maintains the ServerState.xml document during normal operation, and reads it during restart. This allows it to recover its previous state in the event of an unplanned shutdown (such as a power failure or hardware crash).

&#x20;However, Corticon Server can also operate without the benefit of ServerState.xml, either by not reading it upon restart, or by not creating/maintaining it in the first place. In this mode, an unplanned shutdown and restart results in the loss of any settings made through the Corticon Web Console. For example, any properties settings made, or .eds files deployed using the Console, will be lost. The Server will not auto reload the Decision Services because there is no ServerState.xml; however, from within the Web Console, the Decision Services will be in an undeployed state and can be redeployed from the Web Console.&#x20;

To determine whether Corticon Server will persist its state inside of the ServerState.xml, set the following property in your brms.properties file to true or false. By default this feature is turned on. Default value is true.



`com.corticon.server.serverstate.persistchanges=true`

You can customize Corticon Server's state and restart behavior by combining these two property settings:



| serverstate .persistchanges | serverstate .load | Server Restart Behavior                                                                                                                                                                                                                                                                                    |
| --------------------------- | ----------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `true`                      | `true`            | Corticon Server maintains ServerState.xml during operation, and automatically reads it upon restart to restore to the old state.                                                                                                                                                                           |
| `true`                      | `false`           | <p>Corticon Server maintains ServerState.xml during operation, but does NOT automatically read it upon restart. New Server state upon restart is unaffected by ServerState.xml.</p><p>This allows a system administrator to manually control state restoration from the ServerState.xml, if preferred.</p> |
| `false`                     | `true`            | Corticon Server attempts to read ServerState.xml upon restart, but finds nothing there. No old state restored.                                                                                                                                                                                             |
| `false`                     | `false`           | no ServerState.xml document exists, and Corticon Server does not attempt to read it upon restart. No old state restored.                                                                                                                                                                                   |
# Corticon Server's Web Console

Corticon's Web Console provides a central point for administering and monitoring your Corticon Decision Services, whether in Java or .NET environments. Through the console, you can easily deploy individual Decision Services to one or more Corticon Servers. You can also group related Decision Services into an Application to deploy and manage them as one.

Once deployed, you can easily monitor the performance of the Decision Services and Corticon Servers and view both individual and aggregated metrics. Actions on Decision Services associated with a Server Group are automatically applied to each server member of the group that is running. For example, if you have a Decision Service managed by an Application which is deployed to a Server Group and add another server to the group, the Decision Service will be automatically deployed to the new server. This helps you scale up or scale down the servers in a deployment to meet demand.

The Web Console is a web application that can be installed in the same application server as the Corticon Server for single-server environments or installed separately for multiple-server environments. The choice is yours, depending on the nature of your Corticon deployment. The Web Console maintains configuration information and historical metrics in a local data store. The historical metrics let you see changes in the performance of your Decision Services and Corticon Servers over time.

# Java Environments

The Corticon Server for Java provides the necessary components to deploy Corticon as a REST or SOAP service on a Java application server or to deploy Corticon in-process in your custom Java application. Corticon Server provides installers for both Windows and Linux. The actual deployment artifacts - the JAR and WAR files - are platform independent.

# .NET Environments

The Corticon Server for .NET provides the necessary components to deploy Corticon as a REST or SOAP service to Microsoft Internet Information Services (IIS) or to deploy Corticon in-process in your custom .NET application. Corticon Server .NET install is only available on Windows. Corticon uses a high performance bridging technology to call from .NET languages such as C# to Corticon Server.
