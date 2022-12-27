# Rulesheets

You define your rule logic in a Corticon Rulesheet. A rule is like an ‘if-then’ statement.
Each rule consists of one or more conditions (if) that are associated with one or more
actions (then).
Here is an example of a Rulesheet with three rules. The Rulesheet editor has the following
parts:

![Alt text](../assets/BasicRuleModeling_Lessons1.png)


- Conditions—where you define the conditions for each rule. For example, Aircraft.aircraftType = 747. The condition value could be a single value (747), a set of values (747, 777, 787), or a range of values (weight=100000..200000).
- Actions—where you define the actions that need to be triggered when the conditions are satisfied. For example, Aircraft.maxCargoWeight=150000.
- Rule columns—the highlighted columns in this image. Each column represents a rule. It associates a set of conditions with a set of actions. For example, column 1 defines the rule—if the aircraft is a 747, then its maximum cargo weight is 150,000.

The terms Aircraft.aircraftType and Aircraft.maxCargoWeight come from the Rule Vocabulary. Each Rulesheet must be linked to a Rule Vocabulary.
Corticon evaluates all the conditions in each rule. If all the conditions in the rule are
satisfied, the actions in the rule are triggered. 

Note: If an action does not execute for some reason, Corticon still tries to execute the other actions in the rule

## Defining rules in a Rulesheet

![Alt text](../assets/BasicRuleModeling_Lessons4.png)

To define rules in the Rulesheet, you:
-  Drag and drop Vocabulary terms for conditions and actions as follows:
    1. Select the Vocabulary term from the Rule Vocabulary view.
    2. Drag and drop the term to the next empty cell in the Conditions or Actions pane. Each Vocabulary term must go into a separate row.
-  Specify condition and action values for each rule in the rule columns as follows:
    1. Double-click the cell that corresponds with the Vocabulary term.
    2. Enter the value.

When you specify a value in a rule column cell, the equality operator is implied. For example, when you enter 747 in column 1 as shown here, it means (if) Aircraft.aircraftType = ‘747’


## Rule Statements

![Alt text](../assets/BasicRuleModeling_Lessons3.png)

A rule statement serves the following purposes:
- Writing the rule in plain or informal language enables you to articulate the rule quickly and prepares you for the next step—defining the rule formally. You can also use the rule statement to identify Vocabulary terms that you need in the rule.
- The rule statement can be made a part of the output message sent by Corticon when the rule fires. The rule statement describes the rule, so users can understand the action or actions that are triggered by the rule by reading the rule statement in the output message.
- Finally, a rule statement is a way to document a rule so that stakeholders can understand its purpose and logic by reading the rule statement. 

Note that you can define multiple rule statements for a single rule. For example, one rule statement can document the rule, while another is sent as part of the output message
when the rule fires. Follow these steps to create a rule statement:
1. Open the Rulesheet in Corticon Studio. The Rule Statements view becomes active
2. The Rule Statements view comprises several rows and columns. To create the rule statement, double-click a cell in the column named Text and type the rule statement
