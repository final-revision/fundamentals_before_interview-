# Docker + Kubernetes Interview Questions & Answers

## Complete Fresher / Internship / Software Developer Interview Preparation

> Focus: Docker, Dockerfiles, images, containers, Docker Engine, networking, volumes, Compose, registries, Kubernetes architecture, Pods, Deployments, Services, ConfigMaps, Secrets, Ingress, scaling, troubleshooting, Docker vs Kubernetes, and practical interview questions.

---

# PART 1 — DOCKER

# 1. Docker Fundamentals

## Q1. What is Docker?

**Answer:**

Docker is a platform used to package, distribute, and run applications inside lightweight isolated environments called **containers**.

A Docker container includes the application and its required dependencies so that the application can run consistently across different environments.

```text
Application
    +
Dependencies
    +
Libraries
    +
Configuration
    ↓
Docker Image
    ↓
Docker Container
```

---

## Q2. Why is Docker used?

**Answer:**

Docker helps solve the "works on my machine" problem.

Without Docker:

```text
Developer Machine
Different Python version
Different Node version
Different libraries
        ↓
Application may fail
```

With Docker:

```text
Docker Image
   ↓
Same environment
   ↓
Developer
Testing
Production
```

Main benefits:
- Consistent environments
- Easy deployment
- Lightweight isolation
- Fast startup
- Easy scaling
- Dependency management
- Portability
- CI/CD integration

---

## Q3. What is a container?

**Answer:**

A container is a running instance of a Docker image.

For example:

```text
Docker Image
     ↓
docker run
     ↓
Container
```

A container contains the application and its runtime environment but shares the host operating system kernel.

---

## Q4. What is a Docker image?

**Answer:**

A Docker image is an immutable template used to create containers.

It contains:
- Application code
- Runtime
- Libraries
- Dependencies
- Configuration needed to create the container

Example:

```text
Node.js Image
      ↓
Docker Run
      ↓
Node.js Container
```

---

## Q5. Difference between Docker image and container?

| Docker Image | Docker Container |
|---|---|
| Template | Running instance |
| Usually immutable | Has a writable container layer |
| Used to create containers | Runs the application |
| Stored locally/registry | Exists while created/running |
| Example: `node:22` | Container created from `node:22` |

Simple example:

```text
Image = Class
Container = Object
```

---

# 2. Docker Architecture

## Q6. Explain Docker architecture.

**Answer:**

Docker uses a client-server architecture.

Main components:

1. Docker Client
2. Docker Host / Docker Engine
3. Docker Daemon
4. Docker Images
5. Docker Containers
6. Docker Registry

```text
                 Docker Client
                      |
                Docker API
                      |
                      v
              Docker Daemon
              /     |      \
             /      |       \
        Images   Containers  Networks
                    |
                  Volumes
                      |
                      v
                Docker Host
                      |
                      v
               Docker Registry
             Docker Hub / Private
```

---

## Q7. What is Docker Client?

**Answer:**

Docker Client is the command-line interface through which users interact with Docker.

Examples:

```bash
docker build
docker run
docker ps
docker stop
docker pull
```

The client communicates with the Docker daemon through the Docker API.

---

## Q8. What is Docker Daemon?

**Answer:**

The Docker daemon is the background service responsible for managing Docker objects such as:

- Images
- Containers
- Networks
- Volumes

It receives requests from the Docker client and performs the required operations.

---

## Q9. What is Docker Engine?

**Answer:**

Docker Engine is the core technology that builds and runs containers.

It includes components responsible for:
- Docker API
- Container management
- Image management
- Networking
- Storage
- Container runtime integration

---

# 3. Docker Commands

## Q10. How do you check Docker version?

```bash
docker --version
```

or:

```bash
docker version
```

---

## Q11. How do you check running containers?

```bash
docker ps
```

All containers:

```bash
docker ps -a
```

---

## Q12. How do you download an image?

```bash
docker pull nginx
```

---

## Q13. How do you run a container?

```bash
docker run nginx
```

Run in background:

```bash
docker run -d nginx
```

---

## Q14. How do you assign a name to a container?

```bash
docker run -d --name my-nginx nginx
```

---

## Q15. How do you map a port?

```bash
docker run -d -p 8080:80 nginx
```

Meaning:

```text
Host Port 8080
      ↓
Container Port 80
```

---

## Q16. How do you stop a container?

```bash
docker stop container_name
```

---

## Q17. How do you start a stopped container?

```bash
docker start container_name
```

---

## Q18. How do you restart a container?

```bash
docker restart container_name
```

---

## Q19. How do you remove a container?

```bash
docker rm container_name
```

Force:

```bash
docker rm -f container_name
```

---

## Q20. How do you remove an image?

```bash
docker rmi image_name
```

---

## Q21. How do you view container logs?

```bash
docker logs container_name
```

Follow logs:

```bash
docker logs -f container_name
```

---

## Q22. How do you enter a running container?

```bash
docker exec -it container_name bash
```

For Alpine:

```bash
docker exec -it container_name sh
```

---

## Q23. How do you inspect a Docker object?

```bash
docker inspect container_name
```

---

# 4. Dockerfile

## Q24. What is a Dockerfile?

**Answer:**

A Dockerfile is a text file containing instructions used to build a Docker image.

Example:

```dockerfile
FROM node:22

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

EXPOSE 3000

CMD ["npm", "start"]
```

