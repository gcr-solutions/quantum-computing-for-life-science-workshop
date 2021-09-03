---
title: Set Up Your Envrionments
weight: 31
---

## Create A Sagemaker Notebook

1. Go to AWS CloudForamtion [link](https://ap-northeast-1.console.aws.amazon.com/cloudformation/home?region=ap-northeast-1#/stacks/create/template)

fill **Amazon S3 URL**: `https://aws-gcr-rs-sol-workshop-ap-northeast-1-common.s3.ap-northeast-1.amazonaws.com/qc/gcr-sol-qc.yaml`


 ![CloudForamtion Create](/images/qc-setup-cf-s3url.png)


2. Click "Next", fill **Stack name**: `gcr-qc`

 ![CloudForamtion Name](/images/qc-cf-name.png)


3. Click button "Next" -> "Next", and check the checkbox

 ![CloudForamtion checkbox](/images/qc-cf-checkbox.png)

4. Click button "Create Stack"


5. Wait CloudFormation deployment complete
   
   {{% notice info %}}
   This will take about 6 minutes to provision
   {{% /notice %}} 

6. Find the link of notebook

 ![CloudForamtion output](/images/qc-cf-nblink.png)

7. Click and open the link

 ![Notebook](/images/qc-notebook.png)
 
