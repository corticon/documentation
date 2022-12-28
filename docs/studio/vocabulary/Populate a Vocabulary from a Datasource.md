## Populate a Vocabulary from a Datasource

Often you have data sources that you want to use as the basis for your rule modeling that might have many tables, each with many columns. You could transcribe each data source's schema to create a Vocabulary, yet the ability to populate the Vocabulary quickly from the schema would expedite the process dramatically.

When you use this built-in Vocabulary generation utility, Corticon sets up the name patterns and defines the data types and associations as best it can. It is important that you review the Vocabulary against the source schema, to validate that the results are correct.

The following are the relationships between relational Datasources and Corticon Vocabulary elements are:


| Relational database | Corticon Vocabulary |
| --- | --- |
| Schema | Vocabulary |
| Table | Vocabulary: Entity |
| Table Column or Field | Vocabulary: Attribute |
| Relationship between Tables | Vocabulary: Association |

### Step 1: How Datasources are transformed into a Corticon Vocabulary

After you connect to a Datasource and import its metadata, you can constrain the tables and attributes that will be evaluated. Then, the internal algorithm makes its best effort to populate the Vocabulary.

Assuming that you are creating a new Vocabulary, these are the steps it takes:

1.  For each selected Table in the Datasource, create a new Entity in the Vocabulary.
2.  For each Column in the Table:
    1.  Create a new Attribute in the Entity.
    2.  Determine the best Corticon data type for the Attribute by referring to the column's data type information.
    3.  If the column is part of the Table's primary key, then mark the Attribute as part of the Entity identity.
3.  After all Tables and Columns are processed, Associations are created for each foreign key for each table (if the source and target tables are both mapped in the Datasource).

The creation process tries to be complete and accurate, but it has limited abilities:

-   Columns that are referenced by foreign keys are not added as Attributes.
-   Tables that do not have any valid columns are not created (such as, Association middle tables or Sequence tables).
-   The data type for an attribute is evaluated in this order: Datetime, Time, Date, Decimal, Integer, String, and Boolean. Some Corticon data types might not get picked for attributes because of an overload of possible mappings (such as, Date and Time could always be created as Datetime). Note that these decisions are derived from data when data is in a REST source that has no schema.

### Step 2: The Vocabulary generation process for RDBMS sources

Relational databases have well-structured schemas that declare every element's data type. The following steps in Corticon Studio populate a new Vocabulary from a relational database Datasource. For an example, use the Patient/Treatment schema that was created in SQL Server from SQL statements in the Data Integration's **ADC Connectivity** sample.

To generate a Vocabulary from a relational data source:

