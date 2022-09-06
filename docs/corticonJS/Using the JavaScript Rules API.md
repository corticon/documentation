# Using the JavaScript Rules API 

All five platform wrappers have a lot in common. Their fundamental difference is the flow of the operations on each platform. Each of the `sample.js` wrappers is self-documented. The integration of the bundle with your JavaScript application is a simple API, not much more than a call to execute against the bundle. The following sample code is taken from the `node.sample.js` file:

1.  Include the generated rule bundle:

    ```
    const decisionService = require('./decisionServiceBundle');
    ```
2.  Get the JSON payload from your application:

    ```
    const payload = readPayload(payloadFileName);
    ```
3.  Set the configuration:

    ```
    const configuration = { logLevel: 0 };
    ```
4.  Execute the rules on the payload:

    ```
    const result = decisionService.execute(payload, configuration);
    ```
