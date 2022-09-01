# Rule Vocabulary

### What is a Vocabulary?

The first step of the rule modeling process with Corticon is to build the 'dictionary' of business terms used throughout the rules, the Rule Vocabulary.&#x20;

For example, a transport company may have a rule that determines how much cargo each type of vehicle can carry. There are two key business terms used in this rule—cargo and vehicle. You could define these terms as entities in your Vocabulary. A Vocabulary is similar to a data model such as a [Unified Modeling Language ](https://www.uml.org/what-is-uml.htm)(UML) model or an Entity-Relationship model. The terms for the Vocabulary could come from a number of sources—database tables, forms used in business operations, policy and procedure documents, etc.&#x20;

When you build a Vocabulary, you not only define the terms, you also define relationships between those terms. For example, a single vehicle can carry many cargo containers, implying a one-to-many relationship. You would define this as an association in your Vocabulary.&#x20;

The rule vocabulary can be created manually, or it can be auto generated based on an external data source, the schema of any relational database, or the JSON structure of a REST endpoint.

![](../../../.gitbook/assets/image005.png)

### Building a Corticon Vocabulary

Business terms are represented in the Vocabulary as either **entities** or **attributes**.

An attribute is like a data field that holds a value. An entity is a collection of attributes. For example, the term cargo may have data fields such as cargoID, weight, volume, etc. So, cargo should be defined as an entity in a Vocabulary and the terms cargo ID, weight, and volume should be defined as attributes that belong to the entity cargo.


Relationships between entities are represented as associations in a Vocabulary. For example, since a vehicle can carry multiple cargo containers, you could create a one-tomany association between the vehicle entity and the cargo entity in a Vocabulary.

### The Vocabulary Tree

In Corticon Studio, the Vocabulary is represented as a hierarchical tree.

The top-most level, or root node of the tree, is the name of the Vocabulary. It is denoted by an ‘open book’ icon (Cargo in the example).

One level under the Vocabulary name are entities. Entities are denoted by a ‘golden box’ icon (Aircraft, Cargo, FlightPlan). Each entity name must be unique in the Vocabulary.

A level below each entity are its attributes. Each attribute has a name, a data type, and a few other properties. It is denoted by a golden box icon with a green bar in the middle (aircraftType, maxCargoVolume, etc).

![](../../assets/image%20(43).png)
Finally, associations are at the same hierarchical level as attributes. The associated entity is displayed in parentheses. The association icon changes based on the type of association. Since the Cargo entity has a many-to-one relationship with the FlightPlan entity, the icon is multiple bars converging into a single horizontal bar. The FlightPlan to Cargo association shows a reverse of the icon (a single bar diverging into multiple bars).


> There are four types of associations:

> * One-to-many—for example, if a vehicle can contain many cargo containers, from the perspective of the Vehicle (source) entity, the relationship with the Cargo (target) entity is one-to-many. A one-to-many association’s icon is a single bar diverging into multiple branches.
> * Many-to-one—for example, from the perspective of the Cargo (source) entity, the relationship with the Vehicle (target) entity is many-to-one. A many-to-one association’s icon shows multiple branches converging into a single bar.
> * One-to-one—for example, if a vehicle can have only one driver, the relationship is one-to-one. This is true from both perspectives. A one-to-one association’s icon is a single bar.
> * Many-to-many—for example, multiple workers may be assigned to load multiple vehicles through the workday. Each worker may load multiple vehicles, and each vehicle may have multiple workers assigned to load it. A many-to-many association’s icon shows multiple branches converging to a point from both sides.


Note that the vocabulary includes every data point involved in the decision/calculation. Some of this data may be passed into the Decision Service when it is called by another application, some of this data may be [retrieved](https://corticon.github.io/Corticon\_Enablement/Runtime/Server/Data/) by Corticon from an external data source and some of this data may be produced as a result of the rules themselves.

### Custom Data Types

Corticon provides rule modelers with 'base' datatypes (Integer, Decimal, String, Date, Time, DateTime, and Boolean) via a dropdown when building the vocabulary.

You can also define a Custom Data Type based on one of these Base data types. A Custom Data Type enables you to predefine what values can be assigned to an attribute.

You define Custom Data Types in the Custom Data Types tab. You access the Custom Data Types tab by opening a Vocabulary file and clicking on the Vocabulary name, as shown in the image.


#### Enumerated Custom Data Types

A specific list of acceptable values. For example, in the transport company scenario, you may want to limit the acceptable values for the `Aircraft.aircraftType` attribute to 747, 777, and 787. You can achieve this by: – Defining a Custom Data Type that is based on the String data type, – with the values ‘747’, ‘777’, and ‘787’, and, – configure the `aircraftType`attribute to use this Custom Data Type.


#### Constrained Custom Data Types

A constrained Custom Data Type enables you to limit acceptable values through a constraint expression. The constraint expression must include the special term value.

For example, if you want to define a Custom Data Type that constrains the value of an attribute to less than 10,000, the constraint expression would be value < 10000.

Bear in mind the following when you define constraint expressions:

* You can use logical connectors such as AND and OR.
* You can use parentheses to form more complex expressions.
* You can use attribute operators that are compatible with the Base data type.
* You cannot use null or collection operators.

Here are a few examples of constraint expressions:

| Constraint Expression                                                           | Meaning                                                                                                          |
| ------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------- |
| value > 5                                                                       | Integer values greater than 5                                                                                    |
| value >= 10.2                                                                   | Decimal values greater than or equal to 10.2                                                                     |
| value in (1.1..9.9]                                                             | Decimal values between 1.1 (exclusive) and 9.9 \[inclusive]                                                      |
| <p>value in ['1/1/2000 12:30:00 PM'..<br>'1/2/2000 11:00:00 AM')</p>            | <p>DateTime values between '1/1/2000 12:30:00 PM'<br>[inclusive] and '1/2/2000 11:00:00 AM' (exclusive)</p>      |
| value in \['1:00:00 PM'.. '2:00:00 PM']                                         | <p>Time values between '1:00:00 PM' [inclusive] and<br>'2:00:00 PM' [inclusive]</p>                              |
| <p>value.size >= 6 and<br>(value.indexOf(1) > 0 or<br>value.indexOf(2) > 0)</p> | <p>String values of minimum 6 characters in length, whose<br>first or second characters are positive numbers</p> |

![](<../../../.gitbook/assets/image (76).png>)

After you define a Custom Data Type, you can apply the Custom Data Type to attributes.

![](<../../../.gitbook/assets/image (42).png>)

---
### Localization

Corticon Studio enables you to localize Vocabulary terms. This is useful if there are multiple rule modelers who are responsible for developing or maintaining the rule model and they speak different languages.

![](../../assets/image%20(120).png)

To localize Vocabulary terms, you open the Localization panel (select Vocabulary > Localize), select the desired language or languages in the Locale section of the panel, and then manually enter the localized word for each term as shown in this image.

