Q1: Describe the lifecycle of a Docker Container.

Create phase: docker create — name <name-of-container> <docker-image-name>
Running phase: docker run <container-id>
Paused phase/unpause phase: docker pause container <container-id or container-name>, docker unpause <container-id or container-name>
Stopped phase: docker stop <container-id or container-name>
In the stop phase, the container’s main process is shutdown gracefully. Docker sends SIGTERM for graceful shutdown, and if needed, SIGKILL, to kill the container’s main process.
Killed phase: docker kill <container-id or container-name>
In the kill phase, the container’s main processes are shut down abruptly. Docker sends a SIGKILL signal to kill the container’s main process.

Q2: What are the docker namespaces?
Docker uses a technology called namespaces to provide the isolated workspace called the container. When you run a container, Docker creates a set of namespaces for that container. These namespaces provide a layer of isolation.

Q3: What is the difference between CMD and ENTRYPOINT in a Dockerfile?
Both commands are used to execute the first command inside the container however you can override the command written in the CMD but can’t in ENTRYPOINT while running the container.

Q4: Difference between Virtualization and Docker
Virtualization
Virtualization uses a hypervisor to create multiple virtual machines (VMs) on a physical host.
VMs consume more resources as they need a full guest operating system and can be slower to start up.
VMs offer strong isolation as they run separate kernels and operating systems.
VMs can run different operating systems on the same host, allowing for a wide range of application compatibility.
Managing VMs involves more overhead, as each VM needs its own operating system updates, security patches, and resource allocation.

2. Docker
Docker uses containers to package applications and their dependencies. Containers share the host operating system kernel but run in isolated user spaces.
Containers are lightweight and share the host OS, reducing resource overhead and making them faster to start up compared to VMs.
While containers are isolated from each other, they share the same kernel, which means they are generally less isolated than VMs.
Containers are typically used to package single applications and their dependencies, ensuring consistent behavior across different environments.
Managing containers is easier and more efficient, as they share the host OS and can be easily scaled and orchestrated using tools like Kubernetes.

Q5: How to create an image from a running container?
In order to create an image from a running container you need to use docker commit <name of container> <new name of image>

Q6: How to transfer a docker image over the mail or in Pendrive?
For that, first need to save the image using docker save <image-name> > <image-name.tar> and then transfer the image and on the receiver side use docker load < <image-name.tar>

Q7: How to check the layers of the image?
docker history <image-name>

Q8: How to check the metadata of the image?
Docker inspect <image-name>

Q9: How to clean the unused images?
Docker prune: It will only remove the dangling images i.e. the images which do not have a tag or that are not referenced by any container.

Q10: Docker images contain multiple layers so, how can I combine all the layers into one layer?
For that first, we need to run the container from the image and then we can use the docker export command to compress the container (docker export <container-name> > <container-name.tar> and then we need to use 
the docker import command to import the container to an image. (cat <container-nane.tar> | docker import — <image-name>)

Q11: Why use containers and not EC2 instance
Containers:
Containers share the host operating system’s kernel, which reduces overhead compared to virtual machines (like EC2 instances).
Containers are quick to start and stop, enabling rapid deployment and scaling.
Containers can be managed and orchestrated using tools like Kubernetes, Docker Swarm, and Amazon ECS.
Containers facilitate versioning of applications and easy rollbacks to previous versions, which can be crucial for maintaining a reliable and consistent software deployment process

2. EC2:
EC2 instances provide full isolation as each instance runs its own operating system and kernel.
If you have legacy applications that are not easily containerized or require specialized configurations, running them on EC2 instances might be more suitable.
EC2 instances can provide persistent local storage, which might be necessary for applications that require long-term data storage directly on the instance.
EC2 instances offer more flexibility for custom networking configurations and setups, making them a better choice for complex networking architectures.

Q12: What is the use case of docker-compose
Docker Compose is a tool for defining and running multi-container Docker applications.
Docker Compose is particularly useful for orchestrating and managing complex applications that consist of multiple interconnected containers.
In a microservices-based architecture, different parts of an application are split into separate services. Docker Compose allows you to define and manage these services together, making it easier to test and deploy the entire system locally.
If you want to manage your entire application with one command then we can use docker-compose
If your application requires multiple interconnected services, such as a web server, a database, a cache, and a message broker, Docker Compose helps define and manage these components as a single unit.

Q13: What is docker shim?
Docker shim is the container runtime that is used to manage the container lifecycle
The Dockershim is the CRI compliant layer between the Kubelet and the Docker daemon.

Q14: How Will you reduce the size of the Docker image?
Choose a Smaller Base Image: Start with a smaller base image, such as Alpine Linux, which is lightweight and designed for Docker containers.
Minimize Installed Packages: Only install necessary packages and dependencies. Use package managers to remove unnecessary files and keep the image clean.
Use Multi-Stage Builds: Utilize multi-stage builds to separate the build environment from the runtime environment. This allows you to compile and build your application in one stage and copy only the necessary artifacts to the final stage.
Combine RUN Commands: Combine multiple RUN commands into a single command to reduce the number of intermediate layers created in the image.
Use .dockerignore: Create a .dockerignore file to exclude unnecessary files and directories from being copied into the image. This helps keep the image size small.
Use COPY Instead of ADD: If you don't need the additional features of ADD, use COPY instead, as it's more straightforward and doesn't handle URLs or unpack compressed files.
Cleanup Unnecessary Files: Remove temporary and unnecessary files created during the build process, such as log files or cached data.
Use cache data
Minimize Image Layers: Try to minimize the number of layers in your image. Fewer layers reduce the overall image size and improve performance.
Compress Files: Compress files that are copied into the image. Decompress them within the image if needed.

Q15: What is Multi-Stage Build in docker?
Multi-stage builds in Docker is a technique used to create more efficient and smaller Docker images by leveraging multiple build stages within a single Dockerfile. This approach helps reduce the final image size, removes unnecessary dependencies and files, and improves overall image security.
Multi-stage builds address this issue by allowing you to define multiple "stages" within a single Dockerfile. Each stage can have its own base image and set of instructions. The final image will only include the artifacts from the last stage, omitting the intermediate layers. This can significantly reduce the size of the final image.

Q16: What is a Docker swarm?
Docker Swarm is a native clustering and orchestration solution for Docker. It allows you to create and manage a cluster of Docker nodes, and deploy and scale applications on the cluster.
A swarm is a group of Docker engines that are running in swarm mode and joined together. Once the engines are joined in a swarm, they can be used to deploy services. A service is a group of containers that are running a specific image and are deployed on the swarm.