---

## Q25. Explain the Dockerfile above.

### FROM

```dockerfile
FROM node:22
```

Specifies the base image.

### WORKDIR

```dockerfile
WORKDIR /app
```

Sets the working directory inside the image.

### COPY

```dockerfile
COPY package*.json ./
```

Copies package files into the image.

### RUN

```dockerfile
RUN npm install
```

Executes a command while building the image.

### COPY

```dockerfile
COPY . .
```

Copies application source code.

### EXPOSE

```dockerfile
EXPOSE 3000
```

Documents the port the application listens on.

### CMD

```dockerfile
CMD ["npm", "start"]
```

Specifies the default command when the container starts.

---

## Q26. RUN vs CMD?

| RUN | CMD |
|---|---|
| Executes during image build | Executes when container starts |
| Creates image layers | Provides default runtime command |
| Example: `RUN npm install` | Example: `CMD ["npm","start"]` |

---

## Q27. CMD vs ENTRYPOINT?

**CMD** provides a default command/arguments that can generally be overridden.

**ENTRYPOINT** configures the main executable of the container.

Example:

```dockerfile
ENTRYPOINT ["python"]
CMD ["app.py"]
```

Running:

```bash
docker run myimage
```

effectively executes:

```text
python app.py
```

---

## Q28. COPY vs ADD?

**Answer:**

`COPY` is the simpler and generally preferred instruction for copying local files into an image.

`ADD` has additional behavior such as handling local tar archives and certain URL-related behavior.

For ordinary file copying:

```dockerfile
COPY . .
```

is usually preferred.

---

# 5. Docker Image Layers

## Q29. What are Docker image layers?

**Answer:**

Docker images are built from layers. Many Dockerfile instructions create filesystem layers.

Example:

```dockerfile
FROM node:22
RUN npm install
COPY . .
```

Conceptually:

```text
Application Layer
       ↓
Dependencies Layer
       ↓
Node Base Layer
```

Layers can improve build caching and storage efficiency.

---

## Q30. Why should Dockerfile instructions be ordered carefully?

**Answer:**

Docker caches build layers.

For a Node application, this is often better:

```dockerfile
COPY package*.json ./
RUN npm install
COPY . .
```

If source code changes but `package.json` does not, Docker may reuse the dependency installation layer.

---

# 6. Docker Volumes

## Q31. What is a Docker volume?

**Answer:**

A Docker volume is persistent storage managed by Docker.

Containers are generally considered disposable, but important data should be stored outside the container's writable layer.

```text
Container
    |
    | mounted
    v
Volume
    |
    v
Persistent Data
```

---

## Q32. Why use volumes?

**Answer:**

Use volumes when data must survive container removal/recreation.

Examples:
- Database data
- Uploaded files
- Persistent application data

---

## Q33. Volume vs bind mount?

**Volume:**

```bash
docker volume create mydata
```

Docker manages its storage location.

**Bind mount:**

```bash
docker run -v /host/path:/container/path image
```

It maps a specific host filesystem path into the container.

---

# 7. Docker Networking

## Q34. What is Docker networking?

**Answer:**

Docker networking allows containers to communicate with:
- Other containers
- The host
- External networks

---

## Q35. What are common Docker network types?

### 1. bridge

Default network for many standalone Docker containers.

### 2. host

Container shares the host's network namespace more directly.

### 3. none

Disables normal network connectivity.

### 4. overlay

Used for networking across multiple Docker hosts, commonly with Docker Swarm.

### 5. macvlan

Can assign containers addresses that appear directly on the physical network.

---

## Q36. What is a bridge network?

**Answer:**

A bridge network provides isolated container networking on a Docker host.

Containers connected to the same user-defined bridge network can communicate using container/service names.

Example:

```text
Backend Container
       |
       | Docker Network
       |
Database Container
```

---

## Q37. Why create a custom Docker network?

```bash
docker network create mynetwork
```

Then:

```bash
docker run -d --network mynetwork --name backend backend-image
docker run -d --network mynetwork --name db mongo
```

The backend can communicate with the database using:

```text
db
```

rather than relying on a hard-coded container IP.

---

# 8. Docker Compose

## Q38. What is Docker Compose?

**Answer:**

Docker Compose is a tool for defining and running multi-container applications using a YAML configuration file.

Example architecture:

```text
Frontend
   |
Backend
   |
MongoDB
```

---

## Q39. Example docker-compose.yml

```yaml
services:
  backend:
    build: ./backend
    ports:
      - "3000:3000"
    depends_on:
      - mongo

  mongo:
    image: mongo:8
    volumes:
      - mongo_data:/data/db

volumes:
  mongo_data:
```

---

## Q40. Why use Docker Compose?

**Answer:**

It makes local multi-container development easier.

Instead of running multiple commands manually:

```bash
docker compose up
```

The configuration defines:
- Services
- Ports
- Networks
- Volumes
- Environment configuration
- Dependencies

---

## Q41. Docker Compose vs Docker?

**Answer:**

Docker is the container platform/runtime ecosystem.

Docker Compose is used to define and manage applications consisting of multiple containers.

---

# 9. Docker Registry

## Q42. What is Docker Hub?

**Answer:**

Docker Hub is a public registry where Docker images can be stored and downloaded.

Example:

```bash
docker pull nginx
```

