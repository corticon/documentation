# Custom Data Types

Corticon uses seven basic data types: Boolean, Decimal, Integer, String, DateTime, Date, and Time. An attribute must use one of these types. You also have the option of creating custom data types that “extend” any one of these basic seven.

You define and maintain Custom Data Types in a Vocabulary by selecting the Vocabulary name in the tree view.

## Data Type Name

When defining a custom data type, you must give it a name with no blank spaces. The name must comply with standard entity naming conventions (see the Quick Reference Guide for details), and must not overlap (match) any of the base data types, any other custom data type names, or the names of any Vocabulary entities.

## Base Data Type

The selection in this field determines which base data type the custom data type extends.

You already used this feature in the custom data type `containerType`, a `String`, in the [Basic Rule Modeling Tutorial](https://docs.progress.com/bundle/corticon-rule-modeling/page/../../basic-corticon-tutorial/page/Tutorial-Basic-Rule-Modeling-in-Corticon-Studio.html) . The following figure lists its labels and values.

Figure 1. Vocabulary Editor Showing the Custom Data Type containerType

![](https://progress-be-prod.zoominsoftware.io/bundle/corticon-rule-modeling/page/vocabulary_editor.png?_LANG=enus)

## Enumeration or Constraint Expression?

Enumeration—When the Enumeration for a Custom Data Type is set to `Yes`, as shown in the preceding figure, the Constraint Expression field is disabled, and the Label and Value columns are enabled.

Constraint Expression—When the Enumeration for a Custom Data Type is set to `No`, the Constraint Expression field is enabled, and the Label and Value columns are disabled.

The following sections explore each of these features.

### Constraint Expressions

When you want to prompt Rulesheet and Ruletest designers to use a specific range of values for an attribute, a constraint expression will validate entries when the associated Ruletest runs.

Constraint expressions are optional for non-enumerated Custom Data Types, but if none are used, then the Custom Data Type probably is not necessary because it reduces to a base attribute with a custom name.

All **Constraint Expressions** must be `Boolean` expressions: they must return or resolve to a Boolean value of **`true`** or `false`. The supported syntax is the same as Filter expressions with the following rules and exceptions:

-   Use `value` to represent the Custom Data Type value.
-   Logical connectors such as `and` and `or` are supported.
-   Parentheses can be used to form more complex expressions
-   The expression can include references to Base and Extended Operators which are compatible with the Base Data Type chosen.
-   No Collection operators can be referenced in the expression.
-   There should be **no** references to `null`. This is because `null` represents a lack of value and is not a real value. The Constraint Expression is intended to constrain the value space of the data type, and expressions such as attribute `expression <> null` do not belong in it. An attribute that must not have a null value can be designated by selecting `Yes` in its **Mandatory** property value.

The following are typical Constraint Expressions:

| **Constraint Expression** | **Meaning** |
| --- | --- |
| value > 5 | Integer values greater than 5 |
| value >= 10.2 | Decimal values greater than or equal to 10.2 |
| value in (1.1..9.9\] | Decimal values between 1.1 (exclusive) and 9.9 (inclusive) |
| value in \[‘1/1/2014 12:30:00 PM’..’1/2/2019 11:00:00 AM’) | DateTime values between ‘1/1/2014 12:30:00 PM’ (inclusive) and ‘1/2/2019 11:00:00 AM’ (exclusive) |
| value in \[‘1:00:00 PM’..’2:00:00 PM’\] | Time values between ‘1:00:00 PM’ (inclusive) and ‘2:00:00 PM’ (inclusive) |
| value.size >= 6 and (value.indexOf(1) > 0 or value.indexOf(2) > 0) | String values of minimum 6 characters in length that contain at least a 1 or 2 |

### How to use non-enumerated Custom Data Types in Rulesheets and Ruletests

Non-enumerated custom data types use **Constraint Expressions** and do not cause Rulesheet drop-down lists to become populated with custom sets. Also, manually entering a cell value that violates the custom data type's **Constraint Expression** is **not** prohibited in the Rulesheet. For example, in the following figure, `weightRange` is defined as a non-enumerated custom data type with **Base Data Type** of `Decimal`.

Figure 1. Non-enumerated Custom Data Types

![](https://progress-be-prod.zoominsoftware.io/bundle/corticon-rule-modeling/page/yyl1598994749208.image?_LANG=enus)

Then, after assigning it to the Vocabulary attribute `Cargo.weight`, it is used in a Rulesheet Condition row as shown:

Figure 2. Using Custom Data Types in a Rulesheet

![](https://progress-be-prod.zoominsoftware.io/bundle/corticon-rule-modeling/page/aqy1598994770934.image?_LANG=enus)

Notice in the preceding figure that the `300000` entry violates the **Constraint Expression** of the custom data type assigned to `Cargo.weight`,  but _does not turn red or otherwise indicate a problem_. The indication comes when data is entered for the attribute in a Ruletest, as shown:

Figure 3. Violating a Custom Data Type's Constraint Expression

![](https://progress-be-prod.zoominsoftware.io/bundle/corticon-rule-modeling/page/peh1598994792951.image?_LANG=enus)

Notice that the small yellow warning icon ![](https://progress-be-prod.zoominsoftware.io/bundle/corticon-rule-modeling/page/warning_icon.png?_LANG=enus) indicates a problem in the attribute, entity, and both Ruletest tabs. Such an error is hard to miss.  Also, a Warning message will appear in the Problems tab (if open and visible) as shown. If the **Problems** tab is closed, you can display it by selecting Window > Show View > Problems from the Studio menubar.

Figure 4. Violating the Constraint Expression of a Custom Data Type

![](https://progress-be-prod.zoominsoftware.io/bundle/corticon-rule-modeling/page/xgo1598994816507.image?_LANG=enus)

A Warning does not prevent you from running the Ruletest. However, an Error, indicated by a small red icon ![](https://progress-be-prod.zoominsoftware.io/bundle/corticon-rule-modeling/page/red_icon.png?_LANG=enus), will prevent the Ruletest execution. You must fix any errors before testing.

[](https://docs.progress.com/bundle/corticon-rule-modeling/page/Constraint-Expressions.html)

### Enumerations
Enumerations are lists of strictly typed unique values that are the valid values for each attribute that is assigned the custom data type name as its data type. These lists also prompt Rulesheet and Ruletest designers to use a specific list of values. Enumerated lists, often referred to as _enums_, can be maintained directly in the Vocabulary, or retrieved and updated from a data source.

Each item list can be partnered with a unique _label_ that you select in Rulesheets and Ruletests.

Before you start setting up and using enumerations, you should get acquainted with labels and values.

Note: It is important that you determine whether you want to use labels, because changing a set of enumerations later to add or remove the labels data will affect any Rulesheets and Ruletests that use that custom data type's enumerations as you can observe in this topic.

At the Vocabulary root, you created a String enumeration with only values. The base data type can be any Corticon data type except Boolean. Every line requires a unique entry of its type, and the list must have no blank lines from the top down to the last line.

The following examples are String values. They can contain spaces and most other characters. It needs to be set off in plain single quotation marks. If you enter or paste text with the delimiters, they are added for you. Like this:

  
![](https://progress-be-prod.zoominsoftware.io/bundle/corticon-rule-modeling/page/ztg1462396896504.image?_LANG=enus)  

If you want to use labels, then the label is always a String of any alphanumeric characters but cannot contain spaces. Each must be unique and must have a corresponding value. Even when you use labels, the values must be unique.

  
![](https://progress-be-prod.zoominsoftware.io/bundle/corticon-rule-modeling/page/fiw1462396863586.image?_LANG=enus)  

Set `Glove.color` to use the `colorUnlabeled` data type:

  
![](https://progress-be-prod.zoominsoftware.io/bundle/corticon-rule-modeling/page/dod1462396926650.image?_LANG=enus)  

Set `Ball.color` to use the `colorLabeled` data type:

  
![](https://progress-be-prod.zoominsoftware.io/bundle/corticon-rule-modeling/page/mjd1462396912952.image?_LANG=enus)  

When you create a Rulesheet, the list offered at A1 contains the label (`Ball.color = red`) , while the list offered at B1 contains the value in qoutes (`Glove.color='red'`).

  
![](https://progress-be-prod.zoominsoftware.io/bundle/corticon-rule-modeling/page/kat1462396942454.image?_LANG=enus)  

You add Rule Statements so that you can see how the labeled and unlabeled items are handled.

In a simple Ruletest, add some size tests to see what happens. As shown, the labels and values in the resulting **Output** are both unquoted. The **Rule Messages** tab displays the value when the label was in use and the value of the value-only enumeration.

  
![](https://progress-be-prod.zoominsoftware.io/bundle/corticon-rule-modeling/page/ckm1462396959187.image?_LANG=enus)  

Entry of test values in the Ruletest list the label+value's label:

  
![](https://progress-be-prod.zoominsoftware.io/bundle/corticon-rule-modeling/page/fnz1462396970406.image?_LANG=enus)  

The value-only list has quoted values:

  
![](https://progress-be-prod.zoominsoftware.io/bundle/corticon-rule-modeling/page/ftv1462396985978.image?_LANG=enus)  

Both are reconciled to unquoted values in the displayed **Input** and **Output** columns:

  
![](https://progress-be-prod.zoominsoftware.io/bundle/corticon-rule-modeling/page/ijp1462396998150.image?_LANG=enus)  

Note: It is important that you determine in each custom data type whether you want to use labels. Some enumerations can have labels while others do not. Changing a set of enumerations later, to add or remove the labels data, affects any Rulesheets and Ruletests that use that custom data type's enumerations as you can observe in this topic.

#### Enumerations defined in the Vocabulary

To set up an Enumeration, open the project's Vocabulary, and click its root—`Cargo`, in this example. Then, enter a preferred unique name without spaces, and click the Base Data Type cell of the row to choose the data type (the values are all red until you have added a successful value or label/value pair). Click on the Enumeration cell to choose `Yes`. Now, enter a value on the first row, and a label if you want one. All the cells are validated, and the red markers are cleared. Then, you can add other value or label/value pairs on the next lines.

  
![](https://progress-be-prod.zoominsoftware.io/bundle/corticon-rule-modeling/page/zlq1462462694228.image?_LANG=enus)  

When you complete a valid Custom Data Type, choose the attributes in the Vocabulary that will be constrained to the enumeration.

  
![](https://progress-be-prod.zoominsoftware.io/bundle/corticon-rule-modeling/page/frq1462462712878.image?_LANG=enus)  

If your custom data type is a local enumeration, then you enter the enumerated values of the base data type into the Value column, and, if you intend to use labels, then enter label text into the **Labels** column.

Note: **Pasting in labels and values**—If you have the source data in a spreadsheet or text file, you can copy from the source and paste into the Vocabulary after you define the name, base data type, and chosen yes to enumeration. When you paste two columns of data, click the first label row. If you have one column of data you want to use for both the label and the value, paste it in turn into each column. If the data type is String, Date, Time, or DateTime, the paste action will add the required single quote marks.

The Label column is optional: you enter Labels only when you want to provide an easier-to-use or more intuitive set of names for your enumerated values.

The Value column is mandatory: you need to enter the enumerations in as many rows of the Value column as necessary to complete the enumerated set. Be sure to use normal syntax, so custom data types that extend String, DateTime, Date, or Time base data types must be enclosed in single quote characters.

Here are some examples of enumerated custom data types:

Figure 1. Custom Data Type, example 1

![](https://progress-be-prod.zoominsoftware.io/bundle/corticon-rule-modeling/page/ijy1589367761666.image?_LANG=enus)

`PrimeNumbers` is an Integer-based, enumerated custom data type with Value-only set members.

Figure 2. Custom Data Type, example 2

![](https://progress-be-prod.zoominsoftware.io/bundle/corticon-rule-modeling/page/fnr1589367892866.image?_LANG=enus)

`containerType` is a String-based, enumerated custom data type with Label/Value pairs.

Figure 3. Custom Data Type, example 3

![](https://progress-be-prod.zoominsoftware.io/bundle/corticon-rule-modeling/page/gsa1373411874180.image?_LANG=enus)

`USHolidays2015` is a Date-based, enumerated custom data type with Label/Value pairs.

Figure 4. Custom Data Type, example 4

![](https://progress-be-prod.zoominsoftware.io/bundle/corticon-rule-modeling/page/dld1589368660965.image?_LANG=enus)

`ShirtSize` is an Integer-based, enumerated custom data type with Label/Value pairs.

Figure 5. Custom Data Type, example 5

![](https://progress-be-prod.zoominsoftware.io/bundle/corticon-rule-modeling/page/ewa1589368181430.image?_LANG=enus)

`RiskProfile` is an Integer-based, enumerated custom data type with Label/Value pairs

Figure 6. Custom Data Type, example 6

![](https://progress-be-prod.zoominsoftware.io/bundle/corticon-rule-modeling/page/ybt1589368261517.image?_LANG=enus)

`DevTeam` is a String-based, enumerated custom data type with Value-only set members.

Use the Move Up ![](https://progress-be-prod.zoominsoftware.io/bundle/corticon-rule-modeling/page/move_up.png?_LANG=enus) or Move Down ![](https://progress-be-prod.zoominsoftware.io/bundle/corticon-rule-modeling/page/move_down.png?_LANG=enus) toolbar icons to change the order of Label/Value rows in the list.

#### Enumerations retrieved from a database
If you want your custom data type to gets its enumerated labels and values from a database, then you need to define the database table and columns that will be accessed.

This topic covers the significant points of this feature in the context of the Vocabulary.

Note: This functionality uses Corticon's Enterprise Data Connector. For more information, see [Import possible values of an attribute from database tables](https://docs.progress.com/bundle/corticon-rule-modeling/page/../../corticon-data-integration/page/Import-possible-values-of-an-attribute-from-database-tables.html)

When your Vocabulary has a verified connection to a supported database, the Custom Data Types tab presents three additional columns, as shown:

Figure 1. Custom Data Type columns for defining database retrieval

![](https://progress-be-prod.zoominsoftware.io/bundle/corticon-rule-modeling/page/gsa1373395456542.image?_LANG=enus)

These columns are how you specify:

-   Lookup Table Name—The database syntax that specifies the table that has the enumerations.
-   Labels Column—The column in the lookup table that holds the label. This is optional because you can elect to use only values.
-   Values Column - The column in the lookup table that holds the value associated with the label or the solitary value. This is required.

The following examples show two options:

Figure 2. SQL Server table with values to use in the Vocabulary

![](https://progress-be-prod.zoominsoftware.io/bundle/corticon-rule-modeling/page/gsa1373402367335.image?_LANG=enus)

The value data is retrieved into the Vocabulary as highlighted:

Figure 3. Definition and retrieved values in Corticon Studio

![](https://progress-be-prod.zoominsoftware.io/bundle/corticon-rule-modeling/page/gsa1373402726468.image?_LANG=enus)

Another example retrieves name-value pairs.

Figure 4. SQL Server table with labels and values to use in the Vocabulary

![](https://progress-be-prod.zoominsoftware.io/bundle/corticon-rule-modeling/page/gsa1373402330242.image?_LANG=enus)

The label/value data is retrieved into the Vocabulary as highlighted:

Figure 5. Definition and retrieved label/values in Corticon Studio

![](https://progress-be-prod.zoominsoftware.io/bundle/corticon-rule-modeling/page/gsa1373402594830.image?_LANG=enus)

**Previous topic:** [Enumerations defined in the Vocabulary](https://docs.progress.com/bundle/corticon-rule-modeling/page/Enumerations-defined-in-the-Vocabulary.html)

[](https://docs.progress.com/bundle/corticon-rule-modeling/page/Enumerations-defined-in-the-Vocabulary.html)