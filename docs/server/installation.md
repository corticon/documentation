[Corticon Installation](/assets/corticon_install.htm)

> ![image](/assets/corticon_install_files/server_install_Image_003.png)
> 
>   

> 
> ![image](/assets/corticon_install_files/server_install_Image_004.png)
> 
> # 1‌
> 
> ### Learn about Corticon installations
> 
> ![image](/assets/corticon_install_files/server_install_Image_005.png)
> 
>   
> 
> [This guide presents procedures for accessing, downloading, and running Corticon installers, as well as providing dynamic access to information about](https://documentation.progress.com/output/Corticon/6.3/redirectors/supported-platforms.html) [supported](https://documentation.progress.com/output/Corticon/6.3/redirectors/supported-platforms.html) platforms[. Links to the](https://knowledgebase.progress.com/) [Progress](https://knowledgebase.progress.com/) KnowledgeBase provide additional information about third-party software setup.
> 
> Progress® Corticon® is the Business Rules Management System with the patented rules engine that enables you to automate sophisticated decision processes—without having to write code.
> 
>   
> 
> Progress Corticon products
> 
> Progress Corticon distinguishes its development toolsets from its server deployment environments.
> 
> -   [Corticon](/assets/corticon_install.htm#bookmark36) Studio is the Windows-based development environment for creating and testing business rules. Installed as a standalone application, Corticon Studio provides a complete Eclipse development environment for Corticon in the **Corticon Designer** perspective.
>     
> -   Corticon Servers implement and manage web services and in-process servers for deploying business rules defined in Corticon Studio:
>     
>     -   Corticon Server for Java is supported on various application servers, and client web browsers. After you install it on a supported Windows platform, its deployment artifacts can be redeployed on various UNIX and Linux web service platforms as Corticon Decision Services.
>         
>     -   Corticon Server for .NET facilitates deployment of Corticon Decision Services on Windows .NET Framework and Microsoft Internet Information Services (IIS).
>         
>     -   Corticon Web Console enables administration of multiple remote Corticon Servers. A Web Console server is deployed into an application server, and then is accessed by users through authenticated web browser connections.
>         
>           
>         
>         For details, see the following topics:
>         
> -   [System requirements](/assets/corticon_install.htm#bookmark6)
>     
> -   [Download the latest Corticon installer packages](/assets/corticon_install.htm#bookmark7)
>     
>       
>     
>     #### System requirements‌
>     
>     Progress Corticon products are supported on a variety of platforms and third-party components.
>     
>       
>     
>     Corticon Studio
>     
>     [Refer to the Progress Software web page](https://docs.progress.com/bundle/corticon-supported-platforms/page/Corticon-6.3-Supported-Platforms-Matrix.html) [Corticon Supported Platforms](https://docs.progress.com/bundle/corticon-supported-platforms/page/Corticon-6.3-Supported-Platforms-Matrix.html) Matrix to review the currently supported Corticon Studio operating systems, and Eclipse versions.
>     
>     The target system for a Corticon Studio installation requires:
>     
> -   Supported Windows operating system
>     
> -   8 GB System RAM (minimum of 2 GB available RAM)
>     
> -   650 MB disk space
>     
> -   When an existing Eclipse will be used, a supported Eclipse version
>     
>       
>     
>     Corticon Server for Java
>     
>     [Refer to the Progress Software web page](https://docs.progress.com/bundle/corticon-supported-platforms/page/Corticon-6.3-Supported-Platforms-Matrix.html) [Corticon Supported Platforms](https://docs.progress.com/bundle/corticon-supported-platforms/page/Corticon-6.3-Supported-Platforms-Matrix.html) Matrix [to review the currently supported platforms and application servers. Also see the Corticon KnowledgeBase entry](https://knowledgebase.progress.com/articles/Knowledge/Corticon-Server-6-x-sample-WAR-installation-for-different-Application-Servers) [Corticon Server 6.X sample WAR installation for different Application](https://knowledgebase.progress.com/articles/Knowledge/Corticon-Server-6-x-sample-WAR-installation-for-different-Application-Servers) Servers for detailed instructions on configuring Corticon Server on all supported platforms.
>     
>     The target system for a Corticon Server for Java installation requires:
>     
> -   Supported Windows or Linux operating system
>     
> -   When deploying on other platforms, a supported operating system and application server
>     
> -   8 GB System RAM (minimum of 2 GB available RAM)
>     
> -   600 MB disk space
>     
>       
>     
>     Corticon Server for .NET
>     
>     [Refer to the Progress Software web page](https://docs.progress.com/bundle/corticon-supported-platforms/page/Corticon-6.3-Supported-Platforms-Matrix.html) Corticon Supported Platforms Matrix for information on supported
>     
>     [.NET Framework and IIS versions, and the Corticon Knowledgebase article appropriate for your target IIS/platform, as listed in the topic](/assets/corticon_install.htm#bookmark50) How to set up Corticon .NET Server resources on an IIS server on page 34.
>     
>     The target system for a Corticon Server for .NET installation requires:
>     
>     Download the latest Corticon installer packages
>     
>       
>     
>     ![image](/assets/corticon_install_files/server_install_Image_006.png)
>     
> -   Supported Windows operating system
>     
> -   Supported .NET Framework and Internet Information Service (IIS)
>     
> -   8 GB System RAM (minimum of 2 GB available RAM)
>     
> -   500 MB disk space
>     
>       
>     
>     Corticon Web Console
>     
>     [Refer to the Progress Software web page](https://docs.progress.com/bundle/corticon-supported-platforms/page/Corticon-6.3-Supported-Platforms-Matrix.html) Corticon Supported Platforms Matrix for information on supported browser versions.
>     
>     The target system for a Corticon Web Console installation requires:
>     
> -   Supported Windows or Linux operating system
>     
> -   4 GB System RAM (minimum of 2 GB available RAM)
>     
> -   Java option for MaxPermSize set to at least 256m
>     
> -   600 MB disk space
>     
>       
>     
>     ![image](/assets/corticon_install_files/server_install_Image_007.png)
>     
>     Note: When all three Corticon Server components are installed on one machine, the required space for the installation is about 1 GB.
>     
>       
>     
>     ![image](/assets/corticon_install_files/server_install_Image_008.png)
>     
>       
>     
>     #### Download the latest Corticon installer packages‌
>     
>     Corticon installer packages available in each Progress Corticon release
>     
>     CORTICON STUDIO on supported Windows platforms:
>     
> -   PROGRESS\_CORTICON\_6.3.x\_STUDIO\_WIN\_64.exe
>     
>     CORTICON SERVER AND WEB CONSOLE:
>     
> -   Microsoft Windows—Corticon Server and Web Console products for Windows (Java Server, .NET Server, and Web Console) are packaged in executable installer applications and ZIP archives. For supported
>     
>     Windows machines, download: PROGRESS\_CORTICON\_6.3.x\_SERVER\_WIN\_64.exe
>     
> -   **Zip Archives**—Corticon Server and Web Console .war files are available in a Corticon Server .zip archive, PROGRESS\_CORTICON\_6.3.x\_SERVER.zip. Use it to install the Corticon Server or the Corticon Web Console on a supported application server without using the executable installers.
>     
> -   Linux—Corticon Server and Web Console products for Linux (Java Server, and Web Console) are packaged in executable installer applications for supported Linux machines: PROGRESS\_CORTICON\_6.3.x\_SERVER\_LNX\_64.bin
>     
> -   **Docker**—Corticon Server and Web Console .war files are packaged with their Dockerfile in a .zip archive. Use it to install the Server and Web Console on Docker without using the executable installers. Download: PROGRESS\_CORTICON\_6.3.x\_DOCKER.zip
>     
>     For more information, see "How to deploy Corticon on Docker" in the Corticon Deployment Guide.
>     
>       
>     
>     Perform downloads
>     
>     To download required Corticon installers:
>     
>       
>     
>     1.  Get credentials to access and download packages on the Progress Software Electronic Software Download (ESD) site.
>         
>     2.  Connect to the ESD, log in, and then navigate to the Corticon 6.3.x page.
>         
>     3.  Locate, download, and save the required installers to a temporary location accessible by the target machine.
>         
>     
>       
>     
>     ![image](/assets/corticon_install_files/server_install_Image_009.png)
>     
>     # 2‌
>     
>     ### How to prepare for a Corticon installation
>     
>     ![image](/assets/corticon_install_files/server_install_Image_010.png)
>     
>       
>     
>     Before running installers
>     
>     To avoid possible constraints on the installers, do the following:
>     
> -   Confirm that you have Administrator permissions on the target machine \- Administrator rights allow the installer to copy all the Corticon files to their proper locations. You must have Administrator rights and permissions to install this software. See your system administrator to obtain these rights.
>     
> -   Obtain system access \- Several Corticon features write files to the “home” directory structure. If the target machine for the Corticon installation does not have read and write access to this directory, you need to choose a directory location where Corticon will have both read and write access.
>     
> -   Disable anti-virus, anti-malware, and anti-spyware protection applications \- Before performing the
>     
>     installation, consider temporarily disabling any anti-virus and anti-spyware software that may be running on the target machine, as such software might interfere with correct installation.
>     
> -   Review the supported platforms [\- Refer to the Progress Software web page](https://docs.progress.com/bundle/corticon-supported-platforms/page/Corticon-6.3-Supported-Platforms-Matrix.html) [Corticon Supported Platforms](https://docs.progress.com/bundle/corticon-supported-platforms/page/Corticon-6.3-Supported-Platforms-Matrix.html) Matrix to review the operating system versions for Corticon Server and Corticon Studio and supporting software.
>     
>       
>     
>     For details, see the following topics:
>     
> -   [If](/assets/corticon_install.htm#bookmark13) [you are evaluating Corticon](/assets/corticon_install.htm#bookmark13)‌
>     
> -   [If you are upgrading Corticon](/assets/corticon_install.htm#bookmark14)
>     
>       
>     
>     #### If you are evaluating Corticon
>     
>     You can install Studio and Server, start them, and then get underway. The licensing will sustain you for a while:
>     
>       
>     
> -   Studio Licensing \- Corticon embeds a ninety-day evaluation license that enables development of business rules projects, as well as testing of the projects in an embedded test server. You must obtain Studio development licenses from your Progress representative.
>     
> -   Server Licensing \- Corticon embeds a limited evaluation license that enables testing of rule modeling projects on all supported platform configurations except .NET. You must obtain server deployment licenses and .NET evaluation licenses from your Progress representative. The license included in the default Corticon Server installation has pre-set limits on certain Corticon Server and Decision Service parameters. These
>     
>     limits are:
>     
>     -   **Number of Decision Services** – Up to 20 Decision Services may be deployed at any given time. This means the sum total of all Decision Services loaded via .cdd files, Web Console, or APIs cannot exceed 20.
>         
>     -   Number of Rules – All rules in all deployed Ruleflows (that is, all deployed Decision Services) must not exceed 500. A rule generally consists of a single Condition/Action Column or a single Action row in
>         
>         Column 0. Filter expressions do not count because they only modify other rules.
>         
>           
>         
>         ![image](/assets/corticon_install_files/server_install_Image_011.png)
>         
>         **Note:** The Corticon Server log can capture errors and exceptions caused by expired or under-strength licenses. These log messages are detailed in the _Corticon Server logs section of the Server Guide_.
>         
>           
>         
>         ![image](/assets/corticon_install_files/server_install_Image_012.png)
>         
>         If you are Progress Corticon customer, you should have access to an unlimited license that will lift these restrictions. If you are an evaluator, and discover that these limitations are preventing or inhibiting your
>         
>         [evaluation, contact your Progress Software representative to get a license with expanded capabilities. For information on installing an updated license in Studio or Server, see the related topics in](/assets/corticon_install.htm#bookmark15) [Procedures for](/assets/corticon_install.htm#bookmark15) upgrading Corticon installations on page 12.
>         
>           
>         
>         #### If you are upgrading Corticon‌
>         
>         Existing Corticon users advancing to this release will want to know whether their existing products can co-exist with the newer version, as well as any strategies for perpetuating the assets created in their current version.‌
>         
>         [Read through the](/assets/corticon_install.htm#bookmark15) Procedures for upgrading Corticon installations on page 12 to plan your upgrade processes.
>         
>           
>         
>         Procedures for upgrading Corticon installations
>         
>         To synchronize your files and assets with the updated product, perform the tasks that optimize upgrades of Corticon Studios and Servers. These tasks are a checklist of good practices.
>         
>         If your upgrade is:
>         
> -   A patch, which is a minimal step forward, such as 5.6.0.11 > 5.6.0.12 - Read the patch notes to see if there are tasks to consider.
>     
> -   A service pack, such as 5.7.0 > 5.7.1 – Handle changes in the product even though they might not present problems.
>     
> -   A minor or major release, which can be a big step, such as 5.5.2 > 6.3.0—Review, consider, and perform every one of these tasks.
>     
>     IMPORTANT: Corticon Studio and Corticon Server versions must be consistent throughout your infrastructure.
>     
>       
>     
>     ![image](/assets/corticon_install_files/server_install_Image_013.png)
>     
>     **Note:** Do **not** copy a .war file from an older version installation to a new one.
>     
>       
>     
>     ![image](/assets/corticon_install_files/server_install_Image_014.png)
>     
>       
>     
>     In the order of action:
>     
>     ON STUDIO MACHINES
>     
> -   [Update Studio installations](/assets/corticon_install.htm#bookmark16)
>     
> -   [Update the Studio's brms.properties](/assets/corticon_install.htm#bookmark17)
>     
> -   [Update eclipse.ini and Java](/assets/corticon_install.htm#bookmark18)
>     
> -   [Update the Studio license file](/assets/corticon_install.htm#bookmark19)
>     
> -   [Upgrade assets](/assets/corticon_install.htm#bookmark20)
>     
> -   [Update desktop shortcut](/assets/corticon_install.htm#bookmark21)
>     
> -   [Repackage Decision Services and their Datasource Configuration](/assets/corticon_install.htm#bookmark22) file ON SERVER MACHINES
>     
> -   [Undeploy the old Decision Services](/assets/corticon_install.htm#bookmark23)
>     
> -   [Install Corticon Web Console software](/assets/corticon_install.htm#bookmark24)
>     
> -   [Install Corticon Server software](/assets/corticon_install.htm#bookmark25)
>     
> -   [Update the Server license files](/assets/corticon_install.htm#bookmark26)
>     
> -   [Update the Server's brms.properties](/assets/corticon_install.htm#bookmark27)
>     
> -   [Clear browser caches that use the Corticon Web Console](/assets/corticon_install.htm#bookmark28)
>     
> -   [Deploy regenerated Decision Services](/assets/corticon_install.htm#bookmark29)
>     
> -   [Stop](/assets/corticon_install.htm#bookmark30) [load balancers and start the new Server](/assets/corticon_install.htm#bookmark30)
>     
>       
>     
>     ON STUDIO MACHINES
>     
>       
>     
>     Install Studios
>     
>       
>     
>     ![image](/assets/corticon_install_files/server_install_Image_015.png)
>     
>     Note: You can keep an installed prior version of Studio for 90 days. See your EULA for information about the "Replaced Product."
>     
>       
>     
>     ![image](/assets/corticon_install_files/server_install_Image_016.png)
>     
>     [For the updated product, proceed with](/assets/corticon_install.htm#bookmark36) How to install Corticon Studio on page 19
>     
>       
>     
>     Update the Studio's brms.properties file
>     
>     Compare the brms.properties file that is currently in use. If any property adjustments you made in the past are still valid, copy them into the newer installation's brms.properties file. While a minor release installs
>     
>     into a separate location, a service pack overlays an existing installation and does not touch an existing
>     
>     brms.properties file.
>     
>     For information about the brms.properties[, see](https://docs.progress.com/bundle/corticon-rule-modeling/page/Studio-properties-and-settings.html) ["Studio Properties and settings" in the Rule Modeling](https://docs.progress.com/bundle/corticon-rule-modeling/page/Studio-properties-and-settings.html) Guide and .
>     
>       
>     
>     Update eclipse.ini and Java
>     
>     Some Studio installations benefit from tweaking the eclipse.ini[, often for Studio](https://docs.progress.com/bundle/corticon-install/page/Increase-Corticon-Studio-memory-allocation.html) ["Increase Corticon Studio memory allocation" in the Corticon Installation](https://docs.progress.com/bundle/corticon-install/page/Increase-Corticon-Studio-memory-allocation.html) Guide. If you are pointing to your preferred Java, it might not be optimal.
>     
>       
>     
>     ![image](/assets/corticon_install_files/server_install_Image_017.png)
>     
>     **Note:** Do not copy eclipse.ini from an older release. After you do an install, compare your old file to the new one to determine whether any lines are appropriate to migrate.
>     
>       
>     
>     ![image](/assets/corticon_install_files/server_install_Image_018.png)
>     
>     Update the Studio license file
>     
>     A major release likely requires a new license file while minor releases typically do not. When you are provided a license for Corticon Studio and Server, you receive a JAR file, CcLicense.jar. Save the JAR file named CcLicense.jar, which you receive with the Corticon Studio and Server license, on each target machine. To avoid performance issues, Progress strongly recommends that you do not put your Studio license on a network drive, as that may cause network latency issues in Studio due to the frequent check of this license file when
>     
>     rule assets are edited. In this example, the license file that both Studio and Server use is placed at
>     
>     C:\\licenses.
>     
>     To update a Studio license:
>     
>     1.  Go to **Window > Preferences**, and expand the **Progress Corticon** group.
>         
>     2.  In the **License File** field, enter or browse the location of the license JAR:
>         
>         ![image](/assets/corticon_install_files/server_install_Image_019.jpg)
>         
>     3.  Click **Apply**, and then click **OK**.
>         
>     
>       
>     
>     Upgrade assets
>     
>     In Studio, be sure to upgrade all project assets. While you upgrade file by file or project by project, the best way is to advance all the assets you might work with in the current release. Then, it is a good practice to run any Ruletest or unit tests to see that the behaviors are as expected.
>     
>       
>     
>     ![image](/assets/corticon_install_files/server_install_Image_020.png)
>     
>     Note: If you are using a workspace that was used in a previous installation, you might need to refresh the
>     
>     workspace's links to **Welcome** screen topics. In Studio, click the **Home** button to refresh the **Welcome** links.
>     
>       
>     
>     ![image](/assets/corticon_install_files/server_install_Image_021.png)
>     
>       
>     
>     Update desktop shortcut
>     
>     If you want to run your new Studio version in a different language, make changes to your desktop shortcut. In essence you are modifying the desktop shortcut to append \-nl and the preferred language to the target, for example, \-nl ja. For details and examples, see _"Set Studio to run in another language" in the Install Guide_
>     
>       
>     
>     Repackage Decision Services and their Datasource Configuration file
>     
>     Use any of the several techniques in Studio to package projects as Decision Services. Then, stage them for deployment on the new Server installations, together with a freshly generated Datasource Configuration file.
>     
>     ON SERVER MACHINES
>     
>       
>     
>     Undeploy old Decision Services
>     
>     Undeploy every EDS on the target Servers.
>     
>       
>     
>     Install Corticon Web Console software
>     
>     Run the Server download, and choose only Corticon Web Console if you want it to run its corticon.war on a machine that does not collocate with a Corticon Server's axis.war.
>     
>     [After you install servers, you can have the servers register automatically when you install the Corticon Web Console. The properties and instructions you will see](/assets/corticon_install.htm#bookmark27) Update the Server's brms.properties.
>     
>       
>     
>     Install Corticon Servers
>     
>       
>     
>     ![image](/assets/corticon_install_files/server_install_Image_022.png)
>     
>     Note: If you are using load balancers to carry the load during upgrade, take one of its peers offline, and then stop it.
>     
>       
>     
>     ![image](/assets/corticon_install_files/server_install_Image_023.png)
>     
> -   Default Tomcat server—When you install Corticon Server or Corticon Web Console, a Tomcat server is installed that is ready to use.
>     
> -   **.NET server**—The Corticon Server installer option for .NET provides the install.bat script that will setup the axis application on the .NET IIS server. You can edit a copy of install.bat to provide a preferred name for the application or for an additional server.
>     
>     -   Before running the script, it is recommended that you backup and delete the axis directory under c:/inetpub/wwwroot. Alternately, you could use IIS Manager and right-click on the existing axis application, and then choose **Remove** to delete the application files from the IIS server.
>         
>     -   After installation, immediately replace the CcLicense.jar on the IIS server with your authorized .NET license file, otherwise the Corticon .NET server will not run.
>         
>     -   [If the IIS Server does not restart, the classic application pool stops running, and no logs are generated, then it is likely that you did not have adequate write permissions in related folders. For more information, see the Knowledge Base entry](https://knowledgebase.progress.com/articles/Article/Corticon-Server-for-NET-does-not-start) Corticon Server for .NET does not start.
>         
>         [For more information on Corticon .NET server installation as well .NET deployment security, see](https://docs.progress.com/bundle/corticon-web-services/page/Web-services-on-.NET.html) ["Web](https://docs.progress.com/bundle/corticon-web-services/page/Web-services-on-.NET.html) services on .NET" in the Corticon Web Services Guide.
>         
> -   **Other application servers**—The Corticon Server .war files can be downloaded in the PROGRESS\_CORTICON\_6.3.x\_SERVER.zip package. The axis.war or corticon.war file is deployed to the typical deployment directory of the application server. For example:
>     
>     -   For downloaded Tomcat: \[TOMCAT\_HOME\]\\webapps
>         
>     -   For the default Tomcat in the Corticon installer: \[CORTICON\_HOME\]\\Server\\tomcat\\webapps.
>         
>           
>         
>         ![image](/assets/corticon_install_files/server_install_Image_024.png)
>         
>         Note: [To review the currently supported UNIX/Linux platforms and brands of application servers, refer to](https://docs.progress.com/bundle/corticon-supported-platforms/page/Corticon-6.3-Supported-Platforms-Matrix.html) [Corticon Supported Platforms](https://docs.progress.com/bundle/corticon-supported-platforms/page/Corticon-6.3-Supported-Platforms-Matrix.html) Matrix [For detailed instructions on configuring Corticon Server on all supported platforms, see the Corticon KnowledgeBase entry](https://knowledgebase.progress.com/articles/Knowledge/Corticon-Server-6-x-sample-WAR-installation-for-different-Application-Servers) [Corticon Server WAR installation for different Application](https://knowledgebase.progress.com/articles/Knowledge/Corticon-Server-6-x-sample-WAR-installation-for-different-Application-Servers) Servers .
>         
>           
>         
>         ![image](/assets/corticon_install_files/server_install_Image_025.png)
>         
>           
>         
>         Update Server licenses
>         
>         The Server requires you to copy the CcLicense.jar file and then paste it to replace the existing file, as follows:
>         
> -   Java Server license:
>     
>     -   \[CORTICON\_HOME\]\\Server\\lib\\—used by sample applications and Corticon Management Utility.
>         
>     -   \[CORTICON\_HOME\]\\Server\\tomcat\\webapps\\axis\\WEB-INF\\lib[—deployed to the runtime Server. If you are managing a default Java Server from the Corticon Web Console, you can perform this task by referring to](https://docs.progress.com/bundle/corticon-web-console/page/Edit-Server-groups-and-Servers.html) ["Edit Server groups and Servers" in the Corticon Web Console Guide](https://docs.progress.com/bundle/corticon-web-console/page/Edit-Server-groups-and-Servers.html)
>         
>     -   When you install from the .war file for deployment onto other supported platforms and application servers, place the license file adjacent to the Corticon JARs.
>         
>           
>         
> -   .NET Server license :
>     
>       
>     
>     ![image](/assets/corticon_install_files/server_install_Image_026.png)
>     
>     Note: [You must have a license enabling .NET Server to work with Corticon. See](https://knowledgebase.progress.com/articles/Article/Corticon-6-0-licensing) [Knowledge Base article:](https://knowledgebase.progress.com/articles/Article/Corticon-6-0-licensing) [Corticon 6 licensing](https://knowledgebase.progress.com/articles/Article/Corticon-6-0-licensing)
>     
>       
>     
>     ![image](/assets/corticon_install_files/server_install_Image_027.png)
>     
>     -   \[CORTICON\_HOME\]\\Server .NET\\ThirdParty\\lib\\—propagated to the IIS location by the install utility.
>         
>     -   C:\\inetpub\\wwwroot\\axis\\lib\\—deployed at this typical IIS location. If you are managing a .NET Server from the Corticon Web Console, you can perform this task by referring to "Edit Server groups and Servers" in the Corticon Web Console Guide.
>         
>           
>         
>         Update the Server's brms.properties
>         
>         As with Studio, compare and update and tune the brms.properties files on each Java and .NET Server, considering that many properties are effective only on Servers. For more information see, _"Server properties and settings" in the Server Guide_
>         
>           
>         
>         ![image](/assets/corticon_install_files/server_install_Image_028.png)
>         
>         **Note:** On .NET Servers, you can copy the brms.properties file from the Corticon Server root, paste it adjacent to axis in the IIS location, and thereafter apply updates to it.
>         
>           
>         
>         ![image](/assets/corticon_install_files/server_install_Image_029.png)
>         
>         **Corticon Server registration in Corticon Web Console**—When new servers want to be managed in the Web Console, you can add properties to the server's brms.properties file that will connect and authenticate on the Web Console, and even put the server into a specified group so that the server automatically gets decision services deployed in the group. For details, see _"Server registration with Web Console" in the Server Guide_
>         
>           
>         
>         Clear browser caches that use the Corticon Web Console
>         
>         For administrators who use the Corticon Web Console, clear the browser caches.
>         
>           
>         
>         For .NET Servers:
>         
> -   **Install on IIS** \- Run install.bat to refresh the IIS Server libraries and samples. Enter **Y** as the answer for all the overwrite choices, and then restart the IIS Server.
>     
>       
>     
>     ![image](/assets/corticon_install_files/server_install_Image_030.png)
>     
>     Note: [If the IIS Server does not restart, the classic application pool stops running, and no logs are generated, then it is likely that the user performing the upgrade did not have adequate write permissions in related folders. For more information, see the Knowledge Base entry](https://knowledgebase.progress.com/articles/Article/Corticon-Server-for-NET-does-not-start) Corticon Server for .NET does not start.
>     
>       
>     
>     ![image](/assets/corticon_install_files/server_install_Image_031.png)
>     
>     Deploy the fresh Decision Services
>     
>     Deploy the newly created Decision Services to the new Server. When using CDDs, be aware that you might have two types of data access configuration files. The legacy format used a .properties file while new format is a datasources.xml file.
>     
> -   Where you have a legacy .properties file with EDC, use CDD Property :
>     
>     PROPERTY\_DATABASE\_ACCESS\_PROPERTIES\_PATH
>     
>       
>     
> -   Where you are have a new style .xml file, use CDD Property :
>     
>     PROPERTY\_DATASOURCE\_CONFIG\_FILE\_PATH
>     
>       
>     
>     Stop load balancers and start the new Server
>     
>     Use Corticon Web Console (or other techniques) to deploy the upgraded EDS files and license to the new Server. Bring the other load balancers down, and then expose the upgraded Server to carry the load. Uninstall old Servers, and then upgrade and provision to be peers.
>     
>       
>     
>     ![image](/assets/corticon_install_files/server_install_Image_032.png)
>     
>     # 3‌
>     
>     ### How to install Corticon Studio
>     
>     ![image](/assets/corticon_install_files/server_install_Image_033.png)
>     
>       
>     
>     There are several techniques for installing Corticon Studio:
>     
> -   Run the Corticon Studio installer wizard on page 20, the typical use, which enables a complete Corticon Studio Eclipse installation that can standalone, or be tailored into another Eclipse IDE on the same machine.
>     
> -   Perform silent installations of Studio on page 23 that generates a file from an installer wizard run to let you perform silent Studio installations on other machines.
>     
>       
>     
>     What Corticon Studio installers provide
>     
>     The installer wizard package includes:
>     
> -   Corticon Studio resources
>     
> -   Eclipse Development Environment and Eclipse online documentation.
>     
> -   Java Runtime Environment (JRE)
>     
> -   Sample projects
>     
> -   API documentation for extending Corticon
>     
> -   Corticon Server runtime for use in testing rules you create in Corticon Studio
>     
>       
>     
>     For details, see the following topics:
>     
> -   [Run the Corticon Studio installer wizard](/assets/corticon_install.htm#bookmark37)
>     
> -   [Perform silent installations of Studio](/assets/corticon_install.htm#bookmark38)
>     
> -   [Increase Corticon Studio memory allocation](/assets/corticon_install.htm#bookmark39)
>     
> -   [Set Studio to run in another language](/assets/corticon_install.htm#bookmark40)
>     
>       
>     
>     #### Run the Corticon Studio installer wizard‌
>     
>     The Studio installer will install or update Studio 6.3.
>     
>       
>     
>     Installing or updating Studio 6.3
>     
>     To perform an update installation of Corticon Studio 6.3 to the latest release (x) :
>     
>     1.  Double click on the installer file, PROGRESS\_CORTICON\_6.3.x\_STUDIO\_WIN\_64.exe, to launch the Corticon Studio installer.
>         
>           
>         
>         ![image](/assets/corticon_install_files/server_install_Image_034.png)
>         
>         Note: While not typically required, if you are told to do an administrator install, right-click on the EXE file, and then choose Run as administrator.
>         
>           
>         
>         ![image](/assets/corticon_install_files/server_install_Image_035.png)
>         
>         The installer opens in the installer wizard.
>         
>     2.  The first installer panel opens with information about the installer.
>         
>           
>         
>         ![image](/assets/corticon_install_files/server_install_Image_036.jpg)
>         
>           
>         
>         ![image](/assets/corticon_install_files/server_install_Image_037.png)
>         
>         Note: If the same or higher Corticon Studio 6.3.x is installed at any location on the target machine, an alert is posted that denies permission to continue. You will be able to apply 6.3 Studio service packs and patches. You can have other versions of Corticon Studio installed in distinct folders and they can run concurrently, although they must keep their workspaces separate.
>         
>           
>         
>         ![image](/assets/corticon_install_files/server_install_Image_038.png)
>         
>           
>         
>     3.  Click **Next** to continue.
>         
>         The **License Agreement** panel opens.
>         
>           
>         
>         ![image](/assets/corticon_install_files/server_install_Image_039.jpg)
>         
>           
>         
>         This panel displays the Progress Software End User License Agreement (EULA). Use the scroll bar at the right of the screen to read the agreement content.
>         
>     4.  When you understand and agree to the terms, choose **I accept the terms in the license agreement**, and then click **Next** to continue.
>         
>         The **Choose Install Folder** panel opens.
>         
>           
>         
>         ![image](/assets/corticon_install_files/server_install_Image_040.jpg)
>         
>           
>         
>           
>         
>     5.  Specify the installation location. The default location for the installation directory and the work directory are as shown above. (For the work directory, the default subdirectory under Users is the current username.) Either accept the default locations, or specify each preferred (and different) location.
>         
>     6.  Click **Next**.
>         
>     7.  The **Pre-installation Summary** panel opens.
>         
>           
>         
>         ![image](/assets/corticon_install_files/server_install_Image_041.jpg)
>         
>           
>         
>         Confirm that your installation location has adequate disk space for the Corticon Studio components as well as at least 100 MB of workspace.
>         
>     8.  Click **Install** to continue.
>         
>         An installation status window opens to display the state of the installation process. When the process has finished, the **Install Complete** panel opens.
>         
>     9.  Click **Done** to quit and close the installer.
>         
>     
>     The installation or update of Corticon Studio 6.3.x is complete.‌
>     
>       
>     
>     #### Perform silent installations of Studio
>     
>     An unattended (silent) install requires that you first run an installation or updater in the installer wizard to capture the selected options, and then use the captured response file on other targets to 'playback' the responses into the installer without any user interaction.
>     
>     To perform silent installations for Corticon Studio:
>     
>     1.  Run the Studio installer with your preferred locations and options to capture a response file, using the syntax installer.exe **\-r** file where installer is the preferred Studio installer, and file is the response file you will reuse. For example, PROGRESS\_CORTICON\_6.3.x\_STUDIO\_WIN\_64.exe -r C:\\CorticonStudio64\_63x.responses
>         
>     2.  On other target machines, access the Studio 6.3 installer executable and the response file.
>         
>     3.  On those machines, run the installer using the syntax installer.exe \-i silent -f file where installer is the Studio installer, and file is your response file. For example, PROGRESS\_CORTICON\_6.3.x\_STUDIO\_WIN\_64.exe -i silent -f C:\\CorticonStudio64\_63x.responses.
>         
>     
>       
>     
>     #### Increase Corticon Studio memory allocation‌
>     
>     When working on large Rule Projects, you will get better performance by increasing the amount of memory available to Corticon Studio.
>     
>     To change Corticon Studio memory allocation after installation, do the following:
>     
>     1.  Edit the command file eclipse.ini located at \[CORTICON\_HOME\]\\Studio\\eclipse
>         
>     2.  Change (typically, increase) the Xmx value (maximum memory setting). The default Xmx setting is 2 gigabyte, specified as Xmx2g. Often, that is increased to 4g when appropriate memory is available.
>         
>     
>       
>     
>     #### Set Studio to run in another language‌
>     
>     You can specify a preferred language for Corticon Studio. The options are:
>     
> -   English (en \- default)
>     
> -   French (fr)
>     
> -   Japanese (ja)
>     
> -   Portuguese (Brazilian) (pt\_BR)
>     
> -   Spanish (es)
>     
>     To set Corticon Studio to start in your preferred language:
>     
>     1.  On Windows, right-click on the **Start** menu item for **Corticon Studio**, and then choose **More > Open file location**.
>         
>     2.  Right-click on the shortcut **Corticon Studio**, and then choose **Properties**.
>         
>     3.  Choose the **Shortcut** tab, and then add to the **Target** value with the language option, \-nl followed by a language value, as shown setting ja for Japanese:
>         
>           
>         
>         ![image](/assets/corticon_install_files/server_install_Image_042.jpg)
>         
>           
>         
>     4.  Click **Apply**, and then **OK** to set the change.
>         
>     
>     When you start Corticon Studio its labels are in Japanese, as illustrated:
>     
>       
>     
>     ![image](/assets/corticon_install_files/server_install_Image_043.jpg)
>     
>       
>     
>     ![image](/assets/corticon_install_files/server_install_Image_044.png)
>     
>     Note: A preferred user language might use different separator symbols than those documented for decimal values, list ranges, and dates.
>     
>       
>     
>     ![image](/assets/corticon_install_files/server_install_Image_045.png)
>     
>       
>     
>     ![image](/assets/corticon_install_files/server_install_Image_046.png)
>     
>     # 4‌
>     
>     ### How to install Corticon Servers and Web Console
>     
>     ![image](/assets/corticon_install_files/server_install_Image_047.png)
>     
>       
>     
>     This section provides information about the installation procedures for the deployment and administration components of Corticon Server as well as the web application server, Apache Tomcat, that is used by the Java Server and the Web Console.
>     
>       
>     
>     ![image](/assets/corticon_install_files/server_install_Image_048.png)
>     
>     Note: IMPORTANT: Default application server—Corticon Server and Web Console install a standard Tomcat distribution to help you quickly get started. This is a standard Tomcat distribution at the time of Corticon release. It may not have the latest security patches or other security configuration changes recommended for production use. When moving to production, it is recommended to deploy Corticon Server and Web Console to a supported application server that you have supplied and secured. If you choose to use the bundled Tomcat in production, you assume responsibility for applying Tomcat security patches and performing security configuration.
>     
>       
>     
>     ![image](/assets/corticon_install_files/server_install_Image_049.png)
>     
>       
>     
>     ![image](/assets/corticon_install_files/server_install_Image_050.png)
>     
>     **Note: Linux Installation**—When you download and run the Linux server installer, you get shell (.sh) scripts for start/stop and utility tools that correspond to the batch (.bat) scripts in a Windows installation.
>     
>       
>     
>     ![image](/assets/corticon_install_files/server_install_Image_051.png)
>     
>     There are several techniques for installing Corticon Server components:
>     
> -   Run the Server and Web Console installer wizard on page 28, the typical use, which enables a complete Corticon Server for Java, Corticon Server for .NET, and Corticon Web Console.
>     
> -   Perform silent installations of Server components on page 32 that generates a file from an installer wizard run to let you perform silent installations of Server components on other Windows machines.
>     
> -   Perform command-line Linux installations of Server components on page 33 enables the Linux installer to run from the shell as a command with parameters.
>     
> -   Performing a manual installation of Server components— Corticon Server for Java and Web Console are available in zip archives. Use them to manually install Corticon WAR files into a supported application
>     
>       
>     
>     [server on any supported platform. For details about installing Corticon into specific application servers, see](https://knowledgebase.progress.com/articles/Article/Corticon-Server-6-x-sample-WAR-installation-for-different-Application-Servers) Corticon Server 6.X sample WAR installation for different Application Servers .
>     
> -   **Install on other application servers**—The .war files can be downloaded in the PROGRESS\_CORTICON\_6.3.x\_SERVER.zip package. The axis.war or corticon.war is deployed to the Application Server’s typical deployment directory. For example:
>     
>     -   For downloaded Tomcat: \[TOMCAT\_HOME\]\\webapps
>         
>     -   For the default Tomcat in the Corticon installer: \[CORTICON\_HOME\]\\Server\\tomcat\\webapps.
>         
>         [Refer to the Progress Software web page](https://docs.progress.com/bundle/corticon-supported-platforms/page/Corticon-6.3-Supported-Platforms-Matrix.html) Corticon Supported Platforms Matrix [to review the currently supported UNIX/Linux platforms and brands of application servers. Also see the Corticon KnowledgeBase article](https://knowledgebase.progress.com/articles/Article/Corticon-Server-6-x-sample-WAR-installation-for-different-Application-Servers) Corticon Server WAR installation for different Application Servers for detailed instructions on configuring Corticon Server on all supported platforms.
>         
>           
>         
>         ![image](/assets/corticon_install_files/server_install_Image_052.png)
>         
>         Note: Corticon as a Windows Service[—If you want to run Corticon Server as a Windows Service, see the Knowledgebase article](https://knowledgebase.progress.com/articles/Knowledge/000028756) https://knowledgebase.progress.com/articles/Knowledge/000028756.
>         
>           
>         
>         ![image](/assets/corticon_install_files/server_install_Image_053.png)
>         
>           
>         
>         Considerations for Authentication
>         
>         Confirm that servers that will host Corticon Server installations are enabled for authentication, and that Decision Service administrators have the credentials to deploy to those servers.
>         
>         When you run the Corticon Server installer, the application server does not enable authentication by default. To do so, see _"How to set up authentication for secure Java server access" in the Web Services section._
>         
>           
>         
>         For details, see the following topics:
>         
> -   [Run the Server and Web Console installer wizard](/assets/corticon_install.htm#bookmark47)
>     
> -   [Perform silent installations of Server components](/assets/corticon_install.htm#bookmark48)
>     
> -   [Perform command-line Linux installations of Server components](/assets/corticon_install.htm#bookmark49)
>     
> -   [How](/assets/corticon_install.htm#bookmark50) [to set up Corticon .NET Server resources on an IIS server](/assets/corticon_install.htm#bookmark50)‌
>     
>       
>     
>     #### Run the Server and Web Console installer wizard
>     
>     The Server installer will install or update Servers and Web Console 6.3.
>     
>       
>     
>     ![image](/assets/corticon_install_files/server_install_Image_054.png)
>     
>     Note: [You can install Corticon Servers and the Web Console on a machine that has a previous version installed. Where a previous version is installed, you must manage any port overloads that might result from running both versions. However, an installed version of Corticon Server 5.2 or earlier on the target machine must be](/assets/corticon_install.htm#bookmark52) uninstalled, then Corticon Server 6.3 installed. Consult with Progress Corticon Support or your Progress
>     
>     representative to consider your migration strategies for existing assets before you take action.
>     
>       
>     
>     ![image](/assets/corticon_install_files/server_install_Image_055.png)
>     
>     To create or update an installation of Corticon Servers (Java and .NET) and Web Console 6.3:
>     
>     1.  [On the target machine, access the Corticon 6.3.x installers you](/assets/corticon_install.htm#bookmark7) downloaded.
>         
>     2.  To open the Progress Corticon Server Setup Wizard:
>         
>         -   For Windows, double click on: PROGRESS\_CORTICON\_6.3.x\_SERVER\_WIN\_64.exe
>             
>               
>             
>             ![image](/assets/corticon_install_files/server_install_Image_056.png)
>             
>             Note: While not typically required, if you are told to do an administrator install, right-click on the EXE file, and then choose Run as administrator.
>             
>               
>             
>             ![image](/assets/corticon_install_files/server_install_Image_057.png)
>             
>               
>             
>         -   For Linux, run: PROGRESS\_CORTICON\_6.3.x\_SERVER\_LNX\_64.bin
>             
>             The installer opens in the installer wizard. The first installer panel opens with information about the installer.
>             
>             ![image](/assets/corticon_install_files/server_install_Image_058.jpg)
>             
>               
>             
>             ![image](/assets/corticon_install_files/server_install_Image_059.png)
>             
>             Note: If the same or higher Corticon Server 6.3.x is installed at any location on the target machine, an alert is posted that denies permission to continue. You will be able to apply Server 6.3 service packs and patches. You can have other versions of Corticon Server installed in distinct folders and they can run concurrently, although they must run on separate ports.
>             
>               
>             
>             ![image](/assets/corticon_install_files/server_install_Image_060.png)
>             
>               
>             
>     3.  Click **Next** to continue.
>         
>         The **License Agreement** panel opens.
>         
>           
>         
>         ![image](/assets/corticon_install_files/server_install_Image_061.jpg)
>         
>     4.  After you have read, understood, and agreed to the terms of the End User License Agreement, choose **I accept the terms of the license agreement**, and then click **Next.**
>         
>         The **Choose Install Folder** panel opens.
>         
>           
>         
>         ![image](/assets/corticon_install_files/server_install_Image_062.jpg)
>         
>     5.  The default installation directories are shown. To specify preferred directories on each line, either enter the explicit path, or click **Choose** to browse to each preferred directory.
>         
>           
>         
>         ![image](/assets/corticon_install_files/server_install_Image_063.png)
>         
>         Note: For Linux installations, the work directory path must not contain spaces.
>         
>           
>         
>         ![image](/assets/corticon_install_files/server_install_Image_064.png)
>         
>           
>         
>     6.  Click **Next**.
>         
>         The **Choose Server Components** panel opens.
>         
>           
>         
>         ![image](/assets/corticon_install_files/server_install_Image_065.jpg)
>         
>     7.  [Choose the one or more components you want to install at this time. Any components already installed are chosen and grayed out. If you choose Corticon Server for .NET as one of the components, see the topic](/assets/corticon_install.htm#bookmark50) How to set up Corticon .NET Server resources on an IIS server on page 34 for further instructions.
>         
>         ![image](/assets/corticon_install_files/server_install_Image_066.png)
>         
>         ![image](/assets/corticon_install_files/server_install_Image_067.png)
>         
>         Note: The Linux installer does not enable a Corticon Server for .NET installation. Click Next.
>         
>     8.  If you selected the Java Server or Web Console, the **Corticon Port Numbers** panel opens.
>         
>           
>         
>         ![image](/assets/corticon_install_files/server_install_Image_068.jpg)
>         
>     9.  If any of the preferred ports conflict with existing applications, you can change them at this time to an integer value from 1024 to 49151. Be aware that the documentation references these ports as though the default values, as shown, were accepted. Consult with your system administrator to identify alternate ports you might use, or to reset the ports on the conflicting applications.
>         
>         Enter your preferred port numbers, and then click **Next**. The **Pre-Installation Summary** page opens.
>         
>     10.  Verify your selections in the **Pre-Installation Summary** panel. Nothing has happened yet so you can click
>         
>         Previous to go back to a panel to make changes, or click Cancel to quit this installation procedure.
>         
>     11.  Click **Install** to continue. The installation status window opens. When done, the **Install Complete** panel opens.
>         
>     12.  Click **Done** to complete the Corticon Server / Web Console installation and close the installer. The installation and update of Corticon Servers and Web Console 6.3 is complete.
>         
>     
>     ![image](/assets/corticon_install_files/server_install_Image_069.png)
>     
>     Note: Using an LDAP store for Web Console authentication \- You can set up Corticon Web Console to authenticate users using an LDAP server. See the topic _"How to use LDAP for Web Console authentication" in the Web Console Guide._‌
>     
>       
>     
>     ![image](/assets/corticon_install_files/server_install_Image_070.png)
>     
>       
>     
>     #### Perform silent installations of Server components
>     
>     An unattended (silent) install requires that you first run an installation in the installer wizard (Windows or Linux) to capture the selected components and options, and then use the captured response file on targets on the same platform to 'playback' the responses into the installer without any user interaction.
>     
>     Perform command-line Linux installations of Server components
>     
>       
>     
>     ![image](/assets/corticon_install_files/server_install_Image_071.png)
>     
>     Silent installations or updates for Corticon Server Components on Windows:
>     
>     1.  Run the Corticon Server for Windows installer with your preferred locations and options to capture a response file, using the syntax installer.exe **\-r** file where installer is the preferred Server installer, and file is the response file you will reuse. For example:
>         
>         PROGRESS\_CORTICON\_6.3.x\_SERVER\_WIN\_64.exe -r C:\\CorticonServer\_63x\_WIN.responses
>         
>     2.  On other target Windows machines, access the Server 6.3 installer executable and the response file.
>         
>     3.  Run the installer using the syntax installer.exe **\-i silent -f** file where installer is the Server installer, and file is your response file. For example:
>         
>     
>     PROGRESS\_CORTICON\_6.3.x\_SERVER\_WIN\_64.exe -i silent -f C:\\CorticonServer\_63x\_WIN.responses
>     
>       
>     
>     Silent installations or updates for Corticon Server Components on Linux:
>     
>     1.  Run the Corticon Server for Linux installer with your preferred locations and options to capture a response file, using the syntax installer.bin **\-r** file where installer is the preferred Server installer, and file is the response file you will reuse. For example:
>         
>         PROGRESS\_CORTICON\_6.3.x\_SERVER\_LNX\_64.bin -r
>         
>         /usr/corticon/CorticonServer\_63x\_LNX.responses
>         
>     2.  On other target Linux machines, access the Server 6.3 installer binary and the response file.
>         
>     3.  Run the installer using the syntax installer.bin **\-i silent -f** file where installer is the Server installer, and file is your response file. For example:
>         
>     
>     PROGRESS\_CORTICON\_6.3.x\_SERVER\_LNX\_64.bin -i silent -f
>     
>     /usr/corticon/CorticonServer\_63x\_LNX.responses‌
>     
>       
>     
>     #### Perform command-line Linux installations of Server components
>     
>     A command-line install runs a Linux installation in a command shell as a text command with parameters.
>     
>     To perform command-line installations for Corticon Server components:
>     
>     1.  On a supported 64-bit Linux platform, access the downloaded Linux installer binary file,
>         
>         PROGRESS\_CORTICON\_6.3.x\_SERVER\_LNX\_64.bin
>         
>     2.  In a shell, run the binary with the console option. For example:
>         
>           
>         
>         \# ./PROGRESS\_CORTICON\_6.3.x\_SERVER\_LNX\_64.bin -i console
>         
>           
>         
>     3.  Follow the prompts to complete the installation via the command-line.
>         
>     
>       
>     
>     ![image](/assets/corticon_install_files/server_install_Image_072.png)
>     
>     Note: For Linux installations, the work directory path must not contain spaces.
>     
>       
>     
>     ![image](/assets/corticon_install_files/server_install_Image_073.png)
>     
>       
>     
>     #### How to set up Corticon .NET Server resources on an IIS server‌
>     
>     The runtime server for Corticon Server for .NET is Microsoft Internet Information Services (IIS), a distinct setup into which you install and update with the latest Corticon Server for .NET resources.
>     
> -   Obtain an appropriate Corticon license for Corticon Server for .NET.
>     
>       
>     
>     ![image](/assets/corticon_install_files/server_install_Image_074.png)
>     
>     Note: Corticon embeds a limited evaluation license that enables testing of rule modeling projects on all supported platform configurations except .NET. You must obtain .NET evaluation and deployment licenses from your Progress representative.
>     
>       
>     
>     ![image](/assets/corticon_install_files/server_install_Image_075.png)
>     
>       
>     
> -   [Confirm that your target machine meets the system requirements. See](/assets/corticon_install.htm#bookmark6) System requirements on page 8 for more information.
>     
> -   [See the Progress Software web page](https://docs.progress.com/bundle/corticon-supported-platforms/page/Corticon-6.3-Supported-Platforms-Matrix.html) Corticon Supported Platforms Matrix for information on supported
>     
> 
> .NET Framework and IIS.
> 
> [See the instructions for](https://docs.progress.com/bundle/corticon-web-services/page/Web-services-on-.NET.html) "Web services on .NET" in the Web Services guide.
> 
>   
> 
> ![image](/assets/corticon_install_files/server_install_Image_076.png)
> 
> # 5‌
> 
> ### How to uninstall Corticon components
> 
> ![image](/assets/corticon_install_files/server_install_Image_077.png)
> 
>   
> 
> Uninstalling Corticon Studio or Corticon Server results in removing a complete major.minor version of those products, including any service packs or hotfixes applied. It is not possible then to uninstall just a service pack or hotfix.
> 
>   
> 
> Uninstalling Corticon Studio
> 
> To remove a version of Corticon Studio, do the following:
> 
> 1.  Close Corticon Studio.
>     
> 2.  Choose the **Start** menu **Control Panel** function **Programs and Features**, and then double-click on **Progress Corticon Studio 6.3** to launch its uninstaller.
>     
> 
>   
> 
> ![image](/assets/corticon_install_files/server_install_Image_078.png)
> 
> **Note:** You could initiate the same task directly by navigating to \[CORTICON\_HOME\]\\Uninstall\_Progress Corticon Studio 6.3, and then running Uninstall Progress Corticon Studio 6.3.exe.
> 
>   
> 
> ![image](/assets/corticon_install_files/server_install_Image_079.png)
> 
>   
> 
> The installed files in the Studio's \[CORTICON\_HOME\] are removed. Files you created (including the complete workspace) are NOT removed or replaced during this process.
> 
> If the Uninstaller program is unable to fully remove components (usually because they are open), it will display messages, and might require a reboot to complete the process.
> 
>   
> 
> Uninstalling Corticon Server
> 
> The Corticon Server components -- Corticon Server for Java, Corticon Server for .NET, and the Corticon Web Console -- use common installation directories. As such, you cannot choose to uninstall just selected components. Uninstallation will remove all installed server components.
> 
> To uninstall Corticon Server on Windows:
> 
> Chapter 5: How to uninstall Corticon components
> 
>   
> 
> ![image](/assets/corticon_install_files/server_install_Image_080.png)
> 
>   
> 
> 1.  Stop Corticon Server.
>     
> 2.  Backup any files you want to retain.
>     
> 3.  Choose the **Start** menu **Control Panel** function **Programs and Features**, and then double-click on **Progress Corticon Server 6.3.x** to launch its uninstaller.
>     
> 
>   
> 
> ![image](/assets/corticon_install_files/server_install_Image_081.png)
> 
> **Note:** You could initiate the same task directly by navigating to \[CORTICON\_HOME\]\\Uninstall\_Progress Corticon Studio 6.3, and then running Uninstall Progress Corticon Server 6.3.exe.
> 
>   
> 
> ![image](/assets/corticon_install_files/server_install_Image_082.png)
> 
>   
> 
> To uninstall Corticon Server on Linux:
> 
> 1.  Stop Corticon Server.
>     
> 2.  Backup any files you want to retain.
>     
> 3.  In a command shell, navigate to \[CORTICON\_HOME\]\\Uninstall\_Progress Corticon Studio 6.3, and then run Uninstall Progress Corticon Server 6.3.bin.
>     
> 
> The installed files in the Server's \[CORTICON\_HOME\] are removed. Note that files you created are NOT removed or replaced during this process. No server files in the \[CORTICON\_WORK\_DIR\] are removed.