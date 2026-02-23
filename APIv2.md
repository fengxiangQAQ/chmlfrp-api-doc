# API v2
APIv2 还在开发中

也许api今天是这样 明天就变样了

同时该文档可能有不准确 以api实际为准

在 [XCL2](https://github.com/FengXiangqaq/Xingcheng-Chmlfrp-Lanucher/) 开发中发现本文档的错误也会纠正错误

统一调用地址
> https://cf-v2.uapis.cn

## 登录
- 接口
    > GET&POST /login
- 请求参数

    **Query/表单**:
    |参数|类型|必填|说明|
    |:--:|:--:|:--:|:--:|
    |username|str|是|用户名/邮箱|
    |password|str|是|密码|
- 返回

    **JSON**：
    |参数|类型|必返|说明|
    |:--:|:--:|:--:|:--:|
    |code|int|是|返回状态码|
    |state|str|是|请求是否成功|
    |msg|str|是|返回消息|
    |data|map|否|详见下方|

    <b><i>data</b></i>:

    当上方 `state` 为 `success` 返回
    |参数|类型|必返|说明|
    |:--:|:--:|:--:|:--:|
    |id|int|是|用户的id|
    |username|str|是|用户名|
    |usertoken|str|是|用户令牌|
    |email|str|是|用户邮箱|
    |qq|str|是|用户QQ号|
    |usergroup|str|是|用户组|
    |term|str|是|用户组到期时间|
    |realname|str|是|实名状态|
    |tunnel|int|是|用户隧道数|
    |tunnnelCount|int|是|用户隧道上限|
    |totalCurConns|int|是|用户所有隧道被连接数|
    |total_upload|int|是|累计上传量(Byte)|
    |total_download|int|是|累计下载量(Byte)|
    |bandwidth|int|是|详见下方|
    |integral|int|是|用户积分|
    |userimg|str|是|用户头像url|
    |regtime|str|是|用户注册时间|
    |login_attempts|int|是|无用参数 返0|
    |password|null|是|无用参数|
    |realname_count|int|是|无用参数 返0|
    |scgm|str/null|是|无用参数|
    |t_token|null|是|无用参数|

    <b><i>bandwidth</b></i>:

    用户带宽限制

    国内带宽限制(Mdps): 该值*1

    国外宽带限制(Mdps): 该值*4

## 用户信息
- 接口
    > GET&POST /userinfo
- 请求参数

    **Query/表单**:
    |参数|类型|必填|说明|
    |:--:|:--:|:--:|:--:|
    |token|str|是|用户令牌|
- 返回

  [**同上 /login**](#登录)

## 隧道列表
- 接口
    > GET&POST /tunnel
- 请求参数

    **Query/表单**:
    |参数|类型|必填|说明|
    |:--:|:--:|:--:|:--:|
    |token|str|是|用户令牌|
- 返回

    **JSON**：
    |参数|类型|必返|说明|
    |:--:|:--:|:--:|:--:|
    |code|int|是|返回状态码|
    |state|str|是|请求是否成功|
    |msg|str|是|返回消息|
    |data|list|否|详见下方|

    <b><i>data</b></i>:

    当上方 `state` 为 `success` 返回
    
    list中有若干个map 每个map代表一条隧道

    map参数详见下方

    <b><i>Map</b></i>：
    |参数|类型|必返|说明|
    |:--:|:--:|:--:|:--:|
    |id|int|是|隧道id|
    |name|str|是|隧道名|
    |node|str|是|所属节点|
    |nodestate|str/null|是|详见下方|
    |type|str|是|隧道类型|
    |localip|str|是|内网ip|
    |nport|int|是|内网端口|
    |dorp|str|是|外网端口/连接域名|
    |ip|str/null|是|所属节点ip|
    |encryption|str|是|是否数据加密|
    |compression|str|是|是否数据压缩|
    |ap|str|是|frp额外参数|
    |state|str|是|隧道状态|
    |uptime|str/null|是|上次启动时间|
    |client_version|str|是|上次启动frpc版本|
    |userid|int|是|隧道拥有者id|
    |today_traffic_in|int|是|今日该隧道上传流量|
    |today_traffic_out|int|是|今日该隧道下载流量|
    |cur_conns|int|是|当前隧道连接数|

    <b><i>nodestate</b></i>：

    若返回str且值为"online" 则该隧道所属节点在线

    若返回null 则该隧道节点永久下线

## 重置用户令牌
- 接口
    > GET&POST /retoken
- 请求参数

    **Query/表单**:
    |参数|类型|必填|说明|
    |:--:|:--:|:--:|:--:|
    |token|str|是|用户令牌|
- 返回

    **JSON**：
    |参数|类型|必返|说明|
    |:--:|:--:|:--:|:--:|
    |code|int|是|返回状态码|
    |state|str|是|请求是否成功|
    |msg|str|是|返回消息|

## 节点信息列表
```
注: 此接口仅返回在线节点且数据会抖动
    如需完整节点列表 见节点状态列表
```
- 接口
    > GET&POST /node
- 返回

   **JSON**：
    |参数|类型|必返|说明|
    |:--:|:--:|:--:|:--:|
    |code|int|是|返回状态码|
    |state|str|是|请求是否成功|
    |msg|str|是|返回消息|
    |data|map|否|详见下方|

    <b><i>data</b></i>:

    当上方 `state` 为 `success` 返回

    为一个list对象 其中有若干个map 
    
    map：
    |参数|类型|必返|说明|
    |:--:|:--:|:--:|:--:|
    |id|int|是|节点识别编号|
    |name|str|是|节点名称|
    |nodegroup|str|是|节点所属权限组|
    |area|str|是|节点地理位置|
    |china|str|是|是否为国内节点|
    |fangyu|str|是|是否有防御|
    |udp|str|是|是否允许udp|
    |web|str|是|是否允许建站|

## 节点状态列表
```
注: 该接口返回完整节点列表 若节点永久下线 则不存在于该节点列表
```
- 接口
    > GET&POST /node_stats
- 返回

    **JSON**：
    |参数|类型|必返|说明|
    |:--:|:--:|:--:|:--:|
    |code|int|是|返回状态码|
    |state|str|是|请求是否成功|
    |msg|str|是|返回消息|
    |data|map|否|详见下方|

    <b><i>data</b></i>:

    当上方 `state` 为 `success` 返回

    为一个list对象 其中有若干个map 
    
    map：
    |参数|类型|必返|说明|
    |:--:|:--:|:--:|:--:|
    |id|int|是|节点识别编号|
    |node_name|str|是|节点名称|
    |nodegroup|str|是|节点所属权限组|
    |state|str|是|在线状态(online/offline)|
    |client_counts|int|是|客户端连接数|
    |tunnel_counts|int|是|隧道连接数|
    |cur_counts|int|是|活跃连接数|
    |cpu_usage|int|是|cpu使用率%|
    |bandwidth_usage_percent|int|是|带宽占用%|
    |total_traffic_in|int|是|今日下载(bytes)|
    |total_traffic_out|int|是|今日上传(bytes)|

## 节点详情
- 接口
    > GET /nodeinfo
- 请求参数

    **Query**:
    |参数|类型|必填|说明|
    |:--:|:--:|:--:|:--:|
    |token|str|是|用户令牌|
    |node|str|是|节点名|
    ```
    注: 免费用户无权获取vip节点详情(token判断)
    ```
- 返回

    **JSON**：
    |参数|类型|必返|说明|
    |:--:|:--:|:--:|:--:|
    |code|int|是|返回状态码|
    |state|str|是|请求是否成功|
    |msg|str|是|返回消息|
    |data|map|否|详见下方|

    <b><i>data</b></i>:

    当上方 `state` 为 `success` 返回

    为一个list对象 其中有若干个map 
    
    map：
    |参数|类型|必返|说明|
    |:--:|:--:|:--:|:--:|
    |id|int|是|节点识别编号|
    |name|str|是|节点名称|
    |state|str|是|在线状态(online/offline)|
    |notes|string|是|节点简介|
    |nodegroup|string|是|节点可使用用户组|
    |ip|string|是|节点地址|
    |realIp|sting|是|节点的真实ip|
    |ipv6|string|是|顾名思义|
    |port|int|是|节点frp端口|
    |rport|string|是|节点frp端口限制|
    |udp|string|是|节点是否可以使用upd<true/false>|
    |web|string|是|节点是否可以建站<yes/no>|
    |china|string|是|是否是国内节点<yes/no>|
    |area|string|是|节点所属地区|
    |coordinates|string|是|节点地理经纬度|
    |fangyu|string|是|是否有防御<true/false>|
    |version|string|是|frps版本|
    |cpu_info|int|是|cpu信息|
    |num_cores|int|是|cpu核心数|
    |total_traffic_in|int|是|今日下载(bytes)|
    |total_traffic_out|int|是|今日上传(bytes)|
    |bandwidth_usage_percent|int|是|带宽占用%|
    |memory_total|int|是|总内存量(bytes)|
    |storage_total|int|是|总存储量(bytes)|
    |storage_used|int|是|存储使用量(bytes)|
    |uptime_seconds|int|是|正常运行秒数|
    |loadx|number|是|综合负载 详见下方|

    <b><i>loadx</b></i>:

    x为1,5,15 分别代表几分钟内综合负载

    注 返回百分数的浮点数形态

## 创建隧道
- 接口
    > POST /create_tunnel
- 请求参数

    **JSON**:
    |参数|类型|必填|说明|
    |:--:|:--:|:--:|:--:|
    |token|str|是|用户令牌|
    |tunnelname|str|是|隧道名称|
    |node|str|是|节点名称|
    |porttype|str|是|详见下方|
    |localip|str|是|本地ip|
    |localport|int|是|本地端口|
    |remoteport|int|否|详见下方|
    |banddomain|str|否|详见下方|
    |encryption|bool|是|是否数据加密|
    |compression|bool|是|是否数据压缩|
    |extraparams|str|是|frp额外参数|

    <b><i>porttype</b></i>：

    隧道类型

    值为tcp/udp/http/https

    <b><i>banddomain</b></i>：

    绑定域名

    当porttype值为http/https需填

    <b><i>remoteport</b></i>：

    内网端口

    当porttype值为tcp/udp需填 

- 返回
    
    **JSON**：
    |参数|类型|必返|说明|
    |:--:|:--:|:--:|:--:|
    |code|int|是|返回状态码|
    |state|str|是|请求是否成功|
    |msg|str|是|返回消息|
    |data|map|否|详见下方|

    <b><i>data</b></i>:

    当上方 `state` 为 `success` 返回
    |参数|类型|必返|说明|
    |:--:|:--:|:--:|:--:|
    |name|str|是|隧道名|
    |node|str|是|所属节点|
    |type|str|是|隧道类型|
    |localip|str|是|内网ip|
    |nport|int|是|内网端口|
    |dorp|str|是|外网端口/连接域名|
    |encryption|str|是|是否数据加密|
    |compression|str|是|是否数据压缩|
    |ap|str|是|frp额外参数|
    |state|str|是|隧道状态|
    |client_version|str|是|上次启动frpc版本|
    |userid|int|是|隧道拥有者id|
    |today_traffic_in|int|是|今日该隧道上传流量|
    |today_traffic_out|int|是|今日该隧道下载流量|
    |cur_conns|int|是|当前隧道连接数|
    |id|null|是|值为null|
    |ip|null|是|值为null|
    |nodestate|null|是|值为null|
    |uptime|null|是|值为null|

## 修改隧道
- 接口
    > POST /update_tunnel
- 请求参数

    **Query/表单**:
    |参数|类型|必填|说明|
    |:--:|:--:|:--:|:--:|
    |token|str|是|用户令牌|
    |tunnelname|str|是|隧道名称|
    |node|str|是|节点名称|
    |porttype|str|是|详见下方|
    |localip|str|是|本地ip|
    |localport|int|是|本地端口|
    |remoteport|int|是|内网端口|
    |encryption|bool|是|是否数据加密|
    |compression|bool|是|是否数据压缩|
    |extraparams|str|是|frp额外参数|

    <b><i>porttype</b></i>：

    隧道类型

    值为tcp/udp/http/https
    

- 返回
 
    **JSON**：
    |参数|类型|必返|说明|
    |:--:|:--:|:--:|:--:|
    |code|int|是|返回状态码|
    |state|str|是|请求是否成功|
    |msg|str|是|返回消息|
    |data|map|否|详见下方|

    <b><i>data</b></i>:

    当上方 `state` 为 `success` 返回
    |参数|类型|必返|说明|
    |:--:|:--:|:--:|:--:|
    |name|str|是|隧道名|
    |node|str|是|所属节点|
    |type|str|是|隧道类型|
    |localip|str|是|内网ip|
    |nport|int|是|内网端口|
    |dorp|str|是|外网端口|
    |encryption|str|是|是否数据加密|
    |compression|str|是|是否数据压缩|
    |ap|str|是|frp额外参数|
    |state|str|是|隧道状态|
    |client_version|str|是|上次启动frpc版本|
    |userid|int|是|隧道拥有者id|
    |today_traffic_in|int|是|今日该隧道上传流量|
    |today_traffic_out|int|是|今日该隧道下载流量|
    |cur_conns|int|是|当前隧道连接数|
    |id|null|是|值为null|
    |ip|null|是|值为null|
    |nodestate|null|是|值为null|
    |uptime|null|是|值为null|

## 删除隧道
- 接口
    > GET /delete_tunnel
- 请求头
    |参数|必填|说明|
    |:--:|:--:|:--:|
    |authorization|是|详见下方|

    <b><i>authorization</b></i>:

    格式 "Bearer {token}"
    
    用于传递token
- 请求参数
    
    **Query/表单**:
    |参数|类型|必填|说明|
    |:--:|:--:|:--:|:--:|
    |tunnelid|int|是|隧道id|
- 返回
 
    **JSON**：
    |参数|类型|必填|说明|
    |:--:|:--:|:--:|:--:|
    |code|int|是|返回状态码|
    |state|str|是|请求是否成功|
    |msg|str|是|返回消息|

## 签到
- 接口
    > POST /qiandao
- 请求头
    |参数|必填|说明|
    |:--:|:--:|:--:|
    |authorization|是|详见下方|

    <b><i>authorization</b></i>:

    格式 "Bearer {token}"
    
    用于传递token
- 请求参数

    **JSON**:
    |参数|类型|必填|说明|
    |:--:|:--:|:--:|:--:|
    |captcha_output|str|是|人机验证参数|
    |gen_time|str|是|人机验证参数|
    |lot_number|str|是|人机验证参数|
    |pass_token|str|是|人机验证参数|

- 返回
 
    **JSON**：
    |参数|类型|必填|说明|
    |:--:|:--:|:--:|:--:|
    |code|int|是|返回状态码|
    |state|str|是|请求是否成功|
    |msg|str|是|返回消息|

## 签到信息
- 接口
    > GET /qiandao_info
- 请求头
    |参数|必填|说明|
    |:--:|:--:|:--:|
    |authorization|是|详见下方|

    <b><i>authorization</b></i>:

    格式 "Bearer {token}"
    
    用于传递token
- 返回
 
    **JSON**：
    |参数|类型|必返|说明|
    |:--:|:--:|:--:|:--:|
    |code|int|是|返回状态码|
    |state|str|是|请求是否成功|
    |msg|str|是|返回消息|
    |data|map|否|详见下方|

    <b><i>data</b></i>:

    当上方 `state` 为 `success` 返回
    |参数|类型|必返|说明|
    |:--:|:--:|:--:|:--:|
    |count_of_matching_records|int|是|今日签到人数|
    |is_signed_in_today|bool|是|今日签到状态|
    |last_sign_in_time|str|是|最后一次签到时间|
    |total_points|int|是|累计签到获得积分|
    |total_sign_ins|int|是|累计签到次数|
## 生成frpc.ini
- 接口
    > GET&POST /tunnel_config
- 请求参数

    **Query/表单**:
    |参数|类型|必填|说明|
    |:--:|:--:|:--:|:--:|
    |token|str|是|用户令牌|
    |node|str|是|所属节点名称|
    |tunnel_names|str|否|详见下方|

    <b><i>tunnel_names</b></i>:

    隧道名称

    多输入由`,`分隔

    不输入默认返回所属节点all隧道

- 返回

   **JSON**：
    |参数|类型|必返|说明|
    |:--:|:--:|:--:|:--:|
    |code|int|是|返回状态码|
    |state|str|是|请求是否成功|
    |msg|str|是|返回消息|
    |data|str|否|frpc.ini内容|
## 兑换礼品码
- 接口
    > POST /redeem
- 请求头
    |参数|必填|说明|
    |:--:|:--:|:--:|
    |authorization|是|详见下方|

    <b><i>authorization</b></i>:

    格式 "Bearer {token}"
    
    用于传递token
- 请求参数

    **JSON**:
    |参数|类型|必填|说明|
    |:--:|:--:|:--:|:--:|
    |giftcode|str|是|礼品码|
- 返回
 
    **JSON**：
    |参数|类型|必返|说明|
    |:--:|:--:|:--:|:--:|
    |code|int|是|返回状态码|
    |state|str|是|请求是否成功|
    |msg|str|是|返回消息|
## 实名认证
- 接口
    > POST /redeem
- 请求头
    |参数|必填|说明|
    |:--:|:--:|:--:|
    |authorization|是|详见下方|

    <b><i>authorization</b></i>:

    格式 "Bearer {token}"
    
    用于传递token
- 请求参数

    **JSON**:
    |参数|类型|必填|说明|
    |:--:|:--:|:--:|:--:|
    |name|str|是|真实名字|
    |idcard|str|是|身份证号码|
- 返回
 
    **JSON**：
    |参数|类型|必返|说明|
    |:--:|:--:|:--:|:--:|
    |code|int|是|返回状态码|
    |state|str|是|请求是否成功|
    |msg|str|是|返回消息|
## 修改QQ号
- 接口
    > GET&POST /update_qq
- 请求参数

    **Query/表单**:
    |参数|类型|必填|说明|
    |:--:|:--:|:--:|:--:|
    |token|str|是|用户令牌|
    |new_qq|str|是|新QQ号|

- 返回

   **JSON**：
    |参数|类型|必返|说明|
    |:--:|:--:|:--:|:--:|
    |code|int|是|返回状态码|
    |state|str|是|请求是否成功|
    |msg|str|是|返回消息|

## 修改用户名
- 接口
    > GET&POST /update_username
- 请求参数

    **Query/表单**:
    |参数|类型|必填|说明|
    |:--:|:--:|:--:|:--:|
    |token|str|是|用户令牌|
    |new_username|str|是|新用户名|

- 返回

   **JSON**：
    |参数|类型|必返|说明|
    |:--:|:--:|:--:|:--:|
    |code|int|是|返回状态码|
    |state|str|是|请求是否成功|
    |msg|str|是|返回消息|

## 修改用户头像
- 接口
    > GET&POST /update_userimg
- 请求参数

    **Query/表单**:
    |参数|类型|必填|说明|
    |:--:|:--:|:--:|:--:|
    |token|str|是|用户令牌|
    |new_userimg|str|是|详见下方|

    <b><i>tunnel_userimg</b></i>:

    用户新头像图片url

    图片链接仅支持直链，且无反盗链的链接

    必须为 `http://` 或 `https://` 开头
- 返回

   **JSON**：
    |参数|类型|必返|说明|
    |:--:|:--:|:--:|:--:|
    |code|int|是|返回状态码|
    |state|str|是|请求是否成功|
    |msg|str|是|返回消息|
