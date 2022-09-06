# JavaScript Decision Services

With Corticon.js, you can deploy rules to any platform that supports a compatible version of JavaScript. With this flexibility, you automate decisions where the data originates from or where the decisions have the most effect. Supported deployments of Corticon.js include:

* Rules deployed as serverless functions on AWS Lambda, Google Cloud Functions, or Microsoft Azure Functions
* Rules integrated into a cloud work flow such as AWS Step Functions, Microsoft Flow/Logic Apps, or Google Workflows
* Rules run on your own back end as part of your node.js platform
* Rules bundled in a mobile app created with Xamarin, React, Vue.js, or other toolkits
* Rules executed in a browser as part of a web application
* Rules executed in a browser which define a dynamic form's UI behavior

# JSON payloads and results in Corticon.js

When deployed or integrated into your application your Corticon.js decision services execute by accepting a JSON payload and returning a JSON result. The JSON payload contains the item or items your rules are to execute on—for example, a mortgage application to be evaluated or a set of sales leads to be routed. When your rules execute, they will update or add to the input payload—for example, adding a determination for a mortgage application or assigning the sales rep for each sales lead. The JSON result returned from the decision service will contain the state of the payload after rule execution.

![](/docs/assets/corticon_js_integration-1.png)

Corticon.js accepts most well-formatted JSON as the input payload. The result JSON will reflect the input payload plus any changes made by the rules. In addition, it will contain information about the rule execution, such as status indicating if rule execution was successful.

As a very simple example, consider a mortgage approval application where the JSON payload to your decision service is as follows:


![](/docs/assets/mortgage%20approval%20application%20JSON%20payload%20.png)

The rules in the decision service look at the mortgage application information to determine if the applicant should be approved, how much they are approved for, and at what rate. The rules in the decision service set the attributes `approved`, `mortgageRate` and `mortgageAmount` on the application. The result payload would be similar to:

![](/docs/assets/mortgage%20json%20response%20payload.png)

The result payload has the same data as was in the input payload plus the attributes set by the rules. In this case the applicant has been approved for $350,000 at 3.5%.

The result payload also contains a `corticon` object that has the `timestamp` of when the rules were run plus the status, `success`, of the execution. The `corticon` object contains additional information about the execution of your rules.

## JSON to Vocabulary mapping 

When your decision service is invoked, Corticon maps the JSON payload to the internal data model of your Corticon vocabulary to enable the rules to execute on it. To perform this mapping, Corticon must first examine the JSON payload to identify the top-level objects in the JSON and the vocabulary entities they correspond to.

In our simple mortgage application example, the vocabulary could be defined as:

![](/docs/assets/mortgage%20vocab.png)

This is a very simple vocabulary with a single entity, `Application`. Our JSON payload is equally simple:


![](/docs/assets/mortgage%20json.png)

Here the JSON payload represents a single application and Corticon would map it to the `Application` entity. In a real application your Corticon vocabulary and JSON payload are likely to be much more complex.

Once the top-level objects in the JSON payload are mapped to the vocabulary model, Corticon can map any nested objects in the JSON to associations in the vocabulary. Let’s expand our mortgage sample to have a slightly more complex vocabulary:

![](/docs/assets/mortgage%20complex.png)

Here the mortgage application was defined to have an `Application` entity with a one-to-many association to a `CreditReport` entity and a one-to-one association to a `Mortgage` entity. This is more reflective of a real Corticon vocabulary. A real vocabulary is likely to have many entities and associations. A JSON payload for this vocabulary may look like:


![](/docs/assets/complex%20mortgage%20json.png)

Once Corticon has mapped the root object in the JSON to the `Application` entity, it can use the knowledge that the `Application` entity has an association to a `CreditReport` entity to map the nested `creditReport` in the JSON. Corticon will set the association on the `Application` entity to this `CreditReport` entity.

## JSON Path and JSON Element Name 

Corticon employs two strategies to map a JSON payload to the vocabulary. First, it will use the knowledge it has of the vocabulary to identify how to perform the mapping. When this information is insufficient, Corticon will use a "best match" strategy to perform the mapping.

In your Corticon vocabulary, you can define properties on entities, attributes, and associations to provide guidance for Corticon when mapping a JSON payload to the vocabulary. If fully utilized, Corticon may need to perform no "best match" mapping.

In the Corticon Studio vocabulary, you can set the **JSON Path** property on entities and the **JSON Element Name** property on attributes and associations.

