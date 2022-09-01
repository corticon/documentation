##### Rule Vocabulary
 An .ecore file is structured dictionary containing all necessary business terms and relationships between them used by the business rules. 
 
##### Rulesheet
A Rulesheet is a spreadsheet structure where you enter Conditions (IF statements), Actions (THEN statements), and values for them that define a rule in each column. An .ers file is a set of conditions and actions and plain language statements written from a common business Vocabulary. A Rulesheet is associated with one Vocabulary. Multiple Rulesheets can use the same Vocabulary.

##### Ruletest
Using Ruletests, you can submit request data as input to Rulesheets or Ruleflows to see how the rules are evaluated and the resulting output. You can make Ruletests even more powerful by specifying the results you expected, and then seeing how they reconcile with the output. Running the test against a specified Rulesheet or Ruleflow automatically compares the actual Output data to your Expected data, and color codes the differences for easy review and analysis.  An .ert file is a set of one or more Testsheets containing sample data used for testing Rulesheets and Ruleflows, all based on the same Vocabulary. While optional, they are the essence of Corticon's test-as-you-go structure.

##### Ruleflow
A Ruleflow is how Corticon assembles and organizes the components of a set of rules into a single unit. It is a presented as a flow diagram, where Rulesheets, Service Callouts, and even other Ruleflows depict the flow of the rule, allowing it to iterate and to branch. An .erf file is a set of one or more Rulesheets, embedded service call-outs, and other Ruleflows organized on a canvas for sequential execution. A Ruleflow is compiled into a versioned Decision Service.

##### Conflict Checker
Sometimes, conflicts may not be immediately visible just by looking at the rules. This is because each rule is actually made up of sub-rules (rules without dashes) and it is the sub-rules that are in conflict. To see these sub-rules, select Rulesheet > Rule Column(s) > Expand Rules. 