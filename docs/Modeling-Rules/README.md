# Corticon Studio Basics

Corticon Studio is a standalone desktop environment to model, analyze, test, and save business rules as executable decision services. Corticon ‘rule modelers’ are commonly business analysts with expertise in the business domain and its policies, using Corticon Studio to define, author, analyze and test rules.

Once satisfied, rules are then deployed as Decision Services onto Corticon Server or as serverless functions with Corticon.js.

There are four key steps of building rules in Corticon Studio, culminating as a RuleFlow to deploy as a Decision Service.

1. The first step of the rule modeling process with Corticon is to build the 'dictionary' of business terms used throughout the rules, the **Rule Vocabulary**.
2. **Rulesheets** are like Decision Tables. Users ‘model’ the business rules by defining actions to take when specific conditions are met.
3. Once the rules created in the rulesheet are satisfied, the first **Ruletest** in Corticon Studio can be created to run test data through the rules in the test server embedded in the local application.
4. From here, you can continue adding more rules to the rulesheet, or more commonly, compartmentalize our rules into different rulesheets, and create a  **Ruleflow** to specify the sequence from one rulesheet to another. When multiple Rulesheets are included in a Ruleflow, the Rulesheets will execute in a sequence determined by their Rulesheet order in the Ruleflow.

# Rule Vocabulary

## What is a Vocabulary?

The first step of the rule modeling process with Corticon is to build the 'dictionary' of business terms used throughout the rules, the Rule Vocabulary.

