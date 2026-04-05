 Microservices Deployment on AWS (ECS + CI/CD)
Overview

This project demonstrates a fully containerized microservices architecture deployed on AWS using ECS Fargate with an automated CI/CD pipeline.

The system consists of:
	•	A Node.js backend API
	•	A React frontend
	•	Fully automated deployment using AWS CodePipeline and CodeBuild
  Architecture Breakdown:
	•	Amazon ECS (Fargate): Runs containerized services without managing servers
	•	Application Load Balancer (ALB): Routes traffic to backend services
	•	Docker: Used to containerize frontend and backend applications
	•	CodePipeline: Automates deployment process
	•	CodeBuild: Builds Docker images and pushes to registry
	•	ECR / Docker Hub: Stores container images

⸻

Tech Stack
	•	AWS ECS (Fargate)
	•	AWS CodePipeline / CodeBuild
	•	Docker
	•	Node.js (Backend)
	•	React (Frontend)
	•	Application Load Balancer (ALB)

⸻

 What I Built
	•	Containerized backend and frontend applications using Docker
	•	Designed a microservices architecture separating frontend and backend
	•	Deployed services to ECS Fargate for scalable, serverless execution
	•	Configured Application Load Balancer to route traffic to services
	•	Built CI/CD pipeline using CodePipeline and CodeBuild for automated deployments
	•	Integrated container registry (Docker Hub / ECR) for image management

⸻

  Key Features
	•	Scalable architecture using ECS Fargate
	•	Automated deployments via CI/CD pipeline
	•	Load-balanced traffic using ALB
	•	Decoupled services (frontend + backend)

⸻
 Deployment Flow
	1.	Developer pushes code to repository
	2.	CodePipeline triggers build
	3.	CodeBuild builds Docker image
	4.	Image pushed to registry
	5.	ECS service updates with new image
	6.	ALB routes traffic to updated service

⸻

 Validation / Proof

Add:
	•	ECS service screenshot (running tasks)
	•	ALB DNS working
	•	App running in browser

⸻

 Future Improvements
	•	Add Terraform for full infrastructure automation
	•	Implement blue/green deployments
	•	Add monitoring (CloudWatch / Prometheus)
	•	Add authentication (JWT / Cognito)
