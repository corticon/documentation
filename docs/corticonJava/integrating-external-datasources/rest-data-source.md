---
description: >-
  Corticon's REST Connector Enables Codeless, SQL-based Connectivity to REST
  Datasources
---

# REST Data Connectivity

The Corticon REST Datasource provides support for accessing REST services. It allows you to retrieve REST data to enrich the payloads being processed by your rules.

The Corticon REST Datasource uses the DataDirect [Autonomous REST Connector ](https://www.progress.com/connectors/autonomous-rest-connector)which provides the ability to access REST services as if they were databases. This is beneficial to a Corticon user because the process of mapping a vocabulary to a REST service is the same as for EDC and ADC data sources.

{% tabs %}
{% tab title="Converts JSON" %}
Autonomous REST Connector allows Corticon to see this:

`"Vehicles": [ { "VIN": "1B4HS28Y2WF108299", "Color": "Blue", "Make": "Honda", "Model": "Civic" },{ "VIN": "SAJWA2GE6CMV93625", "Color": "White", "Make": "Ford", "Model": "F150" },{ "VIN": "1FAHP2E87DG267888", "Color": "Red", "Make": "Tesla", "Model": "Model 3" }]`
{% endtab %}

{% tab title="into a Database Table" %}
{% hint style="success" %}
As this:  <img src="../../../.gitbook/assets/image (64).png" alt="" data-size="original">&#x20;
{% endhint %}
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Converts Nested JSON" %}
![Autonomous REST Connector allows Corticon to see this](<../../../.gitbook/assets/image (1).png>)
{% endtab %}

{% tab title="Into Multiple Tables with Stored Relations" %}
![As this](<../../../.gitbook/assets/image (7).png>)
{% endtab %}
{% endtabs %}

### Mapping vocabulary to a REST datasource

To configure the REST Datasource you either perform schema discovery or supply your own schema file. When using schema discovery, you supply the URL of the REST data source and query parameters and allow the Autonomous REST Connector to generate a schema for your REST service. To supply your own schema, you can either export a discovered schema from Corticon Studio and make edits or create one from scratch. See the[ Autonomous REST Connector documentation](https://docs.progress.com/bundle/corticon-data-integration/page/Overview-of-the-Autonomous-REST-Connector.html) for details on the its schema file format.

The query parameters for a REST Datasource can either be fixed or dynamically set by data in your payload. Dynamic setting of parameters allows you to access a REST service to retrieve information about a specific entity in your payload. You can also configure the security settings for accessing a REST service.

{% tabs %}
{% tab title="Import" %}
Create new entity instances from the JSON data&#x20;

_Example: retrieving reference data such as exchange rates which will be used in processing a set of purchase orders within a single execute request_
{% endtab %}

{% tab title="Retrieve" %}
Enrich existing entity instances with the JSON data&#x20;

_Example: enriching mortgage applicant data by retrieving their credit rating from a credit bureau_
{% endtab %}
{% endtabs %}

As REST access is limited to read-only, it is ideal for data enrichment. You could have one or several REST Datasources used by a decision service. You can even mix EDC or ADC with REST depending on your data access needs.

The wealth of REST data sources exposed through APIs means that you could be touching multiple sources to build the best complete data set possible. In marketing scenarios that might mean taking sparse info on a prospect from social or business contacts to enrich the data by discovering their profile and preferences to focus campaigns and assign local reps for follow-up. In medical applications, diagnoses and treatments can be enriched with claims approval histories or related clinical trials. For mortgage lenders, quickly scanning multiple credit review resources for a prospect, and then matching their home value and loan to retrieve the best rate from multiple lenders.

### Webinar: Integrate REST API Data into Your Business Rules with Corticon 6

{% embed url="https://www.youtube.com/watch?v=kRx5JgHXGDU&list=PLC679RvCan2CoOLaYQzUEriM3WS-UFQ5N&index=3" %}



#### To learn more, see [Getting Started with REST](https://docs.progress.com/bundle/corticon-data-integration/page/Getting-Started-with-REST.html) on Corticon Information Hub.