---

## Q43. What is a Docker registry?

**Answer:**

A registry stores and distributes container images.

Examples:
- Docker Hub
- Amazon ECR
- Google Artifact Registry
- Azure Container Registry
- Private registries

---

## Q44. How do you push an image?

```bash
docker login
docker tag myapp username/myapp:v1
docker push username/myapp:v1
```

---

# 10. Environment Variables

## Q45. How do you pass environment variables?

```bash
docker run -e NODE_ENV=production myapp
```

Multiple variables:

```bash
docker run \
  -e NODE_ENV=production \
  -e PORT=3000 \
  myapp
```

In Compose:

```yaml
services:
  backend:
    environment:
      NODE_ENV: production
      PORT: 3000
```

---

## Q46. Should secrets be hardcoded in a Dockerfile?

**Answer:**

No.

Avoid:

```dockerfile
ENV DB_PASSWORD=secret123
```

Use an appropriate secret-management mechanism for the deployment environment.

---

# 11. Docker Security

## Q47. How can you make Docker images more secure?

**Answer:**

- Use trusted base images.
- Keep images updated.
- Use minimal images where appropriate.
- Avoid running applications as root when possible.
- Do not hardcode secrets.
- Scan images for vulnerabilities.
- Use `.dockerignore`.
- Pin important dependencies when appropriate.
- Reduce unnecessary packages.

---

## Q48. What is `.dockerignore`?

**Answer:**

It prevents unnecessary files from being sent as part of the Docker build context.

Example:

```text
node_modules
.git
.env
dist
*.log
```

This can improve build performance and reduce accidental inclusion of sensitive/unnecessary files.

---

# 12. Multi-Stage Builds

## Q49. What is a multi-stage Docker build?

**Answer:**

A multi-stage build uses multiple `FROM` statements so that build dependencies can be separated from the final runtime image.

Example:

```dockerfile
FROM node:22 AS build

WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build

FROM nginx:alpine

COPY --from=build /app/dist /usr/share/nginx/html
```

The final image contains the built frontend rather than the complete build environment.

---

## Q50. Why use multi-stage builds?

**Answer:**

Benefits:
- Smaller final images
- Reduced attack surface
- Separation of build and runtime dependencies
- Cleaner production images

---

# 13. Docker vs Virtual Machine

## Q51. Docker container vs Virtual Machine?

| Container | Virtual Machine |
|---|---|
| Shares host kernel | Includes guest OS |
| Lightweight | Heavier |
| Starts quickly | Usually slower startup |
| Lower resource overhead | Higher resource overhead |
| Good for application isolation | Strong full OS isolation |
| Containers share kernel | VMs virtualize hardware/resources |

Conceptually:

```text
Containers:

Application
Libraries
Container
----------------
Host OS
Host Kernel
Hardware
```

```text
VM:

Application
Libraries
Guest OS
Virtual Hardware
----------------
Hypervisor
Host OS
Hardware
```

---

# 14. Docker Troubleshooting

## Q52. Container exits immediately. What do you check?

**Answer:**

1. Check logs:

```bash
docker logs container_name
```

2. Inspect the container:

```bash
docker inspect container_name
```

3. Check the command/entrypoint.
4. Check environment variables.
5. Check whether the application itself is exiting.
6. Check port/configuration problems.

---

## Q53. Application works locally but not inside Docker. What do you check?

**Answer:**

- Environment variables
- Port configuration
- Hostname configuration
- Dependencies
- Working directory
- Dockerfile
- `.dockerignore`
- File paths
- OS-specific assumptions
- Container logs

---

## Q54. Backend cannot connect to MongoDB container. Why?

Common mistake:

```text
mongodb://localhost:27017
```

Inside the backend container, `localhost` refers to the backend container itself, not the MongoDB container.

With a user-defined Docker network, use the service/container name:

```text
mongodb://mongo:27017
```

---

# PART 2 — KUBERNETES

# 15. Kubernetes Fundamentals

## Q55. What is Kubernetes?

**Answer:**

Kubernetes is an open-source container orchestration platform used to deploy, manage, scale, and automate containerized applications.

It can manage:
- Container workloads
- Service discovery
- Scaling
- Rolling updates
- Self-healing
- Configuration
- Secrets
- Networking

---

## Q56. Why do we need Kubernetes if we already have Docker?

**Answer:**

Docker can run containers, but managing many containers across multiple machines becomes difficult.

Kubernetes provides orchestration.

```text
Docker:
Run Containers

Kubernetes:
Manage Containers at Scale
```

Kubernetes can:
- Schedule workloads
- Restart failed containers
- Scale applications
- Provide service discovery
- Perform rolling updates
- Manage desired state

---

## Q57. Docker vs Kubernetes?

| Docker | Kubernetes |
|---|---|
| Container platform/runtime ecosystem | Container orchestration platform |
| Builds/runs containers | Manages workloads across a cluster |
| Dockerfile builds images | Uses manifests to describe workloads |
| Good for local containers | Good for distributed deployments |
| Compose for local multi-container apps | Deployments, Services, etc. for cluster orchestration |

Important: Kubernetes does not require the Docker Engine specifically; modern Kubernetes commonly uses container runtimes such as containerd or CRI-O.

---

# 16. Kubernetes Architecture

## Q58. Explain Kubernetes architecture.

**Answer:**

