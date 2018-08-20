# 系统环境软硬件需求
* 操作系统：Ubuntu 16.04 LTS64位系统
* 硬件：CPU2核心  内存8GB  硬盘100GB  带宽4M

<br/>
<br/>

# 启动rpc服务
支持tcp jsonrpc 以及 http jsonrpc
支持jsonrpc 2.0

### 启动tcp jsonrpc支持（示例）
    cdc --rpcuser admin --rpcpassword 123456 --rpcendpoint 127.0.0.1:10086 --server --data-dir chain_data

### 启动http jsonrpc支持（示例）
    cdc --rpcuser admin --rpcpassword 123456 --httpdendpoint 127.0.0.1:8080 --server --data-dir chain_data

### 客户端发起rpc请求如何使用rpcuser以及rpcpassword
* tcpjsonrpc
需要先发起一个login的请求，参数分别为rpcuser，rpcpassword
* httpjsonrpc
基于basic authentication

<br/>
<br/>

# 交易所涉及接口（用户地址创建）
