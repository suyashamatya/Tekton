Why should you start off Tekton with WSL? (and commands you will use while working with Tekton). Windows Subsystem for Linux (WSL) is beneficial for development in Tekton pipelines for several reasons:
\
Linux Compatibility:

Full Linux Kernel: WSL 2 includes a full Linux kernel, which allows running Linux binaries natively. This ensures better compatibility with Linux tools and applications.
Package Managers: WSL provides access to Linux package managers like APT or Yum, making it easier to install and manage Linux software.
Development Environment:

Familiarity for Linux Developers: Developers accustomed to Linux environments find it more comfortable to work with WSL as it provides a Linux-like shell and tools.
Cross-Platform Development: WSL allows developers to work seamlessly across Windows and Linux platforms, enabling consistent development environments.
Tooling and Scripting:

Bash Shell: WSL supports Bash, a popular shell in the Linux world, which is widely used for scripting and automation.
Linux Commands: Linux commands and utilities work directly in WSL, allowing developers to leverage a vast ecosystem of Linux tools without modification.
File System Performance:

File System Integration: WSL 2 has improved file system performance by integrating better with the host Windows file system. This is particularly beneficial for I/O-intensive tasks.
Containerization:

Docker Integration: WSL integrates well with Docker, allowing for a smoother experience when working with containers and containerized applications.
Compatibility with DevOps Tools:

CI/CD Pipelines: Many CI/CD pipelines and DevOps tools are designed to work with Linux environments. WSL facilitates compatibility with these tools, making it easier to integrate into existing workflows.
Networking:

Network Stack: WSL 2 has its network stack, allowing for improved networking performance and compatibility, especially in scenarios involving networking-intensive tasks.
When working on a project like IBM's Tekton CI/CD pipeline, you'll likely need to interact with various tools and commands. Here are some commands you might find useful:

kubectl: Kubernetes command-line tool. Used to deploy and manage applications on Kubernetes clusters.

```
kubectl get pods
kubectl apply -f deployment.yaml
```

go: The Go programming language. If you're working on a Go project, you'll use commands like:
```
go build
go test
```

ko: A tool for building and deploying Go applications to Kubernetes. Common commands include:

```
ko apply -f deployment.yaml
ko resolve -f deployment.yaml
```

git: Version control system. Common commands:
```
git clone <repository_url>
git pull
git commit -m "Commit message"
```
docker: If your project involves containerization, Docker commands will be essential:
```
docker build -t image_name .
docker run -p 8080:80 image_name
```
Tekton CLI: Commands for interacting with Tekton pipelines:

```
tkn pipeline list
tkn task start
```
