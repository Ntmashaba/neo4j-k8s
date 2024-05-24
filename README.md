# Deploying Neo4j on Kubernetes with Custom Docker Image

This project contains Kubernetes manifests and a custom Docker image to deploy Neo4j, a graph database, in a Kubernetes cluster. This setup avoids using Helm by embedding configuration directly into the Docker image and managing environment variables through CI/CD.

## Prerequisites

- Kubernetes cluster
- `kubectl` configured to communicate with your Kubernetes cluster
- GitLab runner with Docker and Kubernetes access

## Project Structure

neo4j-k8s/  
│  
├── docker/  
│ ├── Dockerfile # Custom Docker image definition  
│ ├── neo4j.conf # Custom Neo4j configuration  
│ ├── custom-env.sh # Custom environment variables script  
│  
├── k8s/  
│ ├── neo4j-loadbalancer.yaml # LoadBalancer service for external access  
│ ├── neo4j-statefulset.yaml # StatefulSet for Neo4j pods  
│ └── neo4j-svc.yaml # Internal services for Neo4j communication  
│  
└── README.md # Project README  

## Building and Deploying

1. **Build the Custom Docker Image**:
   The `Dockerfile` in the `docker/` directory creates a custom Neo4j image with pre-configured settings.

2. **GitLab CI/CD Pipeline**:
   The `.gitlab-ci.yml` file defines a pipeline to build the custom image and deploy the resources to Kubernetes.

## Detailed Component Explanation

1. **neo4j-auth.yaml**: Secret for Neo4j authentication credentials.
2. **neo4j-config.yaml**: Configuration parameters for Neo4j, moved to Docker image.
3. **neo4j-env.yaml**: Environment variables for Neo4j, moved to Docker image.
4. **neo4j-loadbalancer.yaml**: Exposes Neo4j externally.
5. **neo4j-statefulset.yaml**: Manages the deployment and scaling of Neo4j pods.
6. **neo4j-svc.yaml**: Internal services for Neo4j communication.

## Environment Variables

Environment variables such as `NEO4J_AUTH` are set in the GitLab pipeline or directly in the Kubernetes manifests.

## Accessing Neo4j

- **Via LoadBalancer**: Access Neo4j through the LoadBalancer IP retrieved via:
   kubectl get svc -n neo4j

## Teardown

To remove the Neo4j deployment from your cluster:
  kubectl delete -f k8s/