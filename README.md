# spring-boot-oauth2-jwt

[![CircleCI](https://circleci.com/gh/AlissonMedeiros/spring-boot-oatuh2-jwt/tree/master.svg?style=svg)](https://circleci.com/gh/AlissonMedeiros/spring-boot-oatuh2-jwt/tree/master)

### OAuth2 Server

Generate JWT Key

```
$ keytool -genkeypair -alias jwt -keyalg RSA -dname "CN=jwt, L=Berlin, S=Berlin, C=DE" -keypass mySecretKey -keystore jwt.jks -storepass mySecretKey
```

Put the key in `src/main/resources/jwt.jks`

```
$ keytool -list -rfc --keystore jwt.jks | openssl x509 -inform pem -pubkey
▒▒▒▒▒▒Կ▒▒▒▒▒:  mySecretKey
-----BEGIN PUBLIC KEY-----
MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAoLnfiQCCqhXbrRHg/hhR
RIBffp/B/c5xyXqKJ3QYKU2s3iPo9eVFNvZu80KzKhQ6CsTgzRHfujxVp3IOB/CN
tKPfx2P6ulIS0R9sA4mDiXINYLao8Kpg7uK865QehYitB5voMNDTzi3sjUBoKlK5
ps46Pd8YmuXmM7TxonFGYjaGGtdt+w0RiC5ggF3mvzk6AHUR1KupCNPpcsGNMYGG
ek4FMcxZf2QBJEtvRN76blwQiUDX6R7xx4yeKsew2sVU86hE14h2NbuvVtdDIOKM
+F76o3+zGQzn4/Ijcs9faWoHbLUmigEmYU08B2zc3/6eDiaFsa0Lcm8QCWprVfpe
DQIDAQAB
-----END PUBLIC KEY-----
-----BEGIN CERTIFICATE-----
MIIDGTCCAgGgAwIBAgIEULSkdTANBgkqhkiG9w0BAQsFADA9MQswCQYDVQQGEwJE
RTEPMA0GA1UECBMGQmVybGluMQ8wDQYDVQQHEwZCZXJsaW4xDDAKBgNVBAMTA2p3
dDAeFw0xNjExMDUwNjAyNTFaFw0xNzAyMDMwNjAyNTFaMD0xCzAJBgNVBAYTAkRF
MQ8wDQYDVQQIEwZCZXJsaW4xDzANBgNVBAcTBkJlcmxpbjEMMAoGA1UEAxMDand0
MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAoLnfiQCCqhXbrRHg/hhR
RIBffp/B/c5xyXqKJ3QYKU2s3iPo9eVFNvZu80KzKhQ6CsTgzRHfujxVp3IOB/CN
tKPfx2P6ulIS0R9sA4mDiXINYLao8Kpg7uK865QehYitB5voMNDTzi3sjUBoKlK5
ps46Pd8YmuXmM7TxonFGYjaGGtdt+w0RiC5ggF3mvzk6AHUR1KupCNPpcsGNMYGG
ek4FMcxZf2QBJEtvRN76blwQiUDX6R7xx4yeKsew2sVU86hE14h2NbuvVtdDIOKM
+F76o3+zGQzn4/Ijcs9faWoHbLUmigEmYU08B2zc3/6eDiaFsa0Lcm8QCWprVfpe
DQIDAQABoyEwHzAdBgNVHQ4EFgQUaisB+TYSddByoWa9a9Xhpjx3+YQwDQYJKoZI
hvcNAQELBQADggEBAHyLIstXg+O63ETlsyovscyGVv4F1MrWx3nmZT++mlr7Ivbw
UoOzG71knOkaAINox/BrPCciDddBIRkKDdT6orolMg1HiPZGwCt+DJ2c7J/kFyJ3
kCUeQp6JefHIKrQUeEErPSDaQpm+afc0mq5I/FP5Kg0aSg6sUr1SJfqG6aEWf/pg
8V8I3/bGFG1QzHER3R/hX2f+09UElgIvIK8KTJoT1EnVRbzDyG0IEvvheIk/TXG+
ICaxFrDCkavbP2Swx7HuMNi9FQEIQ7lwPYtzX6cfeYYNHJ1CR70uN9YYkroTRWLx
4vsgVFhzRbGvnW5Ufv18lI0IThHsU395F/75aFw=
-----END CERTIFICATE-----
```

### OAuth2 Server

#### 1、password, grant_type=password， `accesstoken`

* Type: `password`

```
$ curl "acme:acmesecret@localhost:8080/oauth/token" -d "grant_type=password&username=user&password=user"
{"access_token":"eyJ...
```

* Type `accesstoken`

```
$ curl "acme:acmesecret@localhost:8080/oauth/token" -d "grant_type=password&username=admin&password=admin"
{"access_token":"eYj...
```

#### 2、refresh_token

`password`authorization_code``accesstoken`，`refresh_token`，`/oauth/token -d grant_type=refresh_token -d refresh_token=$refresh_token``accesstoken`

* password

```
curl "acme:acmesecret@localhost:8080/oauth/token" -d "grant_type=password&username=user&password=user"
{"access_token":"eyJ...
```
`access_token` `refresh_token`，`refresh_token``/oauth/token -d grant_type=refresh_token -d refresh_token``accesstoken`

```
curl acme:acmesecret@localhost:8080/oauth/token -d grant_type=refresh_token -d refresh_token=eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VyX25hbWUiOiJ1c2VyIiwic2NvcGUiOlsib3BlbmlkIl0sImF0aSI6IjQ3NTYwMTc3LWVhODMtNGY3OS04Y2E3LWViMjBhNjAzY2VmZSIsImV4cCI6MTQ5ODgxMTY2OCwiYXV0aG9yaXRpZXMiOlsiUkVBRCJdLCJqdGkiOiI5MzExOTZjOS03NGU2LTQ3ZDUtYjA3MC0xMGNhYzg2NjUzZTAiLCJjbGllbnRfaWQiOiJhY21lIn0.aQqsdkQfCy4L4FjV6TZyRehG6ZjgmuWe-30uuco-g5GKmuxJGEoY6dYOiDhsTOgKoxDXJwN6kACZMePInP4cXrExK6N7n25MbUXn-IxPGb1TTy3YmcaVwLM-oP2IW-dxzYLjmT3XYgA8Xt4vY2z8trzkvR2jefP-cHP0uQq7jFjDVYSq37epJozPNYWd_630jWokjbOQr3MwMcsLjmUz8eUmMm8I7Ln1XM2RFlmw09_eFLk0FNtwuWd-IFXsjPc_2jaNASJYEfurNlTN8OH7LKe34enDZoPgpbsMxUUsF3EW9iq2NwnV9btEPqe-a-wJDCftXvV7GxmOKxdg--X2zw
{"access_token":"eyJ...
```

* authorization_code

Access this url to get a Code (you need to get the code in the response):

`http://localhost:8080/oauth/authorize?response_type=code&client_id=acme&redirect_uri=https://www.google.com.br` 

The response is like this:

`https://www.google.com.br/?code=Axjz0f`

Replace the code:

curl acme:acmesecret@localhost:8080/oauth/token -d grant_type=authorization_code -d client_id=acme -d redirect_uri=https://www.google.com.br -d code={NEW_CODE}
{"access_token":"eyJhb...
```

`/oauth/token -d grant_type=refresh_token -d refresh_token=$refresh_token``accesstoken`

```
curl acme:acmesecret@localhost:8080/oauth/token -d grant_type=refresh_token -d refresh_token=$[TOKEN]
{"access_token":"eyJh...
```

#### 3、client_credentials

grant_type=client_credentials，accesstoken

```
curl acme:acmesecret@localhost:8080/oauth/token -d grant_type=client_credentials -d scope=openid
{"access_token":"eyJ..
```

#### 4、authorization_code

`authorization_code``accesstoken`：

1、`/oauth/authorize?response_type=code``code`

2、`/oauth/token -d grant_type=authorization_code``accesstoken`

```
http://localhost:8080/oauth/authorize?response_type=code&client_id=acme&redirect_uri=https://www.google.com.br
```

`https://www.google.com.br/?code=8JsYwV`，`code`accesstoken

```
$ curl acme:acmesecret@localhost:8080/oauth/token -d grant_type=authorization_code -d client_id=acme -d redirect_uri=https://www.google.com.br -d code=8JsYwV
{"access_token":"eyJhbGciOiJSUzI1NiJ9.eyJleHAiOjE0NzgzNzkzMzQsInVzZXJfbmFtZSI6ImFkbWluIiwiYXV0aG9yaXRpZXMiOlsiUkVBRCIsIldSSVRFIl0sImp0aSI6IjAyMjgyMzNkLWVjY2MtNDU5YS1hYjBkLTg4ZGU2MDQ0MWIwMCIsImNsaWVudF9pZCI6ImFwcENsaWVudCIsInNjb3BlIjpbIm9wZW5pZCJdfQ.tGQjNR_Xg_E52xFEIashqWPnH-hnvBsqkKjbNiQgHUGE-4wHNJ-wxxia-cfvfD4IR5fA3AekSUWzGk3uLaD4q66HmCHgl1zdSjgXEqsEC-C1VqI_FLq0HlunFtJ6i4mHjY0nIxsIx5hhdoyVONJk3HyckegCaVUKy8g1q8hn7qiuBpcZCTUhfuYq5Lb1A3nbCUMQRB72eZ3slC8l3Y60kAhVP3gcY5gLYwPrL-1O2FuwEOO_vpoe-yzdp-WxUabpX7v-78oxkpA2LKxQu-9fNwlJmsTTzk4bZ-onRHdVtHjZr_QvqekXTqDBnXVrv26r2cpSqli69R58M8OIvHKpAw","token_type":"bearer","refresh_token":"eyJhbGciOiJSUzI1NiJ9.eyJ1c2VyX25hbWUiOiJhZG1pbiIsInNjb3BlIjpbIm9wZW5pZCJdLCJhdGkiOiIwMjI4MjMzZC1lY2NjLTQ1OWEtYWIwZC04OGRlNjA0NDFiMDAiLCJleHAiOjE0ODA5MjgxMzQsImF1dGhvcml0aWVzIjpbIlJFQUQiLCJXUklURSJdLCJqdGkiOiIyMzJkZDBiMS1kNzc2LTQ4MTItOTllNy0xNjRiZmNhOTY3ZTgiLCJjbGllbnRfaWQiOiJhcHBDbGllbnQifQ.WRgsM-ZFyYwU7ObLjNSzRFe0CUU0P7TyprKY825qL8teHPhgKLOxYDSXDDdjIwlLzOFXRz0skX6-h6kLXvXvvkPRFG3KK01j7jVmOfn1bXTYP0sgOwZvBvkDeZp0LFZIBL2ruH_ciWou6LleCgRIhtUVyKYMojr4-4eFZ_ou6J8ezykvzlf-xwTXJhwOqXf57jeYsXy9eitUf8A_x7Lrz9HffW0HA5JfhFX1P-_W1vS3uUqwQLZovhAzEK2LctZmUHAfUKIuE9Z4Z1_pQDDK7hWbv2eRHAlceRGRvztrEebv-5cksfEUWpiQmj913t20uXzEfJYU3e9JqbqxbaahKA","expires_in":43199,"scope":"openid","jti":"0228233d-eccc-459a-ab0d-88de60441b00"}
```

#### 5、implicit

`token``accesstoken`（/oauth/authorize?response_type=token）`accesstoken`

```
http://localhost:8080/oauth/authorize?response_type=token&client_id=acme&redirect_uri=https://www.google.com.br
```

`https://www.google.com.br/#access_token=eyJhbGciOiJSUzI1NiJ9.eyJleHAiOjE0NzgzNzg4NjEsInVzZXJfbmFtZSI6ImFkbWluIiwiYXV0aG9yaXRpZXMiOlsiUkVBRCIsIldSSVRFIl0sImp0aSI6ImEyMzE3NTlmLTZhMzktNGQ3YS1iMmMyLWIwOTdlMWZjZTEwMiIsImNsaWVudF9pZCI6ImFwcENsaWVudCIsInNjb3BlIjpbIm9wZW5pZCJdfQ.ASSLsAJa8CsgZDsv5vH8BqYTbmoCCeYKqSmv4m9jl2XpWc2edvauy89Vxvj8z6kKGr8QqDg786u6MMW7fX5CAjP34Mfs9XVI8gfg20Xk0sHoS3WPx0mseIXdJbaxhj0526X5947-eeMr_LDC5N_XlPQ3Qq_PcY3tmyh92IWUri2rRJMKEPHrmVqqWPcPcCSHoEaaMWNTq_gsdbsZiyX4jaW24LVQ0HZ4oYMnmUzbLCvIyPcKF7WR-KKEnOykYX5FJPjnbUz6EK5yG_icdkULsxmDr05JrEgkKR0n_JfL9_gOqpI8mpJFBkAUghM1y9No_fGvvhb22o-H8ar5wnGqYA&token_type=bearer&expires_in=43199&scope=openid&jti=a231759f-6a39-4d7a-b2c2-b097e1fce102`


### OAuth2 Client，accesstoken

```
TOKEN=eyJhbGciOiJSUzI1NiJ9.eyJleHAiOjE0NzgzNzQ3NTcsInVzZXJfbmFtZSI6InVzZXIiLCJhdXRob3JpdGllcyI6WyJSRUFEIl0sImp0aSI6Ijg4Zjk4ZWYxLTZjOGItNDA1MC1iOTc3LWFlYjcxMzhlNjg2OCIsImNsaWVudF9pZCI6ImFwcENsaWVudCIsInNjb3BlIjpbIk9BdXRoMiJdfQ.sop6d8acs6piMgiN1FH8EVw4Qglh69wU5vvdMQZ87YSVjtaTCQqpf4kR65jXtqTNuTTZ8azf_aD5GoIBaqVrDDGEHk8dZLciobgD1vexpX2XnrfAFUt0xHg1LXIO_mJtf7x4CBiF4ysGWdlhWQbX2wq5YNvG3QhIkRHdnvxBNSiLJPSaa2sqHKxdXs4J7tLnNN415K1TI2pV7_6C3p-BQD2qfdIWZXB2JLYSmTVjnvUQtjIvLDNu8OL7mvyfP2F_d-b-PAPYU4ul9RZfnB9hYr02i8M-7lYh7pK-SoA0MlMlIP-QSDpACTqWuWpyP_q8N-tFDwPZ997ES2FOaWArFA
```

`GET`

```
$ curl -H "Authorization: Bearer $TOKEN" "localhost:9090/users"
```

`POST`

```
$ curl -XPOST -H "Authorization: Bearer $TOKEN" "localhost:9090/users"
```


```
$ curl -H "Authorization: Bearer $TOKEN" "localhost:8080/user"
{"details":{"remoteAddress":"0:0:0:0:0:0:0:1","sessionId":null,"tokenValue":"eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJleHAiOjE0NzgzODY3NjcsInVzZXJfbmFtZSI6ImFkbWluIiwiYXV0aG9yaXRpZXMiOlsiUkVBRCIsIldSSVRFIl0sImp0aSI6Ijc2OTYzMzkyLWUxYzItNDdmMC05ODZjLWZhODQxZmZhYTU1NyIsImNsaWVudF9pZCI6ImFwcENsaWVudCIsInNjb3BlIjpbIm9wZW5pZCJdfQ.WiTSjojK0ow1x7fP0y3EZohCozU2kB4Sxi2xPd7A5RSb48N-KDM8PYjSX--D1iiEQiRt2xOdBij0J0A7pIHfqZMijphyJQtPQjyv_82AIP7hFuW-PFMo2P1VVSTWrZeYzCMCr8p1QaHbM5bJ1KTeiT_Ak8vbqmnd7r4KpqoyEehca69tr02nTPhi7YOfAjUm9czwqhhi2w4bL9b2epYhmv_d2B2LwCY4NZxv64xfeCti8ya-AG_hYoqNRGj2nIHaAR_uCWmDD6_tdESy5oKZJ-881Dr0VFduJu4cAcSxJX-PqI6HklknTm_Vzqik9lI9S02z3fj5sBM7trWvNuBnrQ","tokenType":"Bearer","decodedDetails":null},"authorities":[{"authority":"READ"},{"authority":"WRITE"}],"authenticated":true,"userAuthentication":{"details":null,"authorities":[{"authority":"READ"},{"authority":"WRITE"}],"authenticated":true,"principal":"admin","credentials":"N/A","name":"admin"},"principal":"admin","credentials":"","oauth2Request":{"clientId":"acme","scope":["openid"],"requestParameters":{"client_id":"acme"},"resourceIds":[],"authorities":[],"approved":true,"refresh":false,"redirectUri":null,"responseTypes":[],"extensions":{},"grantType":null,"refreshTokenRequest":null},"clientOnly":false,"name":"admin"}
```


org.springframework.security.oauth2.provider.endpoint.TokenEndpoint /oauth/token

org.springframework.security.oauth2.provider.endpoint.AuthorizationEndpoint /oauth/authorize

org.springframework.security.config.annotation.web.configuration.WebSecurityConfigurerAdapter WebSecurityConfigurer。


### Based on:

https://github.com/ameizi/spring-boot-oauth2-example

http://callistaenterprise.se/blogg/teknik/2015/04/27/building-microservices-part-3-secure-APIs-with-OAuth/

http://docs.spring.io/spring-security/site/docs/4.2.2.RELEASE/reference/htmlsingle/#user-schema

https://github.com/spring-projects/spring-security-oauth/blob/master/spring-security-oauth2/src/test/resources/schema.sql
