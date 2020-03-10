# AWS ECS Deploy 

## Overview
* Build Docker Image locally
* Push to AWS ECR from local
* Deploy to EC2 server from GUI console

## Detail
1. Create AIM user with EC2 container registry full access, and allow pragmatical access to AWS resource
2. Configure Local AWS CLI profile by adding access key in ~/.aws/config
3. Create Repository on Elastic Container Registry
4. Get Authenticate token to Docker client like following

```bash
aws ecr get-login-password --region [region] | docker login --username AWS --password-stdin [ecr_url]/[repository]
```

5. Build Docker image with designated tag

```bash
docker tag ecs_test_front:latest [ecr_url]/[repository]:latest
```

6. Push built image to ECR

```bash
docker push [ecr_url]/[repository]:[version]
```

7. Create ECS cluster with a option EC2 Linux + Network
    * Configure Port, machine image, EBS volume, etc as well as the config for EC2 launching setting

8. Create ECS task definition with EC2 (Fargate is also possible), you have to configure port mapping as well as docker-compose setting

9. Create a service which describe deployment type (EC2, Fargate), and (Rolling Deploy or Blue/Green)


## Updating latest AWS CLI

```bash
pip freeze | grep awscli
pip install --user --upgrade awscli
pip freeze | grep awscli
```

## TODO
* Build automatically by using CodeBuild and Github
* Deploy to EC2 server automatically by using CodePipeline


