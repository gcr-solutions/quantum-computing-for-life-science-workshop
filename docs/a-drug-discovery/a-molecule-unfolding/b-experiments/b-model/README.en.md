---
title: Build Models 
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
 * elaboration of .MOL2 file for rotatable bonds
 * the sorting method based on the betweeness centrality 
 * many experiments on a ligand dataset compared with Random Search and GeoDock Search
 * dealing with the elaboration of .MOL2 file for rotatable bonds i
 In this workshop, we only focus on the constructing of equation for molecule unfolding and 
 the application of it in quantum annealer. We make the following assumptions:
 * The elaboration of rotatable bonds is already finished
 * The fragment is considered as the collections of atoms with fixed space 
 * The geometric center of the fragment is chosen as the distances of the atoms inside
 For more details, please refer to the original publication.
{{% /notice %}}

Suppose the ligand has $ M $ torsions, from $ T_i to T_M $, and each torsion must have the angle 
of rotation $\theta$.

# 很多torsion，每个都有theta

The objective of this model is to find the unfolded torsion configuration $ {\Theta}^{unfold} $ which 
can maximizes the sum of distances $ D(\Theta) $.

$$ {\Theta}^{unfold} = [\theta^{unfold}_1,  \theta^{unfold}_2, ..., \theta^{unfold}_M] $$

$$ D(\Theta) = \sum_{a,b}D_{a,b}(\theta)^2 $$

The $ D_{a,b}(\theta)^2 $ is $ || \overrightarrow{a}_0 - R(\theta)\overrightarrow{b}_0||^2  $ . This is 
the distance between fragment a and b. $ R(\theta) $ is the rotation matrix associated the torsion angle 
$ \theta $.

# 图，表示一个torsion的旋转, 同表示出旋转角度

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






However, in this implementation we calculate the distance-pair under different configuration in advance. This 
means that we use the absolute distance instead:

$$ D(\Theta) = \sum_{a,b}D_{a,b}(\theta)^2 $$

that the number of fragments in a molecule is usually double the number of rotatables

debug 1.7

$ {N}(0,\,1) $

$$ {N}(0,\,1) $$

When $a \ne 0$, there are two solutions to $ax^2 + bx + c = 0$ and they are
$$x = {-b \pm \sqrt{b^2-4ac} \over 2a}.$$


## Quantum Annealing

## Prepare For Quantum Anealing






## Create new Cloud9 IDE environment

1. Go to [AWS Cloud9 Console](https://ap-northeast-1.console.aws.amazon.com/cloud9)
2. Use the region drop list to select **Asia Pacific (Tokyo)ap-northeast-1**
3. Click **Create environment** button to create an cloud9 environment

    ![Create Cloud9 Environment](/images/create-cloud9-start.png)

4. Name it `gcr-rs-dev-workshop`, click **Next**
5. If you choose the following regions to proceed workshop, please click **Network Settings (Advanced)** in the **configure settings**, and select the preference settings of the corresponding region in **Subnet**

   |Region |Subnet |
   |--- |--- |
   |us-west-2|Default in us-west-2a |
   |ap-south-1|Default in ap-south-1a |
   |ap-northeast-2|Default in ap-northeast-2a |
   |ca-central-1|Default in ca-central-1a |
   |sa-east-1|Default in sa-east-1a |
   
   If you did not select the above region, keep all the default options, and click **Next** and **Create Environment**

   {{% notice info %}}
   This will take about 2 minutes to provision
   {{% /notice %}}

   When it comes up, the cloud9 console environment should looks like below:

   ![Cloud9 Welcome](/images/cloud9-welcome.png)

### Configure Cloud9 IDE environment

When the environment comes up, customize the environment by:

1. Close the **welcome page** tab, close the **Quick Start** tab, close **lower work area** tab

    ![Cloud9 Close](/images/cloud9-close.png)

2. Open a new **terminal** tab in the main work area.

    ![Cloud9 Open Terminal](/images/cloud9-open-terminal.png)

3. Keep the AWS Cloud9 IDE opened in a browser tab throughout this workshop as we’ll use it for activities like using the AWS CLI and running Bash scripts.

