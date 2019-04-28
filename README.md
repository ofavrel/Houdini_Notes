# Houdini Memo
## A collection of small snippets, notes and examples about Houdini organized by Context that are here so that I hopefully don't Keep forgetting about them 
<p align="right"><small><sup>by Favrel Orson</sup></small></p>

<br>

## Topics
### RBD
* [Bullet Soft Constraints](#bullet-soft-constraints)
* [Wrangling Constraints](#wrangling-constraints)
* [Glue Constraint Relationship](#glue-constraint-relationship)
* [Concave to Convex](#concave-to-convex)

### SOPS
* [Attribute Promote](#attribute-promote)
* [Measure](#measure)

### VOLUMES
* [Attribute Promote](#attribute-promote)

### TIPS
* [Change Nodes Color / Shape](#change-nodes-color--shape)



## RBD
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
_-You sometime want to do some Vex Code on the Constraints. You can use a Geometry wrangle running over **Primitives** and change the name of the "Geometry parameter" to  **ConstraintGeometry**.\
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
-The **Half-life** parameter kicks in if the **impact** wasn't strong enough to break the **Glue Constraints**. It's the rate at which the **impact** Strength Decay.\
<br>
-The **Propagation Rate** is how fast the **impact** propagate throught the neighbours pieces.\
<br>
-The **Propagation Iteration** Parameter control how far the **impact** propagates.
Its by default to -1 which mean use the default of 1. If this value is set to something different than -1 it will override any default or detail attributes created in Sops.\
Since H17, it can be set as a Prim attribute as **propagationiterations** and can vary by primitives._

#### Concave to Convex

_Three Approach can be taken while trying to simulate Concave shapes with Bullet Solver._

##### Concave
-_Set the Geometry Representation Parameter to "Concave". The downside is that performance are pretty low. There's no Notion of Inside and Outside and that can cause issues with fast moving object that goes traverse and object from one frame to the other. So object can get stuck inside other pieces._

##### VDB to Spheres
-_Convert the Geometry pieces to **VDB SDF** and then use the **VdbtoSphere** Node. Each Pieces will tehn be Filled with Spheres. Spheres are really Fast to simulate. You need to tweak the **Vdbtosphere** node params and the Geo to SDF as settings can be different depending on the scale of the object and it's configuration._

##### Convex Decomposition
-_Since H17 we can use the **Convex Decomposition** Node. Only one slider is needed to configure the **Concavity tolerance**. You can Also use a piece Attribute to do this operation per piece (After a voronoi Fracture for exemple. This node is very fast and will only operate on Geo or pieces that are not already Convex._

## SOPS
#### Attribute Promote
-_Since H17 the **Attribute Promote** node got a Piece Attribute Param. This let's you do promotion per pieces so that you can avoid looping over each pieces when doing promotion._

#### Measure 
-_The **Measure Sop** got a lot of new options since H17.5. You can now do Measure per piece calculation (ex: Compare the volume of each Chunk in a fracture)

## TIPS
#### Change Nodes Color / Shape
-_Select a Type of Node and just control Click on the desired color or Shape in the appropriate menue (C or Z). That should change the color and/or Shape of all those type of Node. Note that Future Nodes created will keep this Shape/color.
