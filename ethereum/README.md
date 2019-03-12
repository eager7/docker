#### 构建镜像
在目录下执行make即可构建镜像

#### 启动镜像
执行make run即可启动镜像，容器将在后台运行
```bash
➜  ethereum git:(master) make run
docker-compose up -d
/usr/lib/python2.7/site-packages/requests/__init__.py:91: RequestsDependencyWarning: urllib3 (1.24.1) or chardet (2.2.1) doesn't match a supported version!
  RequestsDependencyWarning)
Creating eos_docker_tools ... done
```

#### 开启挖矿
程序默认是没有开启挖矿功能的，我们需要添加一个账户并且开始挖矿：
进入容器：
```bash
➜  ~ docker exec -it ethereum_private sh
/ethereum # geth attach --datadir /ethereum/ 
```
查询状态：