A Kubernetes cluster generally contains:

### Control Plane

Responsible for managing cluster state.

Important components:
- API Server
- etcd
- Scheduler
- Controller Manager

### Worker Nodes

Run application workloads.

Important components:
- Kubelet
- Container runtime
- Kube-proxy/networking components

```text
                 Kubernetes Cluster
                        |
          +-------------+-------------+
          |                           |
     Control Plane                 Worker Nodes
          |                    +----------------+
    +-----+------+             | Kubelet        |
    | API Server |             | Runtime        |
    | Scheduler  |             | Pod            |
    | Controller |             +----------------+
    | etcd       |
    +------------+
```

---

# 17. Kubernetes Control Plane

## Q59. What is the API Server?

**Answer:**

The Kubernetes API Server is the central interface through which clients and cluster components interact with the Kubernetes API.

Example:

```bash
kubectl get pods
```

communicates with the Kubernetes API.

---

## Q60. What is etcd?

**Answer:**

`etcd` is a distributed key-value store used by Kubernetes to persist cluster state and configuration.

---

## Q61. What is the Scheduler?

**Answer:**

The scheduler determines which eligible worker node should run a newly created Pod based on resource requirements, constraints, affinity rules, and other scheduling considerations.

---

## Q62. What is Controller Manager?

**Answer:**

It runs controllers that continuously work to make the actual cluster state match the desired state.

Example:

```text
Desired:
3 Pods

Current:
2 Pods

Controller:
Create another Pod
```

---

# 18. Kubernetes Worker Node

## Q63. What is a worker node?

**Answer:**

A worker node is a machine that runs application workloads managed by Kubernetes.

It contains components such as:
- Kubelet
- Container runtime
- Networking components

---

## Q64. What is Kubelet?

**Answer:**

Kubelet is an agent running on each node. It communicates with the Kubernetes control plane and ensures that the Pods assigned to the node are running as specified.

---

## Q65. What is a container runtime?

**Answer:**

The container runtime is responsible for running containers.

Examples include:
- containerd
- CRI-O

---

# 19. Kubernetes Pod

## Q66. What is a Pod?

**Answer:**

A Pod is the smallest deployable unit in Kubernetes.

A Pod can contain one or more containers that share:
- Network namespace
- IP address
- Ports
- Volumes where configured

Most common applications use one main application container per Pod.

---

## Q67. Why doesn't Kubernetes directly manage individual containers?

**Answer:**

Kubernetes manages Pods as the basic deployment unit. Containers within a Pod share certain resources and are scheduled together.

---

## Q68. Can a Pod contain multiple containers?

**Answer:**

Yes.

Example:

```text
Pod
├── Application Container
└── Sidecar Container
```

Multiple containers are appropriate when the containers need to closely share lifecycle and resources.

---

# 20. Deployment

## Q69. What is a Deployment?

**Answer:**

A Deployment manages replicated application Pods and supports declarative updates.

It can provide:
- Replica management
- Rolling updates
- Rollbacks
- Desired-state management

---

## Q70. Example Deployment YAML

```yaml
apiVersion: apps/v1
kind: Deployment

metadata:
  name: backend

spec:
  replicas: 3

  selector:
    matchLabels:
      app: backend

  template:
    metadata:
      labels:
        app: backend

    spec:
      containers:
        - name: backend
          image: username/backend:v1
          ports:
            - containerPort: 3000
```

---

## Q71. What does `replicas: 3` mean?

**Answer:**

It declares that the Deployment should maintain three Pod replicas.

```text
Backend Deployment
      |
  +---+---+---+
  |   |   |   |
 Pod Pod Pod
```

If one Pod fails, the Deployment controller attempts to restore the desired replica count.

---

# 21. Kubernetes Service

## Q72. What is a Service?

**Answer:**

A Service provides a stable network endpoint for reaching a set of Pods.

Pods can be recreated and their IP addresses can change. A Service provides stable discovery and routing to matching Pods.

```text
Client
  |
Service
  |
+---+---+---+
|   |   |   |
Pod Pod Pod
```

---

## Q73. What are common Kubernetes Service types?

### ClusterIP

Default type. Accessible inside the cluster.

### NodePort

Exposes the service on a port on each node.

### LoadBalancer

Requests an external load balancer when supported by the environment/cloud provider.

---

## Q74. Deployment vs Service?

**Deployment:**
Manages Pods and application rollout.

**Service:**
Provides stable networking and discovery for Pods.

```text
Deployment
    ↓
Pods

Service
    ↓
Access to Pods
```

---

# 22. ConfigMap

## Q75. What is ConfigMap?

**Answer:**

ConfigMap stores non-sensitive configuration data separately from container images.

Example:

```yaml
apiVersion: v1
kind: ConfigMap

metadata:
  name: app-config

data:
  API_URL: "http://backend:3000"
```

---

# 23. Secret

## Q76. What is a Kubernetes Secret?

**Answer:**

A Secret is intended for sensitive configuration such as passwords, tokens, and credentials.

Important interview point:

> Kubernetes Secrets are not automatically equivalent to a fully secure external secret-management system. In many deployments, encryption at rest and access controls must be configured appropriately.

---

## Q77. ConfigMap vs Secret?

| ConfigMap | Secret |
|---|---|
| Non-sensitive configuration | Sensitive configuration |
| URLs/settings | Passwords/tokens/credentials |
| Not designed for secrets | Designed for secret data |

