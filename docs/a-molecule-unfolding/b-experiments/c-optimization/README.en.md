---
title: Optimization And Analysis
weight: 33 
---

## Adjust Parameters For Optimization

We have our QUBO model for experiments. There are some parameters we should define for optimization.

| Parameter | Description | Value |
|--- |--- |--- |
|A | penalty scalar |1000 |
|hubo_qubo_val | energy penalty of make_quadratic() |5|
|n_c | number of shots for simulated annealing in local instance | 1000|
|n_q | number of shots for quantum annealing in QPU | 1000|
|M | number of torsions for molecule unfolding| [1, all the torsions] |
|D| angle precision of rotation| 8|

We use the following code to set the parameters:

![Parameter](/images/parameter.png)

## Run Optimizers

After setting the parameters, we can run the optimization on classic device and quantum device.

### Classical Optimizer for QUBO

![Classical](/images/classical.png)

### Quantum Optimizer for QUBO

![Quantum](/images/quantum.png)

## Analyze The Quality

After some time, we get the results. As the result indicates, the best answer of quantum annealer only 
occurs once.

### 量子退火只出现一次结果的图片

This does not always indicate an error. It is actually the characteristic of the problem or how the problem 
is formulated. Because we have different linear and quadratic terms that vary by many orders of magnitude. If we 
set change value of $A$ to some smaller number, like 10 or 100, more occurrences of the best answer will be observed. 
However, these answers usually break the constraints. For more information about this phenomenon, please refer to this 
[Link](https://support.dwavesys.com/hc/en-us/community/posts/1500000698522-Number-of-occurrences-?input_string=number%20occurance).

After that, we need some postprocessing to get the results. What we really want are the desired angles of all the torsion.

### postprocessing 图片

We test different values of $M$, and we find that when $M > 5$, the quantum annealer can not embed it into its quantum circuit. When 
$M < 3$, we can get comparable results from quantum annealer. In other cases, the results from the quantum annealer are not stable. 
This is interesting that we cannot get the similar results as the publication explains. Any discussion or help is welcome!

   |M |d | Results|
   |--- |--- |--- |
   |1|4|Comparable|
   |2|4|Comparable|
   |3|4|Comparable|
   |4|4|Not Stable|
   |5|4|Not Stable|
   |>5|4|Not Available (Embedding Fail)|

## Analyze The Efficiency

In this workshop, we have test the efficiency of model with different complexity, $ M * d $, on different devices. We test SA on ml.c5.4xlarge, 
ml.m5.4xlarge, and ml.r5.4xlarge. We also test QA on DW_2000Q_6 and Advantage_system1.1. The result shows that, if the tasks run with the same 
number of shots (1000), the quantum annealer has really nice scaling ability for solving combinatorial problems. The Advantage_system1.1 only needs 
3 minutes to solve the QUBO model ($M=5, d=8$), while all the classic computing instance needs over 3 hours. However, there's suspicion that there is 
still much space for improvement in the SA implemented by D-Wave. More strict bench mark is needed.


### 性能比较图 - 1

If we change the number of shots for SA to 1, we get another group data for efficiency. 

### 性能比较图 - 2


## Carry Out The Batch Test

You can also conduct this test yourself. 

Open the terminal and run the following script to create the following resource:

* ecr repository
* sagemaker processing jobs
* step function

```sh
cd /home/ec2-user/
```

Change the config file the value you want:

Build the image:

Switch to your step function console and click the run icon:

Read the output of data