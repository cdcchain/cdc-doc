
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


# 钱包相关
### 创建钱包
    wallet_create 钱包名 钱包密码（长度不能低于8位）
    示例
    wallet_create  wallet1  12345678

### 打开钱包
    wallet_open 钱包名
    示例
    wallet_open  wallet1

### 解锁钱包
    wallet_unlock 解锁时间 解锁密码
    示例
    wallet_unlock  9999999  12345678

### 锁定钱包
    wallet_lock

### 关闭钱包
    wallet_close

### 列出钱包
    wallet_list

<br/>

# 账户相关（解锁钱包状态下）
### 列出钱包下所有账户
    wallet_list_accounts

### 在钱包下创建本地账户
    wallet_account_create  本地账户名
    示例
    wallet_account_create  acct01

### 获取钱包下本地账户对应地址
    wallet_get_account_public_address  本地账户名
    示例
    wallet_get_account_public_address  acct01

### 获取钱包下本地账户余额
    wallet_account_balance  本地账户名
    示例
    wallet_account_balance  acct01

### 导入wifkey格式私钥
    wallet_import_private_key 私钥 [账户名]  [是否创建账户]
    对于已注册上链账户私钥导入
    示例   
    wallet_import_private_key  私钥
    对于未注册上链账户私钥导入
    示例   
    wallet_import_private_key  私钥  acct01  true

### 导入以太坊格式私钥
    wallet_import_ethereum_private_key 私钥 [账户名]  [是否创建账户]
    对于已注册上链账户私钥导入
    示例   
    wallet_import_ethereum_private_key  私钥
    对于未注册上链账户私钥导入
    示例   
    wallet_import_ethereum_private_key  私钥  acct01  true

### 导出wifkey格式私钥
    wallet_dump_private_key 账户地址
    示例 
    wallet_dump_private_key 0xee2030b1222b8467eb929f0843e60d2d69cbd87f

<br/>

# 交易相关
### 向地址转账
    wallet_transfer_to_address  转账金额 资产标示 本地账户名 入账地址 [memo]
    示例
    wallet_transfer_to_address 100 CDC acct01 0x5046a4334200f78f2f1830a367877f198a6d2020


### 向注册账户转账
    wallet_transfer_to_public_account 转账金额 资产标示 本地账户名 入账账户名 [memo]
    示例
    wallet_transfer_to_public_account 100 CDC acct01 cdc0

### 账户历史交易查询
    wallet_account_transaction_history 账户名 资产名 交易数量limit 开始块号 结束块号
    示例
    wallet_account_transaction_history cdc1 CDC 10 0 100000

<br/>

# 合约相关
### 向合约转账
    wallet_transfer_to_contract 转账金额 资产标示 本地账户名 合约名/地址 gas费
    示例
    wallet_transfer_to_contract 10 CDC cdc1 C9431c4b6308a943bbe0355db48bd5852eaa45a5f 10

### 注册合约
    contract_register 本地账户名 合约gpc文件路径 资产标示 gas费
    示例
    contract_register cdc1 /home/ubuntu/cdc-dapp/user_receipt_data.glua.gpc CDC 10

### 调用合约（产生链上交易）
    contract_call 合约名/地址 本地账户名 调用方法 方法参数 资产标示 gas费
    示例
    contract_call C6c58f2e07af666a1100c9b1fa2f0f4ae45a99e55 cdc1 abolishUserReceiptHash "e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855" CDC 1

### 调用合约本地接口（不产生链上交易）
    contract_call_offline 合约名/地址 本地账户名 调用方法 方法参数
    示例
    contract_call_offline C6c58f2e07af666a1100c9b1fa2f0f4ae45a99e55 cdc1 verifyUserReceiptHash e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855

### 升级合约
    contract_upgrade 合约地址 本地账户名 合约名 合约描述 资产标示 gas费
    示例
    contract_upgrade C6c58f2e07af666a1100c9b1fa2f0f4ae45a99e55 cdc1 "NewContract" "my new contract" CDC 1

### 销毁合约
    contract_destroy 合约地址 本地账户名 资产标示 gas费
    示例
    contract_destroy C6c58f2e07af666a1100c9b1fa2f0f4ae45a99e55 cdc1 CDC 1

### 查询合约基本信息
    contract_get_info 合约名/地址
    示例
    contract_get_info C6c58f2e07af666a1100c9b1fa2f0f4ae45a99e55