---

# 24. Namespace

## Q78. What is a Namespace?

**Answer:**

A Namespace provides logical separation within a Kubernetes cluster.

Example:

```text
Cluster
├── development
├── testing
└── production
```

Namespaces can help organize resources and apply policies/quotas.

---

# 25. Labels and Selectors

## Q79. What are labels?

**Answer:**

Labels are key-value metadata attached to Kubernetes objects.

Example:

```yaml
labels:
  app: backend
  environment: production
```

---

## Q80. What are selectors?

**Answer:**

Selectors identify objects based on labels.

Example:

```yaml
selector:
  matchLabels:
    app: backend
```

A Service also uses selectors to identify which Pods should receive traffic.

---

# 26. Ingress

## Q81. What is Ingress?

**Answer:**

Ingress defines HTTP/HTTPS routing rules for external access to services.

Example:

```text
Internet
   |
Ingress
   |
+--+----------------+
|                   |
/api              /app
 |                  |
Backend           Frontend
```

Ingress requires an appropriate ingress controller to implement the routing.

---

# 27. Kubernetes Storage

## Q82. Why is persistent storage needed in Kubernetes?

**Answer:**

Pods are replaceable and their local writable storage should not generally be treated as durable application data.

Persistent storage is needed for applications such as:
- Databases
- File storage
- Persistent application data

---

## Q83. What is a PersistentVolume?

**Answer:**

A PersistentVolume (PV) represents storage available to the Kubernetes cluster.

## Q84. What is a PersistentVolumeClaim?

**Answer:**

A PersistentVolumeClaim (PVC) is a request for storage made by a workload.

Conceptually:

```text
Pod
 ↓
PVC
 ↓
PV
 ↓
Storage System
```

---

# 28. Kubernetes Scaling

## Q85. How do you scale a Deployment?

```bash
kubectl scale deployment backend --replicas=5
```

This changes the desired number of replicas.

---

## Q86. What is Horizontal Pod Autoscaler?

**Answer:**

HPA automatically adjusts the number of Pod replicas based on configured metrics, commonly resource utilization and, depending on the setup, custom or external metrics.

Example:

```bash
kubectl autoscale deployment backend \
  --cpu-percent=70 \
  --min=2 \
  --max=10
```

---

# 29. Kubernetes Rolling Updates

## Q87. What is a rolling update?

**Answer:**

A rolling update gradually replaces old Pods with new Pods instead of replacing everything simultaneously.

```text
Old Version:
Pod v1
Pod v1
Pod v1

        ↓

Update

Pod v1
Pod v1
Pod v2

        ↓

Pod v1
Pod v2
Pod v2

        ↓

Pod v2
Pod v2
Pod v2
```

---

## Q88. How do you update an image?

```bash
kubectl set image deployment/backend \
  backend=username/backend:v2
```

---

## Q89. How do you rollback a Deployment?

```bash
kubectl rollout undo deployment/backend
```

Check rollout:

```bash
kubectl rollout status deployment/backend
```

---

# 30. Kubernetes Health Checks

## Q90. What is a liveness probe?

**Answer:**

A liveness probe helps Kubernetes determine whether a container is unhealthy and should be restarted.

---

## Q91. What is a readiness probe?

**Answer:**

A readiness probe determines whether an application is ready to receive traffic.

Important difference:

```text
Liveness:
Should the container be restarted?

Readiness:
Should traffic be sent to this Pod?
```

---

## Q92. What is a startup probe?

**Answer:**

A startup probe is useful for applications that take a long time to start. It gives the application time to initialize before liveness/readiness checks become relevant.

---

# 31. Kubernetes Resource Management

## Q93. What are resource requests?

**Answer:**

A resource request indicates the amount of CPU or memory Kubernetes should consider when scheduling a Pod.

Example:

```yaml
resources:
  requests:
    cpu: "250m"
    memory: "256Mi"
```

---

## Q94. What are resource limits?

**Answer:**

Limits define the maximum amount of a resource that a container is allowed to consume, subject to Kubernetes/runtime behavior.

```yaml
resources:
  limits:
    cpu: "500m"
    memory: "512Mi"
```

---

# 32. Kubernetes Commands

## Q95. How do you check cluster information?

```bash
kubectl cluster-info
```

---

## Q96. How do you list Pods?

```bash
kubectl get pods
```

Across namespaces:

```bash
kubectl get pods -A
```

---

## Q97. How do you list Deployments?

```bash
kubectl get deployments
```

---

## Q98. How do you list Services?

```bash
kubectl get services
```

---

## Q99. How do you get detailed information about a Pod?

```bash
kubectl describe pod pod-name
```

---

## Q100. How do you see Pod logs?

```bash
kubectl logs pod-name
```

For a specific container:

```bash
kubectl logs pod-name -c container-name
```

---

## Q101. How do you execute a command inside a Pod?

```bash
kubectl exec -it pod-name -- sh
```

---

## Q102. How do you apply Kubernetes configuration?

```bash
kubectl apply -f deployment.yaml
```

---

## Q103. How do you delete resources?

```bash
kubectl delete -f deployment.yaml
```

---

# 33. Kubernetes Troubleshooting

## Q104. Pod is in `Pending` state. What do you check?

**Answer:**

Check:

