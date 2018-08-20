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


<br/>
<br/>


# 交易所涉及接口（用户地址创建相关接口）

### 创建钱包

    请求方法：wallet_create
    请求参数：创建钱包名称（小写英文字符开头、只能是小写英文字符、数字或中划线）、创建密码（长度不低于8位）

    Request:
    {"method":"wallet_create","id":20180517140651383,"jsonrpc":"2.0","params":["cdc","cdc123456"]}

    
    Response：
    {"id":"20180517140651383","result":null}
    
    注：成功创建钱包后，钱包默认是打开的，并且解锁时长是60分钟，超过60分钟时钱包重新锁定。
    可以通过wallet_unlock方法自定义解锁时长。

### 打开钱包

    请求方法：wallet_open
    请求参数：钱包名

    Request:
    {"method":"wallet_open","id":20180517142746758,"jsonrpc":"2.0","params":["cdc"]}

    
    Response：
    {"id":"20180517142746758","result":null}

### 解锁钱包

    请求方法：wallet_unlock
    请求参数：解锁时长（秒），解锁密码

    Request:
    {"method":"wallet_unlock","id":20180517144003773,"jsonrpc":"2.0","params":["99999999","cdc123456"]}
    
    Response：
    {"id":"20180517144003773","result":null}
    
    注：解锁钱包的前提是需要先打开钱包

### 钱包自动备份（打开/关闭）

    请求方法：wallet_set_automatic_backups
    请求参数：true/false

    Request:
    {"method":"wallet_set_automatic_backups","id":20180517150216550,"jsonrpc":"2.0","params":[true]}

    
    Response：
    {
        "id": "20180517150216550",
        "result":true
    }   
    
    注：自动备份默认设置是打开状态。同时如果自动备份打开的话，当钱包中每新增一个账户，则会钱包目录下的.backups目录下
    自动创建一个钱包备份文件。
    
    注2：交易所在批量创建地址的时候，建议将钱包的自动备份功能关闭，否则每新增一个账户，就会备份一个钱包文件，会导致
    大量的磁盘占用，同时也非常影响地址的创建效率。


### 在钱包中创建账户（地址）

    请求方法：wallet_account_create
    请求参数：本地用户名（小写英文字符开头、只能是小写英文字符、数字或中划线）

    Request:
    {"method":"wallet_account_create","id":20180517144818773,"jsonrpc":"2.0","params":["cdcuser000001"]}

    
    Response：
    {"id":"20180517144818773","result":"0xe51eb7fdaf16b9bbbb48d5f1dc56aac53e4f9fad"}
    
    注：本地用户名不能与已注册上链的用户名一致，也不能与本地钱包中已经存在的用户名一致。
    因此交易所最好有个生成这个用户名的规则，才可以比较方便得将用户的地址批量创建出来    
    
### 列出钱包内的所有账户（地址）

    请求方法：wallet_list_accounts
    请求参数：无

    Request:
    {"method":"wallet_list_accounts","id":20180517144818773,"jsonrpc":"2.0","params":[]}

    
    Response：
    {"id":"20180517144818773", "result": [{
            "index": 17,
            "id": 0,
            "name": "cdc00001",
            "public_data": null,
            "owner_key": "0x7HbYqgoviPWkny7xZ6fnFdweEwwKZUoEfnk8zFgRDsmdEFWMnC",
            "active_key_history": [
                ["2018-08-20T05:59:53", "0x5rXGWYiAuLHNTXVwKSqK5YCPVqpXrZGPNsWSLJ3UWM6nuHo6Lz"]
            ],
            "registration_date": "1970-01-01T00:00:00",
            "last_update": "2018-08-20T05:59:53",
            "is_my_account": true,
            "approved": 0,
            "is_favorite": false,
            "block_production_enabled": false,
            "last_used_gen_sequence": 0,
            "private_data": null
        }, {
            "index": 20,
            "id": 0,
            "name": "cdc00002",
            "public_data": null,
            "owner_key": "0x55W1HQ9UpavLrjDCD9pkXD1vUB1uZDqGfGPsXD9MNiBsU97eWX",
            "active_key_history": [
                ["2018-08-20T06:00:12", "0x5Yc6ngS3P8NDnxVbjVoaQ9AvcKTanirwGFKENM5ZZmrSkGnoAS"]
            ],
            "registration_date": "1970-01-01T00:00:00",
            "last_update": "2018-08-20T06:00:12",
            "is_my_account": true,
            "approved": 0,
            "is_favorite": false,
            "block_production_enabled": false,
            "last_used_gen_sequence": 0,
            "private_data": null
        }, {
            "index": 11,
            "id": 0,
            "name": "cdc00003",
            "public_data": null,
            "owner_key": "0x7QJLBqomLYzPnJPXiUBRBwY5bZ3EfnBVYrRQgZ4xo2Kp7D7fCK",
            "active_key_history": [
                ["2018-08-17T09:55:17", "0x7QJLBqomLYzPnJPXiUBRBwY5bZ3EfnBVYrRQgZ4xo2Kp7D7fCK"]
            ],
            "registration_date": "1970-01-01T00:00:00",
            "last_update": "2018-08-17T09:55:17",
            "is_my_account": true,
            "approved": 0,
            "is_favorite": false,
            "block_production_enabled": false,
            "last_used_gen_sequence": 0,
            "private_data": null
        }]
    }
 
 ### 获取钱包内某账户名的地址

    请求方法：wallet_get_account_public_address
    请求参数：账户名

    Request:
    {"method":"wallet_get_account_public_address","id":20180517150216550,"jsonrpc":"2.0","params":["cdc00001"]}

    
    Response：
    {"id":"20180517150216550","result":"0xe51eb7fdaf16b9bbbb48d5f1dc56aac53e4f9fad"}
  
  
  
