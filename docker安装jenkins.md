| 11.11 | jenkins.example.com | 3G   |
| ----- | ------------------- | ---- |
| 11.12 | test.example.com    | java |
| 11.13 | gitlab.exampls.com  | 3G   |

```shell
cat >> /etc/hosts <<EOF 
192.168.11.11 jenkins.example.com 
192.168.11.12 test.example.com 
192.168.11.13 gitlab.example.com 
EOF

cat /etc/docker/daemon.json { 
	"registry-mirrors": ["https://docker.mirrors.ustc.edu.cn"], 	"insecure-registries": ["httlsp://gitlab.example.com:5000"] 
}

docker info

```

@1 @2 @ 3 安装java环境

```shell
rpm -i jdk-8u171-linux-x64.rpm 
echo "export JAVA_HOME=/usr/java/default" >> /etc/profile.d/java.sh 
. /etc/profile.d/java.sh 
java -version
```

@1 安装maven打包工具

```shell
unzip apache-maven-3.5.4-bin.zip -d /opt/ 
mv /opt/apache-maven-3.5.4 /opt/maven 
cd /opt/maven/bin/ 
./mvn --version

#使用docker部署jenkins
$   docker run -d -p 8080:8080 --name jenkins -u root -v /opt/jenkins:/var/jenkins_home  -v /opt/maven:/maven  -v /usr/bin/docker:/usr/bin/docker -v /var/run/docker.sock:/var/run/docker.sock -v /etc/localtime:/etc/localtime  -v /etc/hosts:/etc/hosts  jenkins/jenkins:lts 
$   docker logs -f jenkins 

# 浏览器访问
http://jenkins.example.com:8080
```

@3   docker部署gitlab

```shell
$  docker run -d -h gitlab.example.com -p 8443:443 -p 48080:80 -p 8022:22 --name gitlab --restart always  -v /opt/gitlab/config:/etc/gitlab  -v /opt/gitlab/logs:/var/log/gitlab -v /opt/gitlab/data:/var/opt/gitlab gitlab/gitlab-ce:latest 
 $  docker logs -f gitlab
 $  cat /opt/gitlab/config/initial_root_password

#  浏览器访问
http://gitlab.example.com:48080

# 部署docke私有镜像仓库
docker run -d -v /opt/registry:/var/lib/registry -p 5000:5000 --restart always --name registry registry
```

@1 

```shell
#安装git
yum -y install git 
git config --global user.email "admin@example.com" 
git config --global user.name "admin"

#上传solo项目到gitlab仓库
git clone http://gitlab.example.com:48080/root/solo.git 
tar xf solo-2.9.3.tar.gz 
mv solo-2.9.3/* solo 

cd solo 
git add . 
git commit -m "add solo" 
git tag 1.0.0 
git push origin 1.0.0


# 使用Dockerfile构建基础tomcat镜像

mkdir tomcat && cd tomcat
ls
apache-tomcat-8.5.66.tar.gz  Dockerfile 

vim Dockerfile 
FROM centos:7 
MAINTAINER kgc 
ENV JAVA_HOME /usr/local/jdk 
ADD apache-tomcat-8.5.66.tar.gz . 
RUN mv apache-tomcat-8.5.66 /usr/local/tomcat \ 
	&& rm -rf /usr/local/tomcat/webapps/* \ 
	&& ln -s /usr/local/tomcat/bin/* /usr/local/bin/ \ 
	&& rm -f /etc/localtime \ 
	&& ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
	
EXPOSE 8080 
CMD ["catalina.sh", "run"] 
docker build -t gitlab.example.com:5000/tomcat8 . 
docker push gitlab.example.com:5000/tomcat8:latest



```

## 二进制搭建k8s步骤

```apl
1. 基础环境准备
2. 部署harbor及haproxy⾼可⽤反向代理，实现控制节点的API反问⼊⼝⾼可⽤
3. 在所有master节点安装指定版本的kubeadm 、kubelet、kubectl、docker
4. 在所有node节点安装指定版本的kubeadm 、kubelet、docker，在node节点kubectl为可选安装，看是否需要在node执⾏kubectl命令进⾏集群管理及pod管理等操作。
5. master节点运⾏kubeadm init初始化命令
6. 验证master节点状态
7. 在node节点使⽤kubeadm命令将⾃⼰加⼊k8s master(需要使⽤master⽣成token认证)
8. 验证node节点状态
9. 创建pod并测试⽹络通信
10、部署web服务Dashboard
```
