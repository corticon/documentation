# Rulesheets


Youdefine your rule logic in a Corticon Rulesheet.

Arule is like an ‘if-then’ statement. Each rule consists of one or more
conditions (if) that are associated with one or more actions (then).

The
Rulesheet
editor has the following parts:

Conditions—where
you define the conditions for each rule. For example, Aircraft.aircraftType = 747. The condition value could be a
single value (747), a set of values (777, 787), or a range of values.

Actions—where
you define the actions that need to be triggered when the conditions are
satisfied. For example, Aircraft.maxCargoWeight=150000.

Rule columns—each column represents a rule. It
associates a set of conditions with a set of actions.  For example, column 1 defines the rule—if
the aircraft is a 747, then its maximum cargo weight is 150,000.

Corticon evaluates all the conditions in each
rule. If all the conditions in the rule are satisfied, the actions in the rule
are triggered. If an action does not execute for some reason, Corticon
still tries to execute the other actions in the rule.
