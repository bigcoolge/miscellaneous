## 鉴权接口


### 1. 登录接口

#### 接口功能

> 用户登录验证

#### URL

> /{version}/payment/operation/user/login

#### 支持格式

> JSON

#### HTTP请求方式

> POST

#### 请求参数

|参数|必须|类型|描述|备注|
|:----- |:-------|:-----|:----- |:----- |
|username |true |String|用户名||
|password |true |String |用户密码|||


#### 返回字段

|参数|必须|类型|描述|备注|
|:----- |:------|:------|:------|:-------------- |
|respCode | true | int |0(成功)，1(失败) ||
|respMsg | true | String | 失败原因描述 ||
|data | true | JSONOBJECT | JWT token |需要用在后续的请求头中|

#### 请求参数示例

http://hostname:port/v1/payment/operation/user/login
```json
{
	"username": "operation",
	"password": "operation"
}
```

#### 响应结果示例

```json
{
    "respCode": 0,
    "respMsg": "OK",
    "data": "eyJhbGciOiJIUzI1NiIsInppcCI6IkdaSVAifQ.H4sIAAAAAAAAAKtWyiwuVrJS8nVU0lHKTCxRsjI0NTazMDI2MbHUUUqtKIAIWBpYWoAESotTi_ISc1OBOvILUosSSzLz85RqAQVosRJFAAAA.Jx7u54y4R6pgX22iY94NZUN7NqZYqnzEqLZhT4nva2A"
}
```
