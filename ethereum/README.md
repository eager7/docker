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
```bash
> eth.mining
false
```
创建账户并开启挖矿：
```bash
> personal.newAccount("eospark")
"0xade1fafd8b3f0c902b06dfac9bf9186c3d5a3a3b"
> miner.start(1)
null
```
查看log：
```bash
NFO [03-12|08:56:25.359] ð¨ mined potential block                  number=1 hash=471807…c06828
INFO [03-12|08:56:25.360] Commit new mining work                   number=2 sealhash=101a8f…0ac386 uncles=0 txs=0 gas=0 fees=0 elapsed=195.735µs
INFO [03-12|08:56:26.575] Generating DAG in progress               epoch=1 percentage=7  elapsed=11.165s
INFO [03-12|08:56:27.913] Generating DAG in progress               epoch=1 percentage=8  elapsed=12.503s
INFO [03-12|08:56:29.103] Generating DAG in progress               epoch=1 percentage=9  elapsed=13.693s
```
此时已经开始出块：
```bash
> eth
{
  accounts: ["0xade1fafd8b3f0c902b06dfac9bf9186c3d5a3a3b"],
  blockNumber: 3,
  coinbase: "0xade1fafd8b3f0c902b06dfac9bf9186c3d5a3a3b",
```