---
title: Docker入门讲解
date: 2025-01-16 10:04:00
tags:
  - 基础知识
categories: Docker
photos: /tupian/Docker.png
---

# Docker 简介

**Docker** 是一个开源的 **容器化平台**，用于开发、部署和运行应用程序。它通过将应用程序及其依赖项打包到一个轻量级的容器中，实现了应用程序的跨平台和一致性运行。

---

## Docker 的核心概念

### 1. **容器（Container）**

- 容器是一个轻量级的、独立的、可执行的软件包，包含运行应用程序所需的所有内容（代码、运行时、库、环境变量等）。
- 容器与虚拟机不同，它共享主机操作系统的内核，因此更加轻量级和高效。

### 2. **镜像（Image）**

- 镜像是一个只读模板，用于创建容器。它包含应用程序的代码、运行时、库和配置文件。
- 镜像可以从 Docker Hub（公共镜像仓库）或私有仓库中拉取。

### 3. **Dockerfile**

- Dockerfile 是一个文本文件，包含构建镜像的指令（如基础镜像、安装软件、复制文件等）。

### 4. **Docker Hub**

- Docker Hub 是一个公共的镜像仓库，用户可以从中拉取官方或社区提供的镜像。

---

## Docker 的本质

- 运行 Docker 的本质就是在 Linux 内核中制造一个隔离的文件环境，来运行相关的操作。

---

## Docker 的优势

- **一致性**：容器在任何环境中都能以相同的方式运行，避免了“在我机器上能运行”的问题。
- **轻量级**：容器共享主机内核，资源占用少，启动速度快。
- **隔离性**：容器之间相互隔离，互不影响。
- **可移植性**：容器可以在任何支持 Docker 的平台上运行（如 Linux、Windows、macOS）。
- **易于扩展**：通过 Docker Compose 或 Kubernetes 可以轻松管理多个容器。

---

## Docker 的使用场景

- **开发环境**：为开发团队提供一致的开发环境，避免环境配置问题。
- **持续集成/持续部署（CI/CD）**：在 CI/CD 流水线中使用 Docker 构建和测试应用程序。
- **微服务架构**：将应用程序拆分为多个微服务，每个微服务运行在独立的容器中。
- **本地测试**：在本地运行复杂的多服务应用程序（如数据库、消息队列等）。
- **云计算**：在云平台上部署和管理容器化应用程序。

---

## 如何在 Windows 上使用 Docker

在 Windows 上使用 Docker 需要安装 **Docker Desktop**，它支持 Windows 10 及以上版本。

### 1. **安装 Docker Desktop**

1. 下载 Docker Desktop：

   - 访问 Docker 官网：[https://www.docker.com/products/docker-desktop](https://www.docker.com/products/docker-desktop)
   - 下载并安装 Docker Desktop。

2. 启用 WSL 2 或 Hyper-V：

   - 系统要求：
     WSL2：⽐较适合开发环境。
     Hyper-V：则更适⽤于⽣产环境，特别是在需要⾼性能和稳定性的情况下。
   - Docker Desktop 需要 WSL 2 或 Hyper-V 支持。
   - 如果使用 WSL 2，请确保已启用 WSL 2 并安装 Linux 发行版。
   - 这里选择的是 WSL2 作为示例
     ![](/tupian/wsl2.png)
   - 并且官方还提到，我们需要先卸载其他的版本，否则造成冲突
     ![](/tupian/wsl2.1.png)

3. 启动 Docker Desktop：
   - 安装完成后，启动 Docker Desktop。
   - Docker 会在系统托盘中运行。

### 2. **使用 Docker**

1. **拉取镜像**：

   - 打开 PowerShell 或命令提示符，运行以下命令拉取一个镜像（如 Ubuntu）：
     ```bash
     docker pull ubuntu
     ```

2. **运行容器**：

   - 使用以下命令运行一个容器：
     ```bash
     docker run -it ubuntu bash
     ```
     这会启动一个 Ubuntu 容器并进入交互式 Shell。

3. **构建镜像**：

   - 创建一个 Dockerfile，然后使用以下命令构建镜像：
     ```bash
     docker build -t my-image .
     ```

4. **管理容器**：
   - 查看运行中的容器：
     ```bash
     docker ps
     ```
   - 停止容器：
     ```bash
     docker stop <容器ID>
     ```
   - 删除容器：
     ```bash
     docker rm <容器ID>
     ```

---

## Docker 的常用命令

### 1. **镜像相关**

- 拉取镜像（从一个仓库取一个装满货物的集装箱）：`docker pull <镜像名>`
- 列出镜像（查看仓库⾥有哪些可⽤的集装箱）：`docker images`
- 删除镜像（删除某个不再需要的集装箱模板）：`docker rmi <镜像ID>`

### 2. **容器相关**

- 运行容器（将集装箱吊装到卡⻋上，启动运输）：`docker run <镜像名>`
- 列出容器（查看哪些集装箱正在运输/使⽤）：`docker ps`（查看运行中的容器），`docker ps -a`（查看所有容器）
- 停止容器（将集装箱从卡⻋上卸下，停⽌运⾏）：`docker stop <容器ID>`
- 删除容器（销毁⼀个不再需要的集装箱实例）：`docker rm <容器ID>`

### 3. **构建镜像**

- 使⽤ Dockerfile 构建镜像（根据⻝谱制作⼀个全新的菜品）：`docker build -t <镜像名>`

### 4. **调试容器**

- 查看容器⽇志（检查运输过程中发⽣了什么）：`docker logs <容器ID>`
- 进入容器（进⼊集装箱内部，检查货物情况）：`docker exec -it <容器ID> bash`

---

## Docker 的生态系统

- **Docker Compose**：用于定义和运行多容器应用程序。
- **Docker Swarm**：Docker 原生的容器编排工具。
- **Kubernetes**：更强大的容器编排平台，支持大规模容器部署。
- **Docker Hub**：公共镜像仓库，提供大量官方和社区镜像。

---

## Docker 汉化

- 这里的 github 仓库中提供了一个汉化包（但是不太建议汉化，虽然汉化后很多操作会比较方便易懂）
  [汉化链接](https://github.com/asxez/DockerDesktop-CN)

---

## 添加一个 hub 源

- 这是一个国内的镜像
  目的：不用魔法，去拉取 docker hop 里面的一些东西
- 请严格按照路径修改对应的文件
  ![图片](/tupian/dockerguonei.png)
  ```bash
  "registry-mirrors": [
    "https://docker.m.daocloud.io"
  ]
  ```

---

## 总结

- Docker 是一个强大的容器化平台，能够显著简化应用程序的开发、测试和部署流程。在 Windows 上，可以通过 Docker Desktop 轻松使用 Docker。如果你需要跨平台、一致性的开发环境，或者正在构建微服务架构，Docker 是一个非常好的选择。