<br/>
<br/>
    
    
# 交易所涉及接口（用户充值）

    交易所通过扫描区块中的交易，并且判断相关交易是否是用户充值交易的方式来判断用户充值交易的。
    这种方式比较安全可靠，不需要在钱包中保留任何私钥，是当前最安全可靠的判定用户充值的方式，强烈推荐使用
    用户充值确认数推荐值：30

### 获取区块中的交易信息

    请求方法：blockchain_get_block_transactions
    请求参数：区块高度

    Request:
    {"method":"blockchain_get_block_transactions","id":20180517150216550,"jsonrpc":"2.0","params":[77]}

    
    Response：
    {
        "id":"20180517150216550"，
        "result": [
            ["a2d62f51e5f82023e7f4f3f7f05c7fc7661831c3", {
                "trx": {
                    "expiration": "2018-08-17T10:44:20",
                    "cdc_account": "",
                    "cdc_inport_asset": {
                        "amount": 0,
                        "asset_id": 0
                    },
                    "operations": [{
                        "type": "withdraw_op_type",
                        "data": {
                            "balance_id": "0xc846875c1345183c6b07d0bf18b7b74997c6951a",
                            "amount": 101000000,
                            "claim_input_data": ""
                        }
                    }, {
                        "type": "deposit_op_type",
                        "data": {
                            "amount": 100000000,
                            "condition": {
                                "asset_id": 0,
                                "slate_id": 0,
                                "type": "withdraw_signature_type",
                                "balance_type": "withdraw_common_type",
                                "data": {
                                    "owner": "0xd8f30845a3f386c42a9722eaf381c86c85c22bd3"
                                }
                            }
                        }
                    }],
                    "result_trx_type": "origin_transaction",
                    "result_trx_id": "0000000000000000000000000000000000000000",
                    "signatures": ["1f7864fb2dac15a05f19ecf8299388045cce6c00e902e1f3e6e37becfb615796b8169ea9083a0172302c7c70b94372b7ab4371d1e64219926f29f7991a26b34947"]
                },
                "signed_keys": [],
                "deposits": [
                    [0, 100000000]
                ],
                "withdraws": [
                    [0, 101000000]
                ],
                "contract_address": "",
                "yield": [],
                "deltas": [
                    [0, [
                        [0, -101000000]
                    ]],
                    [1, [
                        [0, 100000000]
                    ]]
                ],
                "required_fees": {
                    "amount": 0,
                    "asset_id": 0
                },
                "alt_fees_paid": {
                    "amount": 0,
                    "asset_id": 0
                },
                "balance": [
                    [0, 1000000]
                ],
                "delegate_vote_deltas": [],
                "imessage_length": 0,
                "skipexec": false,
                "chain_location": {
                    "block_num": 77,
                    "trx_num": 0
                }
            }]
        ]
    }
    
    注：返回的内容是当前区块中的所有交易信息，在这边可以先对所有的交易列表进行一轮过滤。
    对于 trx.operations[0].type == transaction_op_type 的交易，代表是合约交易，可以直接忽略这笔交易不进行处理
    
    注2：如果需要查看pretty transaction结果，对于非合约交易，可以调用blockchain_get_pretty_transaction方法；
    对于合约交易，可以调用blockchain_get_pretty_contract_transaction方法，对于交易所用户来说，其实并不需要关心任何合约交易。
    

### 获取pretty格式的交易信息

    请求方法：blockchain_get_pretty_transaction
    请求参数：交易id

    Request:
    {"method":"blockchain_get_pretty_transaction","id":20180517150216550,"jsonrpc":"2.0","params":["a2d62f51e5f82023e7f4f3f7f05c7fc7661831c3"]}

    
    Response：
    {
        "id": "20180517150216550",
        "result": {
            "is_virtual": false,
            "is_confirmed": true,
            "is_market": false,
            "is_market_cancel": false,
            "trx_id": "a2d62f51e5f82023e7f4f3f7f05c7fc7661831c3",
            "block_num": 77,
            "block_position": 0,
            "trx_type": 0,
            "ledger_entries": [{
                "from_account": "0x908357335039cf744d153791b7b898219a758209",
                "from_account_name": "cdc0",
                "to_account": "0xd8f30845a3f386c42a9722eaf381c86c85c22bd3",
                "to_account_name": "",
                "amount": {
                    "amount": 100000000,
                    "asset_id": 0
                },
                "memo": "",
                "running_balances": []
            }],
            "fee": {
                "amount": 1000000,
                "asset_id": 0
            },
            "timestamp": "2018-08-17T09:44:30",
            "expiration_timestamp": "2018-08-17T10:44:20"
        }
    }    
    
    注：from_account出账地址  to_account入账地址  amount转账金额（带精度） CDC资产是8位精度的，因此这笔交易是1CDC的转账。
    对于交易所来说，如果某笔交易的to_account地址是交易所中的用户地址，则需要给该用户在交易所中的账户中入账相关金额的CDC。
    
    
