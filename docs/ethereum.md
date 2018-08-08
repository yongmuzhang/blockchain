# 以太坊

## 安装部署
本文提供三种方式，分别是ethereum/client-go的docker镜像、编译执行ethereum/go-ethereum源码和truffle套件

### Docker镜像(推荐)
> Docker环境安装(google)

> 安装部署启动
>> 命令形如：docker run -d --name ethereum-node -v /Users/zym/ethereum:/root -p 8545:8545 -p 30303:30303 ethereum/client-go --rpcaddr 0.0.0.0 --rpc --rpccorsdomain "*" --rpcvhosts=* --syncmode=light --rpcapi "web3,eth" --testnet
>>>JSON-RPC监听端口:8545

>>>UDP监听端口:30303

>>>HTTP-RPC server listening interface:--rpcaddr 0.0.0.0 

>>>--rpc:开启HTTP-RPC server

>>>--rpccorsdomain "*":开启跨域请求

>>>--syncmode:轻节点(light),全节点(full),快节点(fast)

>>>--testnet:--testnet(testnet测试网络),--rinkeby(rinkeby测试网络),默认主网络

>>> --rpcvhosts=*:解决invalid host specified错误，接收请求的主机名字，*表示所有

>在容器中执行命令

>>docker exec -it ethereum-node sh

>>cd /root/.ethereum

>>geth attach ipc://root/.ethereum/geth.ipc

>>personal.listAccounts等


### 编译客户端源码
> 克隆[ethereum/client-go](https://github.com/ethereum/go-ethereum)源码

> 安装GO和C

> 运行make geth或者make all

>> !!!如果报错，很可能是GO的版本小于1.7, [安装说明](https://launchpad.net/~gophers/+archive/ubuntu/archive)
````javascript
sudo apt-get install python-software-properties
sudo add-apt-repository ppa:gophers/go
sudo apt-get update
sudo apt-get install golang-1.9
````
> 部分命令

>> 同步模式：--syncmode，light轻节点，fast快节点，full全节点，默认全节点
````javascript
The Light Ethereum Subprotocol (LES) is the protocol used by “light” clients, which only download block headers as they appear and fetch other parts of the blockchain on-demand.
````
```javascript
Full Sync: Gets the block headers, the block bodies, and validates every element from genesis block.
Fast Sync: Gets the block headers, the block bodies, it processes no transactions until current block - 1024. Then it gets a snapshot state and proceeds like a full sync.
Light Sync: Gets only the current state. To verify elements, it needs to ask to full (archive) nodes for the corresponding tree leaves.
```

>> 接入网络：--testnet(testnet测试网络)，--rinkeby(rinkeby测试网络)，默认主网络

>> --rpcvhosts=*:解决invalid host specified错误，接收请求的主机名字，*表示所有

>> --rpc: 开启rpc调用

>> --rpcaddr: rpc 监听接口地址

### Truffle套件(初学者推荐)
> 参考[trufflesuite/ganache-cli](https://github.com/trufflesuite/ganache-cli)