# 提案超级管理员相关
### 提案超级管理员（提案人必须为当前有效受托人）
    proposal_apply_for_privilege_admin  提案人本地账户名  候选超级管理员地址  提案生效所需赞成数量  提案开始时间戳  提案结束时间戳
    示例 
    proposal_apply_for_privilege_admin cdc0 0x3ba929332e10054d9ff08f5a3bd65551a86bb77c 11 1424653000 1634653001

    超级管理员相关的提案生效所需赞成数量必须达到（受托人数量/2 + 1） 也不能超过受托人数量，所以这块参数中生效所需赞成数量，不能小于11，也不能大于21

    返回 提案id


### 提案撤销超级管理员（提案人必须为当前有效受托人）
    proposal_revoke_privilege_admin  提案人本地账户名  超级管理员地址  提案生效所需赞成数量  提案开始时间戳  提案结束时间戳
    示例
    proposal_revoke_privilege_admin cdc3 0x3ba929332e10054d9ff08f5a3bd65551a86bb77c 11 1524653000 1634653000

    超级管理员相关的提案生效所需赞成数量必须达到（受托人数量/2 + 1） 也不能超过受托人数量，所以这块参数中生效所需赞成数量，不能小于11，也不能大于21

    返回 提案id


### 批准提案（批准者也必须为当前有效受托人）
    proposal_approve 本地账户名 提案id
    示例
    proposal_approve cdc0 3fbc30657863f296792cdef7bc9b2ac229c5f583

### 查询所有特权管理员
    get_all_privilege_admin

<br/>

# 数据管理员相关
### 指派数据管理员（由超级管理员）
    appoint_general_admin  超级管理员本地账户名  候选数据管理员地址
    示例
    appoint_general_admin  test  0x706e253a6184264d3d3ca49466d10be9c8763522

### 撤销数据管理员（由超级管理员）
    revoke_general_admin  超级管理员本地账户名  数据管理员地址
    示例
    revoke_general_admin  test  0x71aa6dd9f5b633998389afe816334b61ca06dba6

### 查询所有数据管理员
    get_all_general_admin

<br/>

# 提案相关
### 提案查询
    proposal_get_info 提案id
    示例
    proposal_get_info 9559a8dc7bbc6105b4a2120afd6b4a61e4382bb6
