---
title: 设置环境
weight: 31
---

## 创建 Sagemaker 笔记本

1. 转到 AWS CloudForamtion [link](https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/create/template)

填写 **Amazon S3 URL**: `https://aws-gcr-rs-sol-workshop-ap-northeast-1-common.s3.ap-northeast-1.amazonaws.com/qc/gcr-sol-qc.yaml`


 ![CloudForamtion Create](/images/qc-setup-cf-s3url.png)


2. 点击 "Next", 填写 **Stack name**: `gcr-qc`

 ![CloudForamtion Name](/images/qc-cf-name.png)


3. 点击按钮 "Next" -> "Next", 勾选下面勾选框

 ![CloudForamtion checkbox](/images/qc-cf-checkbox.png)

4. 点击按钮 "Create Stack"

5. 等待 CloudForamtion 部署完成
   
   {{% notice info %}}
   需要等待 6 分钟左右
   {{% /notice %}} 

6. 从输出中找到记事本链接

 ![CloudForamtion output](/images/qc-cf-nblink.png)

7. 点击并打开记事本链接

 ![Notebook](/images/qc-notebook.png)
 
