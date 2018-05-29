# 合约相关（消费数据hash相关）
注意：
* 当前所有的hash是指sha256，其他类型的hash都不支持
* Remark字段选填，如果不填的话，就传入一个空字符串。为了防止中文各种编码问题，建议不传入中文内容，不过没有做强制性要求。

<br/>

# 用户小票hash数据管理合约
### 合约注册上链（数据管理员拥有合约上链权限）
	contract_register  数据管理员本地账户名  合约字节码文件  资产名  gas费
	示例
	contract_register cdc1 D:\blockchain_project\CDC-DAPP\data_management\user_receipt_data.glua.gpc CDC 10
	返回  合约id

### 查询合约状态
	contract_get_info  合约id
	示例
	contract_get_info C3a66db70fe87c92033dd870f092a0f5e37364882

### 查询合约的调用者地址白名单
	contract_call_offline  合约id  任意本地账户名  getallowedAddrCaller  ""
	示例
	contract_call_offline C3a66db70fe87c92033dd870f092a0f5e37364882 cdc1 getallowedAddrCaller  ""

### 添加合约的调用者地址白名单
	contract_call 合约id  数据管理员本地账户名  addAddrCallerAllowed  想要添加的白名单用户地址
	示例
	contract_call C3a66db70fe87c92033dd870f092a0f5e37364882 cdc1 addAddrCallerAllowed 0xec7a5c2f1ad9f7b57643c82c662ff4ade4c18cdb CDC 1

### 向链上记录用户小票hash数据
	contract_call 合约id  白名单用户本地账户名 checkinUserReceiptHash  “数据hash|remark信息”   CDC  gas费
	示例
	contract_call C3a66db70fe87c92033dd870f092a0f5e37364882 cdc1 checkinUserReceiptHash "e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855| " CDC 1

### 从链上删除用户小票hash数据
	contract_call 合约id  白名单用户本地账户名 abolishUserReceiptHash  数据hash   CDC  gas费
	示例
	contract_call C3a66db70fe87c92033dd870f092a0f5e37364882 cdc1 abolishUserReceiptHash "e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855" CDC 1

### 验证链上是否存在用户小票hash数据
	contract_call_offline 合约id 任意本地账户名 verifyUserReceiptHash 数据hash
	示例
	contract_call_offline C3a66db70fe87c92033dd870f092a0f5e37364882 cdc1 verifyUserReceiptHash e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855

<br/>

# 挖矿结果hash数据管理合约
### 合约注册上链（数据管理员拥有合约上链权限）
	contract_register  数据管理员本地账户名  合约字节码文件  资产名  gas费
	示例
	contract_register cdc1 D:\blockchain_project\CDC-DAPP\data_management\mining_result_data.glua.gpc CDC 10
	返回  合约id

### 查询合约状态
	contract_get_info  合约id
	示例
	contract_get_info C62f46058a794fff8fd6ef7ddb2ffa19076a24cfe

### 查询合约的调用者地址白名单
	contract_call_offline  合约id  任意本地账户名  getallowedAddrCaller  ""
	示例
	contract_call_offline C62f46058a794fff8fd6ef7ddb2ffa19076a24cfe cdc1 getallowedAddrCaller  ""

### 添加合约的调用者地址白名单
	contract_call 合约id  数据管理员本地账户名  addAddrCallerAllowed  想要添加的白名单用户地址
	示例
	contract_call C62f46058a794fff8fd6ef7ddb2ffa19076a24cfe cdc1 addAddrCallerAllowed 0xec7a5c2f1ad9f7b57643c82c662ff4ade4c18cdb CDC 1

### 向链上记录挖矿结果hash数据
	contract_call 合约id  白名单用户本地账户名 checkinMiningResultHash “数据hash|remark信息”   CDC  gas费
	示例
	contract_call C3a66db70fe87c92033dd870f092a0f5e37364882 cdc1 checkinMiningResultHash  "e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b854| " CDC 1

### 从链上删除挖矿结果hash数据
	contract_call 合约id  白名单用户本地账户名 abolishMiningResultHash  数据hash   CDC  gas费
	示例
	contract_call C3a66db70fe87c92033dd870f092a0f5e37364882 cdc1 abolishMiningResultHash e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b854 CDC 1

### 验证链上是否存在挖矿结果hash数据
	contract_call_offline 合约id 任意本地账户名 verifyMiningResultHash 数据hash
	示例
	contract_call_offline C3a66db70fe87c92033dd870f092a0f5e37364882 cdc1 verifyMiningResultHash e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b854

