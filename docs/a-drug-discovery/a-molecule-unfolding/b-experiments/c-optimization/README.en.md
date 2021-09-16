---
title: Optimization And Analysis
weight: 33 
---

## Adjust Parameters For Optimization

We have our QUBO model for experiments. There are some parameters we should define for optimization.

| Parameter | Description | Value |
|--- |--- |--- |
|A | penalty scalar |1000 |
|cost_strength | energy penalty of make_quadratic() |5|
|n_c | number of shots for simulated annealing in local instance | 1000|
|n_q | number of shots for quantum annealing in QPU | 1000|
|M | number of torsions for molecule unfolding| [1, all the torsions] |
|D| angle precision of rotation| 8|

### 代码图片，表示设置的用于实验的参数

## Run Optimizers

After setting the parameters, we can run the optimization on classic device and quantum device.

### 普通优化图片

### 量子优化图片

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


   {{% notice info %}}
   This will take about 2 minutes to provision
   {{% /notice %}}

   ![Cloud9 Welcome](/images/cloud9-welcome.png)

    Close the **welcome page** tab, close the **Quick Start** tab, close **lower work area** tab

Summary as follows:

* simulated annealing

* quantum annealing

1. You need to create an IAM role for Cloud9 service, this IAM role complies with the Principle of least privilege. It contains the following AWS services：
   - AWS IAM
   - AMAZON S3
   - AMAZON EKS
   - AWS SecretsManager
   - AWS CodeBuild
   - AWS EFS
   - AWS EC2
   - AWS Elasticache
   - AWS CloudWatch
   - AWS AutoScaling
   - AWS SSM
   - AWS KMS
   - AWS AutoScaling
   - AWS CloudFormation
   
2. Click the [Link](https://github.com/gcr-solutions/recommender-system-dev-workshop-code/blob/main/scripts/role/gcr-rs-role.json), Copy the content in the `gcr-rs-role.json` file.

3. Click the [Create Policy Link](https://console.aws.amazon.com/iam/home#/policies$new?step=edit), paste the content in the JSON bar. **Attention**: You need to replace `<account_id>` with your AWS Account ID. And click **Next: Tags**.

   ![CREATE POLICY](/images/create-iam-policy.png)
   
4. Enter `gcr-rs-dev-workshop-admin-policy` in the Name bar, and click **Create Policy**.
   
5. Click [Create IAM Role Link](https://console.aws.amazon.com/iam/home#/roles$new?step=review&commonUseCase=EC2%2BEC2&selectedUseCase=EC2). Make sure the **AWS Service** and **EC2** are selected，and click **Next: Permissions**.

   ![IAM Role EC2](/images/iam-role-ec2.png)

6. Search `gcr-rs-dev-workshop-admin-policy` and select it，then click **Next: Tags**.

   ![IAM Role Least Permission](/images/iam-role-leastPermission.png)

7. Enter `gcr-rs-dev-workshop-admin` in the Name bar，Click **Create role**.

   ![IAM Role Created](/images/iam-role-name-create.png)


