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

debug 1.4

$\mathcal{N}(0,\,1)$

When $a \ne 0$, there are two solutions to \(ax^2 + bx + c = 0\) and they are
\[x = {-b \pm \sqrt{b^2-4ac} \over 2a}.\]


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

