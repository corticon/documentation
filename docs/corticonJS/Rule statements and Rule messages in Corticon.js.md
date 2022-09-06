# Rule statements and Rule messages in Corticon.js

In Studio you can add rule statements to rules. Rule statements allow you to add a message to individual rules that will be returned with the result payload from a call to the decision service. Rule statements allow you to capture "why" a decision was made. They are often used to debug rules or to capture an audit trail. Example:

![](https://progress-be-prod.zoominsoftware.io/bundle/corticon-js-integration/page/wbf1601641601822.image?_LANG=enus)

When these rules execute, they produce the corresponding types of rule messages:

![](https://progress-be-prod.zoominsoftware.io/bundle/corticon-js-integration/page/woz1601642070235.image?_LANG=enus)

## Configuration

Each of the target platform wrappers provide the information for implementing and managing rule messaging, as shown:

```
/*
	*******************************************************
	Configuration Properties for Rule Messages
	*******************************************************
	*/
	const configuration = {
		logLevel: 0,
		ruleMessages: {
			 executionProperties: {
				restrictInfoRuleMessages: true, 
				// If true Restricts Info Rule Messages
				restrictWarningRuleMessages: true, 
				// If true Restricts Warning Rule Messages
				restrictViolationRuleMessages: true, 
				// If true Restricts Violation Rule Messages
				
				restrictResponseToRuleMessagesOnly: true, 
				// If true the response returned has only rule messages
			},
		},
	};*/
```
## Setting a configuration

The syntax of a configuration might look like this when we want to suppress violation messages, and put messages in the log:

<table class="table frame-all" id="Rule-statements-and-Rule-messages-in-Corticon.js__id5"><caption></caption><colgroup><col style="width:100%"></colgroup><tbody class="tbody"><tr class="row rowsep-0"><td class="entry colsep-1 rowsep-1"><pre class="pre codeblock"><code>const configuration = {logLevel:0,ruleMessages: {restrictViolationRuleMessages:true,logRuleMessages:true} };</code></pre></td></tr></tbody></table>