<br/>
<br/>    
    
    
# 交易所涉及接口（用户提币）

### 发起转账

    请求方法：wallet_transfer_to_address
    请求参数：转账金额、转账资产名、出账账户名、入账方地址

    Request:
    {"method":"wallet_transfer_to_address","id":20180517150216550,"jsonrpc":"2.0","params":["0.5", "CDC", "cdc001", "0xf5d9041c25dc5e112b2f03abb6a2a70e5d6396e5"]}

    
    Response：
    {
        "id": "20180517150216550",
        "result": {
            "index": 0,
            "entry_id": "5a97c606dd53fcb7489e445f7548b44d7ba40bd9",
            "block_num": 0,
            "is_virtual": false,
            "is_confirmed": false,
            "is_market": false,
            "trx": {
                "expiration": "2018-08-20T09:37:52",
                "cdc_account": "",
                "cdc_inport_asset": {
                    "amount": 0,
                    "asset_id": 0
                },
                "operations": [{
                    "type": "withdraw_op_type",
                    "data": {
                        "balance_id": "0xa87eb9b6bf4975dfde2083adf4807fac06405fa5",
                        "amount": 51000000,
                        "claim_input_data": ""
                    }
                }, {
                    "type": "deposit_op_type",
                    "data": {
                        "amount": 50000000,
                        "condition": {
                            "asset_id": 0,
                            "slate_id": 0,
                            "type": "withdraw_signature_type",
                            "balance_type": "withdraw_common_type",
                            "data": {
                                "owner": "0xf5d9041c25dc5e112b2f03abb6a2a70e5d6396e5"
                            }
                        }
                    }
                }],
                "result_trx_type": "origin_transaction",
                "result_trx_id": "0000000000000000000000000000000000000000",
                "signatures": ["1f52f3d543db03b240af9d39e78857164eb1929541482f925f647ecef8d0d959425e4384e1d0e4f00190ecf07998d7ace4d3d218ce8862ba2cc6690249612f73ec"]
            },
            "ledger_entries": [{
                "from_account": "0x7QJLBqomLYzPnJPXiUBRBwY5bZ3EfnBVYrRQgZ4xo2Kp7D7fCK",
                "to_account": "0x7HbYqgoviPWkny7xZ6fnFdweEwwKZUoEfnk8zFgRDsmdEFWMnC",
                "amount": {
                    "amount": 50000000,
                    "asset_id": 0
                },
                "memo": "To: 0xf5d904..."
            }],
            "fee": {
                "amount": 1000000,
                "asset_id": 0
            },
            "created_time": "2018-08-20T08:37:52",
            "received_time": "2018-08-20T08:37:52",
            "extra_addresses": ["0xf5d9041c25dc5e112b2f03abb6a2a70e5d6396e5"]
        }        
    }    
 
 
 ### 账户余额查询

    请求方法：wallet_account_balance
    请求参数：账户名

    Request:
    {"method":"wallet_account_balance","id":20180517150216550,"jsonrpc":"2.0","params":["cdc00001"]}

    
    Response：
    {
        "id": "20180517150216550",
        "result":[["cdc00001",[[0,50000000]]]]
    }
    
    
 ### 判断交易是否已上链
     可以使用上面那个 blockchain_get_pretty_transaction 那个接口，如果能查询到相关交易id的信息，说明已经成功上链，否则说明还未成功上链。
     

<br/>
<br/>
    
    
    
# 交易所涉及接口（钱包维护）

### 钱包备份
    请求方法：wallet_backup_create
    请求参数：钱包备份的目标文件

    Request:
    {"method":"wallet_backup_create","id":20180517150216550,"jsonrpc":"2.0","params":["/home/ubuntu/backup/mywallet_backup.json"]}

    
    Response：
    {
        "id": "20180517150216550",
        "result":null
    }

### 钱包恢复

    请求方法：wallet_backup_restore
    请求参数：钱包备份的目标文件、恢复钱包名、原钱包密码

    Request:
    {"method":"wallet_backup_restore","id":20180517150216550,"jsonrpc":"2.0","params":["/home/ubuntu/backup/mywallet_backup.json", "cdc", "cdc123456"]}

    
    Response：
    {
        "id": "20180517150216550",
        "result":null
    } 



     
