
# Use a Kubnernetes Based Container as Runtime

|Category    | Value    |
|------------|----------|
| Identifier | adr-0001 |
| Status     | Accepted, replaces [0001](./0001-Platform-Considerations.md) |
| Author(s)  | Brian Mitchell |
| Date:      | October 21, 2017 |

**keywords:** Runtime, Deployment, Kubernetes, Container, Docker  


## Context and Problem Statement

We would like to have this project be used as a demo to showcase some of the interesting blockchain capabilities.  In the real world, consensus-based algorithms are very computationally intensive, and we wanted to simulate creating an architecture that would be suitable and scalable for this type of application.  Best practice dictates the use of a cloud native architecture and a container-based runtime orchestrator. 

Kubernetes (K8s) was chosen as the container solution because it is very popular, supports  development via [Minikube](https://github.com/kubernetes/minikube/), and can be deployed to all major cloud providers (AWS, GCF, Azure)

## Considered Options

* [Kubernetes](https://kubernetes.io/) - Open Source 
* [Amazon EKS](https://aws.amazon.com/eks/) - Amazon's Managed Kubernetes Service
* [Amazon Fargate](https://aws.amazon.com/fargate/) - Amazon's General Purpose Container Solution
* [Amazon's ECS](https://aws.amazon.com/ecs/) - Amazon Elastic Container Service
* Other cloud based container and Kubernetes hosted services were not considered because of expertise on the Amazon platform

## Decision Outcome

Chosen option: **"Amazon EKS"**, because

* Development can be done local with MiniKube
* Deployment to AWS via ECS is simple and can be fully automated
* World class Amazon support and proven scale
* Cost effective

The positioning of the kubernetes runtime is shown in this architecture container diagram:

![Architecure Context](../assets/doc/arch/BC-Architecture-Container.png)