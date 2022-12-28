### To populate a Vocabulary from a JSON payload:

An update generates new entities, attributes, and associations. The existing entities, attributes, and associations are not revised by regenerating over the existing Vocabulary. If you want one element to be regenerated, delete it before you perform the update. You could even delete the vocabulary entirely, and then start fresh. The original sample payload adds a requirement for Billing Address to the sampleCustomer Vocabulary.

```
{
    "orderId": 494748,
    "customer": "Acme Industries",
    "customerStatus": "elite",
    "governmentAgency": false,

    "shippingAddress": {
        "address1": "1234 Industrial Lane",
        "address2": null,
        "city": "Boston",
        "state": "MA",
        "zip": "01234"
    },
    "shippingDetails": {
        "expedite": true,
        "mode": "ground"
    },

    "products": [
        {
            "sku": "XYZ-BB-43",
            "unitPrice": 2300.00,
            "quantity": 2,
            "tags": [
                "industrial",
                "compressor"
            ]
        }
    ],
    "discount": 0.0
}				
```
When you regenerate your vocabulary from this JSON, it will add new entities, attributes and associations to your vocabulary for the new items in the JSON. The Vocabulary shows the added entity, attributes, and association:
![Alt text](../assets/regenerate.png)

### Integrating multiple sources into a Vocabulary

To build a single vocabulary that integrates multiple data feeds, it is convenient to import additional sources into separate vocabulary domains. Corticon enables you to import into an added domain without impacting the rest of the Vocabulary.

Consider a variation on the customer info so that it identifies a partner:

```
{
"orderId": 494749,
"partner": "Acme Partners",
"partnerStatus": "elite",
"shippingAddress": {
	"address1": "2000 Industrial Ave",
	"address2": null,
	"city": "Boston",
	"state": "MA",
	"zip": "01234"
},
"shippingDetails": {
	"expedite": true,
	"mode": "ground"
}
}
"discount": 25.0
}				
```
In the Vocabulary file, right-click at the root and then choose Add Domain:
![Alt text](../assets/domain.png)

Click on the new domain to refactor the name to Partners. 
![Alt text](../assets/partner%20domain.png)

Right-click on the Partners domain and then choose Populate Domain From JSON:
![Alt text](../assets/pop%20domain%20json.png)

Choose the file where the preceding listing was saved, and click Open.

The data is added to the Vocabulary.

Note that a reference to an attribute in an added domain requires the domain as a qualifier of the attribute when used in rules. In this example, the regular ShippingAddress.address1 in a Rulesheet would be differentiated from Partners.ShippingAddress.address1.
![Alt text](../assets/domain%20populated%20json.png)