The **JSON Path** property defines the path to the entity in the JSON payload. When JSON payload is passed to a decision service, Corticon can use this information to map entities in the payload to the vocabulary.

The **JSON Element Name** property defines the attribute a field in the JSON payload is mapped to or the association a nested object in the payload is mapped to.

Both **JSON Path** and **JSON Element name** can be set in the Corticon.js vocabulary editor but the easiest, and least error prone, way to set them in your vocabulary is to generate your vocabulary using the Corticon.js **Populate Vocabulary form JSON** wizard. See [Generate a Vocabulary](https://docs.progress.com/bundle/corticon-js-rule-modeling/page/Generate-a-Vocabulary.html) .

Given this JSON:
![](https://progress-be-prod.zoominsoftware.io/bundle/corticon-js-integration/page/ldn1618946462665.image?\_LANG=enus)


Corticon would generate this vocabulary:

![](https://progress-be-prod.zoominsoftware.io/bundle/corticon-js-integration/page/hdd1618946519504.image?\_LANG=enus)


This is similar to the previous vocabulary, the only differences are that the application entity is named `Root` and the `creditReport` association is one-to-one. Where the root entity in JSON doesn’t have a name, Corticon names it `Root`. It is common to rename this to something more meaningful to rule modelers. The `creditReport` association is one-to-one because there was only one credit report in the JSON.

Let’s examine how **JSON Path** would be set in this vocabulary:

| Entity                 | JSON Path           |
| ---------------------- | ------------------- |
| Application (aka Root) | `$`                 |
| CreditReport           | `$[*].creditReport` |
| Mortgage               | `$[*].mortgage`     |

**JSON Path** is a robust syntax for defining the path to elements in a JSON file. In our example the **JSON Path** element `$` indicates the root of the document. Where `Application` is the root entity in the JSON, its JSON Path is simply `$`. A period, `.`, Is used to identify a nested entity.

The **JSON Path** syntax can be complex but fortunately Corticon.js can set it for you when populating a vocabulary from a JSON file. In most cases, all you need set is the **JSON Path** for the root entities in the JSON.

Now let’s examine how **JSON Element Name** would be set in this vocabulary:

| Entity                | JSON Element Name |
| --------------------- | ----------------- |
| Application.firstName | firstName         |
| Application.lastName  | lastName          |
| Application.income    | income            |
| CreditReport.agency   | agency            |
| CreditReport.score    | score             |
| Mortgage.amount       | amount            |
| Mortgage.rate         | rate              |
| Mortgage.approved     | approved          |

| Association              | JSON Element Name |
| ------------------------ | ----------------- |
| Application.creditReport | creditReport      |
| Application.mortgage     | mortgage          |

The JSON Element Name is the name of the field or nested object in the JSON. You can rename attributes and associations in your vocabulary to be a name more meaningful to a rule modeler. If specified, the JSON Element Name must match the JSON payload.

## Best Match Mapping

You don’t have to specify **JSON Path** or **JSON Element Name** in your vocabulary. When not specified, Corticon.js will use a "best match" algorithm to map JSON payload to your vocabulary. This algorithm is dependent on the object and field names in your JSON closely matching the entity, attribute, and association names in your vocabulary.

You also don’t have to specify the top-level objects in the JSON payload. When not specified, Corticon.js will examine the attributes on the top-level objects in the JSON payload and use them to map to the best matching entity.

Corticon.js "best matching" is very effective in most use cases. The negative aspect is that the mapping is slower. For performance critical applications or those processing large JSON payloads, this performance impact may be significant.

At minimum, you should have **JSON Path** specified for the top-level entities in your JSON payload and identify these as the top-level entities when packaging your rules for deployment.

## Identifying Top-Level Entities

When you package your rules for deployment, you can specify the top-level entities of interest in the JSON payload that will be processed when integrated with your application. This information can then be used by Corticon.js to optimize the mapping of JSON payloads to your vocabulary. It is not uncommon for a Corticon vocabulary to have hundreds of entities. If only one of these entities will be at the top-level, identifying the entity allows Corticon.js to map payloads to the vocabulary much more efficiently.

In Corticon.js Studio, the **Package Rules for Deployment** wizard provides a dialog where you can select the top-level entities.


![](https://progress-be-prod.zoominsoftware.io/bundle/corticon-js-integration/page/gro1618946665965.image?\_LANG=enus)

In this example, the vocabulary was expanded to have many more entities as would be typical in a real application. Here, `Application` is selected to indicate that `Application` is the top-level entity in the JSON payloads the decision service will process.

Top-level entities do not need to be at the root of your JSON payload. Often the objects of interest to your rules may be nested in a larger JSON document.

![](https://progress-be-prod.zoominsoftware.io/bundle/corticon-js-integration/page/hcx1618946775550.image?\_LANG=enus)

Here the mortgage application is nested in a JSON document where the other information is not needed by the rules. Setting JSON Path for the Application entity to `$.FDO.application` will let Corticon know where it is within the JSON document. It and its nested objects are the only portions of the JSON that need to be mapped to the vocabulary.

Corticon.js allows the top-level entities to be identified when a Ruleflow is packaged for deployment. The integration API allows you to override this within your application. See [Config options](https://docs.progress.com/bundle/corticon-js-integration/page/Config-options.html).

## Unmapped JSON Payload

Any objects or fields in the JSON payload that are not mapped to your vocabulary are preserved and included in the result payload.

##  Error handling 

If there is an error during the execution of the decision service, the status `"error"` is returned to the user along with the description of the error which will be part of the `"corticon"` JSON object as follows:

```
{
    "corticon": {
        "status": "error",
        "description": "<error message>"
    }
}							
```
> Note: The pattern for an error was different in V1.2 where the status "error" and description were returned in the root JSON response as follows:

```
{
    "status" : "error",
    "description" : "<error message>"
}						
```
# Custom JavaScript functions

Corticon.js provides data access operators in a mechanism that will execute custom JavaScript functions. The custom functions are accessed as a group of built-in operators available from Studio's Rule operator tree under **General > Functions** as standalone GET and SET operators for each Corticon.js data type:


![](https://progress-be-prod.zoominsoftware.io/bundle/corticon-js-integration/page/fvh1629311110121.image?\_LANG=enus)

Each `get` operator works the same way; only the returned data type is different.

Each `set` operator works in a fashion similar to the `get` operators yet each has an additional parameter, the _value_ to set. Set operators do not return any data as they are void operators.

### Sample project: Get and Set Operators

The sample project provides JavaScript provides examples of the operators as well as Rulesheets, a RuleFlow, and a Ruletest that demonstrates the features.

###  getData 

A custom `get` function takes two parameters:

1. The name of the custom function to call.
2. A string parameter. For multiple parameters, the JSON string can encapsulate all the parameters to pass to the custom function.

The sample Rulesheet `getData.ers` shows each data type with data to fetch.

![](https://progress-be-prod.zoominsoftware.io/bundle/corticon-js-integration/page/elf1629316701131.image?\_LANG=enus)

For example, to call the custom function `getData` with parameter `key2` using the `getString` operator, the result is stored in the string attribute, `Ent1.str2`.

### setData 

![](https://progress-be-prod.zoominsoftware.io/bundle/corticon-js-integration/page/mns1629315531750.image?\_LANG=enus)

A custom `set` function takes three parameters:

1. The name of the custom function to call.
2. A string parameter. If you need to pass more than one parameter, the JSON string can encapsulate all the parameters to pass to the custom function.
3. The value to set. The type of this parameter corresponds to the operator name. For example, `setDateTime`, requires a `DateTime` object.

For example, to call the custom decimal function `setData` with the parameter `key5` using the `setDecimal` operator, use the following action. The result is stored in the string attribute, `Ent1.decimal3`.

### Mock implementation in Studio tester 

Studio tester runs the Ruleflows and Rulesheets in the context of a local Node.js process. Consequently, it is possible that:

* the production environment data may not be available
* the production context is not available. For example, in studio tester the browser session context or the Serverless function context is not available .

However, you can specify a mock implementation to run local unit tests by appending the implementation to the project. The configuration of the extensions in the sample is in `getSetData.js`:

<pre><code>const sessionData = new Map();

function getData ( helper, name ) {
	if ( name === 'key4' )  // example showing how to construct a DateTime
		return helper.dateTime.constructDateTime(sessionData.get(name));
	else if ( name === 'key5' ) // example showing how to construct a Decimal
		return helper.decimal.constructDecimal(sessionData.get(name));
	else
		return sessionData.get(name); 
}

function setData ( helper, name, value ) {
	if ( name === 'key4' )  // example showing how to construct a DateTime
		 sessionData.set('key4', helper.dateTime.outputToJson(value));
	else if ( name === 'key5' ) // example showing how to construct a Decimal
		sessionData.set('key5', helper.decimal.outputToJson(value) );
	else
		sessionData.set(name, value); // for all other data we simply store as is.
}

module.exports = { getData, setData }; // export the names to be used in studio</code></pre> 

This code is appended to the project for testing in Studio.

**To append the extension file to the project:**

1. In Corticon.js Studio, open your project.
2. Click on your project, and then select **Properties**.
3. Select **Corticon.js Extensions**.
4. Click **Add**, and then select your .js implementation file, as illustrated:
   
   ![](https://progress-be-prod.zoominsoftware.io/bundle/corticon-js-integration/page/aic1629310034311.image?\_LANG=enus)

5. Click **Apply and Close**.

> Note: The functions from this code are not added to a production bundle that is generated by **Package Rules for Deployment**.

### Running the Sample's Ruletest 

A Ruleflow puts the setters Rulesheet to process ahead of the getters Rulesheet:

![](https://progress-be-prod.zoominsoftware.io/bundle/corticon-js-integration/page/dfy1629896547953.image?\_LANG=enus)

Open the Sample Ruletest, and then run it:

![](https://progress-be-prod.zoominsoftware.io/bundle/corticon-js-integration/page/dws1629896738699.image?\_LANG=enus)

### Runtime

**Writing implementations for runtime**

The implementation file contains the custom functions. You export them using the following syntax:

**`module.exports={name of function as used in rulesheet:reference to custom function};`**

For example:

`module.exports={getSessionData:getSessionData};`

That can be abbreviated to `module.exports ={getSessionData};`

The following code shows a more complete example with two custom functions:
```
<pre><code>const sessionData = new Map();
sessionData.set('key1', true);
sessionData.set('key2', 'my session string');
sessionData.set('key3', 12);
																	
function getSessionData ( helper, name ) {
	if ( !sessionData.has(name) )
		return 'ERROR - no session data for ' + name;
	else
		return sessionData.get(name);
}
											
function getMoreData ( helper, name ) {
	return name;
}
																	
 module.exports = { getSessionData, "from session data": getMoreData };
```
These definitions enable you to use `getSessionData` `from session data` as custom function names in any of the simplified extended operators.

For example:

![](https://progress-be-prod.zoominsoftware.io/bundle/corticon-js-integration/page/ufv1614181387040.image?\_LANG=enus)

### How to specify implementation of custom functions for runtime 

The custom functions are specified at runtime in the configuration object. This allows for complete separation of the custom functions from the rulesheets and their bundles.

The custom functions can be:

* Shared across several decision services.
* Developed and managed with your own build pipeline.

The custom functions are specified in the configuration object using the attribute "**customFunctions**".

This attribute points to an array of object literals. Each object literal contains the information for one custom function.

The syntax of the object literal is: **{ \<name of function as used in rulesheet>: \<reference to custom function> }**

For example, here is the configuration for the custom function examples in previous section:

 ```<pre><code>const sessionData = new Map();
sessionData.set('key1', true);
sessionData.set('key2', 'my session string');
sessionData.set('key3', 12);
sessionData.set('key4', '2021-02-10T00:00:00.000Z');
sessionData.set('key5', 10.23);
 
function getSessionData ( helper, name ) {
    console.log("Custom function called for " + name);
    if ( name === 'key4' )  // example showing how to construct a DateTime
        return helper.dateTime.constructDateTime(sessionData.get(name));
    else if ( name === 'key5' ) {// example showing how to construct a Decimal
        return helper.decimal.constructDecimal(sessionData.get(name));
    }
    else if ( !sessionData.has(name) )
        return 'ERROR - no session data for ' + name;
    else
        return sessionData.get(name);
    }
 
function setSessionData ( helper, name, value ) {
    if ( name === 'key4' )  // example showing how to construct a DateTime
         sessionData.set('key4', helper.dateTime.outputToJson(value));
    else if ( name === 'key5' ) {// example showing how to construct a Decimal
        sessionData.set('key5', helper.decimal.outputToJson(value) );
    }
    else
        sessionData.set(name, value);
}
 
const configuration = { logLevel: 1,
    customFunctions: [
        { getSessionData: getSessionData },
        { setSessionData: setSessionData }
    ]
}
```



Custom functions are specified at run time in the configuration object. This allows for complete separation of the custom functions from the rulesheets and its bundle.

In particular, the custom functions can easily be:

* Shared across several decision services.
* Developed and managed with your own build pipeline.

The custom functions are specified in the configuration object using the attribute `customFunctions`.

This attribute points to an array of object literals. Each object literal contains the information for one custom function.

The syntax of the object literal is:

`{name of function as used in rulesheet:reference to custom function};`

For example, the following is a configuration for the custom function example:

```
const configuration = {
	logLevel: 0,
	customFunctions: [  {"getSessionData": getSessionData}, 
				 	 {"from data store":getMoreData}
				   ]
};const configuration = {
	logLevel: 0,
	customFunctions: [  {"getSessionData": getSessionData}, 
				 	 {"from data store":getMoreData}
				   ]
};
```

### Custom function signatures 

A custom function must have the following signature:

`function <functionName> ( helper, name )`

The name parameter contains the second argument string as entered in the Rulesheet editor.

For example, in the Rulesheet editor:

```
Ent1.str1 = getString('getSessionData','key2')
```

The `getSessionData` custom function name parameter will contain the string `key2`.

The helper function is an object literal containing references to Decimal and DateTime operators.

It has the following syntax:

```
helper={'decimal': <all decimal operators>,
        'dateTime': <all dateTime operators> }
```

### Implementing custom functions for runtime 

You can implement the body of a custom function with whatever logic your use case requires.

The only constraints are:

* The custom function has the proper signature.
* You return the proper object type. A `getDecimal` call needs to return a Decimal, likewise a `getDateTime` needs to return a DateTime.
* You use the helper object to create or operate on Decimal and DateTime objects.

### Custom GET functions

The following code shows how to construct and return a decimal and a dateTime:

```
sessionData.set('key1', true);
sessionData.set('key2', 'my session string');
sessionData.set('key3', 12);
 
function getSessionData ( helper, name ) {
    if ( name === 'key4' ) {  // example showing how to construct a DateTime
        return helper.dateTime.constructDateTime('2021-02-10T00:00:00.000Z');
    }
    else if ( name === 'key5' ) { // example showing how to construct a Decimal
        return helper.decimal.constructDecimal('10.23');
    }
    else if ( name === 'key6' ) { // example showing how to use additional built-in operators like now and addDays
        const dt = helper.dateTime.now();
        const dt2 = helper.dateTime.addDays(dt, 7);
        return dt2;
    }                  
    else if ( !sessionData.has(name) )
        return 'ERROR - no session data for ' + name;
    else
        return sessionData.get(name);
}
 
function getMoreData ( helper, name ) {
    return name;
}	
module.exports = { getSessionData, "from session data": getMoreData };							
```


### Custom SET functions

Similar to `get` custom functions, notice how the functions are exposed via the configuration object:

```
sessionData.set('key1', true);
sessionData.set('key2', 'my session string');
sessionData.set('key3', 12);
sessionData.set('key4', '2021-02-10T00:00:00.000Z');
sessionData.set('key5', 10.23);
 
function getSessionData ( helper, name ) {
    console.log("Custom function called for " + name);
    if ( name === 'key4' )  // example showing how to construct a DateTime
        return helper.dateTime.constructDateTime(sessionData.get(name));
    else if ( name === 'key5' ) {// example showing how to construct a Decimal
        return helper.decimal.constructDecimal(sessionData.get(name));
    }
    else if ( !sessionData.has(name) )
        return 'ERROR - no session data for ' + name;
    else
        return sessionData.get(name);
    }
 
function setSessionData ( helper, name, value ) {
    if ( name === 'key4' )  // example showing how to construct a DateTime
         sessionData.set('key4', helper.dateTime.outputToJson(value));
    else if ( name === 'key5' ) {// example showing how to construct a Decimal
        sessionData.set('key5', helper.decimal.outputToJson(value) );
    }
    else
        sessionData.set(name, value);
}
 
const configuration = { logLevel: 1,
    customFunctions: [
        { getSessionData: getSessionData },
        { setSessionData: setSessionData }
    ]
};</code></pre> |
```

### Helper functions 

A helper function is an object literal containing references to Decimal and DateTime operators. It has the following syntax:

```
helper = { 'decimal': <all decimal operators>, 'dateTime': <all dateTime operators> }
```

The list of operators is nearly identical to the one listed in the studio operator tree.

> Note: The list of operators is nearly identical to the one listed in the studio operator tree. See [DateTime](https://docs.progress.com/bundle/corticon-js-rule-language/page/DateTime.html) and [Decimal](https://docs.progress.com/bundle/corticon-js-rule-language/page/Decimal.html) .

The lists of helper functions are documented in the operator tree. Exceptions are distinguished at the bottom of each list.

**Decimal helper functions**

The helper Decimal functions are as follows:

* `multiply`
* `divide`
* `negated`
* `exponent`
* `add`
* `minus`
* `absVal`
* `floor`
* `ceiling`
* `ln`
* `log`
* `logBase`
* `lessThan`
* `lessThanOrEqual`
* `equal`
* `different`
* `greaterThan`
* `greaterThanOrEqual`
* `min`
* `max`
* `random`
* `toString`
* `toInteger`
* `round`

Exceptions:

* `isDecimal` returns a boolean `true` if the object is a Decimal else returns `false`
* `constructDecimal` returns a Decimal object. It accepts number or strings as parameter. For example, `constructDecimal(10.5)` or `constructDecimal("100000000000000000000000.56789")`
* `outputToJson` returns a string representation suitable for inclusion in a JSON payload.

### DateTime helper functions 

The helper DateTime functions are as follows:

* `lessThan`
* `lessThanOrEqual`
* `equal`
* `notEqualTo`
* `greaterThan`
* `greaterThanOrEqual`
* `addYears`
* `addMonths`
* `addDays`
* `addHours`
* `addMinutes`
* `addSeconds`
* `yearsBetween`
* `monthsBetween`
* `weeksBetween`
* `daysBetween`
* `hoursBetween`
* `minutesBetween`
* `secondsBetween`
* `year`
* `month`
* `day`
* `hour`
* `min`
* `sec`
* `now`
* `dayOfWeek`
* `dayOfYear`
* `getMilliseconds`
* `weekOfMonth`
* `weekOfYear`
* `afterDate`
* `beforeDate`
* `isSameDate`
* `afterTime`
* `beforeTime`
* `isSameTime`

Exceptions:

* `constructDateTime` create a DateTime object. It accepts either a string which has to be an ISO-8601 representation of a DateTime or a long value which represents the time since epoch in milliseconds.
* `isDateTime` returns a boolean `true` if the object is a DateTime else returns `false`
* `outputToJson` returns a string representation in ISO-8601 format as UTC. The string is suitable for inclusion in a JSON payload.


# Scripting

You can use the `corticonjs` command line utility with the following options and sub-options:

* Package rules for deployment
* Generate rule reports
* Run rule tests

The utility is bundled with the Corticon JavaScript Studio installation in its `Utilities` directory.

| corticonJS.bat options                                                                                                                                                                                                                                                                                  |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <pre><code>usage: corticonJS
-c,--compile             compile a ruleflow into a decision service
-h,--help                print this message
-r,--report              generate the report for a Corticon asset
-t,--test                execute tests for a set of ruleflows or rulesheets</code></pre> |

| --compile options                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <pre><code>usage: compile
-b,--bundle &#x3C;name>     the name of the decision service bundle
-h,--help              print this message
-i,--input &#x3C;file>      ruleflow (.erf file) to compile
-o,--output &#x3C;folder>   folder to place the decision service Javascript bundle in
-p,--platform &#x3C;target platform> target platform (Azure, Browser, Google, Lambda, 
					Node, Progress Kinvey)	
-t,--top &#x3C;entities>   space separated list of entity names 
					that are expected at the root of the payload</code></pre> |

| --report options                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <pre><code>usage: report
-c,--css &#x3C;CSS file>         CSS file to use in report
-h,--help                   print this message
-i,--input &#x3C;file>           Corticon asset (.ecore, .ers, .erf, .ert) to report
-if,--image &#x3C;image folder>  image folder to copy to output folder
-o,--output &#x3C;folder>        folder to place the report files in
-p,--project &#x3C;project name> Corticon project name to use in report
-x,--xslt &#x3C;XSLT file>       XSLT file to use in report</code></pre> |

The files for generating reports are in your Corticon Work directory's `Reports` folder.

| --test options                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <pre><code>usage: test
-a,--all                          run all test sheets in the ruletest
-dj,--dependentjs &#x3C;dependentJS>   comma separated list of dependent javascript files
-h,--help                         print this message
-i,--input &#x3C;file>                 comma separated list of input (.ert) files to run, 
                                         wildcards allowed
-o,--output &#x3C;file>                file to contain output of test run
-s,--sheet &#x3C;Sheet names>          comma separated list of test sheets to run</code></pre> |

Note: The `test` option requires a valid JavaScript enabled license file (`CcLicense.jar`) in the `Utilities/lib` folder.