<br/>

# 广告投放结果hash数据管理合约
### 合约注册上链（数据管理员拥有合约上链权限）
	contract_register  数据管理员本地账户名  合约字节码文件  资产名  gas费
	示例
	contract_register cdc1 D:\blockchain_project\CDC-DAPP\data_management\ad_putting_result_data.glua.gpc CDC 10
	返回  合约id

### 查询合约状态
	contract_get_info  合约id
	示例
	contract_get_info C3a97a93211f7694d603d2e52c562274c47311804

### 查询合约的调用者地址白名单
	contract_call_offline  合约id  任意本地账户名  getallowedAddrCaller  ""
	示例
	contract_call_offline C3a97a93211f7694d603d2e52c562274c47311804 cdc1 getallowedAddrCaller  ""

### 添加合约的调用者地址白名单
	contract_call 合约id  数据管理员本地账户名  addAddrCallerAllowed  想要添加的白名单用户地址
	示例
	contract_call C3a97a93211f7694d603d2e52c562274c47311804 cdc1 addAddrCallerAllowed 0xec7a5c2f1ad9f7b57643c82c662ff4ade4c18cdb CDC 1

### 向链上记录广告投放结果hash数据
	contract_call 合约id  白名单用户本地账户名 checkinAdPuttingResultHash “数据hash|remark信息”   CDC  gas费
	示例
	contract_call C3a66db70fe87c92033dd870f092a0f5e37364882 cdc1 checkinAdPuttingResultHash "e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b851| " CDC 1

### 从链上删除广告投放结果hash数据
	contract_call 合约id  白名单用户本地账户名 abolishAdPuttingResultHash  数据hash   CDC  gas费
	示例
	contract_call C3a66db70fe87c92033dd870f092a0f5e37364882 cdc1 abolishAdPuttingResultHash e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b851 CDC 1

### 验证链上是否存在广告投放结果hash数据
	contract_call_offline 合约id 任意本地账户名 verifyAdPuttingResultHash 数据hash
	示例
	contract_call_offline C3a66db70fe87c92033dd870f092a0f5e37364882 cdc1 verifyAdPuttingResultHash e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b851

<br/>

# 广告投放结果反馈hash数据管理合约
### 合约注册上链（数据管理员拥有合约上链权限）
	contract_register  数据管理员本地账户名  合约字节码文件  资产名  gas费
	示例
	contract_register cdc1 D:\blockchain_project\CDC-DAPP\data_management\ad_putting_feedback_data.glua.gpc CDC 10
	返回  合约id

### 查询合约状态
	contract_get_info  合约id
	示例
	contract_get_info Cc65fad1ebe11a07f917207d0beee4027dfc5c80f

### 查询合约的调用者地址白名单
	contract_call_offline  合约id  任意本地账户名  getallowedAddrCaller  ""
	示例
	contract_call_offline Cc65fad1ebe11a07f917207d0beee4027dfc5c80f cdc1 getallowedAddrCaller  ""

### 添加合约的调用者地址白名单
	contract_call 合约id  数据管理员本地账户名  addAddrCallerAllowed  想要添加的白名单用户地址
	示例
	contract_call Cc65fad1ebe11a07f917207d0beee4027dfc5c80f cdc1 addAddrCallerAllowed 0xec7a5c2f1ad9f7b57643c82c662ff4ade4c18cdb CDC 1

### 向链上记录广告投放结果反馈hash数据
	contract_call 合约id  白名单用户本地账户名 checkinAdPuttingFeedbackHash “数据hash|remark信息”   CDC  gas费
	示例
	contract_call C3a66db70fe87c92033dd870f092a0f5e37364882 cdc1 checkinAdPuttingFeedbackHash "e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b857| " CDC 1

### 从链上删除广告投放结果反馈hash数据
	contract_call 合约id  白名单用户本地账户名 abolishAdPuttingFeedbackHash  数据hash   CDC  gas费
	示例
	contract_call C3a66db70fe87c92033dd870f092a0f5e37364882 cdc1 abolishAdPuttingFeedbackHash e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b857 CDC 1

### 验证链上是否存在广告投放结果反馈hash数据
	contract_call_offline 合约id 任意本地账户名 verifyAdPuttingFeedbackHash 数据hash
	示例
	contract_call_offline C3a66db70fe87c92033dd870f092a0f5e37364882 cdc1 verifyAdPuttingFeedbackHash e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b857
