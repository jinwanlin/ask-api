### JSON接口目录  
  1. [注册](#注册)  
  2. [登陆](#登陆)  
  3. [商品列表](#商品列表)  
  4. [订单列表](#订单列表)  
  5. [订单明细](#订单明细)  
  6. [账单列表](#账单列表)  

==========
#注册、登陆、忘记密码、修改密码
##注册  
####1、输入手机号，系统发送验证码到客户手机上
<!-- 
curl -d "user[phone]=18628405094" http://lvh.me:3000/api/v1/users/sign_up
curl -d "user[phone]=18628405091" http://115.28.160.65/api/v1/users/sign_up

-->
接口：http://115.28.160.65/api/v1/users/sign_up  
方法：POST  
参数：
```ruby
user[phone]=18628405091  #手机号
```
返回值:  
```ruby
{
	"status": 0, # 0成功，-1失败
  "message": "请输入验证码",
  "phone_can_use": true,
  "is_send_validate_code": true
}
``` 

----
####2、输入短信验证码校验并注册
<!-- 
curl -d "user[phone]=18628405093&user[password]=11111111&user[validate_code]=3320" http://lvh.me:3000/api/v1/users/validate
-->
接口：http://115.28.160.65/api/v1/users/validate  
方法：POST  
参数：
```ruby
user[phone]=18628405091
user[password]=11111111  #密码(明码)
user[validate_code]=5921  #验证码
``` 
返回值:  
```ruby
{
  "status": 0, #0成功， -1失败
  "message": "\u9a8c\u8bc1\u6210\u529f!",
  "user": {
    "id": 6,
    "name": null,
    "phone": 18628405093,
    "token": "7745fd11fcdc68896f71fa8710ede9f7",
    "address": "   ",
    "latitude": null,
    "longitude": null,
    "state": "unaudited",
    "level": 1,
    "desc": null
  }
}
```


----

##登陆  
<!-- 
curl -d "user[phone]=18628405091&user[password]=111111" http://lvh.me:3000/api/v1/users/sign_in
curl -d "user[phone]=18628405091&user[password]=111111" http://115.28.160.65/api/v1/users/sign_in
-->
接口：http://115.28.160.65/api/v1/users/sign_in  
方法：POST  
参数：
```ruby
	user[phone]=15657715360  
	user[password]=abc123  #密码明码
``` 
返回值:  
```ruby
	{
		"status":0,
		"message": "登陆失败",
		"user":{  
			"id":1,  
			"name":"成都小吃",  
			"phone":15657715360,  
			"token":"66a26195a3aec740ca2274a16d1c6bd0",  
			"address":"",  #完整地址
			"latitude":null,  #纬度
			"longitude":"",  #经度
			"state":"actived",  #actived（可用）
			"desc":""  
		}
	}
```


##忘记密码
  
##修改密码


#商品列表
方法：POST  
接口：http://115.28.160.65/api/v1/products/list  
<!-- 
curl -d "user[id]=1" http://lvh.me:3000/api/v2/products/list
-->
参数：
```ruby
	user[id]=1
	user[level]=3
	type=Vegetable  #蔬菜
	last_update_at=2014-02-08T10:28:07+08:00  #上次更新时间
``` 
返回值:  
```ruby
{
	"status":0,
	"message": "",
  "user": {
    "level": 4
  },
  "now": "2014-02-12T14:12:19+08:00",
  "products": [{
    "id": 361,
    "sn": "000001",
    "name": "\u5927\u767d\u83dc",
    "type": "Vegetable",
    "amounts": [1, 2, 3, 4, 5, 6, 7, 10, 12, 15, 20, 25, 30],
    "price": 0.0,
    "unit": "\u5343\u514b"
  },
  {
    "id": 366,
    "sn": "000366",
    "name": "\u7ea2\u76ae\u8471\u5934",
    "type": "Vegetable",
    "amounts": [1, 2, 3, 4, 5, 6, 7, 10, 12, 15, 20, 25, 30],
    "price": 1.2,
    "nuit": "\u5343\u514b"
  }]
}
```

#订单
####购买
方法：POST  
接口：http://115.28.160.65/api/v1/order_items  
<!-- 
curl -d "user[id]=1&order_item[product_id]=362&order_item[order_amount]=15" http://lvh.me:3000/api/v1/order_items
-->
参数：
```ruby
	user[id]=4
	order_item[product_id]=2813
	order_item[order_amount]=15
``` 
返回值:  
```ruby
	{
		"status":0,
		"message":"购买成功",  #验证成功  或  验证失败 
	}
```


----

##订单列表
方法：POST  
接口：http://115.28.160.65/api/v1/orders/list  
<!-- 
curl -d "user[id]=1" http://lvh.me:3000/api/v1/orders/list
curl -d "user[id]=1" http://lvh.me:3000/api/v2/orders/list
-->
参数：
```ruby
	user[id]=1
``` 
返回值:  
```ruby
{
  "status": 0,
  "message": null,
  "orders": [{
    "order": {
      "id": 1,
      "sn": "751210",
      "order_sum": 9.6,
      "ship_sum": 0.0,
      "state": "pending",
      "desc": null,
      "created_at": "2014-02-11T14:08:54Z",
      "updated_at": "2014-02-11T14:10:48Z"
    }
  }]
}
```
##订单明细
接口：http://115.28.160.65/api/v1/orders/{id}  
<!-- 
curl http://lvh.me:3000/api/v1/orders/1
-->
方法：GET  
参数：无  
返回值:  
```ruby
{
  "status": 0,
  "message": null,
  "order": {
    "id": 1,
    "sn": "751210",
    "order_sum": 9.6,
    "ship_sum": 0.0,
    "state": "pending",
    "desc": null,
    "created_at": "2014-02-11T14:08:54Z",
    "updated_at": "2014-02-11T14:10:48Z"
  }
}
```



#账单
方法：POST  
接口：http://115.28.160.65/api/v1/payments 
<!-- 
curl -d "user[id]=1" http://lvh.me:3000/api/v1/payments/list
curl -d "user[id]=1" http://lvh.me:3000/api/v2/payments/list
-->
参数：
```ruby
	user[id]=1
``` 
返回值:  
```ruby
[{
  "id": 9,
  "operator_name": null,
  "amount": 23.0,
  "overage": 23.0,
  "order_id": null,
  "order_sn": null,
  "created_at": "2014-02-22 10:06:13",
  "updated_at": "2014-02-22 10:06:13"
},
{
  "id": 10,
  "operator_name": null,
  "amount": 27.0,
  "overage": 50.0,
  "order_id": null,
  "order_sn": null,
  "created_at": "2014-02-22 10:07:48",
  "updated_at": "2014-02-22 10:07:48"
}]
```