```bash
kubectl describe pod pod-name
```

Possible causes:
- Insufficient CPU/memory
- Scheduling constraints
- Node availability
- Persistent volume issues
- Taints/tolerations
- Affinity/anti-affinity constraints

---

## Q105. Pod is in `CrashLoopBackOff`. What do you check?

**Answer:**

Check:

```bash
kubectl logs pod-name
kubectl describe pod pod-name
```

Possible causes:
- Application crashes
- Wrong environment variables
- Missing configuration
- Incorrect command
- Failed dependency connection
- Failed health probes

---

## Q106. Pod is `Running` but application is not accessible. What do you check?

**Answer:**

Check:

1. Pod logs
2. Container port
3. Service port
4. Service selector
5. Endpoints
6. Readiness probe
7. Ingress configuration
8. Network policies if present

Useful commands:

```bash
kubectl get svc
kubectl describe svc backend
kubectl get endpoints
```

---

## Q107. ImagePullBackOff. What does it mean?

**Answer:**

Kubernetes cannot successfully pull the required container image.

Possible causes:
- Wrong image name
- Wrong tag
- Private registry authentication problem
- Network/registry issue
- Image does not exist

---

# 34. Kubernetes Deployment Architecture Example

Suppose you have:

```text
Angular Frontend
Node.js Backend
MongoDB
```

A conceptual Kubernetes deployment could be:

```text
                    Internet
                       |
                    Ingress
                    /     \
                   /       \
             Frontend     Backend
                |            |
             Service       Service
                |            |
             Pods          Pods
                            |
                         MongoDB
                            |
                     Persistent Storage
```

A production architecture may instead use a managed database outside the Kubernetes cluster depending on requirements.

---

# 35. Docker + Kubernetes End-to-End Flow

## Q108. Explain the complete deployment process.

**Answer:**

```text
Developer writes application
          ↓
Create Dockerfile
          ↓
docker build
          ↓
Docker Image
          ↓
Push image to registry
          ↓
Kubernetes Deployment
          ↓
Kubernetes pulls image
          ↓
Pod created
          ↓
Container starts
          ↓
Service exposes application
          ↓
Ingress provides HTTP/HTTPS routing
```

Example:

```bash
docker build -t username/backend:v1 .
docker push username/backend:v1

kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
```

---

# 36. Docker + Kubernetes Interview Scenarios

## Q109. Your application works locally but fails in Kubernetes. What do you do?

**Answer:**

I would debug systematically:

```text
1. Check Pod status
       ↓
2. kubectl describe pod
       ↓
3. Check logs
       ↓
4. Check environment variables
       ↓
5. Check image/tag
       ↓
6. Check Service
       ↓
7. Check readiness/liveness probes
       ↓
8. Check networking
       ↓
9. Check external dependencies
```

---

## Q110. How would you deploy your Node.js backend using Docker and Kubernetes?

**Answer:**

1. Create a Dockerfile.
2. Build the image.
3. Test the container locally.
4. Push the image to a registry.
5. Create a Kubernetes Deployment.
6. Create a Kubernetes Service.
7. Configure environment variables.
8. Add readiness/liveness probes.
9. Configure Ingress if external HTTP/HTTPS access is required.
10. Monitor logs and resource usage.

---

## Q111. How would you deploy an Angular application?

**Answer:**

For a production build, Angular can be compiled into static files and served by a web server such as Nginx.

Typical multi-stage process:

```text
Angular Source
     ↓
Node Build Stage
     ↓
ng build
     ↓
Static Files
     ↓
Nginx Runtime Image
     ↓
Docker Container
     ↓
Kubernetes Pod
```

---

# 37. Important Docker Interview Rapid-Fire Questions

## Q112. What is `docker build`?

Builds an image from a Dockerfile and build context.

## Q113. What is `docker run`?

Creates and starts a container from an image.

## Q114. What is `docker pull`?

Downloads an image from a registry.

## Q115. What is `docker push`?

Uploads an image to a registry.

## Q116. What is `docker ps`?

Lists running containers.

## Q117. What is `docker logs`?

Displays container logs.

## Q118. What is `docker exec`?

Executes a command inside a running container.

## Q119. What is `EXPOSE`?

Documents a container port in the image. It does not itself publish the port to the host.

## Q120. What is `-p`?

Publishes/maps a container port to a host port.

Example:

```bash
docker run -p 8080:3000 app
```

---

# 38. Important Kubernetes Rapid-Fire Questions

## Q121. Smallest deployable Kubernetes unit?

**Pod.**

## Q122. What manages replicated Pods?

**Deployment**, typically through ReplicaSets.

## Q123. What provides stable access to Pods?

**Service.**

## Q124. What stores non-sensitive configuration?

**ConfigMap.**

## Q125. What stores sensitive configuration?

**Secret.**

## Q126. What provides HTTP routing?

**Ingress**, together with an ingress controller.

## Q127. What stores cluster state?

**etcd.**

## Q128. What chooses a node for a new Pod?

**Scheduler.**

## Q129. What runs on worker nodes and manages Pods?

**Kubelet.**

## Q130. What automatically changes replica count based on metrics?

**Horizontal Pod Autoscaler (HPA).**

---

# 39. Docker and Kubernetes Comparison

