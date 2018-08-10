
# 基本指令（链相关）

### 获取当前区块链高度
	blockchain_get_block_count 
	示例
	blockchain_get_block_count
	返回  当前区块链的块高度
  
### 获取当前区块链同步状态
	blockchain_is_synced 
	示例
	blockchain_is_synced
	返回  同步状态
  
### 获取当前区块链基本信息
	info
	示例
	info
	返回 当前当前区块链基本信息
  
### 获取块信息
	blockchain_get_block 区块高度
	示例
	blockchain_get_block 1
	返回 当前块信息
  
### 获取交易信息  
	blockchain_get_transaction 交易hash
	示例
	blockchain_get_transaction f4659e6c32aedc937c63c4a41bd5e60be65cc453
	返回 当前交易信息

### 获取区块签名者  
	blockchain_get_block_signee 区块高度
	示例
	blockchain_get_block_signee 1
	返回 区块签名者
  
### 获取区块中交易  
	blockchain_get_block_transactions 区块高度
	示例
	blockchain_get_block_transactions 1
	返回 区块中的交易信息

### 获取资产总发行量  
	blockchain_calculate_supply 资产id
	示例
	blockchain_calculate_supply 0
	返回 资产总发行量
  
### 获取激活代理  
	blockchain_list_active_delegates
	示例
	blockchain_list_active_delegates
	返回 出块代理人
  
### 获取地址余额信息 
	blockchain_list_address_balances 地址
	示例
	blockchain_list_address_balances 地址
	返回 地址拥有的余额信息
  
### 获取未确认的交易信息 
	blockchain_list_pending_transactions
	示例
	blockchain_list_pending_transactions
	返回 未确认的交易信息
