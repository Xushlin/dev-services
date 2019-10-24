
# 基于 Kubernetes 为 .NET Core 应用程序 CI/CD 环境


## 创建 Kubernetes 环境

推荐使用 [Azure Kubernetes](https://azure.microsoft.com/zh-cn/services/kubernetes-service/) 服务。你也可以使用 [Minikube](https://minikube.sigs.k8s.io/) 在自己的电脑上运行一个 Minikube 环境。

本 Workshop 所需的 Minikube 集群至少需要 8GB 内存。

## 部署 CI/CD 工作坊环境

确保你能够运行 Shell 脚本。在 Windows 机器上，请安装并运行 [Git](http://git-scm.com)，并启动 Git Bash 命令行工具。

**第一步，确保登录到 Kubernetes 环境**

在你本地安装 `kubectl` 命令行工具，运行以下命令，以确保你的 `kubectl` 命令安装正确：

```sh
kubectl cluster-info
kubectl get namespaces
```

**第二步，编辑变量文件**

找到本项目目录下的 `templates/vars` 文件，使用文本编辑器编辑其中的变量。各个变量的含义如下：

| 变量 |  描述  |  
|----|----|
| dns_suffix | 环境中 Ingress 使用的顶级域名
| import_repo | 要向 gogs、Jenkins 中默认导入的 Git 项目 |
| gogs_repo_name | 将项目导入 gogs 时，使用的名称 |
| deploy_suffix | 本次部署的标识（可不改，在运行部署脚本时指定） |

**第二步，运行部署脚本**

运行以下脚本，并部署你的 CI/CD 环境

```sh
./provision.sh --suffix $(id -un)
```