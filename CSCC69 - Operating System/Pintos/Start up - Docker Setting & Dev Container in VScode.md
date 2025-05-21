---
tags:
  - setting
  - debug
---
## 🧩 遇到的问题...

### 1. 问题表现

- 在使用 VSCode 的 Dev Container 自动构建 `pintos1` 镜像时，频繁出现如下问题：
    
    - "pull access denied for pintos1" 错误（即使本地已有 image）
        
    - "An error occurred setting up the container"，devContainersSpecCLI 报错
        
    - 构建与运行流程中反复报错但本地 `docker run` 手动执行成功
        
- DevContainer 通过 `.devcontainer/devcontainer.json` 自动构建失败，即使使用了 `--platform=linux/amd64`。
    

### 2. 基本环境和条件

- 本机是 Mac（Apple Silicon，ARM 架构）
    
- 使用 VSCode Remote - Containers 插件构建 DevContainer
    
- 使用的是本地自定义 Dockerfile，镜像名为 `pintos1`
    
- Docker Desktop 和 `docker build` 均可正常运行，并能手动运行构建好的容器

---

## 📦 Docker 架构与 DevContainer 配置结构

### Dockerfile 的作用

- 定义如何构建你的基础开发环境，包括安装依赖、设置环境变量、默认工作目录等
    

### devcontainer.json 的作用

- 定义 VSCode 如何运行这个环境，包括：
    
    - 使用镜像或构建 Dockerfile
        
    - 启动参数（如 `runArgs`）
        
    - 工作目录、挂载方式
        
    - 构建后执行的初始化命令等
        

### Dockerfile 重要字段

- `FROM`：基础镜像（如 ubuntu）
    
- `RUN`：安装软件、配置环境
    
- `ENV`：设置环境变量
    
- `WORKDIR`：指定容器默认工作目录
    
- `CMD`：容器启动后默认执行的命令（可选，但建议指定， 比如`"bash"`）
    

### devcontainer.json 重要字段

- `image`：使用本地构建的镜像名
    
- `build`：构建配置（若希望让 VSCode 构建 Dockerfile）
    
- `workspaceFolder`：容器中的工作目录路径
    
- `mounts`：挂载本地目录到容器中
    
- `runArgs`：额外的 `docker run` 参数，如 `--platform`
    
- `postCreateCommand`：容器构建后自动执行脚本
    

---

## 🔁 mount & COPY 

### mount 是什么？具体作用？
-  Docker 中的 `mount` 是挂载机制，用来把主机（host）上的目录或文件挂载到容器（container）内部。
- 在 `devcontainer.json` 中定义挂载（mount）后，本地文件会映射到容器中，实时同步。
    
- 类型：
    
    - `type=bind`：将主机文件夹直接挂载, 例如：
    ```json
    "mounts": [
      "source=${localWorkspaceFolder},target=/pintos,type=bind"
    ]
    ```
        
    - `type=volume`：Docker 自己管理的数据卷
        

### COPY 与 mount 区别

- `COPY` 是在构建阶段将文件复制到镜像中，是静态的
    
- `mount` 是在运行时将主机目录映射进容器，是动态的
    

📌 如果一个路径既 `COPY` 又被 `mount`，则运行时 `mount` 会覆盖 `COPY` 的内容。

---

## 🔨 build vs image

- `docker build`：执行 Dockerfile，生成镜像（image）
    
- `image`：镜像是可以被用来启动容器的“模板”
    

### `devcontainer` 中的两种方式：

1. 用 `"image": "pintos1"` 表示用已有镜像，不重建
    
2. 用 `"build"` 字段表示 VSCode 使用 Dockerfile 自动构建
####  `build` 中的`context` (构建上下文) 说明:

- 构建上下文是指 `docker build` 命令中 `.` 所代表的目录
    
- 它决定了 Dockerfile 中 `COPY` 指令可以访问的文件范围
    
- 在 VSCode DevContainer 中，默认是整个工作目录

⚠️但是要注意: 每个路径path对应的目录，到底是工作目录，根目录还是当前目录，不要搞混了呀