For example, a transport company may have a rule that determines how much cargo each type of vehicle can carry. There are two key business terms used in this rule—cargo and vehicle. You could define these terms as entities in your Vocabulary. A Vocabulary is similar to a data model such as a [Unified Modeling Language ](https://www.uml.org/what-is-uml.htm)(UML) model or an Entity-Relationship model. The terms for the Vocabulary could come from a number of sources—database tables, forms used in business operations, policy and procedure documents, etc.

When you build a Vocabulary, you not only define the terms, you also define relationships between those terms. For example, a single vehicle can carry many cargo containers, implying a one-to-many relationship. You would define this as an association in your Vocabulary.

The rule vocabulary can be created manually, or it can be auto generated based on an external data source, the schema of any relational database, or the JSON structure of a REST endpoint.

![](../../assets/pop-from-json.png)

## Building a Corticon Vocabulary

Business terms are represented in the Vocabulary as either **entities** or **attributes**.

![](../../assets/vocab-overview.png)

An attribute is like a data field that holds a value. An entity is a collection of attributes. For example, the term cargo may have data fields such as cargoID, weight, volume, etc. So, cargo should be defined as an entity in a Vocabulary and the terms cargo ID, weight, and volume should be defined as attributes that belong to the entity cargo.

Relationships between entities are represented as associations in a Vocabulary. For example, since a vehicle can carry multiple cargo containers, you could create a one-tomany association between the vehicle entity and the cargo entity in a Vocabulary.

## The Vocabulary Tree

In Corticon Studio, the Vocabulary is represented as a hierarchical tree.

The top-most level, or root node of the tree, is the name of the Vocabulary. It is denoted by an ‘open book’ icon (Cargo in the example).

One level under the Vocabulary name are entities. Entities are denoted by a ‘golden box’ icon (Aircraft, Cargo, FlightPlan). Each entity name must be unique in the Vocabulary.

A level below each entity are its attributes. Each attribute has a name, a data type, and a few other properties. It is denoted by a golden box icon with a green bar in the middle (aircraftType, maxCargoVolume, etc).

Finally, associations are at the same hierarchical level as attributes. The associated entity is displayed in parentheses. The association icon changes based on the type of association. Since the Cargo entity has a many-to-one relationship with the FlightPlan entity, the icon is multiple bars converging into a single horizontal bar. The FlightPlan to Cargo association shows a reverse of the icon (a single bar diverging into multiple bars).

> There are four types of associations:
> * One-to-many—for example, if a vehicle can contain many cargo containers, from the perspective of the Vehicle (source) entity, the relationship with the Cargo (target) entity is one-to-many. A one-to-many association’s icon is a single bar diverging into multiple branches.
> * Many-to-one—for example, from the perspective of the Cargo (source) entity, the relationship with the Vehicle (target) entity is many-to-one. A many-to-one association’s icon shows multiple branches converging into a single bar.
> * One-to-one—for example, if a vehicle can have only one driver, the relationship is one-to-one. This is true from both perspectives. A one-to-one association’s icon is a single bar.
> * Many-to-many—for example, multiple workers may be assigned to load multiple vehicles through the workday. Each worker may load multiple vehicles, and each vehicle may have multiple workers assigned to load it. A many-to-many association’s icon shows multiple branches converging to a point from both sides.


Note that the vocabulary includes every data point involved in the decision/calculation. Some of this data may be passed into the Decision Service when it is called by another application, some of this data may be [retrieved](https://docs.progress.com/bundle/corticon-data-integration/page/Why-your-rules-might-want-to-access-external-data.html) by Corticon from an external data source and some of this data may be produced as a result of the rules themselves.

## Custom Data Types

Corticon provides rule modelers with 'base' datatypes (Integer, Decimal, String, Date, Time, DateTime, and Boolean) via a dropdown when building the vocabulary.

You can also define a Custom Data Type based on one of these Base data types. A Custom Data Type enables you to predefine what values can be assigned to an attribute.

You define Custom Data Types in the Custom Data Types tab. You access the Custom Data Types tab by opening a Vocabulary file and clicking on the Vocabulary name, as shown in the image.

### Enumerated Custom Data Types

A specific list of acceptable values. For example, in the transport company scenario, you may want to limit the acceptable values for the `Aircraft.aircraftType` attribute to 747, 777, and 787. You can achieve this by: – Defining a Custom Data Type that is based on the String data type, – with the values ‘747’, ‘777’, and ‘787’, and, – configure the `aircraftType`attribute to use this Custom Data Type.

![](../../assets/enumDataType.png)

### Constrained Custom Data Types
A constrained Custom Data Type enables you to limit acceptable values through a constraint expression. The constraint expression must include the special term value.

For example, if you want to define a Custom Data Type that constrains the value of an attribute to less than 10,000, the constraint expression would be value < 10000.

![](../../assets/constraint-cdt.png)

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

## Localization

Corticon Studio enables you to localize Vocabulary terms. This is useful if there are multiple rule modelers who are responsible for developing or maintaining the rule model and they speak different languages.

![](../../assets/local.png)

To localize Vocabulary terms, you open the Localization panel (select Vocabulary > Localize), select the desired language or languages in the Locale section of the panel, and then manually enter the localized word for each term as shown in this image.

# Rulesheets

## Parts of a Rulesheet

**Rulesheets** are like Decision Tables. Users 'model' the business rules, where the rule is like an ‘if-then’ statement. Each rule consists of one or more conditions (if) that are associated with one or more actions (then).

Here is an example of a Rulesheet with three rules. The Rulesheet editor has the following parts:

![](../../assets/rulesheet-highighted.png)


* **Conditions**—where you define the conditions for each rule. For example, `Aircraft.aircraftType` = 747. The condition value could be a single value (747), a set of values (747, 777, 787), or a range of values (weight=100000..200000).
* **Actions**—where you define the actions that need to be triggered when the conditions are satisfied. For example, `Aircraft.maxCargoWeight`=150000.
* **Rule columns**—the highlighted columns in this image. Each column represents a rule. It associates a set of conditions with a set of actions. For example, column 1 defines the rule—if the aircraft is a 747, then its maximum cargo weight is 150,000.


The terms `Aircraft.aircraftType` and `Aircraft.maxCargoWeight` come from the Rule Vocabulary. Each Rulesheet must be linked to a Rule Vocabulary.

Corticon evaluates all the conditions in each rule. If all the conditions in the rule are satisfied, the actions in the rule are triggered. 

_Note: If an action does not execute for some reason, Corticon still tries to execute the other actions in the rule._

## Rule Statements

Each rule is documented with **Rule Statements**. Rule Statements will be sent along with the new/changed data resulting from the rules in the response from Corticon back to the calling application. Rule statements will only be sent back to the calling application if that rule was triggered as part of that decision's execution.

Note that you can define multiple rule statements for a single rule. For example, one rule statement can document the rule, while another is sent as part of the output message when the rule fires

![](../../assets/rule-statements.png)

## Rule Operators

When you use your Vocabulary to build rules, you also make use of rule operators such as =, <, and . Corticon Studio provides a rich set of predefined rule operators in the Rule Operators view. By default, this view is located at the bottom-left of the Corticon Designer perspective.

The Rule Operators view organizes operators into folders based on their function and purpose. For example, the Attribute Operators folder contains subfolders for different data types. The folder for each data type contains rule operators that you can use when defining rules that use attributes of that data type.

You can learn about each rule operator in the Rule Operators view by hovering the mouse pointer over it. A tooltip appears, describing the rule operator, as shown in this image. The Rule Language Guide in the documentation set provides details of all rule operators available in Corticon Studio.

![](../../assets/rule-operators.png)

---

## Logical Integrity Checks

_Instead of having to find problems during user acceptance testing or production, Corticon enables you to find them during the design or development phase, which saves you time and money._

Rulesheets  provide rule modelers with multiple click-of-a-button **Logical Integrity Checks** which identify incompleteness, conflict between rules, and infinite loops. For example, the rule completeness check on the below rule sheet reveals scenarios which are plausible based upon the rules we have thus far.

### Rule Conflicts


A conflict occurs when two or more rules overlap in some way. They have condition expressions that apply to the same input data in some scenarios, but have different actions that need to be performed on that data. For example, consider the following rules:

* A person who is less than or equal to 55 years of age has a low risk rating.
* A person who is a skydiver has a high risk rating.

These rules conflict with each other because a person who is, for instance, 45 years old and also a skydiver, satisfies the conditions of both the rules. So which rule fires?

In Corticon, if two or more rules are in conflict, and data is received that satisfies the conditions of all the conflicting rules, they all fire.

However, the rules do not fire concurrently. They fire in a sequence. The rule that fires first updates the value of the attribute or attributes at the center of the conflict (in this example riskRating). The rule that fires next updates the value of the attribute or attributes again and so on until the last conflicting rule fires and the attribute is sent in an outgoing response message.

In addition, all rule statements linked to the rules that fire are sent as rule messages in the response message. In this example, instance 3 in the input data triggers the first rule (with the condition Person.age <= 55) first, which updates the riskRating value to low. However, it also triggers the second rule (with the condition Person.skydiver = true) which fires next and updates the value of the riskRating attribute to high. The output panel in the Ruletest reflects only the latest value.

Note that since all conflicting rules fire, all rule statements linked to the rules are sent as rule messages. If you look closely at the image of the Ruletest, you will see that instance 3 generates two rule messages—one for each rule fired.

#### Check and resolve conflicts in a Rulesheet


A conflict occurs when two or more rules overlap in some way. They have condition expressions that apply to the same input data in some scenarios, but have different actions that need to be performed on that data.

The rules in this Rulesheet conflict with each other because a person who is, for instance, 45 years old and also a skydiver, satisfies the conditions of both the rules.

![](../../assets/pre-con-check.png)

To perform a conflict check, open the Rulesheet, and click on the Check for Conflicts icon or select Rulesheet > Logical Analysis > Check for Conflicts.

#### Expand rules

When you define a rule in a Rulesheet, Corticon Studio creates sub-rules that address different scenarios that are within the boundaries of the rule. The sub-rules are hidden by default. However, you can view the sub-rules by expanding the ‘main’ rule.

To do this you must double-click the column number in the main rule. The sub-rules are numbered by adding a decimal point to the main rule’s column number (if the main rule is in column 1, the sub-rules are numbered 1.1, 1.2, 1.3, etc).
Each sub-rule addresses one scenario within the main rule. In this example, both rules are expanded. Consider the rule that verifies if a person is less than or equal to 55 years of age and assigns a low risk rating. Since, in this rule, it does not matter if the person is a skydiver, Corticon Studio identifies three scenarios1 within the rule:

![](../../assets/conflict-highlight.png)

* Where Person.age <= 55 and Person.skydiver = true (sub-rule 1.1)
* Where Person.age <= 55 and Person.skydiver = false (sub-rule 1.2)
* Where Person.age <= 55 and Person.skydiver = null (sub-rule 1.3)

Similarly, the rule that verifies if a person is a skydiver or not is expanded into three subrules. As you can see here, sub-rule 1.1 conflicts with sub-rule 2.1. In this case, the conflict is quite clear—the condition expressions in these rules are the same but the action is different. Sub-rules give you clarity about the cause of the conflict. Based on this, you can decide what steps to take to resolve the conflict.

Conflicts are not necessarily wrong. Whether or not you have to resolve them depends on their context and the business requirement. Only the domain or subject matter expert responsible for articulating the rules will know for sure.

If you do need to resolve the conflicts, you can choose to do one of the following things:

* Delete one or more of the conflicting rules until there are no conflicts in the Rulesheet.
* Modify the condition or actions to resolve the conflict.
* Specify overriding behavior.

Again, how you choose to resolve a conflict depends on the context and business requirements.

#### Specify overriding behavior


You can specify one rule to override another if they are in conflict. During testing or in production, if data satisfies the conditions in both rules, only the rule that overrides the other will fire. To specify overriding you must:

1. Identify which rule or sub-rule you want to ‘keep’ and which rule or sub-rule you want to override.
2. Click the Overrides cell in the rule column of the rule or sub-rule that you want to keep. A drop-down list appears, displaying a list of all rules or sub-rules in the Rulesheet that can be overridden.
3. Select the rule or sub-rule that you want to override.


### Rule completeness

Typically, you define multiple rules in the same Rulesheet because they have something in common. They address different aspects of a decision point, for example, risk rating in the insurance underwriting exercise. The rules cover different aspects of the decision— what risk rating to give to a person based on criteria such as the age of the person, whether the person is a skydiver or not, etc.

Based on the rules that you define, Corticon Studio detects if any scenarios are missing. For instance, if you have defined that a person less than or equal 55 years of age has a low risk, Corticon Studio detects that the scenario “greater than 55” is missing.

Corticon Studio has a built-in completeness checking algorithm that calculates the set of all possible mathematical combinations of all values in all conditions. The algorithm then compares this set of possible combinations to those already specified in the Rulesheet and detects missing combinations.

![](../../assets/comp.png)

#### Check and resolve incomplete rules

To perform a conflict check, open the Rulesheet, and click on the Check for Completeness icon or select Rulesheet > Logical Analysis > Check for Completeness.

After you run a completeness check, either of the following may happen:

* If there are no missing scenarios, Corticon Studio displays a dialog box indicating that the Rulesheet is complete and no new rules are added.
* If there are missing scenarios, Corticon Studio:
  * Displays a dialog box indicating the number of missing scenarios found and the number of rules added.
  * Highlights the newly added rules in green, as shown in the image.

You can expand and view the sub-rules of the newly added rules. Examine these subrules and see if the missing scenarios that they address are valid or not.

#### Act on newly added rules

Like a conflict, incompleteness is not necessarily wrong—only a subject matter expert can decide. For example, consider a Rulesheet with rules that determine fetal risk for pregnant women. Suppose the gender attribute used in these rules is an enumerated custom data type with two possible values—male and female. You may define rules for scenarios where the value of the gender attribute is female, but Corticon Studio will detect missing scenarios for the value male.

You can resolve incompleteness in one of the following ways:

* If the newly added rules suit your requirements, you can keep them.
* If they don’t meet your requirements you can:
  * Delete them, or,
  * Disable them, and write rule statements to document the scenarios.

#### Disable rules

Sometimes you may want to keep newly added rules in a Rulesheet but only for reference so that you know which scenarios you want to leave out of the decision-making process. You can disable a rule by right-clicking the column number and selecting Disable. You can optionally write a rule statement and link it to the disabled rule to document the scenario.

### Rulesheet optimization

Typically, you do not have to worry about optimizing Rulesheet execution because both rule compilation and rule execution are efficient and fast. The only time you should consider optimizing a Rulesheet is:

* When it contains a very large number of columns, and,
* You want rules to be processed in the fastest possible time.

The way to optimize a Rulesheet is by compressing rules. You compress rules by clicking the Compress Rules icon in the Rulesheet.

Compression creates hyphens wherever possible in rule column cells by looking for overlap among rule columns with specific data and summarizing them into fewer columns. Compressing Rulesheets helps improve efficiency, but does not affect a Rulesheet’s logical operation. Note, however, that compressing a Rulesheet can change the way columns look and possibly make them less familiar to you and harder to maintain.


#### Identifying dependencies in the Rulesheet


The Logical Dependency Graph is a flowchart-like display of how rules in a Rulesheet execute and which attributes are updated at which point in the execution process.

The Logical Dependency Graph is contained in a GIF file. You open it by selecting Rulesheet > Logical Analysis > Logical Dependency Graph.

The Logical Dependency Graph displays attributes in elliptical shapes and rule column numbers in squares. Arrows link the attributes and squares, denoting the sequence in which the rules execute and in which the attributes acquire their values, either from rule execution or from input data.

Generally, if an attribute does not have an arrow leading to it, it means the value of that attribute is retrieved from input data. An arrow from an attribute to a rule means that the value of the attribute is passed to the rule, which then processes the value in some way. An arrow from a rule to an attribute means that the attribute value is assigned or updated as a result of the rule firing.

So how do you spot dependencies in the Logical Dependency Graph? If rules are in the same logical path or chain—where the chain of arrows eventually lead from one rule to the other—there is dependency. The first rule in a chain is an independent rule. All rules that follow are dependent.

#### Execution Sequence Diagram

The Execution Sequence Diagram displays the order in which rules are executed based on the logic in the Rulesheet.

The Execution Sequence Diagram is contained in a GIF file. You open it by selecting Rulesheet > Logical Analysis > Execution Sequence Diagram.

Dependent rules fire in a sequence that is different from independent rules. So by taking a quick glance at the Execution Sequence Diagram you should be able to tell if there are any dependent rules.

The best way to use the Execution Sequence Diagram and the Logical Dependency Graph is to first check the diagram for anomalies and then inspect the graph to understand where the dependencies exist.

### Loops

To help identify inadvertent loops, Corticon Studio provides a Check for Logical Loops tool in the Corticon Studio toolbar. The tool contains a powerful algorithm that analyzes dependencies between rules on the same Rulesheet, and reports discovered loops to the rule modeler. For the Loop Detector to notice mutual dependencies, a Rulesheet must have looping enabled using one of the choices described earlier.

Clicking the Check for Logical Loops icon displays a window that describes the mutual dependencies found on the Rulesheet. To illustrate loop detection, we will use a few of the same examples from before.

![Example of an Infinite Single-Rule Loop
](../../assets/looping.png)

When applied to a Rulesheet containing just the single-rule loop shown in this figure, the Check for Logical Loops tool displays the following window:
Figure 2. Checking for Logical Loops in a Rulesheet
Figure 3. A Single-Rule Loop Detected by the Check for Logical Loops Tool

The Check for Logical Loops tool first lists rules where mutual dependencies exist. Then, it lists the distinct, independent loops in which those rules participate, and finally it lists where self-triggering rules exist (if any). In this simple single-rule loop example, only one rule contains a mutual dependency, and only one loop exists in the Rulesheet.

Note: The Check for Logical Loops tool does not automatically fix anything, it just points out that our rules have loops, and gives us an opportunity to remove or modify the offending logic.

# Ruletests

## Ruletests Overview

A Ruletest simulates a business scenario where the rules are applied to input data. If the data satisfies all the conditions in a rule, the rule fires and some output containing the results of the rule execution is produced.

You can define different sets of input data to test how the rules behave in different scenarios. You can also use a Ruletest to compare the output of a rule execution with expected results.

A Ruletest stores this information in a Ruletest file, enabling you to save use-cases that are of interest, change rules, and run the test again to see how the modified rules behave when applied to the same use-cases.

Take a close look at the images. Here is an example of a Rulesheet (`AircraftRules.ers`) with two rules and a Ruletest (`TestingAircraftRules.ert`) that has been executed.

![](../../assets/rulesheet-highighted.png)

![](../../assets/ruletest-output-vs-expected.png)

## The Ruletest editor

The Rulesheet has rules that define a value for `Aircraft.maxCargoWeight` based on the value of `Aircraft.aircraftType` received in input data.

The Ruletest tests the Rulesheet. The Ruletest editor has four parts:

* **Test Subject**—specifies which Rulesheet or Ruleflow is being tested (in this case `AircraftRules.ers`).
* **Input**—where you define input data to be processed by the rules in the Rulesheet. In this example, there are two instances of the Aircraft entity with different values for `Aircraft.aircraftType`.
* **Output**—where Corticon Studio displays the result of a Ruletest execution. As you can see, a value for `Aircraft.maxCargoWeight` has been assigned based on the rules in the AircraftRules.ers Rulesheet.
* **Expected**—where you can optionally define the result that you expect.


## When you run a Ruletest

![](../../assets/rule-messages.png)

1. Input data is processed by the rules in the Rulesheet.
2. If the input data satisfies all the conditions in one or more rules, those rules fire. The Ruletest then displays output that could include the same data as the input but with changed values, and/or additional data and values.
3. If the input data does not trigger any rules, the Ruletest displays the unchanged input data as the output.
4. f you specify expected results for a test, the Ruletest automatically compares the output with the expected results and displays any differences through color-coding

The Ruletest reproduces how the rules will behave once deployed as a decision service. At runtime, decision service invocations can take different formats such as XML, JSON, Java, or .NET objects.

A fully formatted sample request in each form can be exported from the ruletest. This provides visibility to the data structure that Corticon expects and can also be copied into third party testing applications such as Postman, Insomnia, or SoapUI as test message parameters.


## How to link a rule statement to multiple rules


Using dynamic data, you can create a single rule statement that describes multiple rules. You can then link the rule statement to each of the rules. When any of the rules fire, attribute names will be replaced by actual values in the rule message.

# Ruleflows

## Building a Ruleflow

From here, you can continue adding more rules to the rulesheet, or more commonly, compartmentalize our rules into different rulesheets, and create a **Ruleflow** to specify the sequence from one rulesheet to another. When multiple Rulesheets are included in a Ruleflow, the Rulesheets will execute in a sequence determined by their Rulesheet order in the Ruleflow. With ruleflows, behavior like branching into separate rules for different scenarios can be defined and specify when the execution of a given Decision Service call that Corticon should retrieve additional data from external datasources.

![](../../assets/ruleflowBreakdown.png)

As more rulesheets are added to our Ruleflow, Ruletests can be run against entire Ruleflows, instead of testing only the Rulesheets as they are developed. This enables you to test not only the rules as they are defined in the Rulesheet, but also how the Ruleflow works, and how the rules behave as part of the Ruleflow. This way, problems can be detected and fixed earlier in the lifecycle.

![](../../assets/multi-branch.png)


## Ruleflow Properties

Ruleflows are the final step in the rule development process and are thus deployed as Decision Services. Ruleflows can always be versioned as well, with either a major/minor version tag or effective date range for which they will execute when invoked. The invocation (request) payload must contain a version number or data parameter to consume the desired "versioned" decision service.

![](../../assets/ruleflow-props.png)

## Test Ruleflows using Ruletests

You can test a Ruleflow using a Ruletest just as you use it to test a Rulesheet. When you test a Ruleflow in a Ruletest, the input data that you define is processed by the first Rulesheet in the Ruleflow’s sequence. After the first Rulesheet completes executing, its output becomes the input to the next Rulesheet in the sequence, and so on, until the last Rulesheet completes executing.

The Output pane then displays the final output of the Ruleflow. The Rule Messages view displays all rule messages that are created as a result of rules firing in each Rulesheet.

To test a Ruleflow using a Ruletest, you must select the Ruleflow as the Ruletest’s test subject either while creating the Ruletest or by modifying the Test Subject property in the Ruletest editor.

## Advanced Ruleflow features

* **Nested Ruleflows**—you can reduce the complexity of large Ruleflows by breaking them into smaller, ‘child’ Ruleflows and adding them to the parent Ruleflow, referred to as “a Ruleflow in a Ruleflow.”
* **Conditional Branching**—you can create branches in a Ruleflow, where the value of an attribute determines which branch the data is routed to.
* **Subflows**—you can configure an Iteration for a Subflow to enable looping behavior.
* **Versioning**—you can assign Major and Minor Version number that the Server responds correctly to requests for the different versions.
* **Effective Dates**—you can have identically named Ruleflows with slight variations that respond to requests only when in the specified date range.
* **Service Call-outs**—you can access Datasources to enrich your rules, and update databases

[](/docs/assets/branching-node.png)