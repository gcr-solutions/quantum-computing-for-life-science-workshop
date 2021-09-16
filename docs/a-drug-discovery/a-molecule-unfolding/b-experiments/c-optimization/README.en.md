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
|M | number of torsions for quantum annealing in QPU | 1000|
|D| num of shots for quantum annealing in QPU | 1000|

代码图片，表示设置的用于实验的参数

## Analyze 

1. 为启动优化器做准备
2. 优化可以调整的参数
3. carry out your own experiment (cost estimate)




   |Region |Subnet |
   |--- |--- |
   |us-west-2|Default in us-west-2a |
   |ap-south-1|Default in ap-south-1a |
   |ap-northeast-2|Default in ap-northeast-2a |
   |ca-central-1|Default in ca-central-1a |
   |sa-east-1|Default in sa-east-1a |

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