| Feature | Docker | Kubernetes |
|---|---|---|
| Main purpose | Build/run containers | Orchestrate workloads |
| Image building | Yes | Usually uses externally built images |
| Container execution | Yes | Via container runtime |
| Multi-container local development | Docker Compose | Not its main purpose |
| Scaling | Basic/manual mechanisms | Built-in orchestration/scaling |
| Self-healing | Limited at standalone Docker level | Yes |
| Rolling deployments | Not the core standalone feature | Yes |
| Service discovery | Docker networking | Kubernetes Services/DNS |
| Cluster management | Limited | Core purpose |
| Production orchestration | Possible with other tools | Core use case |

---

# 40. Docker Compose vs Kubernetes

| Docker Compose | Kubernetes |
|---|---|
| Simple multi-container development | Large-scale orchestration |
| Easy local setup | More complex |
| YAML configuration | YAML manifests/resources |
| Excellent for local development | Designed for clusters |
| Simple scaling | Advanced scheduling/scaling |
| Limited orchestration | Extensive orchestration features |

---

# 41. Frequently Asked Practical Questions

## Q131. Why should you not store database data only inside a container?

Because the container can be deleted/recreated. Persistent data should be stored using appropriate persistent storage.

---

## Q132. Why shouldn't you use `localhost` to connect to another Docker container?

Because `localhost` inside a container refers to that same container.

Use the Docker service/container hostname when containers are on the same user-defined network.

---

## Q133. Why shouldn't you put `.env` or secrets into a Docker image?

Because image layers can persist data even after the file is removed in a later layer. Secrets should be supplied through appropriate runtime/deployment secret mechanisms.

---

## Q134. Why use a small base image?

A smaller image can:
- Reduce download time
- Reduce storage
- Reduce attack surface
- Improve deployment efficiency

But image choice should also consider compatibility, security updates, and debugging needs.

---

# 42. Project Explanation Example

If the interviewer asks:

> "Have you used Docker in your project?"

A truthful fresher answer can be:

**Sample Answer:**

"I have used Docker to containerize my application. I created a Dockerfile for the backend, installed the required dependencies inside the image, exposed the application port, and ran the backend as a container. I also understand how Docker Compose can be used when the application contains multiple services such as a frontend, backend, and database."

Only mention steps you have actually performed.

---

# 43. If Asked About Kubernetes When You Have Learning Knowledge

If you have studied Kubernetes but have not deployed a real production application, say:

> "I have studied Kubernetes and practiced the core concepts such as Pods, Deployments, Services, ConfigMaps, Secrets, Ingress, scaling, probes, and kubectl commands. I understand the deployment flow, although I have not yet managed a large production Kubernetes cluster."

This is better than claiming production Kubernetes experience you do not have.

---

# 44. Scenario: Deploy a MERN Application

Suppose your application is:

```text
React/Angular Frontend
        |
        v
Node.js + Express Backend
        |
        v
MongoDB
```

Containerized architecture:

```text
                 Docker
        +-----------------------+
        |                       |
        | Frontend Container    |
        |                       |
        | Backend Container     |
        |                       |
        | MongoDB Container     |
        |                       |
        +-----------------------+
```

Kubernetes architecture:

```text
              Kubernetes Cluster
                     |
          +----------+----------+
          |                     |
    Frontend Deployment   Backend Deployment
          |                     |
       Service                Service
          |                     |
       Pods                  Pods
                                |
                             Database
```

For production, the database may be provided by a managed database service instead of being run inside Kubernetes.

---

# 45. CI/CD Connection

## Q135. How do Docker and Kubernetes fit into CI/CD?

**Answer:**

A typical pipeline can be:

```text
Developer
   ↓
Git Push
   ↓
CI Pipeline
   ↓
Run Tests
   ↓
Build Docker Image
   ↓
Security Scan
   ↓
Push Image to Registry
   ↓
Deploy to Kubernetes
   ↓
Rolling Update
   ↓
Monitoring
```

Tools may include:
- GitHub Actions
- GitLab CI/CD
- Jenkins
- AWS CodePipeline
- Azure DevOps

---

# 46. Important Production Concepts

## Q136. What is self-healing?

Kubernetes can maintain the desired state by replacing failed or unhealthy workloads when configured appropriately.

Example:

```text
Desired = 3 Pods
Current = 2 Pods
       ↓
Controller
       ↓
Creates replacement
       ↓
Current = 3 Pods
```

---

## Q137. What is service discovery?

Service discovery allows applications to find services without hardcoding changing Pod IP addresses.

Kubernetes provides service discovery through Services and cluster DNS.

---

## Q138. What is rolling deployment?

It updates an application gradually while maintaining the configured availability constraints.

---

## Q139. What is blue-green deployment?

Two environments are maintained:

```text
Blue = Current
Green = New
```

Traffic can be switched from the current version to the new version after validation.

This is a deployment strategy rather than a Kubernetes-specific resource.

---

## Q140. What is canary deployment?

A canary deployment gradually exposes a new application version to a subset of users/traffic before broader rollout.

---

# 47. Most Important Interview Questions to Prepare

## Docker

