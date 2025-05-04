# API v2
APIv2 还在开发中

也许api今天是这样 明天就变样了

同时该文档可能有不准确 以api实际为准

在 [XCL2](https://github.com/FengXiangqaq/Xingcheng-Chmlfrp-Lanucher/) 开发中发现本文档的错误也会纠正错误

统一调用地址
> https://cf-v2.uapis.cn/

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

    **json**：
    |参数|类型|必返|说明|
    |:--:|:--:|:--:|:--:|
    |code|int|是|返回状态码|
    |state|str|是|请求是否成功|
    |msg|str|是|返回消息|
    |data|map|否|详见下方|

    ***data***:

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

    ***bandwidth***:

    用户带宽限制：

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

  [**同上**](#登录)
## 隧道列表
- 接口
    > GET&POST /tunnel
- 请求参数

    **Query/表单**:
    |参数|类型|必填|说明|
    |:--:|:--:|:--:|:--:|
    |token|str|是|用户令牌|
- 返回

    **json**：
    |参数|类型|必返|说明|
    |:--:|:--:|:--:|:--:|
    |code|int|是|返回状态码|
    |state|str|是|请求是否成功|
    |msg|str|是|返回消息|
    |data|list|否|详见下方|

    ***data***:

    当上方 `state` 为 `success` 返回
    
    list中有若干个map 每个map代表一条隧道

    map参数详见下方

    ***Map***：
    |参数|类型|必返|说明|
    |:--:|:--:|:--:|:--:|
    |id|int|是|隧道id|
    |name|str|是|隧道名|
    |node|str|是|所属节点|
    |nodestate|str/null|是|节点状态|
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
## 创建隧道
- 接口
    > POST /create_tunnel
- 请求参数

    **json**:
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

    ***porttype***：

    隧道类型

    值为tcp/udp/http/https

    ***banddomain***：

    绑定域名

    当porttype值为http/https需填

    ***remoteport***：

    内网端口

    当porttype值为tcp/udp需填 

- 返回

    
    **json**：
    |参数|类型|必返|说明|
    |:--:|:--:|:--:|:--:|
    |code|int|是|返回状态码|
    |state|str|是|请求是否成功|
    |msg|str|是|返回消息|
    |data|map|否|详见下方|

    ***data***:

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