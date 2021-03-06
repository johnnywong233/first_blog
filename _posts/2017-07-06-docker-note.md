//必知

```
<image_id> == <rigestry_name>/<org_name>/<image_name>:<tag_name>
```
一个<image_id>可以对应多个完整的<image_name>

//删除空悬的images，即```<none>:<none>```

```
docker rmi --force $(docker images -f dangling=true -q) 
```

//下载镜像images

```
docker pull <rigestry_name>/<org_name>/<image_name>:<tag_name>
```

//如果pull下载失败，依据提示可能需要登录

```
docker login <rigestry_name>
```

//上传镜像images，不仅仅需要登录，还需要push的admin权限
```
docker push <rigestry_name>/<org_name>/<image_name>:<tag_name>
```
docker push时不指定tag，会把当前host环境所有的匹配images的都push上去。如：

//build 镜像images, 需要在dockerfile所在目录下面执行，注意后面的点
```
docker build --build-arg http_proxy=http://<host>:<port>--build-arg https_proxy=https://<host>:<port> -t hello-world:1.0 .
docker build --build-arg http_proxy=http://web-proxy.sgp.hpecorp.net:8080 --build-arg https_proxy=https://web-proxy.sgp.hpecorp.net:8080 -t hub.docker.hpecorp.net/shared/itom-demo-core-tech-service:1.0 .
```

//将镜像run起来，变成container
```
docker run -it -p 15432:5432 -v /root:/mount hello-world:1.0 /bin/bash
```

//保存镜像images为tar包，分别不同是主机的拷贝：
```
docker save -o /<save_path>/*.tar <image_id>
docker save -o /<save_path>/*.tar <image_name>
docker save <image_name> -o /<save_path>/*.tar
```

//从tar包load 生成images
```
docker load -i *.tar
```

//重新生成tar，新打一个image
```
docker tag <image_id> localhost:5000/mng-portal:1.5
```

//kill running containers
```
docker kill `docker ps -q`
```

//从容器拷贝文件到主机host上去
```
docker cp <containerId>:<containerPath> <hostPath>
```
//示例
```
docker cp 4755137f8c52:/opt/apache-tomcat-8.0.24/webapps/idm-service/WEB-INF/classes/seeded/hellfire__1.1.0001_1__Add_Seeded_Users.json /root
```

//从主机上拷贝文件到容器内
```
docker cp ./xxxx.json 4755137f8c52:/
```

//list all containers：
```docker ps -a```

//删除images
```
docker rmi -f <images_id>
```

//删除容器containers
```
docker rm -f <container_id>
```

在build data images时要有不同的version, folder, suitefeature.json，HCM suite的做法是设置一个变量：
![](https://github.com/johnnywong233/first_blog/raw/gh-pages/_posts/img/data_images.png)




