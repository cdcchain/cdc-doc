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

# 交易所涉及接口（基本接口）
### RPC登录

    请求方法：login
    请求参数：rpc 用户名、 rpc 密码

    Request:
    {"method":"login","id":20180517134424944,"jsonrpc":"2.0","params":["admin","123456"]}
    
    Response：
    {"id":"20180517134424944","result":true}
    
    
### 获取节点信息

    请求方法：info
    请求参数：无

    Request:
    {"method":"info","id":20180523092052345,"jsonrpc":"2.0","params":[]}
    
    Response：
    {
	  "blockchain_head_block_num": 23324,
	  "blockchain_head_block_age": "3 seconds old",
	  "blockchain_head_block_timestamp": "2018-08-20T02:19:00",
	  "blockchain_head_block_id": "1a0898af285ac0be5c4073f1d8c1de1a67a822bf",
	  "blockchain_average_delegate_participation": "100.00 %",
	  "blockchain_confirmation_requirement": 1,
	  "blockchain_share_supply": "10,000,000,000.00000000 CDC",
	  "blockchain_blocks_left_in_round": 7,
	  "blockchain_next_round_time": "at least 67 seconds in the future",
	  "blockchain_next_round_timestamp": "2018-08-20T02:20:10",
	  "blockchain_random_seed": "9ae06503a1343fa3547b3011b158d1a3970b7a28",
	  "client_data_dir": "/home/ubuntu/cdc-data",
	  "client_version": "CDC",
	  "network_num_connections": 6,
	  "network_num_connections_max": 200,
	  "ntp_time": "2018-08-20T02:19:03",
	  "ntp_time_error": "0.00314100000000000",
	  "wallet_open": true,
	  "wallet_unlocked": true,
	  "wallet_unlocked_until": "3 years2 months in the future",
	  "wallet_unlocked_until_timestamp": "2021-10-17T19:30:31",
	  "wallet_last_scanned_block_timestamp": "2018-08-20T02:19:00",
	  "wallet_scan_progress": "100.00 %",
	  "wallet_block_production_enabled": true,
	  "wallet_next_block_production_time": "at least 67 seconds in the future",
	  "wallet_next_block_production_timestamp": "2018-08-20T02:20:40"
	}
    
    当blockchain_head_block_age的值小于10秒，说明本地最新区块的区块高度已经达到了CDC区块链的最新高度
    blockchain_head_block_num 本地最新区块的区块高度
    
    
### 获取最新区块高度

    请求方法：blockchain_get_block_count
    请求参数：无

    Request:
    {"method":"blockchain_get_block_count","id":20180523112440522,"jsonrpc":"2.0","params":[]}
    
    Response：
	{"id":"20180523112440522","result":23324}    
