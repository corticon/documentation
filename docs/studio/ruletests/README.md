# Ruletests

## Ruletests Overview

A Ruletest simulates a business scenario where the rules are applied to input data. If the data satisfies all the conditions in a rule, the rule fires and some output containing the results of the rule execution is produced.&

You can define different sets of input data to test how the rules behave in different scenarios. You can also use a Ruletest to compare the output of a rule execution with expected results.

A Ruletest stores this information in a Ruletest file, enabling you to save use-cases that are of interest, change rules, and run the test again to see how the modified rules behave when applied to the same use-cases.


## When you run a Ruletest

1. Input data is processed by the rules in the Rulesheet.&
2. If the input data satisfies all the conditions in one or more rules, those rules fire. The Ruletest then displays output that could include the same data as the input but with changed values, and/or additional data and values.&
3. If the input data does not trigger any rules, the Ruletest displays the unchanged input data as the output.&
4. f you specify expected results for a test, the Ruletest automatically compares the output with the expected results and displays any differences through color-coding

The Ruletest reproduces how the rules will behave once deployed as a decision service. At runtime, decision service invocations can take different formats such as XML, JSON, Java, or .NET objects.&

A fully formatted sample request in each form can be exported from the ruletest. This provides visibility to the data structure that Corticon expects and can also be copied into third party testing applications such as Postman, Insomnia, or SoapUI as test message parameters.


## How to link a rule statement to multiple rules

Using dynamic data, you can create a single rule statement that describes multiple rules. You can then link the rule statement to each of the rules. When any of the rules fire, attribute names will be replaced by actual values in the rule message.

For example, suppose you have three rules, as shown in this image. Each of these rules specifies the maximum cargo weight for a certain type of aircraft. A single rule statement that embeds the aircraft tail number, the aircraft type, and the maximum cargo weight, can be used to cover all three rules.&
