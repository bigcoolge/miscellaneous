## 支付服务统计接口（需通过鉴权验证）


### 1. CPSP管理统计接口

#### 接口功能

> 查询指定时间段的订单

#### URL

> /{version}/payment/operation/cpsp

#### 支持格式

> JSON

#### HTTP请求方式

> GET

#### 请求参数

|参数|必须|类型|描述|备注|
|:----- |:-------|:-----|:----- |:----- |
|startDate |true |String|查询开始时间节点 <br> (2011-11-11 11:11:11，yyyy-MM-dd HH:mm:ss）||
|endDate |true |String |查询结束时间节点 <br> (2011-11-11 11:11:11，yyyy-MM-dd HH:mm:ss）|统计时间范围是 [startDate, endDate] <br> 以订单生成时间作为依据|
|category |false |int |业务分类, 当前分为 0(停车) 1(充电) |不指定该值将返回包含所有业务类别的数据|
|merchant |false |String |CPSP名称，当前支持 ETCP(ETCP停车) ，EVCS(星星充电) |不指定该值将返回包含所有CPSP的数据|
|accType |false |int |支付渠道，0(未知)，1(支付宝)，2(微信) |不指定该值将返回包含所有支付方式的数据； <br> 目前Kodai项目没有银联支付方式； <br> 由于CPSP传入数据时不准确，会导致统计数据的不准确； 比如用户多次用不同支付方式拉取支付二维码，会在数据库中存入多次同一订单的数据，由此将产生未支付订单|


#### 返回字段

|参数|必须|类型|描述|备注|
|:----- |:------|:------|:------|:-------------- |
|respCode | true | int |0(成功)，1(失败) ||
|respMsg | true | String | 失败原因描述 ||
|data | true | JSONARRAY | 详细数据 | 数组格式 |
| 丨 count | true | int | 订单数 | |
| 丨 category | true | int | 业务分类 (定义同上)| |
| 丨 merchant | true | String | CPSP名称 (定义同上) | |
| 丨 accType | true | int | 支付渠道 (定义同上) | |
| 丨 status | true | int | 订单状态 1(已完成订单) 2(未完成订单) | 已完成订单会包含坏账情况 <br> 未完成订单会包含重复的订单和尚未支付的订单 |

#### 请求参数示例

http://hostname:port/v1/payment/operation/cpsp?startDate=2011-11-11%2011%3A11%3A11&endDate=2011-11-12%2012%3A12%3A12&merchant=ETCP

#### 响应结果示例

```json
{
  "respCode": 0,
  "respMsg": "SUCCESS",
  "data": [
    {
      "count": 100,
      "category": 0,
      "merchant": "ETCP",
      "accType": 1,
      "status": 1
    },
    {
      "count": 10,
      "category": 0,
      "merchant": "ETCP",
      "accType": 1,
      "status": 2
    },
    {
      "count": 200,
      "category": 0,
      "merchant": "ETCP",
      "accType": 2,
      "status": 1
    },
    {
      "count": 20,
      "category": 0,
      "merchant": "ETCP",
      "accType": 2,
      "status": 2
    },
    {
      "count": 35,
      "category": 0,
      "merchant": "ETCP",
      "accType": 0,
      "status": 1
    }
  ]
}
```