1.  In Corticon Studio, create a new Rules Project named **GenMed**.
2.  In the new project, create a Vocabulary named **GenMed**.
3.  Open the Vocabulary in its editor, and then select the menu command **Vocabulary > Add Datasource > Add ADC Datasource**.
4.  Define the Datasource name as **Patient Data**. Connect to SQL Server database **PatientRecords**. Enter credentials, and the click **CONNECTION Test**:
    
    ![](https://progress-be-prod.zoominsoftware.io/bundle/corticon-rule-modeling/page/bee1613764156636.image?_LANG=enus)
    
    Note: You might want to add a **Schema Filter** value, such as `dbo`, to constrain the results of the next step.
    
5.  Click **METADATA Import**, and then choose the option to choose the tables you want to use. For this example, choose just the two `dbo` tables, as shown:
    
    ![](https://progress-be-prod.zoominsoftware.io/bundle/corticon-rule-modeling/page/pws1571670182276.image?_LANG=enus)
    
    and click **Finish**.
6.  Select **Vocabulary > Populate Vocabulary From Datasource**:
    
    ![](https://progress-be-prod.zoominsoftware.io/bundle/corticon-rule-modeling/page/cdk1570789386967.image?_LANG=enus)
    
7.  Choose the **Patient Data** Datasource. If there were several Datasources defined, choose them one at a time for this process. In this example, there is only one. Click **Next**.
8.  A wizard opens to let you review the Datasource prior to creating the Vocabulary elements, where you can select the Tables and Columns that create Entities and Attributes. In the following image, the tree was expanded:
    
    ![](https://progress-be-prod.zoominsoftware.io/bundle/corticon-rule-modeling/page/tsf1570475706648.image?_LANG=enus)
    
9.  Click **Finish**. The Vocabulary is generated, as shown:
    
    ![](https://progress-be-prod.zoominsoftware.io/bundle/corticon-rule-modeling/page/wze1571671232209.image?_LANG=enus)
    

[](https://docs.progress.com/bundle/corticon-rule-modeling/page/Step-1-How-Datasources-are-transformed-into-a-Corticon-Vocabulary.html)

### Step 3: The Vocabulary generation process from REST sources
REST sources are usually not as clearly structured as relational databases. Some provide a schema, but generally they do not. REST sources can conform to a relational database schema when Corticon uses the Progress® DataDirect® Autonomous Rest Connector to access REST sources. The REST connector maps the JSON in a REST source to a relational database schema, and then translates SQL statements to REST API requests. These steps in Corticon Studio populate a new Vocabulary from the REST Datasource used in the REST connectivity sample from the Data Integration guide. The REST source has no schema; its data looks this:

  
![](https://progress-be-prod.zoominsoftware.io/bundle/corticon-rule-modeling/page/lap1546026664607.image?_LANG=enus)  

To generate a Vocabulary from a REST data source:

1.  In Corticon Studio, create a new Rule Project named **GenRates**.
2.  In the new project, create a Vocabulary named **GenRates**.
3.  Open the Vocabulary in its editor, and then select **Vocabulary > Add Datasource > Add REST Datasource**.
4.  Define the Datasource connection for the URL `https://bj36i9ki66.execute-api.us-east-2.amazonaws.com/prod/ReimbursementRate?procedureCode=B5120ZZ` as shown, and then click **CONNECTION Test**:


![](https://progress-be-prod.zoominsoftware.io/bundle/corticon-rule-modeling/page/cje1597856316359.image?_LANG=enus)
    
1.  Click **SCHEMA Discover**. If your REST source has a schema, or is one that you exported in an earlier processing of this source you could import it now. For this source, you need to let the Progress® DataDirect® Autonomous Rest Connector map the JSON in the REST source to a relational database schema, and then translate SQL statements to REST API requests.
2.  Select **Vocabulary > Populate Vocabulary From Datasource**
    
![](https://progress-be-prod.zoominsoftware.io/bundle/corticon-rule-modeling/page/cdk1570789386967.image?_LANG=enus)
    
7.  Choose the **REST Service** Datasource. If there were several Datasources defined, choose them one at a time for this process. In this example, there is only one, **REST Service**. Click **Next**.
8.  A wizard opens to let you review the Datasource prior to creating the Vocabulary elements, where you can select the Tables and Columns to create as Entities and Attributes. Here, the tree was expanded for `REST_DATA`, the primary table that was unnamed so it was given this default name. You can see links between tables to all the other tables at the bottom of the table.
    
![](https://progress-be-prod.zoominsoftware.io/bundle/corticon-rule-modeling/page/vas1571674814421.image?_LANG=enus)
    
9.  Click **Finish**. The Vocabulary is generated, as shown:
    
![](https://progress-be-prod.zoominsoftware.io/bundle/corticon-rule-modeling/page/llf1571675600191.image?_LANG=enus)
    
    The Primary Key in `RATES` is `POSITION`, a standard that REST connector uses to ensure keys are unique, plus the `REST_DATA_PROCEDURECODE`, the default name of the primary entity. The Primary Key in the `REST_DATA` entity is the single primary key, `PROCEDURECODE`

Here is an association:

![](https://progress-be-prod.zoominsoftware.io/bundle/corticon-rule-modeling/page/qmt1571675569345.image?_LANG=enus)

[](https://docs.progress.com/bundle/corticon-rule-modeling/page/Step-2-The-Vocabulary-generation-process-for-RDBMS-sources.html)

### Step 4: Verify and update the generated Vocabulary

#### Produce a Vocabulary Report

The import of Datasource metadata to build a Vocabulary is a processed through a best-effort algorithm. You should produce a Vocabulary report to review the entity names, attribute names and their data types, and the implied associations.

#### Adding and deleting

You can delete any entity (which deletes all its attributes) and any attributes and associations. Be careful not to delete primary keys. The effect of deletions in the Vocabulary are local. The deletions do not affect the Datasource. You can add attributes, and because the metadata you imported was not deleted, you can re-add a deleted attribute and bind it to the column in the Datasource.

Doing updates from a Datasource is not a synching operation. There is no provision for removing metadata that is no longer in the Datasource.

#### Refactoring names

You can rename any entity and attribute even if it is a just a case change. For example, you can refactor `dob` with `DOB`. It is important that you _refactor_, not _rename_, so that other instances of the name in the Vocabulary such as associations are also updated.

If you repopulate the Vocabulary from the Datasource, then the name you entered is retained while it is still logically the Datasource column name.

Note: **MS Dynamics as a Datasource**: Some table names in Dynamics might map to an unexpected name. For example, a Case table might become an Incident entity by default on the initial import.

#### Data types

The algorithm in the import makes a best effort to map the Datasource's data type to a corresponding Corticon data type. The data type for an attribute is evaluated in this order: Datetime, Time, Date, Decimal, Integer, String, and Boolean. Some Corticon data types might not get picked for attributes because of an overload of possible mappings (such as, Date and Time could always be created as Datetime). Note that these decisions are derived from data when data is in a REST source that does not have a schema. After import, you can revise the data type, for example when you have custom data types that apply constraints, or date of birth imports as Datetime when your rules want just Date, or when `"flight_number":55` is imported as an integer data type when you want it as a String,

#### Mandatory

Whether an attribute is mandatory is set by you. It is not changed on a re-import.

#### Associations

The metadata from the Datasource often provides correct associations. When you use multiple Datasources, you need to create the associations between entities. In all cases, review your associations.

#### Transients

You can add transients. If you change an imported attribute to a transient, then its binding to its Datasource column is dropped.

#### Foreign keys

When if both the source and target table are mapped in the Datasource, then an association is created for each foreign key for each table.

#### Domains

You might need multiple domains. If you use REST Datasources, then you need to rename the existing domains before importing a new one.

[](https://docs.progress.com/bundle/corticon-rule-modeling/page/Step-3-The-Vocabulary-generation-process-from-REST-sources.html)