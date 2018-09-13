## 鉴权接口（需通过鉴权验证）


### 2. 更新令牌接口

#### 接口功能

> 更新用户令牌

#### URL

> /{version}/payment/operation/token

#### 支持格式

> JSON

#### HTTP请求方式

> POST

#### 请求参数

> 无

#### 返回字段

|参数|必须|类型|描述|备注|
|:----- |:------|:------|:------|:-------------- |
|respCode | true | int |0(成功)，1(失败) ||
|respMsg | true | String | 失败原因描述 ||
|data | true | JSONOBJECT | JWT token |||

#### 请求参数示例

http://hostname:port/v1/payment/operation/token


#### 响应结果示例

```json
{
    "respCode": 0,
    "respMsg": "OK",
    "data": "eyJhbGciOiJIUzI1NiIsInppcCI6IkdaSVAifQ.H4sIAAAAAAAAAKtWyiwuVrJS8nVU0lHKTCxRsjI0NTazMDI2MbHUUUqtKIAIWBpYWoAESotTi_ISc1OBOvILUosSSzLz85RqAQVosRJFAAAA.Jx7u54y4R6pgX22iY94NZUN7NqZYqnzEqLZhT4nva2A"
}
```