## ⚠️ Apple Silicon 架构下 VSCode 的构建陷阱

- 在 Apple Silicon（arm64 架构）Mac 上，VSCode Dev Container 默认会使用本地主机架构（即 arm64）进行构建
    
- VSCode 无法通过 `devcontainer.json` 使用 `buildx` 构建跨架构镜像
    
- 即使你在 `runArgs` 中添加了 `--platform=linux/amd64`，也只影响运行，不影响构建架构
    
- 如果你构建出的镜像是 arm64 架构，而在运行阶段使用 `--platform=linux/amd64` 启动容器，则 VSCode 会找不到架构匹配的镜像，即使镜像名相同，也会报出:
🚫 **"pull access denied for pintos1"** 错误

### ✅ 解决方法：手动使用 buildx 构建目标平台镜像

```bash
docker buildx build --platform linux/amd64 -t pintos-amd64 . --load
```

然后在 `devcontainer.json` 中：

```json
"image": "pintos-amd64",
"runArgs": ["--platform=linux/amd64"]
```

- 这样 VSCode 会直接运行你已构建好的镜像，避免架构不一致
    
- `--load` 是必须的，否则镜像只会存在于 cache 中，VSCode 无法识别
- 镜像一旦在本地存在，VSCode 就能稳定使用它，无需再次 QEMU 模拟
    

---


## 💻 ARM 架构相关问题与 QEMU 模拟

### 为何必须使用 `--platform=linux/amd64`

- Mac M 系列是 ARM 架构，但 Pintos（基于 x86）只能在 amd64 环境运行
    
- 默认构建出的镜像是 arm64 架构，直接运行会导致兼容性问题
    

### QEMU 模拟与两种方式对比

| 构建方式      | 描述                      | 问题                          |
| --------- | ----------------------- | --------------------------- |
| 默认构建      | VSCode 使用主机架构（arm64）构建  | 构建出的镜像架构为 arm64，无法运行 Pintos |
| buildx 模拟 | 手动通过 QEMU 模拟 amd64 架构构建 | 构建阶段较慢，成功后运行稳定              |

### QEMU 是什么？

- 是一种动态二进制翻译器（DBT）
    
- 在构建阶段负责将 Dockerfile 中 amd64 指令翻译为 ARM64 执行
    
- 效率低、容易出错、构建过程不稳定
    

📌 **但构建成功后，使用 `--load` 将镜像载入本地镜像池，运行阶段将直接使用该真实的 amd64 架构镜像，避免再次触发 QEMU 模拟，因此容器启动过程将更稳定，性能也更高。**

⚠️ **但需要注意：运行时仍必须使用 `--platform=linux/amd64` 来确保 VSCode 正确使用该架构镜像。如果省略该参数，VSCode 可能会尝试拉取与主机架构（arm64）匹配的镜像，从而导致镜像找不到或不兼容。**

### Bochs 与 QEMU 的关系

- Bochs 是你在容器中主动运行的 x86 模拟器，用于运行 Pintos
    
- 与宿主机架构无关，bochs 本身就是模拟器，在任何平台都通过软件方式模拟硬件环境
    

---

## 🔍 buildx 的原理与用途

- `buildx` 是 Docker 的 BuildKit 构建引擎扩展，支持：
    
    - 并行构建
        
    - 缓存复用
        
    - 多平台构建（跨架构）
        

### 为什么需要 `--platform` 和 `--load`

- `--platform=linux/amd64`：模拟并构建出 x86 架构镜像（而非默认的 arm64）
    
- `--load`：将构建结果写入本地镜像池，让 `docker run` 和 VSCode 找到该镜像
    

```bash
docker buildx build --platform linux/amd64 -t pintos1 . --load
```

若不加 `--load`，镜像不会出现在 `docker images` 中，VSCode 无法使用。

---
## 🧱 VSCode Dev Container 的架构限制总结

- VSCode 默认构建流程使用主机架构（arm64）
    