1. What is Docker?
2. Why use Docker?
3. Container vs VM?
4. Image vs container?
5. Explain Docker architecture.
6. What is Docker Engine?
7. What is Docker daemon?
8. Explain Dockerfile.
9. Explain `FROM`, `RUN`, `COPY`, `CMD`, `ENTRYPOINT`, `EXPOSE`.
10. RUN vs CMD.
11. CMD vs ENTRYPOINT.
12. What are image layers?
13. What is Docker volume?
14. Volume vs bind mount.
15. Explain Docker networking.
16. Explain bridge network.
17. What is Docker Compose?
18. Docker vs Docker Compose.
19. What is Docker Hub/registry?
20. How do you push an image?
21. What is `.dockerignore`?
22. What is a multi-stage build?
23. How do you reduce Docker image size?
24. How do you debug a container?
25. Why does a container exit immediately?
26. Why does `localhost` cause problems between containers?
27. How do you handle environment variables?
28. How do you secure Docker images?

## Kubernetes

29. What is Kubernetes?
30. Why Kubernetes?
31. Docker vs Kubernetes.
32. Explain Kubernetes architecture.
33. What is Control Plane?
34. What is API Server?
35. What is etcd?
36. What is Scheduler?
37. What is Controller Manager?
38. What is a Worker Node?
39. What is Kubelet?
40. What is a Pod?
41. Can a Pod have multiple containers?
42. What is a Deployment?
43. What is a ReplicaSet?
44. What is a Service?
45. ClusterIP vs NodePort vs LoadBalancer.
46. Deployment vs Service.
47. What is ConfigMap?
48. What is Secret?
49. What is Namespace?
50. What are labels/selectors?
51. What is Ingress?
52. What is PV?
53. What is PVC?
54. What is HPA?
55. What are liveness/readiness/startup probes?
56. What are resource requests and limits?
57. Explain rolling updates.
58. How do you rollback?
59. What is CrashLoopBackOff?
60. What is ImagePullBackOff?
61. How do you debug a Pending Pod?
62. How do you debug an inaccessible Service?
63. Explain Docker-to-Kubernetes deployment flow.

---

# 48. Final Quick Revision

```text
DOCKER
│
├── Image
│    └── Template
│
├── Container
│    └── Running instance
│
├── Dockerfile
│    └── Image instructions
│
├── Docker Engine
│    ├── API
│    ├── Daemon
│    └── Runtime
│
├── Network
│    ├── bridge
│    ├── host
│    ├── none
│    └── overlay
│
├── Volume
│    └── Persistent data
│
├── Compose
│    └── Multi-container applications
│
└── Registry
     └── Store/distribute images


KUBERNETES
│
├── Cluster
│
├── Control Plane
│    ├── API Server
│    ├── etcd
│    ├── Scheduler
│    └── Controller Manager
│
├── Worker Node
│    ├── Kubelet
│    ├── Runtime
│    └── Networking
│
├── Pod
│    └── Smallest deployable unit
│
├── Deployment
│    └── Manages Pods/rollouts
│
├── Service
│    └── Stable networking
│
├── ConfigMap
│    └── Configuration
│
├── Secret
│    └── Sensitive configuration
│
├── Ingress
│    └── HTTP/HTTPS routing
│
├── PV/PVC
│    └── Persistent storage
│
└── HPA
     └── Automatic Pod scaling
```

---

# 49. Golden Interview Strategy

For Docker and Kubernetes interviews, don't only memorize definitions.

For every topic, prepare these four things:

```text
WHAT?
  ↓
What is it?

WHY?
  ↓
Why do we use it?

HOW?
  ↓
How do we implement it?

REAL EXAMPLE?
  ↓
Where would you use it in a project?
```

For example:

**Question:** What is a Docker volume?

**Good answer structure:**

> "A Docker volume is persistent storage managed by Docker. We use it because container storage is not appropriate for important persistent data. For example, if I run MongoDB in Docker, I can mount a volume to keep database data even if the MongoDB container is recreated."

This structure makes your answers sound practical rather than memorized.

---

# 50. Final Interview Checklist

Before the interview, make sure you can explain without notes:

### Docker
- [ ] Docker architecture
- [ ] Image vs container
- [ ] Container vs VM
- [ ] Dockerfile
- [ ] Docker commands
- [ ] Ports
- [ ] Volumes
- [ ] Networks
- [ ] Docker Compose
- [ ] Registry
- [ ] Multi-stage builds
- [ ] `.dockerignore`
- [ ] Environment variables
- [ ] Docker security
- [ ] Container troubleshooting

### Kubernetes
- [ ] Kubernetes architecture
- [ ] Control Plane
- [ ] Worker Node
- [ ] Pod
- [ ] Deployment
- [ ] ReplicaSet
- [ ] Service
- [ ] ConfigMap
- [ ] Secret
- [ ] Namespace
- [ ] Ingress
- [ ] PV/PVC
- [ ] Probes
- [ ] Requests/limits
- [ ] HPA
- [ ] Rolling update
- [ ] Rollback
- [ ] kubectl commands
- [ ] Troubleshooting

### Practical
- [ ] Containerize Node.js backend
- [ ] Containerize Angular/React frontend
- [ ] Connect containers
- [ ] Use environment variables
- [ ] Push image to registry
- [ ] Create Kubernetes Deployment
- [ ] Create Kubernetes Service
- [ ] Configure health probes
- [ ] Debug failed Pods
- [ ] Explain complete deployment flow

---

# Final One-Line Summary

**Docker packages and runs applications in containers; Kubernetes orchestrates those containerized workloads across a cluster by managing deployment, networking, scaling, configuration, and desired state.**
