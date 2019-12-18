## 安装 Kubectl

> 使用Kubernetes命令行工具kubectl在Kubernetes上部署和管理应用程序。使用kubectl，可以检查集群资源; 创建，删除和更新组件。
>
> 还没有测试安装。 
> 安装Kubernetes集群以后再来安装这个。
> // TODO 

### 目录
* 安装
    * [通过curl安装kubectl二进制文件](#通过curl安装kubectl二进制文件)
    * 作为Google Cloud SDK的一部分下载
* [配置kubectl](#配置kubectl)


### 通过curl安装kubectl二进制文件

#### Linux

1. 下载最新版本：

    ```text
    curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl
    ```
    
    要下载特定版本，请使用特定版本替换`$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)`命令的一部分。

2. 使kubectl二进制可执行

    ```text
    chmod +x ./kubectl
    ```

3. 将二进制文件移动到PATH中

    ```text
    sudo mv ./kubectl /usr/local/bin/kubectl
    ```

### 配置kubectl

#### Linux
为了使kubectl找到并访问Kubernetes集群，需要一个kubeconfig文件，当你使用kube-up.sh创建集群或成功部署Minikube集群时，该文件将自动创建。

1. 检查kubectl配置
    
    通过获取集群状态来检查kubectl是否正确配置：
    ```text
    $ kubectl cluster-info
    ```
    
    如果看到一个URL响应，kubectl被正确配置为访问您的集群。
    
2. 启用shell，使用bash

    要将kubectl自动完成添加到当前shell，请运行source <(kubectl completion bash)。
    
    要将kubectl自动完成添加到你的配置文件中，因此将在以后的shell中自动加载运行：
    
    ```text
    echo "source <(kubectl completion bash)" >> ~/.bashrc
    ```


