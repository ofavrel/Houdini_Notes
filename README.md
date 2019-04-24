# Houdini Memo
## A collection of small snippets notes and examples about Houdini organized by Context that are hopefully here so that I don't Keep forgetting about them 
<p align="right"><small><sup>by Favrel Orson</sup></small></p>

<br>

## Topics
### RBD
* [Bullet Soft Constraints](#bullet-soft-constraints)
* [Wrangling Constraints](#wrangling-constraints)
* [Glue Constraint Relationship](#glue-constraint-relationship)
* [Reading arrays](#reading-arrays)
* [Arrays](#arrays)
* [Arrays and strings example](#arrays-and-strings-example)
* [Reading and writing Matrices](#reading-and-writing-matrices)
* [Checking for attributes](#checking-for-attributes)
* [Automatic attribute creation](#automatic-attribute-creation)
* [Getting transformation from OBJs](#getting-transformation-from-objs)
* [Intrinsics](#intrinsics)
* [VDB intrinsics](#vdb-intrinsics)
* [Volumes](#volumes)
* [VOPs / Using Snippets](#vops--using-snippets)
* [VOPs / Using Inline Code](#vops--using-inline-code)
* [DOPs / Volumes workflow](#dops--volumes-workflow)
* [DOPs / Gas Field Wrangle](#dops--gas-field-wrangle)
<br>



#### Bullet Soft Constraints
-_The Bullet **Soft Constraint** is a New Type of constraint that was Shipped with Houdini 17.
It is acting like a **Spring constraint** by applying a force that is proportional to the distance between two anchors points.\
The big difference is that the **Stiffness** and **Damping** are mass independant. So modifying the mass of the objects shouldn't affect too much the Simulation.\
<br>
-Shouldn't be able to blow up and should be very stable. But a trade off is made comparing to *Spring Constraint* were some artifical damping can happen with a low number of Substeps even if **Damping** is set to 0.\
<br>
-Use **Soft Constraint** instead of **Spring Constraint** in any scenario except if you need a lot of oscillation and you can't afford cranking up the Substeps.
<br>
-A larger **Stiffness** value reduce the Stretchiness  until at some point it approximate what a **Pin Constraint** would do.\
If the **Stiffness** doesn't get you stiff engouh result you might need to increase the **Constraint Iterations**_

<br>

#### Wrangling Constraints
-_You sometime want to do some Vex Code on the Constraints. You can use a Geometry wrangle running over **Primitives** and change the name of the "Geometry parameter" to  **ConstraintGeometry**.\
<br>
-Deleting Constraints:_
```C
if (f@torque > chf("max_torque"))
{
    removeprim(0, @primnum, 1);
}
```

#### Glue Constraint Relationship

-_The **Glue Constraints** get deleted if the **impact** primitive attribute of the pieces is higher that the Constraint **Strength** primitive attribute/parameter.\
<br>
-The **Half-life** parameter kicks in if the **impact** wasn't strong enough to break the **Glue Constraints**. It's the rate at which the **impact** Strength Decay.
<br>
-The **Propagation Rate** is how fast the **impact** propagate throught the neighbours pieces
<br>
-The **Propagation Iteration** Parameter control how far the **impact** propagates.
Its by default to -1 which mean use the default of 1. If this value is set to something different than -1 it will override any default or detail attributes created in Sops.\
Since H17, it can be set as a Prim attribute as **propagationiterations** and can vary by primitives.
