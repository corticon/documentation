# Serverless Target Platforms

When you package rules for deployment, you select the **target platform**. Corticon will generate a JavaScript bundle with your rules and a wrapper specific to the target platform. The available target platforms are:

* **AWS Lambda Functions**
* **Azure Functions**
* **Google Cloud Functions**
* **Browser**
* **Node.js**

Selecting AWS Lambda, Azure Functions, or Google Cloud Functions as the target platform generates the rules and a wrapper ready for deployment as a serverless function. After the rules are deployed, you can use them on your cloud platform—for example, to expose the decision service through a REST endpoint, to respond to a database update, or to integrate into a cloud vendor workflow system such as AWS step functions.

The Node.js target can be used for running decision services in Node server and as well to run them in Mobile applications created with NativeScript and ReactNative.

Selecting Browser generates the decision service and simple example code that demonstrates how to integrate the rules into your application.

> Note: See the [Corticon.js Supported Platforms Matrix](https://documentation.progress.com/output/Corticon/js-1.2.0/redirectors/supported-platforms.html) to review the supported JavaScript and web platforms, and mobile apps. You are not limited to these JavaScript platforms. The API for integrating rules in your JavaScript application allows you to develop your own wrapper or integration code that calls rules.

**To create a Corticon JavaScript package:**

1. In Corticon.js Studio, select a project, and then select Project > Package Rules for Deployment. The Package Rules for Deployment dialog box opens.
2. Select the **Ruleflow** for your application.
3. Choose the **Target Platform**
4. Enter a preferred **Bundle** name so that you produce your package in a distinctly named folder. Each Ruleflow selected generates a separate package.
5. Enter a preferred **to Directory** where your package will be placed.
6. Click **Next**. The second panel of the dialog opens.
7. Choose the top-level entities for this package. In our example, only the Cargo entity is referenced so just that entity is selected.
8. Click **Finish** to generate the packaged JavaScript as a Decision Service plus everything you need to deploy it. The packaging process generates a single JavaScript bundle that is the entry point for the rules, which contain all the decision logic in its enclosed components for the selected Ruleflow. The generated bundle is compressed and obfuscated. It is valid, executable JavaScript, but it is not readable and cannot be edited.

# AWS Lambda Functions

When packaging for AWS Lambda deployment, Corticon.js generates the files:

* `decisionServiceBundle.js`: Your rules, obfuscated
* `index.js`: Sample AWS Lambda wrapper
* `lambda.zip`: Zip file with both `.js` files to simplify deployment.

The wrapper, index.js, implements the AWS Lambda API to be invoked as a serverless function and returns the results of its execution.

When invoked, the AWS Lambda function is passed a JSON payload. Examples of how this could be triggered include using a REST API gateway to call your function, and using the function as a step in an AWS Step Functions workflow. Once deployed as a serverless function, your rules are available to the AWS ecosystem.

The wrapper is a complete, ready-to-deploy, Lambda function but you can also modify it to meet the specific needs of your application.

The `lambda.zip` file is generated as a convenience. AWS makes it easy to deploy a Lambda function in one step using a `.zip` file.

See the [AWS Lambda documentation](https://docs.aws.amazon.com/lambda/index.html) for details on deploying serverless functions.

# Azure Functions

When packaging for Microsoft Azure Functions deployment, Corticon.js generates the files:

* `decisionServiceBundle.js`: Your rules, obfuscated
* `azure.sample.js`: Sample Azure Functions wrapper

The wrapper, `azure.sample.js`, implements the Azure Functions API for responding to HTTP triggers.

When invoked the Azure function is passed a JSON payload. This is most likely triggered by a REST call to invoke the function.

The wrapper is a complete, ready-to-run, Azure function, yet you can also modify it to meet the specific needs of your application. The Azure functions API has different signatures for different triggers. You can modify the wrapper to meet the needs of different triggers.

See the [Azure Functions documentation](https://docs.microsoft.com/en-us/azure/azure-functions/) for details on deploying serverless functions.

# In-Browser Decision Services

When packaging for browser deployment, Corticon.js generates the files:

* `decisionServiceBundle.js`: Your obfuscated rules
* `browser.sample.js`: Sample code demonstrating calling Corticon.js rules
* `browser.sample.html`: Sample HTML page for testing browser deployment

The HTML page, `browser.sample.html`, present a simple form where you can provide a JSON payload, invoke your rules, and see the resulting JSON.

The wrapper, `browser.sample.js`, simply invokes the rules with the payload input provided in the form.

The html page and wrapper are pure sample code. They just demonstrate how Corticon.js rules can be embedded into a JavaScript application running in a browser.

The `browser.sample.html` is ready to run a simple page in a browser.

Paste in the JSON you exported from Studio tester into the left panel, and then click **Run Decision Service**. The results in the right panel as shown:

![Note that the rules replaced the default shipping mode and added a message.](https://progress-be-prod.zoominsoftware.io/bundle/corticon-js-integration/page/oso1617031637426.image?\_LANG=enus)

You can tailor `browser.sample.html` to build your UI around the Decision Service that you have now validated.

## Multiple decision services on a browser page 

An integrator can put more than one Decision Services on a single HTML page so that a set of Corticon engine execution functions are created with one execute function per included Decision Service. In the browser bundle, the file `browser.sample.multipleDS.html` provides the format for multiple decision services. In it, you see the array property **corticonEngines**. Each entry in the array contains an object literal with the **execute** function. The script inclusion order determines where in the array a specific decision is located. The first included Decision Service is available at index 0 `window.corticonEngines[0].execute`):

```
<script type="text/javascript" src="decisionServiceBundle.js" </script>
<script type="text/javascript" src="decisionServiceBundle2.js" </script>
const result1 = window.corticonEngines[0].execute(payload1, configuration);
const result2 = window.corticonEngines[1].execute(payload2, configuration);
```

You could specify a different configuration for each of the services.

### To set up multiple Decision Services to run in one browser instance

1. In Studio, generate the first package as a bundle.
2. Generate the second package as a bundle with a different bundle name.
3. In the second bundle's folder, rename `decisionServiceBundle.js` to `decisionServiceBundle2.js`, and then copy it to the browser folder of the first bundle.
4. Opening `browser.sample.multipleDS.html` opens with two input and output areas for the Decision Services.

Note: If you want to add additional Decision Services, follow the pattern of steps two and three, and then revise `browser.sample.multipleDS.html` to specify each of the added Decision Services.

When you include only one decision service, you can access the execute function with either of the following code excerpts:

```
// Using the first array element
const result = window.corticonEngines[0].execute(payload, configuration);
```

```
// Using the last included one						
const result = window.corticonEngine.execute(payload, configuration)
```
# Google Cloud Functions

When packaging for Google Cloud Functions deployment, Corticon.js generates the files:

* `decisionServiceBundle.js`: Your rules, obfuscated
* `index.js`: Sample Google Cloud Functions wrapper

The wrapper, `index.js`, implements the Google Cloud Functions API for responding to HTTP triggers.

When invoked, the Google Cloud function is passed a JSON payload. This is most likely triggered by a REST call to invoke the function.

The wrapper is a complete, ready-to-run, Google Cloud function, yet you can also modify it to meet the specific needs of your application. The Google Cloud functions API has different signatures for different triggers. You can modify the wrapper to meet the needs of different triggers.

See the [Google Cloud Functions documentation](https://cloud.google.com/functions/docs) for details on deploying serverless functions.
# node.js

When packaging for Node deployment, Corticon.js will generate the files:

* `decisionServiceBundle.js`: Your obfuscated rules
* `node.sample.js`: Sample Node.js wrapper

The wrapper, `node.sample.js`, is pure sample code demonstrating how to embed rules in a Node.js application. How you invoke rules from your own Node.js application depends on your needs.

You need to define a file named `payload.json` that contains the decision service request. You can export the data from Corticon rule tester. To do so, open the Ruletest file (`.ert`) file, and then choose the menu option: **Rulesheet->RuleTest -> Data -> Input -> Export Request JSON**

The sample wrapper reads the file `payload.json`, passes it to your rules, and writes the result to `result.json`.

See the [Node.js documentation](https://nodejs.org/en/docs/) for details on deploying serverless functions.
