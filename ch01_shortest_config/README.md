## 获取code

```http
GET /oauth2/authorize?response_type=code&client_id=oidc-client&redirect_uri=http%3A%2F%2F127.0.0.1%3A8080%2Flogin%2Foauth2%2Fcode%2Foidc-client&scope=openid%20profile&state=123456789
Host: localhost:9000
```

浏览器中输入以上请求后，会先跳到一个登录页面。输入user password登录后，会跳转到一个带有code的地址：

```shell
http://127.0.0.1:8080/login/oauth2/code/oidc-client?code={{code}}&state=123456789
```

## 获取token

```http
POST /oauth2/token HTTP/1.1
Host: localhost:9000
Content-Type: application/x-www-form-urlencoded
Authorization: Basic b2lkYy1jbGllbnQ6c2VjcmV0

grant_type=authorization_code&code={{code}}&redirect_uri=http%3A%2F%2F127.0.0.1%3A8080%2Flogin%2Foauth2%2Fcode%2Foidc-client
```

以上的Authorization中的值是clientId clientSecre通过base64编码得到，即basicAuth的方式，用户名是clientId，密码是clientSecret。

获取到的token：

```json
{
    "access_token": "xxx",
    "refresh_token": "yyy",
    "scope": "openid profile",
    "id_token": "zzz",
    "token_type": "Bearer",
    "expires_in": 299
}
```

## 刷新token

```http
POST /oauth2/token HTTP/1.1
Host: localhost:9000
Content-Type: application/x-www-form-urlencoded
Authorization: Basic b2lkYy1jbGllbnQ6c2VjcmV0

grant_type=refresh_token&refresh_token={{refresh_token}}
```

