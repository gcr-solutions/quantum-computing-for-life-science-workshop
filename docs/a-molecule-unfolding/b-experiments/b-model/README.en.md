---
title: Build The Model
weight: 32
---

## Problem Definition

In this problem, the ligand is considered as a flexible set of atoms. Strictly speaking, 
it can be seen as a set of chemical bonds (edges). These bonds have fixed length and 
only a subset of them are rotatable. Because there are some rotatable bonds (torsions)
, the molecule is split into different disjointed fragments. Take one bond for instance, 
the rightmost rotatable one, it splits the molecule into the left and right fragments. 
These fragments can rotate independently from each other around the axis of the bond. This 
idea is graphically reported in the following figure. 

 ![Rotatable Bonds](/images/rotatable-bonds.png)

 As it indicates, the objective of MU is to find the shape of the ligand that can maximizes 
 the molecular volume. The shape of the ligand can be expressed as the unfolded shape of the
  ligand (the torsion configuration of all the rotatable bonds).

## Formulation

{{% notice warning %}}

 The original paper has some work to make the story of molecular unfolding complete:

 1. elaboration of .MOL2 file for rotatable bonds
 2. the sorting method based on the betweeness centrality 
 3.  many experiments on a ligand dataset compared with Random Search and GeoDock Search
 4. dealing with the elaboration of .MOL2 file for rotatable bonds i

 In this workshop, we only focus on the constructing of equation for molecule unfolding and 
 the application of it in quantum annealer. We make the following assumptions:

 1. The elaboration of rotatable bonds is already finished
 2. The fragment is considered as the collections of atoms with fixed space 
 3. The geometric center of the fragment is chosen as the distances of the atoms inside

 For more details, please refer to the original publication.

{{% /notice %}}

Suppose the ligand has $ M $ torsions, from $ T_i $ to $ T_M $, and each torsion must have the angle 
of rotation $\theta$.

![Multiple Torsion](/images/multiple-torsion.png)

The objective of this model is to find the unfolded torsion configuration $ {\Theta}^{unfold} $ which 
can maximizes the sum of distances $ D(\Theta) $.

$$ {\Theta}^{unfold} = [\theta^{unfold}_1,  \theta^{unfold}_2, ..., \theta^{unfold}_M] $$

$$ D(\Theta) = \sum_{a,b}D_{a,b}(\theta)^2 $$

The $ D_{a,b}(\theta)^2 $ is $ || \overrightarrow{a}_0 - R(\theta)\overrightarrow{b}_0||^2  $ . This is 
the distance between fragment a and b. $ R(\theta) $ is the rotation matrix associated the torsion angle 
$ \theta $.

![Single Torsion](/images/single-torsion.png)

Since this is the problem of portfolio optimization, the final configuration can be the combination of any 
angle of any torsion. However, there are some constraints for applying it to real problem.
* In terms of the limitation of computation resource, the torsion cannot have the rotation with infinitely small 
precision. This means that there are limited candidates of rotation angles for each torsion. Suppose we have $ M $ 
torsions and they have the same precision of rotation angle : $ \Delta\theta $ . This means that we need $ d $ variables 
for each torsion:

$$ d = \frac{2\pi}{\Delta\theta} $$

For the whole model, we need $ n = d \times M $ binary variables $ x_{ik} $ to represent all the combinations. 
For example, for the torsion $ T_i $, its torsion angle $ \theta_i $ can have $ d $ possible values:

$$ \theta_i = [\theta_i^1,\theta_i^2,\theta_i^3, ..., \theta_i^d] $$

* If we only consider the distance, the final result or configuration may have multiple results from the same torsion as long 
as this combination means smaller distance. For example, there may be two binary variables of the same torsion, $ T_i $, in the 
final result:

$$ {\Theta}^{unfold} = [\theta^2_1,  \theta^4_1, ..., \theta^3_M] $$

This cannot happen in real world. $ T_1 $ can only have one of $ d $ angles finally. So we need to integrate the following constraint into our final model:

$$ \displaystyle\sum\limits_{k=1}^{d} x_{ik} = 1 $$

With these two constraints, this problem can be formulated as the high-order unconstrained binary optimization (HUBO).

$$ O(x_{ik}) = A\displaystyle\sum\limits_i (\displaystyle\sum\limits_{k=1}^d x_{ik}-1)^2 - \displaystyle\sum\limits_{a,b} D_{ab} (\theta)^2 $$

The first part is the constraint for each torsion. If one torsion has more than one angles at last, we will add the punishment term $ A $. 
However, in this implementation we calculate the distance-pair under different configuration in advance. This 
means that we use the absolute distance instead:

$$ O(x_{ik}) = A\displaystyle\sum\limits_i (\displaystyle\sum\limits_{k=1}^d x_{ik}-1)^2 - \displaystyle\sum\limits_{a,b} |D_{ab} (\theta)| $$

### 在这里描述代码

## Quantum Annealing

The quantum annealing (QA) can be seen as a variation of the simulated annealing (SA). Both QA and SA are meta-heuristic technique for address 
challenging combinatorial problems. QA uses the quantum fluctuation to explore the configuration space instead of thermal effects. Here, we use 
Amazon Braket API to access the Canadian company D-Wave. This annealer is implemented using superconductive qubits. Natively, the quadratic 
unconstrained binary optimization (QUBO) can be solved using quantum annealer:

$$ O(x) = \displaystyle\sum\limits_i h_i x_i + \displaystyle\sum_{i>j} J_{i,j} x_i x_j $$

In QUBO form, $ x_i \in \{0, 1\} $ are binary variables. We can consider it as the angle that we choose for a particular torsion. $h_i$ and $J_{i,j}$
 can be considered as the values encoding the optimization task when we use corresponding angles. However, in our task, it is common that there are 
 more than one torsion between fragments, we model it as the high-order quadratic unconstrained binary optimization (HUBO) problem:

$$ O(x) = \displaystyle\sum\limits_i \alpha_i x_i + \displaystyle\sum_{i,j} \beta_{i,j} x_i x_j + \displaystyle\sum_{i,j,k} \gamma_{i,j,k} x_i x_j x_k + ... $$

### 这里有图，描述多个torsion的情况

It is often possible to convert HUBOs to QUBOs by using some tricks, 
like adding new ancillary binary variables to replace high-order term. 
In practice, we use the API $$ make\_quadratic() $$ in D-Wave software package to 
make this conversion.

### 这里有图，描述构建HUBO，用QUBO进行convert

Congratulations! We have already prepared the model and it is time to test it.
