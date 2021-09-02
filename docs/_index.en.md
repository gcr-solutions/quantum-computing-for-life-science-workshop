---
title: Quantum Computing For Life Science Workshop
chapter: true
---

# Quantum Computing For Life Science Solution

Quantum Computing For Life Science Solution is a cloud-native solution for the application of quantum computing
technology in different aspects of life science. This solution is trying to bridge the gap between the industrial
knowledge and the novel computation model provided by the quantum technologies. This solution will continually 
implement the Proof of Concepts (PoC) based on the recent publications or reports. It is suitable for customers
with needs to evaluate the possible useful cases of quantum computing in their industries. No matter you just
start to consider this new technology or on the way, you can use this solution to speed up the process, save
time and cost. It is an open-source projects, anyone can contribute to features of adding more related solutions.

![What is Recommender System](/images/what-is-recsys.png)

### Recommender System Solution will build a cloud-native recommender system for you from three aspects 

#### Online Services

The core services of the recommender system are constructed using Amazon EKS, including user portrait, data loader, event notice, recall, rank, filter and so on. Some services will interact with redis. This design provides the customers with online service the recommender system based on microservice architecture.
#### Offline Logic

The offline logic is implemented using AWS Step Functions and Amazon Sagemaker. This includes data preprocess, model training, model validation, batch process and so on. Whenever new files or models are generated, the online services will be noticed to reload.

#### End-to-end Development

The CI/CD of system is implemented using AWS CodeBuild and Argo CD. This design helps the customers deploy the latest software into the production environment.