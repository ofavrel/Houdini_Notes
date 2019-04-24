# Houdini Memo
## A collection of small snippets notes and examples about Houdini organized by Context that are hopefully here so that I don't Keep forgetting about them 
<p align="right"><small><sup>by Favrel Orson</sup></small></p>

<br>

## Topics
### RBD
* [Bullet Soft Constraints](#bullet-soft-constraints)
* [Wrangling Constraints](#wrangling-constraints)
* [Exporting attributes](#exporting-attributes)
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
_The Bullet Soft Constraint is a New Type of constraint that was Shipped with Houdini 17.
It is acting like a spring constraint by applying a force that is proportional to the distance between two anchors points.\
The big difference is that the **Stiffness** and **Damping** are mass independant. So modifying the mass of the objects shouldn't affect too much the Simulation.\
A larger **Stiffness** value reduce the Strechiness  until at some point it aproximate what a Pin Constraint would do.\
If the stiffness does'nt get you stiff engouh result you might need to increase the **Constraint Iteration**_

<br>

#### Wrangling Constraints
_You sometime want to do some Vex Code on the Constraints. Use can use a Geometry wrangle running over **Primitives** and change the name of the "Geometry parameter" to  "ConstraintGeometry"._