## 支付服务统计接口


### 2. 业务管理统计接口

#### 接口功能

> 查询指定时间段的服务总计

#### URL

> /{version}/payment/operation/business

#### 支持格式

> JSON

#### HTTP请求方式

> GET

#### 请求参数

|参数|必须|类型|描述|备注|
|:----- |:-------|:-----|:----- |:----- |
|startDate |true |String|查询开始时间节点 <br> (2011-11-11 11:11:11，yyyy-MM-dd HH:mm:ss）||
|endDate |true |String |查询结束时间节点 <br> (2011-11-11 11:11:11，yyyy-MM-dd HH:mm:ss）|统计时间范围是 [startDate, endDate] <br> 以订单生成时间作为依据|


#### 返回字段

|参数|必须|类型|描述|备注|
|:----- |:------|:------|:------|:-------------- |
|respCode | true | int |0(成功)，1(失败) ||
|respMsg | true | String | 失败原因描述 ||
|data | true | JSONOBJECT | 详细数据 | |
| 丨 userCount | true | int | 总用户数 | 以userId作为统计依据 |
| 丨 amount | true | BigDecimal | 总支付金额 | |
| 丨 payment | true | JSONOBJECT | | 支付成功统计 |
| 丨丨 totalCount | true | int | 总支付次数 | |
| 丨丨 accType | true | JSONOBJECT | | 支付渠道 |
| 丨丨丨 alipayCount | true | int | 支付宝支付次数 | |
| 丨丨丨 wechatpayCount | true | int | 微信支付次数 | |
| 丨丨 payMethod | true | JSONOBJECT | | 支付方式 |
| 丨丨丨 freePwdCount | true | int | 免密支付次数 | |
| 丨丨丨 proactiveCount | true | int | 主动支付次数 | <br> |

#### 请求参数示例

http://hostname:port/v1/payment/operation/business?startDate=2011-11-11%2011%3A11%3A11&endDate=2011-11-12%2012%3A12%3A12

#### 响应结果示例

```json
{
  "respCode": 0,
  "respMsg": "SUCCESS",
  "data": {
    "userCount": 500,
    "amount": 10020.55,
    "payment": {
      "totalCount": 2000,
      "accType": {
        "alipayCount": 1500,
        "wechatpayCount": 500
      },
      "payMethod": {
        "freePwdCount": 70,
        "proactiveCount": 1930
      }
    }
  }
}
```