- 不支持自动使用 `buildx` 构建 amd64 镜像
    
- 构建出的镜像和运行指定架构不一致时，即使镜像名一致，也会报错找不到镜像
    

✅ 解决方案：

1. 使用 `buildx` 构建 amd64 镜像
    
2. 使用 `--load` 将镜像载入本地镜像池
    
3. `devcontainer.json` 中使用 `image` 字段显式引用镜像
    
4. 使用 `runArgs` 指定运行架构

---

## 🔧 Bochs 安装问题

| 安装方式 | Dockerfile 中安装 | init.sh 中延迟安装 |
| ---- | -------------- | ------------- |
| 优点   | 一步到位           | 避免构建失败、可调试    |
| 缺点   | 安装过程复杂、易失败     | 增加容器首次启动时间    |
换成新版本的ubuntu之后，Bochs可能会因为old library version安装失败。
又一个版本不兼容问题(大概吧)

![[Screenshot 2025-05-21 at 1.57.03 AM.png]]

✅**可能的误打误撞的解决方法**：在 Dockerfile 中安装基础依赖，在 `init.sh` 中延迟安装 bochs。
- 缺点大概是每次rebuild 都要重装吧, 但是目前rebuild和reopen都是稳定的，欣慰住了

![[Screenshot 2025-05-21 at 1.58.32 AM.png]]

---

## 🧾 init.sh 脚本


```bash
#!/bin/bash

set -e # 如果有错误就停止执行

cd /pintos/src/misc

wget --no-check-certificate https://sourceforge.net/projects/bochs/files/bochs/2.6.11/bochs-2.6.11.tar.gz
sh ./bochs-2.6.11-build.sh /usr/local
rm -f bochs-2.6.11.tar.gz

cd /pintos/src/utils
make
 
cd /pintos/src/threads
make

```

确保：

- 文件具备执行权限：`chmod +x init.sh`
    
- 设置在 devcontainer.json 中：
    
```json
"postCreateCommand": "init.sh"
```
- 可能是这个脚本的问题，意外的解决了Bochs的安装问题嘛，反正确实是成功装上了

---

## ✅ 当前配置

- 希望它能好好的🙏

### Dockerfile

```Dockerfile
FROM ubuntu:22.04

RUN apt-get update \
	&& DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
		bash \
		build-essential \
		gdb \
		gcc \
		emacs \
		vim \
		nano \
		qemu \
		wget \
		xorg-dev \
		libncursesw5 \
		libncurses5-dev \
		dos2unix \
		expect \
		rsync \
		git\
	&& apt-get clean \
	&& rm -rf /var/lib/apt/lists/* 

RUN mkdir -p /pintos/src

ENV PINTOS_HOME=/pintos

ENV PATH=/pintos/src/utils:$PATH

WORKDIR /pintos
```

### 构建镜像

```bash
docker buildx build --platform linux/amd64 -t pintos-amd64 . --load
```

### `.devcontainer/devcontainer.json`

```json
{
	"name": "C69-Pintos",
	"image": "pintos-amd64",
	"workspaceFolder": "/pintos",
	"mounts": [
		"source=${localWorkspaceFolder},target=/pintos,type=bind"
		],
	"runArgs": ["--platform=linux/amd64"],
	"customizations": {
		"vscode": {
			"settings": {
				"terminal.integrated.defaultProfile.linux": "bash"
			},
			"extensions": [
				"ms-vscode.cpptools"
			]
		}
	},
	"postCreateCommand": "./init.sh"
}
```

---

## 📌 其他注意事项
  
- `mount` 路径不要重叠（如既挂项目又单挂 src）
- chatGPT不行，自己看log debug真的快很多（但是整理文档很不错， 希望它没有给我提供错误的知识hope so）
- 要在Docker  Desktop的setting中分配足够的资源，尤其是memory limit！
	- （还好买电脑的时候特意定了32gb 的ram，让我可以安心分配 ）（风扇都不跑的感觉真好）（我之前是怎么用的下去那个8gb ram的MacBook的，年少无知啊）




