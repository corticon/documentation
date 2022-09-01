# The Vocabulary Tree

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
