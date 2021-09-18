---
title: Batch Experiment
weight: 41
---

## Create Stepfunctions

1. Go to AWS CloudForamtion [link](https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/create/template)

 **Amazon S3 URL**: `https://aws-gcr-rs-sol-workshop-ap-northeast-1-common.s3.ap-northeast-1.amazonaws.com/qc/qc-batch.yaml`



2. Click "Next",  **Stack name**: `qcBatch`



3. Click button "Next" -> "Next", and check all checkbox items


4. Click button "Create Stack"


5. Wait CloudFormation deployment complete
   
   {{% notice info %}}
   This will take about 3 minutes to provision
   {{% /notice %}} 

6. Find the link of StepFunctions in the output

 ![CloudForamtion Output](/images/qc-batch-stepfunc-links.png)

7. Open the link of BatchExperimentStepFunctions


8. Run the StepFunctions
  
  Click button "Start exection", keep default input no change, then clicke "Start exection"

 ![Run batchstepfuncs](/images/qc-batch-run-stepfunc.png)
 ![batchstepfuncs execution ](/images/qc-batch-exec-stepfunc.png)

