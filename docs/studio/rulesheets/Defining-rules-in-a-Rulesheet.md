# Defining rules in a Rulesheet

![Alt text](../assets/BasicRuleModeling_Lessons4.png)

To define rules in the Rulesheet, you:

- Drag and drop Vocabulary terms for conditions and actions as follows:
  1. Select the Vocabulary term from the Rule Vocabulary view.
  2. Drag and drop the term to the next empty cell in the Conditions or Actions pane. Each Vocabulary term must go into a separate row.
- Specify condition and action values for each rule in the rule columns as follows:
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

![Alt text](../assets/statements.png)

You must explicitly link each rule statement with its rule. To link a rule statement with its rule, enter the number of the rule column in the rule statement's **Ref** cell.
If you only want to document the rule, you do not need to configure any other properties.
If you want to post the rule statement as part of the output message, configure these properties:

- **Post**: The Post property enables you to indicate the severity of the rule violation. You can select from three levels—Info, Warning, and Violation. Note that these severity levels are user-defined and have no special meaning in Corticon. You can define them to match your requirements.
- **Alias**: Specify the Vocabulary entity in the rule condition that you want displayed with the output message when there is a rule violation.

After you link a rule statement with a rule, when you select the rule statement in the **Rule Statements** view, the corresponding rule column is highlighted in orange. Similarly, if you select a cell or a group of cells within the rule column, the corresponding rule statement is highlighted in orange. This indicates that the rule statement and the rule are linked.

## Syntax for values in rule column cells

The values that you specify must conform to the following syntax:

- If the Vocabulary term’s data type is String, Date, DateTime, or Time, the corresponding value in the rule column must be enclosed in single quotes.

  - CORRECT: ‘apple’
  - INCORRECT: “apple”, apple
- If the Vocabulary term’s data type is Integer, the corresponding value must not be enclosed in quotes and it must not contain decimal points or delimiters.

  - CORRECT: 4, -4
  - INCORRECT: 4.0, ‘4’
- If the Vocabulary term is Decimal, the corresponding value can contain a decimal point, but the decimal point is optional. Commas are not allowed, and the value must not be enclosed in quotes.

  - CORRECT: 10, -10.0, 10.5
  - INCORRECT: 10,25, 1,025.00
- If the Vocabulary term is Boolean, the corresponding value can only be T, F, true, or false. The value must not be enclosed in quotes. The case does not matter.

  - CORRECT: t, F, FALSE
  - INCORRECT: ‘false’
