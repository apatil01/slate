--- 

title: ExternalAPI 

language_tabs: 
  - shell: Shell
  - http: HTTP
  - javascript: JavaScript
  - javascript--nodejs: Node.JS
  - ruby: Ruby
  - python: Python
  - java: Java
  - go: Go

<!--toc_footers: 
   - <a href='#'>Sign Up for a Developer Key</a> 
   - <a href='https://github.com/lavkumarv'>Documentation Powered by lav</a> -->

includes: 
   - errors 

search: true 

--- 

# Introduction 
PEX is a commercial prepaid card that helps your company control employee spending. You can issue cards, add funds to cards, and apply spend controls (including restricting specific merchant categories) through our Admin portal which includes 24/7 access to your PEX account as well as mobile support. 

The PEX platform is also available through a complete set of JSON-based APIs which can be used to duplicate every feature available in our Admin portal, and to support a few features that aren’t. The PEX platform can be used to power any proprietary expense management or business payment application to create a seamless payment experience for your users. 

##***Sign up for PEX API***
PEX offers a collection of APIs to help build integrations for a variety of use cases, including Card Funding and Reporting. Customers are provided with a sandbox environment to familiarize themselves with the PEX API system. The sandbox environment offers the opportunity to explore all API calls before enacting production APIs.

**Sandbox API Access**

* Step 1: Create Account

[Sign up](https://developer.pexcard.com/signup")for an account at developer.pexcard.com. This account represents you as a developer in the PEX developer portal.
You will receive a welcome email from PEX with more information.
Already have an account? Click [Sign in]("https://developer.pexcard.com/signup") to continue.. 

* Step 2:Access your "Client Id" and "Client Secret" 

Log in to developer.pexcard.com with your developer credentials
Click on the Dashboard tab 
Click the lock icon next to "Client Id" and "Client Secret" to reveal the values

* Step 3: Create Token 

Create Base64 encoded values of your Client Id and Client Secret by using a tool such as [base64encode.com]("https://www.base64encode.org")
Generate a new access token by using the POST /token endpoint with the inputs documented below: 

    * Your Base64-encoded Client Id and Client Secret

    * Your Sandbox admin username and password (sent in an email in step 1)

For details about the token end point, please refer to [Create Token](#create-token)

After successfully generating the token, you can explore the APIs in Sandbox by visiting: [Ping end point](https://sandbox-coreapi.pexcard.com/v4/ping)

**Production API Access.**

Once you finish development of your integration in Sandbox, and the integration has been reviewd by PEX, your production "Client Id" and "Client Secret" will be provided to you. The production token can be generated in same way described above in Step 2 and Step 3 using production log in credentials. 

<aside class="notice">
For additional assistance, please email apisupport@pexcard.com or use the forums available in your developer account
</aside>

##Rate Limit

In order to assure consistent, reliable service for all of our customers, all API users are subject to an overall limit of 120 calls per minute. 

Certain APIs have individual limits:

End Point | Limit
-------------- | -------------- 
GET/Details/TransactionDetails | 1 hit per minute
GET/Details/AccountDetails | 10 hits per hour
GET/Details/AllCardholderTransactions | 10 hits per hour
POST/Bulk/Zero | 2 hits per hour
POST/Card/Zero/{Id} | 1 hit per 4 mins for same card account
POST/Business/OneTimeTransfer | 2 hits per hour
POST/Token | 2 hits per day
DELETE/Token | 2 hits per day


<aside class="notice">
For POST/Card/Zero/{Id} end point, system will allow only 1 hit per 4 mins for same card account.
</aside>

<aside class="notice">
If you exceed any API limits, you will receive error **429: Usage Limits Exceeded**. Please contact 
your API support manager for work-arounds and help if you are receiving error responses related to Usage Limits Exceeded.
</aside>


##Backword Compatible Changes

We strive to avoid making any changes that would break our API calls, but we do make changes over time that may result in changes to the data that you pull from PEX.</p>

We consider the following changes to be backwards compatible:

* Adding new API endpoints

* Adding new data elements to existing response schemas

* Adding new webhooks

* Changing the length or content of any API identifier





#Token Management
##Create Token
```shell
# You can also use wget
curl -X POST https://coreapi.pexcard.com/v4/Token \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: basic '

```

```http
POST https://coreapi.pexcard.com/v4/Token HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: basic 

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'basic '

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/Token',
  method: 'post',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');
const inputBody = '{
  "Username": "",
  "Password": ""
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'basic '

};

fetch('https://coreapi.pexcard.com/v4/Token',
{
  method: 'POST',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json',
  'Authorization' => 'basic '
}

result = RestClient.post 'https://coreapi.pexcard.com/v4/Token',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'Authorization': 'basic '
}

r = requests.post('https://coreapi.pexcard.com/v4/Token', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/Token");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("POST");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Content-Type": []string{"application/json"},
        "Accept": []string{"application/json"},
        "Authorization": []string{"basic "},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("POST", "https://coreapi.pexcard.com/v4/Token", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

> Body Parameter

```json
{
  "Username": ""
  "Password": ""
}
```

> Example responses

> 201 Response

```json
{
  "Token": ""
}
```
**Summary:** Generate a new access token

**Description:** Create a token.<br/>
            <br/>
            A token is required to make all API calls. The life of a token is six (6) months.<br/>
            <br/>
            Tokens are the equivalent of a username/password combination and must not be shared or distributed to untrusted parties.<br/>
            <br/>
            Token authentication is only secure if SSL is used. Therefore, all requests (both to obtain and use the tokens) must use HTTPS endpoints. Please follow the best practices using SSL - peers should always be verified. To find our latest VeriSign certificate, please go to <A href="https://coreapi.pexcard.com" target="_blank">https://coreapi.pexcard.com</A>.<br/>
            <br/>
            If you are a partner (API user), your customer will provide a PEX administrator or cardholder username/password that you (partner) will generate the token from. You (partner) then use that token to authenticate.<br/>
            <br/>
            If you are a customer, you received your API username/password from PEX Operations.<br/>  
            <br/>
            Before creating your first token the following pre-steps are required:<br/>
            <list type="number">
            <item>1. On developer.pexcard.com, select Dashboard in the blue menu bar.</item><br/>
            <item>2. In the API Keys section, click on the lock and key icons to show the values on the screen. If you have access to both Beta and Production, each will be listed separately.</item><br/>
            <item>3. From the returned (beta or production) values, create a Base64 encoded value for authorization. To do this you can use a simple tool like the one found here <A href="https://www.base64encode.org" target="_blank">https://www.base64encode.org</A>.
            The input should be in the following format: ClientID:ClientSecret. (HELPFUL TIP: If you copy the copy and paste the ClientId and ClientSecret please be sure that no extra characters or spaces are included. Correct: <b>ClientID:ClientSecret</b> Incorrect: <b>ClientID: ClientSecret</b>)</item></br>
            <item>4. The returned encoded value should be used in all API calls.</item><br/>
            </list>
            Note: To see the Curl example -  in the Authorization field, prepend the word basic to the Base64 encoded value, for example,<br/>
            basic MmRlMWZjZgq6OTU0MzQwYmY3OGIwNjFjnJcxIIY0MWM2NWE4NWIxPPO=<br/>

**HTTP Request**
`***POST*** /Token` 



**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| userRequest | body | Username and password | Yes |  |
| Authorization | header | basic {Base64Encoded appId:appSecret} | Yes | string |



**Responses**

| Code | Description |
| ---- | ----------- |
| 201 | Created |
| 401 | <list type="number">    <item>      <description>- Invalid authorization parameter (appId:appSecret as base64)<br /></description>    </item>    <item>      <description>- Invalid username or password</description>    </item>  </list> |

## Renew Token 

```shell
# You can also use wget
curl -X POST https://coreapi.pexcard.com/v4/Token/Renew \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
POST https://coreapi.pexcard.com/v4/Token/Renew HTTP/1.1
Host: coreapi.pexcard.com

Accept: application/json
Authorization: string

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/Token/Renew',
  method: 'post',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');

const headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/Token/Renew',
{
  method: 'POST',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.post 'https://coreapi.pexcard.com/v4/Token/Renew',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.post('https://coreapi.pexcard.com/v4/Token/Renew', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/Token/Renew");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("POST");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("POST", "https://coreapi.pexcard.com/v4/Token/Renew", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

> Example responses

> 200 Response

```json
{
  "Username": "",
  "Token": "",
  "AppId": "",
  "TokenExpiration": ""
}
```

**Summary:** Reissue token prior to expiration

**Description:** Reissue an existing token. A new token will be generated based on your existing valid token.  This end-point does not extend the expiration date of an existing token.<br/>
            <br/>
            All tokens expire 6 months after creation. You can reissue the token one (1) month prior to its expiration date. Once the token is expired, it cannot be renewed and you will need to generate a new one.<br/>
            <br/>
            If you know a token has been compromised, please delete it and generate a new one.<br/>
            <br/>
            To get the expiration date of a token, use GET /Token.

**HTTP Request** 
`***POST*** /Token/Renew` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| Authorization | header | token {USERTOKEN} | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Success |
| 403 | Cannot renew token |


## Retrieve Token 

```shell
# You can also use wget
curl -X GET https://coreapi.pexcard.com/v4/Token/GetAuthTokens \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
GET https://coreapi.pexcard.com/v4/Token/GetAuthTokens HTTP/1.1
Host: coreapi.pexcard.com

Accept: application/json
Authorization: string

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/Token/GetAuthTokens',
  method: 'get',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');

const headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/Token/GetAuthTokens',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.get 'https://coreapi.pexcard.com/v4/Token/GetAuthTokens',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.get('https://coreapi.pexcard.com/v4/Token/GetAuthTokens', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/Token/GetAuthTokens");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "https://coreapi.pexcard.com/v4/Token/GetAuthTokens", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

> Example responses

> 200 Response

```json
{
  "Tokens": [
    {
      "Token": "",
      "SecondsUntilExpire": 0,
      "ExpirationTime": ""
    }
  ]
}
```
**Summary:** Return all tokens for the business

**Description:** List all tokens for the business, including the expiration date/time.

**HTTP Request**
`***GET*** /Token/GetAuthTokens` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| Authorization | header | basic {Base64Encoded appId:appSecret} / token {USERTOKEN} | Yes | string |


**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |

## Delete Token

```shell
# You can also use wget
curl -X DELETE https://coreapi.pexcard.com/v4/Token \
  -H 'Authorization: string'

```

```http
DELETE https://coreapi.pexcard.com/v4/Token HTTP/1.1
Host: coreapi.pexcard.com

Authorization: string

```

```javascript
var headers = {
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/Token',
  method: 'delete',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');

const headers = {
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/Token',
{
  method: 'DELETE',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Authorization' => 'string'
}

result = RestClient.delete 'https://coreapi.pexcard.com/v4/Token',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Authorization': 'string'
}

r = requests.delete('https://coreapi.pexcard.com/v4/Token', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/Token");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("DELETE");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("DELETE", "https://coreapi.pexcard.com/v4/Token", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```
**Summary:** Revoke access for the authenticated user

**Description:** To revoke API access, delete the token.<br/>
            <br/>
            The following error responses will result in PEX deleting the token (after the first error):<br/>
             401: Password has changed  (Administrator has changed the password)<br/>
             403: User is not active  (Administrator is terminated/closed)<br/>
             403: Token expired or does not exist .<br/> 
            <br/>  
            If the token will expire in one month or less, use POST /Token/Renew.

**HTTP Request**
`***DELETE*** /Token` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| Authorization | header | token {USERTOKEN} | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |


#Business Management 
##Business Profile
### Update Business Profile 
```shell
# You can also use wget
curl -X POST https://coreapi.pexcard.com/v4/Business/Profile \
  -H 'Content-Type: application/json' \
  -H 'Authorization: string'

```

```http
POST https://coreapi.pexcard.com/v4/Business/Profile HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json

Authorization: string

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/Business/Profile',
  method: 'post',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');
const inputBody = '{
  "ProfileAddress": {
    "AddressLine1": "",
    "AddressLine2": "",
    "City": "",
    "State": "",
    "PostalCode": ""
  },
  "Phone": "",
  "PhoneExtension": "",
  "NormalizeAddress": false
}';
const headers = {
  'Content-Type':'application/json',
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/Business/Profile',
{
  method: 'POST',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.post 'https://coreapi.pexcard.com/v4/Business/Profile',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Authorization': 'string'
}

r = requests.post('https://coreapi.pexcard.com/v4/Business/Profile', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/Business/Profile");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("POST");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Content-Type": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("POST", "https://coreapi.pexcard.com/v4/Business/Profile", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

> Body parameter

```json
{
  "ProfileAddress": {
    "AddressLine1": "",
    "AddressLine2": "",
    "City": "",
    "State": "",
    "PostalCode": ""
  },
  "Phone": "",
  "PhoneExtension": "",
  "NormalizeAddress": false
}
```
**Summary:** Update the PEX business profile

**Description:** Update the PEX business profile with the specified information.<br/>
            <br/>
            All fields are optional for update, however, some profile fields are required in the system and cannot be replaced by null or empty strings. Required system profile fields are:<br/>
            <list type="number">
            <item><description>- First Name<br/></description></item>
            <item><description>- Last Name<br/></description></item>
            <item><description>- Profile Address<br/></description></item>
            <item><description>- Contact Name<br/></description></item>
            <item><description>- Mobile Phone<br/></description></item>
            <item><description>- Country<br/></description></item>
            <item><description>- Date of Birth<br/></description></item>
            <item><description>- Email.<br/></description></item>
            </list> 
            <br/>
            Email format: name@domain.com<br/>
            Date format: MM-DD-YYYY, ex. 01-31-1970<br/>
            Phone format: 2125551212<br/>
            Zip code should be 5 digits: 10018.<br/>
            <br/>
            The API user must have EditBusinessProfile = true.

*HTTP Request* 
`***POST*** /Business/Profile` 


**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| UserRequest | body | Profile data | Yes |  |
| Authorization | header | token {USERTOKEN} | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |




### Retrieve Business Profile 
```shell
# You can also use wget
curl -X GET https://coreapi.pexcard.com/v4/Business/Profile \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
GET https://coreapi.pexcard.com/v4/Business/Profile HTTP/1.1
Host: coreapi.pexcard.com

Accept: application/json
Authorization: string

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/Business/Profile',
  method: 'get',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');

const headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/Business/Profile',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.get 'https://coreapi.pexcard.com/v4/Business/Profile',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.get('https://coreapi.pexcard.com/v4/Business/Profile', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/Business/Profile");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "https://coreapi.pexcard.com/v4/Business/Profile", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```
> Example responses

> 200 Response

```json
{
  "BusinessAcctId": 0,
  "FirstName": "",
  "LastName": "",
  "ProfileAddress": {
    "ContactName": "",
    "AddressLine1": "",
    "AddressLine2": "",
    "City": "",
    "State": "",
    "PostalCode": "",
    "Country": ""
  },
  "Phone": "",
  "PhoneExtension": "",
  "DateOfBirth": "",
  "Email": ""
}
```
**Summary:** Return the PEX business profile information

**Description:** Return the PEX business profile information including address, phone and initial contact information.

*HTTP Request*
`***GET*** /Business/Profile` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| Authorization | header | token {USERTOKEN} | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |


##Business Admin
### Retrieve All Business Admin
```shell
# You can also use wget
curl -X GET https://coreapi.pexcard.com/v4/Business/Admin \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
GET https://coreapi.pexcard.com/v4/Business/Admin HTTP/1.1
Host: coreapi.pexcard.com

Accept: application/json
Authorization: string

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/Business/Admin',
  method: 'get',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');

const headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/Business/Admin',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.get 'https://coreapi.pexcard.com/v4/Business/Admin',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.get('https://coreapi.pexcard.com/v4/Business/Admin', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/Business/Admin");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "https://coreapi.pexcard.com/v4/Business/Admin", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

> Example responses

> 200 Response

```json
{
  "BusinessAdmins": [
    {
      "BusinessAdminId": 0,
      "FirstName": "",
      "MiddleName": "",
      "LastName": "",
      "ProfileAddress": {
        "ContactName": "",
        "AddressLine1": "",
        "AddressLine2": "",
        "City": "",
        "State": "",
        "PostalCode": "",
        "Country": ""
      },
      "Phone": "",
      "AltPhone": "",
      "DateOfBirth": "",
      "Email": "",
      "Permissions": {
        "ViewAdministration": false,
        "AddEditTerminateAdministrator": false,
        "RequestDeleteACHTransfer": false,
        "EditBusinessProfile": false,
        "AddEditTerminateCard": false,
        "RequestCardFunding": false,
        "ViewCardNumberReport": false,
        "ModifyTransactionNotes": false,
        "AdministerInstantIssueCards": false
      },
      "Status": ""
    }
  ]
}
```

**Summary:** List all administrator details for the business

**Description:** Return all active PEX administrator details, including administrator website permissions.  Any deleted or terminated administrators will not be returned.

*HTTP Request*
`***GET*** /Business/Admin` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| Authorization | header | token {USERTOKEN} | Yes | string |


**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Success |
| 403 | <list type="number">    <item>      <description>- Business is not open<br /></description>    </item>    <item>      <description>- Admin does not have permission</description>    </item>  </list> |
| 500 | System error |


### Create Business Admin
```shell
# You can also use wget
curl -X POST https://coreapi.pexcard.com/v4/Business/Admin \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
POST https://coreapi.pexcard.com/v4/Business/Admin HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/Business/Admin',
  method: 'post',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');
const inputBody = '{
  "FirstName": "",
  "MiddleName": "",
  "LastName": "",
  "NormalizeAddress": false,
  "ProfileAddress": {
    "AddressLine1": "",
    "AddressLine2": "",
    "City": "",
    "State": "",
    "PostalCode": ""
  },
  "Phone": "",
  "AltPhone": "",
  "DateOfBirth": "",
  "Email": "",
  "Permissions": {
    "ViewAdministration": false,
    "AddEditTerminateAdministrator": false,
    "RequestDeleteACHTransfer": false,
    "EditBusinessProfile": false,
    "AddEditTerminateCard": false,
    "RequestCardFunding": false,
    "ViewCardNumberReport": false,
    "ModifyTransactionNotes": false,
    "AdministerInstantIssueCards": false
  }
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/Business/Admin',
{
  method: 'POST',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.post 'https://coreapi.pexcard.com/v4/Business/Admin',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.post('https://coreapi.pexcard.com/v4/Business/Admin', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/Business/Admin");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("POST");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Content-Type": []string{"application/json"},
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("POST", "https://coreapi.pexcard.com/v4/Business/Admin", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

> Body parameter

```json
{
  "FirstName": "",
  "MiddleName": "",
  "LastName": "",
  "NormalizeAddress": false,
  "ProfileAddress": {
    "AddressLine1": "",
    "AddressLine2": "",
    "City": "",
    "State": "",
    "PostalCode": ""
  },
  "Phone": "",
  "AltPhone": "",
  "DateOfBirth": "",
  "Email": "",
  "Permissions": {
    "ViewAdministration": false,
    "AddEditTerminateAdministrator": false,
    "RequestDeleteACHTransfer": false,
    "EditBusinessProfile": false,
    "AddEditTerminateCard": false,
    "RequestCardFunding": false,
    "ViewCardNumberReport": false,
    "ModifyTransactionNotes": false,
    "AdministerInstantIssueCards": false
  }
}
```

> Example responses

> 200 Response

```json
{
  "Admin": {
    "BusinessAdminId": 0,
    "FirstName": "",
    "MiddleName": "",
    "LastName": "",
    "ProfileAddress": {
      "ContactName": "",
      "AddressLine1": "",
      "AddressLine2": "",
      "City": "",
      "State": "",
      "PostalCode": "",
      "Country": ""
    },
    "Phone": "",
    "AltPhone": "",
    "DateOfBirth": "",
    "Email": "",
    "Permissions": {
      "ViewAdministration": false,
      "AddEditTerminateAdministrator": false,
      "RequestDeleteACHTransfer": false,
      "EditBusinessProfile": false,
      "AddEditTerminateCard": false,
      "RequestCardFunding": false,
      "ViewCardNumberReport": false,
      "ModifyTransactionNotes": false,
      "AdministerInstantIssueCards": false
    },
    "Status": ""
  }
}
```
**Summary:** Create a new business administrator

**Description:** Create a new PEX administrator. Once created, an email is automatically sent from PEX Card to the new administrator detailing that an account was created and providing the details required for completing the first time login process. If the correct year of birth was not used in creating this administrator, you (the API administrator) must inform the new administrator what year of birth should be used to successfully complete the first time login process.<br/>
            <br/>
            Email format: name@domain.com<br/>
            Date format: MM-DD-YYYY, ex. 01-31-1970<br/>
            Phone format: 2125551212<br/>
            Zip Code should be 5 digits: 10018<br/>
            <br/>
            System email notifications can be set by each administrator in their profile on admin.pexcard.com.<br/>
            <br/>
            In order to perform all API operations, the API administrator user MUST have all of the following:<br/>
            <list type="number">
            <item><description>- AddEditTerminateAdministrator = true<br/></description></item>
            <item><description>- RequestDeleteACHTransfer = true<br/></description></item>
            <item><description>- EditBusinessProfile = true<br/></description></item>
            <item><description>- AddEditTerminateCard = true<br/></description></item>
            <item><description>- RequestCardFunding = true.</description></item>
            </list>

**HTTP Request**
`***POST*** /Business/Admin` 


**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| CreateRequest | body | Profile and permission data | Yes |  |
| Authorization | header | token {USERTOKEN} | Yes | string |


**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |





###Retrieve a Business Admin
```shell
# You can also use wget
curl -X GET https://coreapi.pexcard.com/v4/Business/Admin/{Id} \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
GET https://coreapi.pexcard.com/v4/Business/Admin/{Id} HTTP/1.1
Host: coreapi.pexcard.com

Accept: application/json
Authorization: string

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/Business/Admin/{Id}',
  method: 'get',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');

const headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/Business/Admin/{Id}',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.get 'https://coreapi.pexcard.com/v4/Business/Admin/{Id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.get('https://coreapi.pexcard.com/v4/Business/Admin/{Id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/Business/Admin/{Id}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "https://coreapi.pexcard.com/v4/Business/Admin/{Id}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

> Example responses

> 200 Response

```json
{
  "Admin": {
    "BusinessAdminId": 0,
    "FirstName": "",
    "MiddleName": "",
    "LastName": "",
    "ProfileAddress": {
      "ContactName": "",
      "AddressLine1": "",
      "AddressLine2": "",
      "City": "",
      "State": "",
      "PostalCode": "",
      "Country": ""
    },
    "Phone": "",
    "AltPhone": "",
    "DateOfBirth": "",
    "Email": "",
    "Permissions": {
      "ViewAdministration": false,
      "AddEditTerminateAdministrator": false,
      "RequestDeleteACHTransfer": false,
      "EditBusinessProfile": false,
      "AddEditTerminateCard": false,
      "RequestCardFunding": false,
      "ViewCardNumberReport": false,
      "ModifyTransactionNotes": false,
      "AdministerInstantIssueCards": false
    },
    "Status": ""
  }
}
```
**Summary:** Return administrator profile and permissions

**Description:** Return the profile and permissions for a specific active PEX administrator. A deleted or terminated administrator will not be returned.<br/>
            <br/>
            To obtain the administrator ID, use GET /Business/Admin.

**HTTP Request**
`***GET*** /Business/Admin/{Id}` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| Id | path | Business admin ID | Yes | integer |
| Authorization | header | token {USERTOKEN} | Yes | string |



**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Success |
| 403 | <list type="number">    <item>      <description>- Invalid business admin ID<br /></description>    </item>    <item>      <description>- Business is not open<br /></description>    </item>    <item>      <description>- Admin does not have permission</description>    </item>  </list> |
| 500 | System error |


### Update Business Admin
```shell
# You can also use wget
curl -X PUT https://coreapi.pexcard.com/v4/Business/Admin/{Id} \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
PUT https://coreapi.pexcard.com/v4/Business/Admin/{Id} HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/Business/Admin/{Id}',
  method: 'put',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');
const inputBody = '{
  "FirstName": "",
  "MiddleName": "",
  "LastName": "",
  "NormalizeAddress": false,
  "ProfileAddress": {
    "AddressLine1": "",
    "AddressLine2": "",
    "City": "",
    "State": "",
    "PostalCode": ""
  },
  "Phone": "",
  "AltPhone": "",
  "DateOfBirth": "",
  "Email": "",
  "Permissions": {
    "ViewAdministration": false,
    "AddEditTerminateAdministrator": false,
    "RequestDeleteACHTransfer": false,
    "EditBusinessProfile": false,
    "AddEditTerminateCard": false,
    "RequestCardFunding": false,
    "ViewCardNumberReport": false,
    "ModifyTransactionNotes": false,
    "AdministerInstantIssueCards": false
  }
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/Business/Admin/{Id}',
{
  method: 'PUT',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.put 'https://coreapi.pexcard.com/v4/Business/Admin/{Id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.put('https://coreapi.pexcard.com/v4/Business/Admin/{Id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/Business/Admin/{Id}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("PUT");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Content-Type": []string{"application/json"},
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("PUT", "https://coreapi.pexcard.com/v4/Business/Admin/{Id}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```
> Body parameter

```json
{
  "FirstName": "",
  "MiddleName": "",
  "LastName": "",
  "NormalizeAddress": false,
  "ProfileAddress": {
    "AddressLine1": "",
    "AddressLine2": "",
    "City": "",
    "State": "",
    "PostalCode": ""
  },
  "Phone": "",
  "AltPhone": "",
  "DateOfBirth": "",
  "Email": "",
  "Permissions": {
    "ViewAdministration": false,
    "AddEditTerminateAdministrator": false,
    "RequestDeleteACHTransfer": false,
    "EditBusinessProfile": false,
    "AddEditTerminateCard": false,
    "RequestCardFunding": false,
    "ViewCardNumberReport": false,
    "ModifyTransactionNotes": false,
    "AdministerInstantIssueCards": false
  }
}
```

> Example responses

> 200 Response

```json
{
  "Admin": {
    "BusinessAdminId": 0,
    "FirstName": "",
    "MiddleName": "",
    "LastName": "",
    "ProfileAddress": {
      "ContactName": "",
      "AddressLine1": "",
      "AddressLine2": "",
      "City": "",
      "State": "",
      "PostalCode": "",
      "Country": ""
    },
    "Phone": "",
    "AltPhone": "",
    "DateOfBirth": "",
    "Email": "",
    "Permissions": {
      "ViewAdministration": false,
      "AddEditTerminateAdministrator": false,
      "RequestDeleteACHTransfer": false,
      "EditBusinessProfile": false,
      "AddEditTerminateCard": false,
      "RequestCardFunding": false,
      "ViewCardNumberReport": false,
      "ModifyTransactionNotes": false,
      "AdministerInstantIssueCards": false
    },
    "Status": ""
  }
}
```
**Summary:** Update an existing business administrator

**Description:** Edit an active PEX administrator�s profile address or permissions.<br/>
            <br/>
            Email format: name@domain.com<br/>
            Date format: MM-DD-YYYY, ex. 01-31-1970<br/>
            Phone format: 2125551212<br/>
            Zip code should be 5 digits: 10018<br/>
            <br/>
            To retrieve a list of all active PEX administrators, use GET /Business/Admin.

**HTTP Request**
`***PUT*** /Business/Admin/{Id}` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| EditRequest | body | Profile and permission data | Yes |  |
| Id | path | The business admin id to edit | Yes | integer |
| Authorization | header | token {USERTOKEN} | Yes | string |


**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Success |
| 403 | Invalid business admin ID |


### Delete a Business Admin

```shell
# You can also use wget
curl -X DELETE https://coreapi.pexcard.com/v4/Business/Admin/{Id} \
-H 'Authorization: string'

```

```http
DELETE https://coreapi.pexcard.com/v4/Business/Admin/{Id} HTTP/1.1
Host: coreapi.pexcard.com

Authorization: string

```

```javascript
var headers = {
'Authorization':'string'

};

$.ajax({
url: 'https://coreapi.pexcard.com/v4/Business/Admin/{Id}',
method: 'delete',

headers: headers,
success: function(data) {
console.log(JSON.stringify(data));
}
})

```

```javascript--nodejs
const request = require('node-fetch');

const headers = {
'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/Business/Admin/{Id}',
{
method: 'DELETE',

headers: headers
})
.then(function(res) {
return res.json();
}).then(function(body) {
console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
'Authorization' => 'string'
}

result = RestClient.delete 'https://coreapi.pexcard.com/v4/Business/Admin/{Id}',
params: {
}, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
'Authorization': 'string'
}

r = requests.delete('https://coreapi.pexcard.com/v4/Business/Admin/{Id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/Business/Admin/{Id}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("DELETE");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
"bytes"
"net/http"
)

func main() {

headers := map[string][]string{
"Authorization": []string{"string"},

}

data := bytes.NewBuffer([]byte{jsonReq})
req, err := http.NewRequest("DELETE", "https://coreapi.pexcard.com/v4/Business/Admin/{Id}", data)
req.Header = headers

client := &http.Client{}
resp, err := client.Do(req)
// ...
}

```
**Summary:** Delete a PEX administrator account

**Description:** Delete a PEX administrator account.<br/>
<br/>
Once an administrator account is deleted, it cannot be turned on again. Use POST /Business/Admin to create a new administrator record.<br/>
<br/>
To obtain the administrator ID, use GET /Business/Admin.
<br/>

*HTTP Request*
`***DELETE*** /Business/Admin/{Id}` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| Id | path | Business admin ID | Yes | integer |
| Authorization | header | token {USERTOKEN} | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 403 | Invalid business admin ID |



## Retrieve Business Balance
```shell
# You can also use wget
curl -X GET https://coreapi.pexcard.com/v4/Business/OneTimeTransfer \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
GET https://coreapi.pexcard.com/v4/Business/OneTimeTransfer HTTP/1.1
Host: coreapi.pexcard.com

Accept: application/json
Authorization: string

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/Business/OneTimeTransfer',
  method: 'get',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');

const headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/Business/OneTimeTransfer',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.get 'https://coreapi.pexcard.com/v4/Business/OneTimeTransfer',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.get('https://coreapi.pexcard.com/v4/Business/OneTimeTransfer', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/Business/OneTimeTransfer");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "https://coreapi.pexcard.com/v4/Business/OneTimeTransfer", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

> Example responses

> 200 Response

```json
{
  "OneTimeTransferDetails": [
    {
      "TransferRequestId": 0,
      "BankInformation": {
        "ExternalBankAcctId": 0,
        "RoutingNumber": "",
        "BankAccountNumber": "",
        "BankName": "",
        "BankAccountType": "",
        "IsActive": false
      },
      "Amount": 0,
      "Status": "",
      "RequestedDate": "",
      "FundAvailableDate": ""
    }
  ]
}
```
**Summary:** Return list of PEX initiated ACH transfer requests for the business

**Description:** Return all one-time transfers for the business.<br/>
            <br/>
            One-time transfers are PEX initiated debit or credit ACH requests to/from your external business checking account-on-file to/from your PEXCard business account.<br/>
            <br/>
            One-time transfer Status definitions:<br/>
            <list type="number">
            <item><description>- Request: Not sent to bank yet, can be deleted up to 9:00pm ET on the day the request is made.<br/></description></item>
            <item><description>- Pending: Sent to bank and will take up to four (4) business days to complete.<br/></description></item>
            <item><description>- Complete: Funds were posted to the PEX account.<br/></description></item>
            <item><description>- Rejected: Your bank refused the transaction. Most likely cause? Insufficient funds.<br/></description></item>
            <item><description>- Deleted: Canceled by a PEX administrator.<br/></description></item>
            <item><description>- Canceled: Bank Inactive, canceled by PEX due to external bank account status.<br/></description></item>
            <item><description>- Cancel: Older transfers canceled by a PEX administrator.</description></item>
            </list>

**HTTP Request**
`***GET*** /Business/OneTimeTransfer` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| Authorization | header | token {USERTOKEN} | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |



## One Time Transfer
###Create One Time Transfer
```shell
# You can also use wget
curl -X POST https://coreapi.pexcard.com/v4/Business/OneTimeTransfer \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
POST https://coreapi.pexcard.com/v4/Business/OneTimeTransfer HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/Business/OneTimeTransfer',
  method: 'post',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');
const inputBody = '{
  "ExternalBankAcctId": 0,
  "Amount": 0
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/Business/OneTimeTransfer',
{
  method: 'POST',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.post 'https://coreapi.pexcard.com/v4/Business/OneTimeTransfer',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.post('https://coreapi.pexcard.com/v4/Business/OneTimeTransfer', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/Business/OneTimeTransfer");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("POST");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Content-Type": []string{"application/json"},
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("POST", "https://coreapi.pexcard.com/v4/Business/OneTimeTransfer", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

> Body parameter

```json
{
  "ExternalBankAcctId": 0,
  "Amount": 0
}
```

> Example responses

> 201 Response

```json
{
  "TransferRequestId": 0,
  "BankInformation": {
    "ExternalBankAcctId": 0,
    "RoutingNumber": "",
    "BankAccountNumber": "",
    "BankName": "",
    "BankAccountType": "",
    "IsActive": false
  },
  "Amount": 0
}
```
**Summary:** Create a one-time transfer for the business.

**Description:** Create a one-time transfer for the business.<br/>
            <br/>
            One-time transfers allows the administrator to move funds between your PEX business account and your registered external business checking account-on-file. The minimum amount for each request is $10.00 and the maximum is $100,000.00.<br/>
            <br/>
            To request a transfer, the bank account field �IsActive� should be true and the API user must have permission RequestDeleteACHTransfer = true.<br/>
            <br/>
            To transfer funds from an external bank account to your PEX business account, enter a positive amount. PEX Card will initiate an ACH debit transaction. This transaction is free but takes up to four (4) business days to complete. Once the funds are posted, PEX Card administrators that have the email notification 'PEX Account Funding' checked in their profile will receive an email.<br/>
            <br/>
            To transfer funds from your PEX business account to your external bank account, enter a negative amount. PEX will initiate an ACH credit transaction. PEX Card charges a $5.00 fee to return funds to your external bank account and it takes up to two (2) business days to complete. (Note: you PEX Card business account must have a minimum balance of $50.00 at all times and cannot be reduced to less than $50.00. If you are attempting to close your PEX Card account and retrieve all funds, contact adminsupport@pexcard.com so that we may initiate program closure.)<br/>
            <br/>
            One-time transfer requests are processed at 9pm ET Sunday - Thursday; once successfully processed the transfer status will change from Request to Pending. Pending transfers cannot be deleted.<br/>
            <br/>
            One-time transfer Status definitions:<br/>
            <list type="number">
            <item><description>- Request: Not sent to bank yet, can be deleted up to 9:00pm ET on the day the request is made.<br/></description></item>
            <item><description>- Pending: Sent to bank and will take up to four (4) business days to complete.<br/></description></item>
            <item><description>- Complete: Funds were posted to the PEX account.<br/></description></item>
            <item><description>- Rejected: Your bank refused the transaction. Most likely cause? Insufficient funds.<br/></description></item>
            <item><description>- Deleted: Canceled by a PEX administrator.<br/></description></item>
            <item><description>- Canceled: Bank Inactive, canceled by PEX due to external bank account status.<br/></description></item>
            <item><description>- Cancel: Older transfers canceled by a PEX administrator.<br/></description></item>
            </list>
            <br/>
            To retrieve the valid bank accounts on file for your PEX business account, use GET /Details/AccountDetails.<br/>
            <br/>
            If you do not have an account-on-file, fund your PEX business account by sending a wire or ACH from your external bank. Details required for sending funds to PEX Card can be found on the Transfer page at admin.pexcard.com.<br/>
            <br/>
            To link an external bank account to your PEX business account, log into admin.pexcard.com and click on the Transfers page. The bank account must be a business checking account in the name of your business.

**HTTP Request** 
`***POST*** /Business/OneTimeTransfer` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| TransferRequest | body | Bank Account ID and Amount | Yes |  |
| Authorization | header | token {USERTOKEN} | Yes | string |


**Responses**

| Code | Description |
| ---- | ----------- |
| 201 | Created |
| 403 | <list type="number">    <item>      <description>- External bank account not found<br /></description>    </item>    <item>      <description>- Transfer amount too small<br /></description>    </item>    <item>      <description>- Transfer amount too large<br /></description>    </item>    <item>      <description>- Insufficient funds<br /></description>    </item>    <item>      <description>- Business is not open<br /></description>    </item>    <item>      <description>- Admin does not have permission</description>    </item>  </list> |
| 500 | System error |




### GET One Time Transfer
```shell
# You can also use wget
curl -X GET https://coreapi.pexcard.com/v4/Business/OneTimeTransfer \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
GET https://coreapi.pexcard.com/v4/Business/OneTimeTransfer HTTP/1.1
Host: coreapi.pexcard.com

Accept: application/json
Authorization: string

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/Business/OneTimeTransfer',
  method: 'get',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');

const headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/Business/OneTimeTransfer',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.get 'https://coreapi.pexcard.com/v4/Business/OneTimeTransfer',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.get('https://coreapi.pexcard.com/v4/Business/OneTimeTransfer', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/Business/OneTimeTransfer");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "https://coreapi.pexcard.com/v4/Business/OneTimeTransfer", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

> Example responses

> 200 Response

```json
{
  "OneTimeTransferDetails": [
    {
      "TransferRequestId": 0,
      "BankInformation": {
        "ExternalBankAcctId": 0,
        "RoutingNumber": "",
        "BankAccountNumber": "",
        "BankName": "",
        "BankAccountType": "",
        "IsActive": false
      },
      "Amount": 0,
      "Status": "",
      "RequestedDate": "",
      "FundAvailableDate": ""
    }
  ]
}
```
**Summary:** Return list of PEX initiated ACH transfer requests for the business

**Description:** Return all one-time transfers for the business.<br/>
            <br/>
            One-time transfers are PEX initiated debit or credit ACH requests to/from your external business checking account-on-file to/from your PEXCard business account.<br/>
            <br/>
            One-time transfer Status definitions:<br/>
            <list type="number">
            <item><description>- Request: Not sent to bank yet, can be deleted up to 9:00pm ET on the day the request is made.<br/></description></item>
            <item><description>- Pending: Sent to bank and will take up to four (4) business days to complete.<br/></description></item>
            <item><description>- Complete: Funds were posted to the PEX account.<br/></description></item>
            <item><description>- Rejected: Your bank refused the transaction. Most likely cause? Insufficient funds.<br/></description></item>
            <item><description>- Deleted: Canceled by a PEX administrator.<br/></description></item>
            <item><description>- Canceled: Bank Inactive, canceled by PEX due to external bank account status.<br/></description></item>
            <item><description>- Cancel: Older transfers canceled by a PEX administrator.</description></item>
            </list>

**HTTP Request** 
`***GET*** /Business/OneTimeTransfer` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| Authorization | header | token {USERTOKEN} | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |



### Delete One Time Transfer
```shell 
# You can also use wget 
curl -X DELETE https://coreapi.pexcard.com/v4/Business/OneTimeTransfer/{Id} \ 
-H 'Authorization: string' 

``` 

```http 
DELETE https://coreapi.pexcard.com/v4/Business/OneTimeTransfer/{Id} HTTP/1.1 
Host: coreapi.pexcard.com 

Authorization: string 

``` 

```javascript 
var headers = { 
'Authorization':'string' 

}; 

$.ajax({ 
url: 'https://coreapi.pexcard.com/v4/Business/OneTimeTransfer/{Id}', 
method: 'delete', 

headers: headers, 
success: function(data) { 
console.log(JSON.stringify(data)); 
} 
}) 

``` 

```javascript--nodejs 
const request = require('node-fetch'); 

const headers = { 
'Authorization':'string' 

}; 

fetch('https://coreapi.pexcard.com/v4/Business/OneTimeTransfer/{Id}', 
{ 
method: 'DELETE', 

headers: headers 
}) 
.then(function(res) { 
return res.json(); 
}).then(function(body) { 
console.log(body); 
}); 

``` 

```ruby 
require 'rest-client' 
require 'json' 

headers = { 
'Authorization' => 'string' 
} 

result = RestClient.delete 'https://coreapi.pexcard.com/v4/Business/OneTimeTransfer/{Id}', 
params: { 
}, headers: headers 

p JSON.parse(result) 

``` 

```python 
import requests 
headers = { 
'Authorization': 'string' 
} 

r = requests.delete('https://coreapi.pexcard.com/v4/Business/OneTimeTransfer/{Id}', params={ 

}, headers = headers) 

print r.json() 

``` 

```java 
URL obj = new URL("https://coreapi.pexcard.com/v4/Business/OneTimeTransfer/{Id}"); 
HttpURLConnection con = (HttpURLConnection) obj.openConnection(); 
con.setRequestMethod("DELETE"); 
int responseCode = con.getResponseCode(); 
BufferedReader in = new BufferedReader( 
new InputStreamReader(con.getInputStream())); 
String inputLine; 
StringBuffer response = new StringBuffer(); 
while ((inputLine = in.readLine()) != null) { 
response.append(inputLine); 
} 
in.close(); 
System.out.println(response.toString()); 

``` 

```go 
package main 

import ( 
"bytes" 
"net/http" 
) 

func main() { 

headers := map[string][]string{ 
"Authorization": []string{"string"}, 

} 

data := bytes.NewBuffer([]byte{jsonReq}) 
req, err := http.NewRequest("DELETE", "https://coreapi.pexcard.com/v4/Business/OneTimeTransfer/{Id}", data) 
req.Header = headers 

client := &http.Client{} 
resp, err := client.Do(req) 
// ... 
} 

``` 
**Summary:** Delete an one-time transfer request. 

**Description:** One-time transfer request can only be deleted if it has not been sent to the bank for processing. Transfer requests are processed at 9pm ET Sunday - Thursday. The system will only allow you to delete the transfer if the status = Request.<br/> 
<br/> 
To obtain the TransferRequestId, use GET /Business/OneTimeTransfer.<br/> 
<br/> 
The API user must have RequestDeleteACHTransfer = true. 

*HTTP Request*
`***DELETE*** /Business/OneTimeTransfer/{Id}` 

**Parameters** 

| Name | Located in | Description | Required | Type | 
| ---- | ---------- | ----------- | -------- | ---- | 
| Id | path | TransferRequestId | Yes | integer | 
| Authorization | header | token {USERTOKEN} | Yes | string | 

**Responses** 

| Code | Description | 
| ---- | ----------- | 
| 403 | <list type="number"> <item> <description>- Transfer not found<br /></description> </item> <item> <description>- Transfer not in request status</description> </item> </list> |





##Group
### Create a Group
```shell
# You can also use wget
curl -X POST https://coreapi.pexcard.com/v4/Group \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
POST https://coreapi.pexcard.com/v4/Group HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/Group',
  method: 'post',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');
const inputBody = '{
  "Name": ""
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/Group',
{
  method: 'POST',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.post 'https://coreapi.pexcard.com/v4/Group',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.post('https://coreapi.pexcard.com/v4/Group', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/Group");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("POST");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Content-Type": []string{"application/json"},
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("POST", "https://coreapi.pexcard.com/v4/Group", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

> Body parameter

```json
{
  "Name": ""
}
```

> Example responses

> 200 Response

```json
{
  "Group": {
    "Id": 0,
    "Name": ""
  }
}
```
**Summary:** Create a group

**Description:** Add a group to the business. The administrator website will display fourteen (14) characters of the group name in the cardlist.<br/>
            <br/>
            Group is an administrator defined category that can be used for sorting and reporting. For example, your business has an office in both Boston and New York City, by creating and assigning cards to those Groups, you can sort cards on the admin.pexcard.com website so that the Boston cards are listed together at the top. In transaction reports, you can sort card spending by Group to roll up total spending for each office location.

*HTTP Request*
`***POST*** /Group` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| createRequest | body | Group name | Yes |  |
| Authorization | header | token {USERTOKEN} | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Success |
| 403 | Group has already been added |



### GET Group 
```shell
# You can also use wget
curl -X GET https://coreapi.pexcard.com/v4/Group \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
GET https://coreapi.pexcard.com/v4/Group HTTP/1.1
Host: coreapi.pexcard.com

Accept: application/json
Authorization: string

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/Group',
  method: 'get',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');

const headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/Group',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.get 'https://coreapi.pexcard.com/v4/Group',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.get('https://coreapi.pexcard.com/v4/Group', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/Group");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "https://coreapi.pexcard.com/v4/Group", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

> Example responses

> 200 Response

```json
{
  "Groups": [
    {
      "Id": 0,
      "Name": ""
    }
  ]
}
```
**Summary:** Return a list of groups for the business

**Description:** Retrieve the list of groups for the business, including the Id and group name.<br/>
            <br/>
            Group is an administrator defined category that can be used for sorting and reporting. For example, your business has an office in both Boston and New York City, by creating and assigning cards to those Groups, you can sort cards on the admin.pexcard.com website so that the Boston cards are listed together at the top. In transaction reports, you can sort card spending by Group to roll up total spending for each office location.

*HTTP Request*
`***GET*** /Group` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| Authorization | header | token {USERTOKEN} | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |


### GET Group{ID} 
```shell
# You can also use wget
curl -X GET https://coreapi.pexcard.com/v4/Group/{id} \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
GET https://coreapi.pexcard.com/v4/Group/{id} HTTP/1.1
Host: coreapi.pexcard.com

Accept: application/json
Authorization: string

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/Group/{id}',
  method: 'get',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');

const headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/Group/{id}',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.get 'https://coreapi.pexcard.com/v4/Group/{id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.get('https://coreapi.pexcard.com/v4/Group/{id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/Group/{id}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "https://coreapi.pexcard.com/v4/Group/{id}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

> Example responses

> 200 Response

```json
[
  {
    "FirstName": "",
    "MiddleName": "",
    "LastName": "",
    "AccountId": 0,
    "AccountNumber": "",
    "AvailableBalance": 0,
    "LedgerBalance": 0,
    "SpendRules": false,
    "AccountCreationTime": "",
    "ManualStatus": "",
    "SystemStatus": "",
    "PinSet": false,
    "BSAcctId": 0,
    "IsVirtual": false,
    "Group": {
      "Id": 0,
      "GroupName": ""
    },
    "SpendingRulesetModel": {
      "RulesetId": 0,
      "Name": ""
    },
    "EmbossingDetails": [
      {
        "AccountId": 0,
        "CardNumber": "",
        "ManualStatus": "",
        "SystemStatus": "",
        "CreatedDate": "",
        "PlasticDetails": [
          {
            "PlasticSequence": "",
            "ManualStatus": "",
            "IssuedDate": "",
            "ExpirationDate": ""
          }
        ]
      }
    ],
    "CustomId": ""
  }
]
```
**Summary:** Return all cardholders in a group

**Description:** To retrieve the GroupID, use Get /Group<br/>
            <br/>
            Return all cardholders assigned to a group.<br/>
            <br/>
            Group is an administrator defined category that can be used for sorting and reporting. For example, your business has an office in both Boston and New York City. By creating and assigning cards to those groups, you can sort cards on the admin website so that the Boston cards are listed together at the top. In transaction reports, you can sort card spending by group to roll up total spending for each office location.<br/>

*HTTP Request*
`***GET*** /Group/{id}` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| Id | path |  | Yes | integer |
| Authorization | header | token {USERTOKEN} | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |



### Update Group
```shell
# You can also use wget
curl -X PUT https://coreapi.pexcard.com/v4/Group?id=0 \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
PUT https://coreapi.pexcard.com/v4/Group?id=0 HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/Group',
  method: 'put',
  data: '?id=0',
  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');
const inputBody = '{
  "Name": ""
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/Group?id=0',
{
  method: 'PUT',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.put 'https://coreapi.pexcard.com/v4/Group',
  params: {
  'id' => 'integer(int32)'
}, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.put('https://coreapi.pexcard.com/v4/Group', params={
  'id': '0'
}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/Group?id=0");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("PUT");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Content-Type": []string{"application/json"},
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("PUT", "https://coreapi.pexcard.com/v4/Group", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```
> Body parameter

```json
{
  "Name": ""
}
```

> Example responses

> 200 Response

```json
{
  "Group": {
    "Id": 0,
    "Name": ""
  }
}
```
**Summary:** Update the group name

**Description:** To retrieve the GroupID, use Get /Group<br/>
            <br/>
            Edit the group name. Cardholders assigned to the group will be updated with the new group name. The administrator website will display fourteen (14) characters of the group name in the cardlist.<br/>
            <br/>
            Group is an administrator defined category that can be used for sorting and reporting. For example, your business has an office in both Boston and New York City, by creating and assigning cards to those Groups, you can sort cards on the admin.pexcard.com website so that the Boston cards are listed together at the top. In transaction reports, you can sort card spending by Group to roll up total spending for each office location.

*HTTP Request*
`***PUT*** /Group` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| id | query |  | Yes | integer |
| updateRequest | body | Details required to update group name | Yes |  |
| Authorization | header | token {USERTOKEN} | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Success |
| 403 | <list type="number">    <item>      <description>- Group has already been added<br /></description>    </item>    <item>      <description>- Group ID is invalid</description>    </item>  </list> |


### Update Group{ID}
```shell
# You can also use wget
curl -X PUT https://coreapi.pexcard.com/v4/Group/{id} \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
PUT https://coreapi.pexcard.com/v4/Group/{id} HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/Group/{id}',
  method: 'put',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');
const inputBody = '{
  "Name": ""
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/Group/{id}',
{
  method: 'PUT',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.put 'https://coreapi.pexcard.com/v4/Group/{id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.put('https://coreapi.pexcard.com/v4/Group/{id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/Group/{id}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("PUT");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Content-Type": []string{"application/json"},
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("PUT", "https://coreapi.pexcard.com/v4/Group/{id}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

> Body parameter

```json
{
  "Name": ""
}
```

> Example responses

> 200 Response

```json
{
  "Group": {
    "Id": 0,
    "Name": ""
  }
}
```
**Summary:** Update the group name

**Description:** To retrieve the GroupID, use Get /Group<br/>
            <br/>
            Edit the group name. Cardholders assigned to the group will be updated with the new group name. The administrator website will display fourteen (14) characters of the group name in the cardlist.<br/>
            <br/>
            Group is an administrator defined category that can be used for sorting and reporting. For example, your business has an office in both Boston and New York City, by creating and assigning cards to those Groups, you can sort cards on the admin.pexcard.com website so that the Boston cards are listed together at the top. In transaction reports, you can sort card spending by Group to roll up total spending for each office location.

*HTTP Request*
`***PUT*** /Group/{id}` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| id | path |  | Yes | integer |
| updateRequest | body | Details required to update group name | Yes |  |
| Authorization | header | token {USERTOKEN} | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Success |
| 403 | <list type="number">    <item>      <description>- Group has already been added<br /></description>    </item>    <item>      <description>- Group ID is invalid</description>    </item>  </list> |


### DELETE Group{ID} 
```shell
# You can also use wget
curl -X DELETE https://coreapi.pexcard.com/v4/Group/{id} \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
DELETE https://coreapi.pexcard.com/v4/Group/{id} HTTP/1.1
Host: coreapi.pexcard.com

Accept: application/json
Authorization: string

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/Group/{id}',
  method: 'delete',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');

const headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/Group/{id}',
{
  method: 'DELETE',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.delete 'https://coreapi.pexcard.com/v4/Group/{id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.delete('https://coreapi.pexcard.com/v4/Group/{id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/Group/{id}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("DELETE");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("DELETE", "https://coreapi.pexcard.com/v4/Group/{id}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```
> Example responses

> 200 Response

```json
{
  "GroupId": 0
}
```

**Summary:** Delete a group

**Description:** Delete the group. If cardholders are assigned to a group that is deleted, the cardholders will no longer have a group set.<br/>
            <br/>
            Group is an administrator defined category that can be used for sorting and reporting. For example, your business has an office in both Boston and New York City, by creating and assigning cards to those Groups, you can sort cards on the admin.pexcard.com website so that the Boston cards are listed together at the top. In transaction reports, you can sort card spending by Group to roll up total spending for each office location.

*HTTP Request*
`***DELETE*** /Group/{id}` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| id | path |  | Yes | integer |
| Authorization | header | token {USERTOKEN} | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Success |
| 403 | Group ID is Invalid |


##Spending Ruleset

### Create Spending Ruleset
```shell
# You can also use wget
curl -X POST https://coreapi.pexcard.com/v4/SpendingRuleset \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
POST https://coreapi.pexcard.com/v4/SpendingRuleset HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/SpendingRuleset',
  method: 'post',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');
const inputBody = '{
  "Name": "",
  "DailySpendLimit": 0,
  "SpendingRulesetCategories": {
    "CategoryId": 0,
    "AssociationsOrganizationsAllowed": false,
    "AutomotiveDealersAllowed": false,
    "EducationalServicesAllowed": false,
    "EntertainmentAllowed": false,
    "FuelPumpsAllowed": false,
    "GasStationsConvenienceStoresAllowed": false,
    "GroceryStoresAllowed": false,
    "HealthcareChildcareServicesAllowed": false,
    "ProfessionalServicesAllowed": false,
    "RestaurantsAllowed": false,
    "RetailStoresAllowed": false,
    "TravelTransportationAllowed": false,
    "HardwareStoresAllowed": false
  },
  "InternationalAllowed": false,
  "CardNotPresentAllowed": false,
  "UsePexAccountBalanceForAuths": false,
  "UseCustomerAuthDecision": false
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/SpendingRuleset',
{
  method: 'POST',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.post 'https://coreapi.pexcard.com/v4/SpendingRuleset',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.post('https://coreapi.pexcard.com/v4/SpendingRuleset', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/SpendingRuleset");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("POST");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Content-Type": []string{"application/json"},
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("POST", "https://coreapi.pexcard.com/v4/SpendingRuleset", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

> Body parameter

```json
{
  "Name": "",
  "DailySpendLimit": 0,
  "SpendingRulesetCategories": {
    "CategoryId": 0,
    "AssociationsOrganizationsAllowed": false,
    "AutomotiveDealersAllowed": false,
    "EducationalServicesAllowed": false,
    "EntertainmentAllowed": false,
    "FuelPumpsAllowed": false,
    "GasStationsConvenienceStoresAllowed": false,
    "GroceryStoresAllowed": false,
    "HealthcareChildcareServicesAllowed": false,
    "ProfessionalServicesAllowed": false,
    "RestaurantsAllowed": false,
    "RetailStoresAllowed": false,
    "TravelTransportationAllowed": false,
    "HardwareStoresAllowed": false
  },
  "InternationalAllowed": false,
  "CardNotPresentAllowed": false,
  "UsePexAccountBalanceForAuths": false,
  "UseCustomerAuthDecision": false
}
```

> Example responses

> 200 Response

```json
{
  "RulesetId": 0
}
```

**Summary:** Create spending ruleset for the business

**Description:** What it does:<br/>
            Create a new spending ruleset for the business.<br/>
            Once the ruleset is created, it can be assigned to one or many cards.<br/>
            <br/>
            A spending ruleset is a group of spend rules that can be applied to multiple card accounts. For example, if all cardholders should be allowed to spend at restaurants and fuel pumps, the administrator can create a spending ruleset that has only those merchant categories 'checked'. Every card with that ruleset applied can only spend at restaurants and fuel pumps.<br/>
            <br/>
            At card creation, the spend rule defaults are:<br/>
            <list type="number">
            <item><description>- Daily spend limit NONE<br/></description></item>
            <item><description>- International spending is OFF<br/></description></item>
            <item><description>- All merchant categories are ON<br/></description></item>
            </list>
            <br/>
            If your business allows cardholders to "Use your PEX Account balance" for transactions, you must set a value for "DailySpendLimit" for those cardholders. The "DailySpendLimit" value must be less than or equal to the PEX assigned daily spend limit for your business (typically $5,000 USD).<br/>
            <br/>
            CardNotPresentEnabled: This parameter allows you to control if PEX card can be used for the purchase when it is not present physically at POS (point of sale) E.g. Using PEX card for purchases over Internet or Telephone.<br/>
            True - Can use when card is not present.<br/>
            False - Cannot use when card is not present.<br/>
            <br/>
            PEX has combined Merchant Category Codes (MCC) into larger groupings based upon merchant or service type. Below is the list of those combinations with examples of merchant types for each (this is not an exhaustive merchant listing):<br/>
            <list type="number">
            <item><description>- Associations & organizations: Post Office, local and federal government services, religious organizations<br/></description></item>
            <item><description>- Automotive dealers: Vehicle dealerships (car, RV, motorcycle, boat, recreational)<br/></description></item>
            <item><description>- Educational services: Schools, training programs<br/></description></item>
            <item><description>- Entertainment: Movies, bowling, golf, sports clubs<br/></description></item>
            <item><description>- Fuel &amp; Convenience stores: Service stations (non-pump purchases), miscellaneous food stores, convenience stores and specialty markets<br/></description></item>
            <item><description>- Grocery stores: Food, bakeries, candy<br/></description></item>
            <item><description>- Hardware Stores: Hardware, building supplies, construction materials, paint stores, and industrial equipment.<br/></description></item>
            <item><description>- Healthcare & Childcare services: Medical services, hospitals, daycare<br/></description></item>
            <item><description>- Professional services: Heating, plumbing, HVAC, freight, storage, utilities, fuel oil, coal, dry cleaners<br/></description></item>
            <item><description>- Restaurants: Fast food and sit-down restaurants<br/></description></item>
            <item><description>- Retail stores: Clothing, office supplies, hardware, building supplies, furniture, electronics<br/></description></item>
            <item><description>- Travel & transportation: Airlines, rental cars, trains, tolls, hotels, parking<br/></description></item>
            <item><description>- Fuel Pump Only: Outdoor fuel pumps (i.e. Pay at the Pump)<br/></description></item>
            <item><description>- Hardware Stores: Hardware, building supplies, construction materials, paint stores, and industrial equipment.<br/></description></item>
            </list>

*HTTP Request* 
`***POST*** /SpendingRuleset` 


**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| req | body |  | Yes |  |
| Authorization | header | token {USERTOKEN} | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |


### GET Spending Ruleset 


```shell
# You can also use wget
curl -X GET https://coreapi.pexcard.com/v4/SpendingRuleset \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
GET https://coreapi.pexcard.com/v4/SpendingRuleset HTTP/1.1
Host: coreapi.pexcard.com

Accept: application/json
Authorization: string

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/SpendingRuleset',
  method: 'get',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');

const headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/SpendingRuleset',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.get 'https://coreapi.pexcard.com/v4/SpendingRuleset',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.get('https://coreapi.pexcard.com/v4/SpendingRuleset', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/SpendingRuleset");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "https://coreapi.pexcard.com/v4/SpendingRuleset", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

> Example responses

> 200 Response

```json
{
  "SpendingRulesets": [
    {
      "RulesetId": 0,
      "SpendingRulesetCategories": {
        "CategoryId": 0,
        "AssociationsOrganizationsAllowed": false,
        "AutomotiveDealersAllowed": false,
        "EducationalServicesAllowed": false,
        "EntertainmentAllowed": false,
        "FuelPumpsAllowed": false,
        "GasStationsConvenienceStoresAllowed": false,
        "GroceryStoresAllowed": false,
        "HealthcareChildcareServicesAllowed": false,
        "ProfessionalServicesAllowed": false,
        "RestaurantsAllowed": false,
        "RetailStoresAllowed": false,
        "TravelTransportationAllowed": false,
        "HardwareStoresAllowed": false
      },
      "MccRestrictions": false,
      "BacctId": 0,
      "Name": "",
      "CountCardsPresent": 0,
      "DailySpendLimit": 0,
      "WeeklySpendLimit": 0,
      "MonthlySpendLimit": 0,
      "YearlySpendLimit": 0,
      "LifetimeSpendLimit": 0,
      "InternationalAllowed": false,
      "CardNotPresentAllowed": false,
      "UsePexAccountBalanceForAuths": false,
      "UseCustomerAuthDecision": false
    }
  ]
}
```

**Summary:** Return all spending rulesets for the business

**Description:** What it does:<br/>
            Return details of all spending rulesets for the business. <br/>

*HTTP Request*
`***GET*** /SpendingRuleset` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| Authorization | header | token {USERTOKEN} | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |


### GET Spending Ruleset{ID} 
```shell
# You can also use wget
curl -X GET https://coreapi.pexcard.com/v4/SpendingRuleset/{Id} \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
GET https://coreapi.pexcard.com/v4/SpendingRuleset/{Id} HTTP/1.1
Host: coreapi.pexcard.com

Accept: application/json
Authorization: string

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/SpendingRuleset/{Id}',
  method: 'get',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');

const headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/SpendingRuleset/{Id}',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.get 'https://coreapi.pexcard.com/v4/SpendingRuleset/{Id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.get('https://coreapi.pexcard.com/v4/SpendingRuleset/{Id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/SpendingRuleset/{Id}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "https://coreapi.pexcard.com/v4/SpendingRuleset/{Id}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

> Example responses

> 200 Response

```json
{
  "SpendingRuleset": {
    "RulesetId": 0,
    "Name": "",
    "DailySpendLimit": 0,
    "SpendingRulesetCategories": {
      "CategoryId": 0,
      "AssociationsOrganizationsAllowed": false,
      "AutomotiveDealersAllowed": false,
      "EducationalServicesAllowed": false,
      "EntertainmentAllowed": false,
      "FuelPumpsAllowed": false,
      "GasStationsConvenienceStoresAllowed": false,
      "GroceryStoresAllowed": false,
      "HealthcareChildcareServicesAllowed": false,
      "ProfessionalServicesAllowed": false,
      "RestaurantsAllowed": false,
      "RetailStoresAllowed": false,
      "TravelTransportationAllowed": false,
      "HardwareStoresAllowed": false
    },
    "MccRestrictions": false,
    "InternationalAllowed": false,
    "CardNotPresentAllowed": false,
    "UsePexAccountBalanceForAuths": false,
    "UseCustomerAuthDecision": false
  }
}
```

**Summary:** Return a spending ruleset for the business

**Description:** What it does:<br/>
            Retrieve details of a specific spending ruleset.<br/>

*HTTP Request* 
`***GET*** /SpendingRuleset/{Id}` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| Id | path |  | Yes | integer |
| Authorization | header | token {USERTOKEN} | Yes | string |


**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |




### Update Spending Ruleset
```shell
# You can also use wget
curl -X PUT https://coreapi.pexcard.com/v4/SpendingRuleset \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
PUT https://coreapi.pexcard.com/v4/SpendingRuleset HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/SpendingRuleset',
  method: 'put',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');
const inputBody = '{
  "RulesetId": 0,
  "Name": "",
  "CountCardsPresent": 0,
  "DailySpendLimit": 0,
  "SpendingRulesetCategories": {
    "CategoryId": 0,
    "AssociationsOrganizationsAllowed": false,
    "AutomotiveDealersAllowed": false,
    "EducationalServicesAllowed": false,
    "EntertainmentAllowed": false,
    "FuelPumpsAllowed": false,
    "GasStationsConvenienceStoresAllowed": false,
    "GroceryStoresAllowed": false,
    "HealthcareChildcareServicesAllowed": false,
    "ProfessionalServicesAllowed": false,
    "RestaurantsAllowed": false,
    "RetailStoresAllowed": false,
    "TravelTransportationAllowed": false,
    "HardwareStoresAllowed": false
  },
  "InternationalAllowed": false,
  "CardNotPresentAllowed": false,
  "UsePexAccountBalanceForAuths": false,
  "UseCustomerAuthDecision": false
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/SpendingRuleset',
{
  method: 'PUT',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.put 'https://coreapi.pexcard.com/v4/SpendingRuleset',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.put('https://coreapi.pexcard.com/v4/SpendingRuleset', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/SpendingRuleset");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("PUT");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Content-Type": []string{"application/json"},
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("PUT", "https://coreapi.pexcard.com/v4/SpendingRuleset", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

> Body parameter

```json
{
  "RulesetId": 0,
  "Name": "",
  "CountCardsPresent": 0,
  "DailySpendLimit": 0,
  "SpendingRulesetCategories": {
    "CategoryId": 0,
    "AssociationsOrganizationsAllowed": false,
    "AutomotiveDealersAllowed": false,
    "EducationalServicesAllowed": false,
    "EntertainmentAllowed": false,
    "FuelPumpsAllowed": false,
    "GasStationsConvenienceStoresAllowed": false,
    "GroceryStoresAllowed": false,
    "HealthcareChildcareServicesAllowed": false,
    "ProfessionalServicesAllowed": false,
    "RestaurantsAllowed": false,
    "RetailStoresAllowed": false,
    "TravelTransportationAllowed": false,
    "HardwareStoresAllowed": false
  },
  "InternationalAllowed": false,
  "CardNotPresentAllowed": false,
  "UsePexAccountBalanceForAuths": false,
  "UseCustomerAuthDecision": false
}
```

> Example responses

> 200 Response

```json
{
  "RulesetId": 0
}
```

**Summary:** Update spending ruleset for the business

**Description:** What it does:<br/>
            Modify an existing spending ruleset.<br/>
            <br/>
            When you might use it.<br/>
            <list type="number">
            <item>1. Renaming the spend ruleset.</item><br/>
            <item>2. Resetting the daily spending limit (including the ability to assign no limit).</item><br/>
            <item>3. Allowing or not allowing international use.</item><br/>
            <item>4. Allowing or not allowing card not present use.</item><br/>
            <item>5. Turning merchant categories on or off.</item><br/>
            </list>

*HTTP Request*
`***PUT*** /SpendingRuleset` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| req | body |  | Yes |  |
| Authorization | header | token {USERTOKEN} | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |


### Delete Spending Ruleset 
```shell
# You can also use wget
curl -X DELETE https://coreapi.pexcard.com/v4/SpendingRuleset \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
DELETE https://coreapi.pexcard.com/v4/SpendingRuleset HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/SpendingRuleset',
  method: 'delete',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');
const inputBody = '{
  "RulesetId": 0
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/SpendingRuleset',
{
  method: 'DELETE',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.delete 'https://coreapi.pexcard.com/v4/SpendingRuleset',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.delete('https://coreapi.pexcard.com/v4/SpendingRuleset', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/SpendingRuleset");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("DELETE");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Content-Type": []string{"application/json"},
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("DELETE", "https://coreapi.pexcard.com/v4/SpendingRuleset", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

> Body parameter

```json
{
  "RulesetId": 0
}
```


> Example responses

> 200 Response

```json
{
  "RulesetId": 0
}
```
**Summary:** Delete spending ruleset for the business

**Description:** What it does:<br/>
            Delete an existing spending ruleset for the business.<br/>
            If one or more cards are assigned to a ruleset, that ruleset cannot be deleted.<br/>

*HTTP Request*
`***DELETE*** /SpendingRuleset` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| req | body |  | Yes |  |
| Authorization | header | token {USERTOKEN} | Yes | string |
**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |


### GET All Cards with Spending Ruleset 
```shell
# You can also use wget
curl -X GET https://coreapi.pexcard.com/v4/SpendingRuleset/{Id}/Cards \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
GET https://coreapi.pexcard.com/v4/SpendingRuleset/{Id}/Cards HTTP/1.1
Host: coreapi.pexcard.com

Accept: application/json
Authorization: string

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/SpendingRuleset/{Id}/Cards',
  method: 'get',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');

const headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/SpendingRuleset/{Id}/Cards',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.get 'https://coreapi.pexcard.com/v4/SpendingRuleset/{Id}/Cards',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.get('https://coreapi.pexcard.com/v4/SpendingRuleset/{Id}/Cards', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/SpendingRuleset/{Id}/Cards");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "https://coreapi.pexcard.com/v4/SpendingRuleset/{Id}/Cards", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

> Example responses

> 200 Response

```json
[
  {
    "AccountId": 0,
    "Group": {
      "Id": 0,
      "GroupName": ""
    },
    "AccountStatus": "",
    "LedgerBalance": 0,
    "AvailableBalance": 0,
    "ProfileAddress": {
      "ContactName": "",
      "AddressLine1": "",
      "AddressLine2": "",
      "City": "",
      "State": "",
      "PostalCode": "",
      "Country": ""
    },
    "Phone": "",
    "ShippingAddress": {
      "ContactName": "",
      "AddressLine1": "",
      "AddressLine2": "",
      "City": "",
      "State": "",
      "PostalCode": "",
      "Country": ""
    },
    "ShippingPhone": "",
    "DateOfBirth": "",
    "Email": "",
    "IsVirtual": false,
    "CardList": [
      {
        "CardId": 0,
        "IssuedDate": "",
        "ExpirationDate": "",
        "Last4CardNumber": "",
        "CardStatus": ""
      }
    ],
    "SpendingRulesetId": 0,
    "SpendRules": {
      "UseMerchantCategory": false,
      "MerchantCategories": {
        "AssociationsAndOrganizations": false,
        "AutomotiveDealers": false,
        "EducationalServices": false,
        "Entertainment": false,
        "FuelAndConvenienceStores": false,
        "GroceryStores": false,
        "HealthcareAndChildcareServices": false,
        "ProfessionalServices": false,
        "Restaurants": false,
        "RetailStores": false,
        "TravelAndTransportation": false,
        "FuelPumpOnly": false,
        "HardwareStores": false
      },
      "InternationalSpendEnabled": false,
      "IsDailySpendLimitEnabled": false,
      "DailySpendLimit": 0,
      "CardNotPresentUse": false,
      "UsePexAccountBalanceForAuths": false,
      "UseCustomerAuthDecision": false
    },
    "ScheduledFunding": {
      "Amount": 0,
      "Frequency": 0
    },
    "LowBalanceFunding": {
      "ThresholdAmount": 0,
      "AmountToFund": 0
    },
    "CustomId": ""
  }
]
```
**Summary:** Return all cards with the spending rulesets

**Description:** What it does:<br/>
            Retrieve all cards assigned to a particular spending ruleset.  The response includes all card details. <br/>

*HTTP Request*
`***GET*** /SpendingRuleset/{Id}/Cards` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| Id | path |  | Yes | integer |
| Authorization | header | token {USERTOKEN} | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | No cards found. |



### Create Advanced Spending Ruleset

 
```shell
# You can also use wget
curl -X POST https://coreapi.pexcard.com/v4/SpendingRuleset/Advanced \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
POST https://coreapi.pexcard.com/v4/SpendingRuleset/Advanced HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/SpendingRuleset/Advanced',
  method: 'post',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');
const inputBody = '{
  "Name": "",
  "DailySpendLimit": 0,
  "WeeklySpendLimit": 0,
  "MonthlySpendLimit": 0,
  "YearlySpendLimit": 0,
  "LifetimeSpendLimit": 0,
  "MerchantCategories": [
    {
      "Id": 0,
      "Name": "",
      "TransactionLimit": 0,
      "DailySpendLimit": 0,
      "WeeklySpendLimit": 0,
      "MonthlySpendLimit": 0,
      "YearlySpendLimit": 0,
      "LifetimeSpendLimit": 0
    }
  ],
  "InternationalAllowed": false,
  "CardNotPresentAllowed": false,
  "UsePexAccountBalanceForAuths": false,
  "UseCustomerAuthDecision": false
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/SpendingRuleset/Advanced',
{
  method: 'POST',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.post 'https://coreapi.pexcard.com/v4/SpendingRuleset/Advanced',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.post('https://coreapi.pexcard.com/v4/SpendingRuleset/Advanced', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/SpendingRuleset/Advanced");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("POST");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Content-Type": []string{"application/json"},
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("POST", "https://coreapi.pexcard.com/v4/SpendingRuleset/Advanced", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```
> Body parameter

```json
{
  "Name": "",
  "DailySpendLimit": 0,
  "WeeklySpendLimit": 0,
  "MonthlySpendLimit": 0,
  "YearlySpendLimit": 0,
  "LifetimeSpendLimit": 0,
  "MerchantCategories": [
    {
      "Id": 0,
      "Name": "",
      "TransactionLimit": 0,
      "DailySpendLimit": 0,
      "WeeklySpendLimit": 0,
      "MonthlySpendLimit": 0,
      "YearlySpendLimit": 0,
      "LifetimeSpendLimit": 0
    }
  ],
  "InternationalAllowed": false,
  "CardNotPresentAllowed": false,
  "UsePexAccountBalanceForAuths": false,
  "UseCustomerAuthDecision": false
}
```

> Example responses

> 200 Response

```json
{
  "RulesetId": 0
}
```
**Summary:** Create advanced spending ruleset for the business

**Description:** What it does:<br/>
            Create a new advanced spending ruleset for the business.<br/>
            Once the ruleset is created, it can be assigned to one or many cards.<br/>
            <br/>
            An advanced spending ruleset is a group of spend rules that can be applied to multiple card accounts. For example, if all cardholders should be allowed to spend at restaurants and fuel pumps, the administrator can create a spending ruleset that has only those merchant categories 'checked'. Every card with that ruleset applied can only spend at restaurants and fuel pumps.<br/>
            <br/>
            At card creation, the spend rule defaults are:<br/>
            <list type="number">
            <item><description>- Daily spend limit NONE<br/></description></item>
            <item><description>- Weeklyly spend limit NONE<br/></description></item>
            <item><description>- Monthly spend limit NONE<br/></description></item>
            <item><description>- Yearly spend limit NONE<br/></description></item>
            <item><description>- Lifetime spend limit NONE<br/></description></item>
            <item><description>- International spending is OFF<br/></description></item>
            <item><description>- All merchant categories are ON<br/></description></item>
            </list>
            <br/>
            If your business allows cardholders to "Use your PEX Account balance" for transactions, you must set a value for "DailySpendLimit" for those cardholders. The "DailySpendLimit" value must be less than or equal to the PEX assigned daily spend limit for your business (typically $5,000 USD).<br/>
            <br/>
            CardNotPresentEnabled: This parameter allows you to control if PEX card can be used for the purchase when it is not present physically at POS (point of sale) E.g. Using PEX card for purchases over Internet or Telephone.<br/>
            True - Can use when card is not present.<br/>
            False - Cannot use when card is not present.<br/>
            <br/>
            PEX has combined Merchant Category Codes (MCC) into larger groupings based upon merchant or service type. Below is the list of those combinations with examples of merchant types for each (this is not an exhaustive merchant listing):<br/>
            <list type="number">
            <item><description>- Associations & organizations: Post Office, local and federal government services, religious organizations<br/></description></item>
            <item><description>- Automotive dealers: Vehicle dealerships (car, RV, motorcycle, boat, recreational)<br/></description></item>
            <item><description>- Educational services: Schools, training programs<br/></description></item>
            <item><description>- Entertainment: Movies, bowling, golf, sports clubs<br/></description></item>
            <item><description>- Fuel &amp; Convenience stores: Service stations (non-pump purchases), miscellaneous food stores, convenience stores and specialty markets.<br/></description></item>
            <item><description>- Grocery stores: Food, bakeries, candy<br/></description></item>
            <item><description>- Hardware Stores: Hardware, building supplies, construction materials, paint stores, and industrial equipment.<br/></description></item>
            <item><description>- Healthcare & Childcare services: Medical services, hospitals, daycare<br/></description></item>
            <item><description>- Professional services: Heating, plumbing, HVAC, freight, storage, utilities, fuel oil, coal, dry cleaners<br/></description></item>
            <item><description>- Restaurants: Fast food and sit-down restaurants<br/></description></item>
            <item><description>- Retail stores: Clothing, office supplies, hardware, building supplies, furniture, electronics<br/></description></item>
            <item><description>- Travel & transportation: Airlines, rental cars, trains, tolls, hotels, parking<br/></description></item>
            <item><description>- Fuel Pump Only: Outdoor fuel pumps (i.e. Pay at the Pump)<br/></description></item>
            <item><description>- Hardware Stores: Hardware, building supplies, construction materials, paint stores, and industrial equipment.<br/></description></item>
            </list>

*HTTP Request*
`***POST*** /SpendingRuleset/Advanced` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| req | body |  | Yes |  |
| Authorization | header | token {USERTOKEN} | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |
| 400 | <list type='number'><item><description>- Invalid merchant category<br/></description></item><item><description>- Merchant categories duplicated<br/></description></item><item><description>- Merchant spend limit exceeds overall spend limit<br/></description></item></list> |
| 403 | <list type='number'><item><description>- Name already exists<br/></description></item><item><description>- This business does not support the Customer Authorization Decision<br/></description></item><item><description>- This business does not support the PEX Account balance instead of card balance<br/></description></item></list> |
| 500 | InternalServerError |



### GET Advanced Spending Ruleset 
```shell
# You can also use wget
curl -X GET https://coreapi.pexcard.com/v4/SpendingRuleset/Advanced \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
GET https://coreapi.pexcard.com/v4/SpendingRuleset/Advanced HTTP/1.1
Host: coreapi.pexcard.com

Accept: application/json
Authorization: string

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/SpendingRuleset/Advanced',
  method: 'get',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');

const headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/SpendingRuleset/Advanced',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.get 'https://coreapi.pexcard.com/v4/SpendingRuleset/Advanced',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.get('https://coreapi.pexcard.com/v4/SpendingRuleset/Advanced', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/SpendingRuleset/Advanced");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "https://coreapi.pexcard.com/v4/SpendingRuleset/Advanced", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

> Example responses

> 200 Response

```json
[
  {
    "Id": 0,
    "Name": "",
    "CardCount": 0,
    "DailySpendLimit": 0,
    "WeeklySpendLimit": 0,
    "MonthlySpendLimit": 0,
    "YearlySpendLimit": 0,
    "LifetimeSpendLimit": 0,
    "InternationalAllowed": false,
    "CardNotPresentAllowed": false,
    "UsePexAccountBalanceForAuths": false,
    "UseCustomerAuthDecision": false,
    "MccRestrictions": false,
    "MerchantCategories": [
      {
        "Id": 0,
        "Name": "",
        "Description": "",
        "TransactionLimit": 0,
        "DailySpendLimit": 0,
        "WeeklySpendLimit": 0,
        "MonthlySpendLimit": 0,
        "YearlySpendLimit": 0,
        "LifetimeSpendLimit": 0
      }
    ]
  }
]
```
**Summary:** Return all advanced spending rulesets for the business

**Description:** What it does:<br/>
            Return details of all advanced spending rulesets for the business. <br/>

*HTTP Request*
`***GET*** /SpendingRuleset/Advanced` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| Authorization | header | token {USERTOKEN} | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |
| 404 | NotFound |
| 500 | InternalServerError |



### Update Advance Spending Ruleset 
```shell
# You can also use wget
curl -X PUT https://coreapi.pexcard.com/v4/SpendingRuleset/Advanced \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
PUT https://coreapi.pexcard.com/v4/SpendingRuleset/Advanced HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/SpendingRuleset/Advanced',
  method: 'put',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');
const inputBody = '{
  "Id": 0,
  "Name": "",
  "DailySpendLimit": 0,
  "WeeklySpendLimit": 0,
  "MonthlySpendLimit": 0,
  "YearlySpendLimit": 0,
  "LifetimeSpendLimit": 0,
  "MerchantCategories": [
    {
      "Id": 0,
      "Name": "",
      "TransactionLimit": 0,
      "DailySpendLimit": 0,
      "WeeklySpendLimit": 0,
      "MonthlySpendLimit": 0,
      "YearlySpendLimit": 0,
      "LifetimeSpendLimit": 0
    }
  ],
  "InternationalAllowed": false,
  "CardNotPresentAllowed": false,
  "UsePexAccountBalanceForAuths": false,
  "UseCustomerAuthDecision": false
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/SpendingRuleset/Advanced',
{
  method: 'PUT',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.put 'https://coreapi.pexcard.com/v4/SpendingRuleset/Advanced',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.put('https://coreapi.pexcard.com/v4/SpendingRuleset/Advanced', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/SpendingRuleset/Advanced");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("PUT");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Content-Type": []string{"application/json"},
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("PUT", "https://coreapi.pexcard.com/v4/SpendingRuleset/Advanced", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

> Body parameter

```json
{
  "Id": 0,
  "Name": "",
  "DailySpendLimit": 0,
  "WeeklySpendLimit": 0,
  "MonthlySpendLimit": 0,
  "YearlySpendLimit": 0,
  "LifetimeSpendLimit": 0,
  "MerchantCategories": [
    {
      "Id": 0,
      "Name": "",
      "TransactionLimit": 0,
      "DailySpendLimit": 0,
      "WeeklySpendLimit": 0,
      "MonthlySpendLimit": 0,
      "YearlySpendLimit": 0,
      "LifetimeSpendLimit": 0
    }
  ],
  "InternationalAllowed": false,
  "CardNotPresentAllowed": false,
  "UsePexAccountBalanceForAuths": false,
  "UseCustomerAuthDecision": false
}
```

> Example responses

> 200 Response

```json
{
  "Id": 0,
  "Name": "",
  "CardCount": 0,
  "DailySpendLimit": 0,
  "WeeklySpendLimit": 0,
  "MonthlySpendLimit": 0,
  "YearlySpendLimit": 0,
  "LifetimeSpendLimit": 0,
  "InternationalAllowed": false,
  "CardNotPresentAllowed": false,
  "UsePexAccountBalanceForAuths": false,
  "UseCustomerAuthDecision": false,
  "MccRestrictions": false,
  "MerchantCategories": [
    {
      "Id": 0,
      "Name": "",
      "Description": "",
      "TransactionLimit": 0,
      "DailySpendLimit": 0,
      "WeeklySpendLimit": 0,
      "MonthlySpendLimit": 0,
      "YearlySpendLimit": 0,
      "LifetimeSpendLimit": 0
    }
  ]
}
```
**Summary:** Update advanced spending ruleset for the business

**Description:** What it does:<br/>
            Modify an existing advanced spending ruleset.<br/>
            <br/>
            When you might use it.<br/>
            <list type="number">
            <item>1. Renaming the advanced spend ruleset.</item><br/>
            <item>2. Resetting the daily spending limit (including the ability to assign no limit).</item><br/>
            <item>3. Allowing or not allowing international use.</item><br/>
            <item>4. Allowing or not allowing card not present use.</item><br/>
            <item>5. Turning merchant categories on or off.</item><br/>
            </list>

*HTTP Request* 
`***PUT*** /SpendingRuleset/Advanced` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| req | body |  | Yes |  |
| Authorization | header | token {USERTOKEN} | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |
| 400 | <list type='number'><item><description>- Invalid merchant category<br/></description></item><item><description>- Invalid ruleset ID<br/></description></item><item><description>- Merchant categories duplicated<br/></description></item><item><description>- Merchant spend limit exceeds overall spend limit<br/></description></item></list> |
| 403 | <list type='number'><item><description>- Name already exists<br/></description></item><item><description>- This business does not support the Customer Authorization Decision<br/></description></item><item><description>- This business does not support the PEX Account balance instead of card balance<br/></description></item></list> |
| 500 | InternalServerError |


### Delete Advance Spending Ruleset 
```shell
# You can also use wget
curl -X DELETE https://coreapi.pexcard.com/v4/SpendingRuleset/Advanced \
  -H 'Content-Type: application/json' \
  -H 'Authorization: string'

```

```http
DELETE https://coreapi.pexcard.com/v4/SpendingRuleset/Advanced HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json

Authorization: string

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/SpendingRuleset/Advanced',
  method: 'delete',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');
const inputBody = '{
  "Id": 0
}';
const headers = {
  'Content-Type':'application/json',
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/SpendingRuleset/Advanced',
{
  method: 'DELETE',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.delete 'https://coreapi.pexcard.com/v4/SpendingRuleset/Advanced',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Authorization': 'string'
}

r = requests.delete('https://coreapi.pexcard.com/v4/SpendingRuleset/Advanced', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/SpendingRuleset/Advanced");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("DELETE");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Content-Type": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("DELETE", "https://coreapi.pexcard.com/v4/SpendingRuleset/Advanced", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

> Body parameter

```json
{
  "Id": 0
}
```
**Summary:** Delete advanced spending ruleset for the business

**Description:** What it does:<br/>
            Delete an existing advanced spending ruleset for the business.<br/>
            If one or more cards are assigned to a ruleset, that ruleset cannot be deleted.<br/>

*HTTP Request* 
`***DELETE*** /SpendingRuleset/Advanced` 


**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| req | body |  | Yes |  |
| Authorization | header | token {USERTOKEN} | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |
| 400 | Invalid ruleset ID |
| 403 | This spending ruleset is currently assigned to one or more cards. |
| 500 | InternalServerError |



### GET Advance Spending Ruleset{ID} 
```shell
# You can also use wget
curl -X GET https://coreapi.pexcard.com/v4/SpendingRuleset/{Id}/Advanced \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
GET https://coreapi.pexcard.com/v4/SpendingRuleset/{Id}/Advanced HTTP/1.1
Host: coreapi.pexcard.com

Accept: application/json
Authorization: string

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/SpendingRuleset/{Id}/Advanced',
  method: 'get',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');

const headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/SpendingRuleset/{Id}/Advanced',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.get 'https://coreapi.pexcard.com/v4/SpendingRuleset/{Id}/Advanced',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.get('https://coreapi.pexcard.com/v4/SpendingRuleset/{Id}/Advanced', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/SpendingRuleset/{Id}/Advanced");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "https://coreapi.pexcard.com/v4/SpendingRuleset/{Id}/Advanced", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

> Example responses

> 200 Response

```json
{
  "Id": 0,
  "Name": "",
  "CardCount": 0,
  "DailySpendLimit": 0,
  "WeeklySpendLimit": 0,
  "MonthlySpendLimit": 0,
  "YearlySpendLimit": 0,
  "LifetimeSpendLimit": 0,
  "InternationalAllowed": false,
  "CardNotPresentAllowed": false,
  "UsePexAccountBalanceForAuths": false,
  "UseCustomerAuthDecision": false,
  "MccRestrictions": false,
  "MerchantCategories": [
    {
      "Id": 0,
      "Name": "",
      "Description": "",
      "TransactionLimit": 0,
      "DailySpendLimit": 0,
      "WeeklySpendLimit": 0,
      "MonthlySpendLimit": 0,
      "YearlySpendLimit": 0,
      "LifetimeSpendLimit": 0
    }
  ]
}
```
**Summary:** Return an advanced spending ruleset for the business

**Description:** What it does:<br/>
            Retrieve details of a specific advanced spending ruleset.<br/>

*HTTP Request* 
`***GET*** /SpendingRuleset/{Id}/Advanced` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| Id | path |  | Yes | integer |
| Authorization | header | token {USERTOKEN} | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |
| 400 | Invalid ruleset ID |
| 404 | NotFound |
| 500 | InternalServerError |


### GET Cards With Advance Spending Ruleset
```shell
# You can also use wget
curl -X GET https://coreapi.pexcard.com/v4/SpendingRuleset/{Id}/Advanced/Cards \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
GET https://coreapi.pexcard.com/v4/SpendingRuleset/{Id}/Advanced/Cards HTTP/1.1
Host: coreapi.pexcard.com

Accept: application/json
Authorization: string

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/SpendingRuleset/{Id}/Advanced/Cards',
  method: 'get',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');

const headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/SpendingRuleset/{Id}/Advanced/Cards',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.get 'https://coreapi.pexcard.com/v4/SpendingRuleset/{Id}/Advanced/Cards',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.get('https://coreapi.pexcard.com/v4/SpendingRuleset/{Id}/Advanced/Cards', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/SpendingRuleset/{Id}/Advanced/Cards");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "https://coreapi.pexcard.com/v4/SpendingRuleset/{Id}/Advanced/Cards", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

> Example responses

> 200 Response

```json
[
  {
    "AccountId": 0,
    "Group": {
      "Id": 0,
      "GroupName": ""
    },
    "AccountStatus": "",
    "LedgerBalance": 0,
    "AvailableBalance": 0,
    "ProfileAddress": {
      "ContactName": "",
      "AddressLine1": "",
      "AddressLine2": "",
      "City": "",
      "State": "",
      "PostalCode": "",
      "Country": ""
    },
    "Phone": "",
    "ShippingAddress": {
      "ContactName": "",
      "AddressLine1": "",
      "AddressLine2": "",
      "City": "",
      "State": "",
      "PostalCode": "",
      "Country": ""
    },
    "ShippingPhone": "",
    "DateOfBirth": "",
    "Email": "",
    "CardList": [
      {
        "CardId": 0,
        "IssuedDate": "",
        "ExpirationDate": "",
        "Last4CardNumber": "",
        "CardStatus": ""
      }
    ],
    "SpendingRulesetId": 0,
    "SpendRules": {
      "MerchantCategories": [
        {
          "Id": 0,
          "Name": "",
          "Description": "",
          "TransactionLimit": 0,
          "DailySpendLimit": 0,
          "WeeklySpendLimit": 0,
          "MonthlySpendLimit": 0,
          "YearlySpendLimit": 0,
          "LifetimeSpendLimit": 0
        }
      ],
      "InternationalSpendEnabled": false,
      "IsDailySpendLimitEnabled": false,
      "DailySpendLimit": 0,
      "WeeklySpendLimit": 0,
      "MonthlySpendLimit": 0,
      "YearlySpendLimit": 0,
      "LifetimeSpendLimit": 0,
      "CardNotPresentUse": false,
      "UsePexAccountBalanceForAuths": false,
      "UseCustomerAuthDecision": false
    },
    "ScheduledFunding": {
      "Amount": 0,
      "Frequency": 0
    },
    "LowBalanceFunding": {
      "ThresholdAmount": 0,
      "AmountToFund": 0
    },
    "CustomId": "",
    "IsVirtual": false
  }
]
```
**Summary:** Return all cards with the advanced spending rulesets

**Description:** What it does:<br/>
            Retrieve all cards assigned to a particular spending ruleset.  The response includes all card details. <br/>

*HTTP Request*
`***GET*** /SpendingRuleset/{Id}/Advanced/Cards` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| Id | path |  | Yes | integer |
| Authorization | header | token {USERTOKEN} | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | No cards found. |


#Card Management
##Create Card 

```shell
# You can also use wget
curl -X POST https://coreapi.pexcard.com/v4/Card/CreateAsync \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
POST https://coreapi.pexcard.com/v4/Card/CreateAsync HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/Card/CreateAsync',
  method: 'post',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');
const inputBody = '{
  "Cards": [
    {
      "Phone": "",
      "ShippingPhone": "",
      "ShippingMethod": 0,
      "DateOfBirth": "",
      "Email": "",
      "GroupId": 0,
      "RulesetId": 0,
      "CustomId": "",
      "FirstName": "",
      "LastName": "",
      "NormalizeProfileAddress": false,
      "ProfileAddress": {
        "AddressLine1": "",
        "AddressLine2": "",
        "City": "",
        "State": "",
        "PostalCode": ""
      },
      "NormalizeShippingAddress": false,
      "ShippingAddress": {
        "ContactName": "",
        "AddressLine1": "",
        "AddressLine2": "",
        "City": "",
        "State": "",
        "PostalCode": ""
      }
    }
  ],
  "NormalizeHomeAddress": false,
  "NormalizeShippingAddress": false
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/Card/CreateAsync',
{
  method: 'POST',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.post 'https://coreapi.pexcard.com/v4/Card/CreateAsync',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.post('https://coreapi.pexcard.com/v4/Card/CreateAsync', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/Card/CreateAsync");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("POST");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Content-Type": []string{"application/json"},
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("POST", "https://coreapi.pexcard.com/v4/Card/CreateAsync", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

> Body parameter

```json
{
  "Cards": [
    {
      "Phone": "",
      "ShippingPhone": "",
      "ShippingMethod": 0,
      "DateOfBirth": "",
      "Email": "",
      "GroupId": 0,
      "RulesetId": 0,
      "CustomId": "",
      "FirstName": "",
      "LastName": "",
      "NormalizeProfileAddress": false,
      "ProfileAddress": {
        "AddressLine1": "",
        "AddressLine2": "",
        "City": "",
        "State": "",
        "PostalCode": ""
      },
      "NormalizeShippingAddress": false,
      "ShippingAddress": {
        "ContactName": "",
        "AddressLine1": "",
        "AddressLine2": "",
        "City": "",
        "State": "",
        "PostalCode": ""
      }
    }
  ],
  "NormalizeHomeAddress": false,
  "NormalizeShippingAddress": false
}
```

> Example responses

> 201 Response

```json
{
  "CardOrderId": 0
}
```

**Summary:** Create cards for the business

**Description:** Create cards for the business. The response to this call is a CardOrderId.<br/>
            <br/>
            To retrieve card details, including the card AccountId, use GET /Card/CardOrder/{Id}<br/>
            <br/>
            Cards have an expiration date of 3 years and will renew automatically 60 days prior to expiration. If the card expiration is 01/17, the card will expire on the last day of the month, January 31, 2017.<br/>
            <br/>
            ShippingMethod is a required field and maps to the same choices available on the admin website:<br/>
            <list type="number">
            <item><description>ShippingMethod = 0  i.e 'FirstClassMail' (10-15 business days) Free<br/></description></item>
            <item><description>ShippingMethod = 1  i.e 'Expedited' (up to 4 business days) $35<br/></description></item>
            <item><description>ShippingMethod = 2  i.e 'Rush' (up to 3 business days) $45.<br/></description></item>
            </list>
            <br/>
            non-ASCII characters. Ex: " " not allowed<br/>
            Cardholder name may only include letters, numbers and the following punctuation symbols: , . - & '<br/>
            Cardholder first + last names must be no more than 23 characters<br/>
            Email format: name@domain.com<br/>
            Date format: MM-DD-YYYY, ex. 01-31-1970<br/>
            Phone format: 2125551212 or 212-555-1212<br/>
            Zip Code should be 5 digits: 10018.<br/>
            Address format: letters, numbers and the following punctuation symbols: . ' () , # - /<br/>
            City format: letters, numbers and the following punctuation symbols: . ' () , # - /<br/>
            State format:  two letter format ex. "CA" <br/>
            Max AddressLine1 field length: 26 characters<br/>
            Max AddressLine2 field length: 26 characters<br/>
            Max City field length: 25 characters<br/>
            CustomId: User defined Id which can be assigned to Card holder profile (alphanumeric up to 50 characters). This is optional field. <br/>
            <br/>
            Shipping address is used for card mailing. PEX uses this address for all future card replacements including: lost, stolen, compromised and renewal.<br/> 
            Valid Shipping address need to be populated as part of request while creating new cards.<br/>
            <br/> 
            If PEX card is used for fuel authorizations, transit passes or online purchases, there will be times where the cardholder will have to key in the billing zip code as it appears on the cardholder profile. To avoid issues at the time of purchase, let the cardholder know what their billing (i.e. profile) address is.<br/>
            <br/>
            If the cardholder enters an invalid Zip Code 2 times, the merchant may refuse to accept additional card swipes. If this occurs, cardholders will have to see the attendant to complete a gas transaction, or use another form of payment.<br/> 
            <br/>
            If the cardholder should have access to ch.pexcard.com to review their transaction history, etc., they will need the four (4) digit year of birth from their profile. If you are using a generic value, you will need to convey that to the cardholder.<br/>
            <br/>
            At card creation, the spend rule defaults are:<br/>
            <list type="number">
            <item><description>- Daily spend limit is NONE<br/></description></item>
            <item><description>- International spending is OFF<br/></description></item>
            <item><description>- Card-not-present spending is ON<br/></description></item>
            <item><description>- All merchant categories are ON.<br/></description></item>
            </list>
            <br/>
            To add a card account to a group, use GET /Group to retrieve GroupIds <br/>
            To add spend rules to a card account, use GET /SpendingRuleset to retrieve all the Spend rule sets for your business. <br/>

*HTTP Request* 
`***POST*** /Card/CreateAsync` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| UserRequest | body | Profile and shipping data | Yes |  |
| Authorization | header | token {USERTOKEN} | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 201 | Created |
| 400 | Invalid shipping method |
| 403 | Admin does not have permission |


## Card Order
### GET Card Order  
```shell
# You can also use wget
curl -X GET https://coreapi.pexcard.com/v4/Card/CardOrder \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
GET https://coreapi.pexcard.com/v4/Card/CardOrder HTTP/1.1
Host: coreapi.pexcard.com

Accept: application/json
Authorization: string

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/Card/CardOrder',
  method: 'get',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');

const headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/Card/CardOrder',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.get 'https://coreapi.pexcard.com/v4/Card/CardOrder',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.get('https://coreapi.pexcard.com/v4/Card/CardOrder', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/Card/CardOrder");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "https://coreapi.pexcard.com/v4/Card/CardOrder", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

> Example responses

> 200 Response

```json
{
  "CardOrders": [
    {
      "CardOrderId": 0,
      "OrderDateTime": "",
      "UserName": "",
      "BusinessAdminId": 0,
      "BusinessAccountId": 0,
      "NumberOfCards": 0
    }
  ]
}
```
**Summary:** Get general informati2on about card orders

**Description:** This endpoint returns all the card order Ids those were created in the duration specified by Start date and End date. <br/>
            With the CardOrderId from response you can use GET/Card/CardOrder/{Id} to get more information about the cards created within that CardOrder. <br/>
            Please make sure time frame selected between StartDate and EndDate is no more than last 12 months.<br/>
            <br/>
            CardOrderId: Order ID returned as a response to POST/Card/CreateAsync, when you submit card creation request. <br/>
            OrderDateTime: Date time when the card order was placed. <br/>
            UserName: Username of the user who placed the order <br/>
            BusinessAdminId: Unique identifier for the business admin who placed the card order. More information about admin can be obtained by 2/{Id}. It can have null value in some cases. <br/>
            BusinessAccountId: Account Id to which card order belongs to. <br/>
            NumberofCards: Total count of number of cards successfully created in the card order. <br/>

*HTTP Request* 
`***GET*** /Card/CardOrder` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| StartDate | query | Start date (format - YYYY-MM-DDThh:mm:ss) | No | dateTime |
| EndDate | query | End date (format - YYYY-MM-DDThh:mm:ss) | No | dateTime |
| Authorization | header | token {USERTOKEN} | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |


### GET Card Order{ID}
```shell
# You can also use wget
curl -X GET https://coreapi.pexcard.com/v4/Card/CardOrder/{Id} \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
GET https://coreapi.pexcard.com/v4/Card/CardOrder/{Id} HTTP/1.1
Host: coreapi.pexcard.com

Accept: application/json
Authorization: string

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/Card/CardOrder/{Id}',
  method: 'get',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');

const headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/Card/CardOrder/{Id}',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.get 'https://coreapi.pexcard.com/v4/Card/CardOrder/{Id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.get('https://coreapi.pexcard.com/v4/Card/CardOrder/{Id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/Card/CardOrder/{Id}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "https://coreapi.pexcard.com/v4/Card/CardOrder/{Id}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```
> Example responses

> 200 Response

```json
{
  "CardOrderId": 0,
  "OrderDateTime": "",
  "UserName": "",
  "BusinessAccountId": 0,
  "Cards": [
    {
      "AcctId": 0,
      "Status": "",
      "FirstName": "",
      "MiddleName": "",
      "LastName": "",
      "DateOfBirth": "",
      "HomePhone": "",
      "MobilePhone": "",
      "Email": "",
      "HomeAddress": {
        "AddressLine1": "",
        "AddressLine2": "",
        "City": "",
        "State": "",
        "PostalCode": "",
        "Country": ""
      },
      "ShippingAddress": {
        "AddressLine1": "",
        "AddressLine2": "",
        "City": "",
        "State": "",
        "PostalCode": "",
        "Country": ""
      },
      "Recipient": "",
      "ShipToShippingAddress": false,
      "ShippingContactNumber": "",
      "BundleCards": false,
      "ShippingMethod": "",
      "ShippingDate": "",
      "Errors": [
        {
          "Code": "",
          "Message": ""
        }
      ],
      "FailReason": "",
      "AccountNumber": "",
      "SpendingRulesetId": 0,
      "GroupId": 0,
      "CustomId": ""
    }
  ]
}
```
**Summary:** Return all cards for a CardOrderId

**Description:** After using POST /Card/CreateAsync to create one or more cards, you can retrieve the card information, including the card AccountId, by using this call.

*HTTP Request*
`***GET*** /Card/CardOrder/{Id}` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| Id | path | Card order ID | Yes | integer |
| Authorization | header | token {USERTOKEN} | Yes | string |


**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Success |
| 403 | Order belongs to another business |


##Activate Card 

```shell
# You can also use wget
curl -X POST https://coreapi.pexcard.com/v4/Card/Activate/{Id} \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
POST https://coreapi.pexcard.com/v4/Card/Activate/{Id} HTTP/1.1
Host: coreapi.pexcard.com

Accept: application/json
Authorization: string

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/Card/Activate/{Id}',
  method: 'post',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');

const headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/Card/Activate/{Id}',
{
  method: 'POST',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.post 'https://coreapi.pexcard.com/v4/Card/Activate/{Id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.post('https://coreapi.pexcard.com/v4/Card/Activate/{Id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/Card/Activate/{Id}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("POST");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("POST", "https://coreapi.pexcard.com/v4/Card/Activate/{Id}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

> Example responses

> 200 Response

```json
{}
```
**Summary:** Activate a card

**Description:** Activate a card using the card accountID.<br/>
            <br/>
            A card must be activated before the cardholder can spend. For security reasons, you should not activate a card until it is received by the cardholder.<br/>
            <br/>
            The PEX system will prevent you from activating a card within 24 hours of creation.<br/>
            <br/>
            If the card is a replacement for an existing, damaged or expiring card, make sure the cardholder has the new card prior to activating it. Card activation immediately terminates all other cards on the account, including the one the cardholder is currently using. The card termination process is immediate and NOT reversible.

**HTTP Request**
`***POST*** /Card/Activate/{Id}` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| Id | path | Card account ID | Yes | integer |
| Authorization | header | token {USERTOKEN} | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Success |
| 403 | <list type="number">    <item>      <description>- Invalid card account ID<br /></description>    </item>    <item>      <description>- Cannot change status</description>    </item>  </list> |

##Create PIN 

```shell
# You can also use wget
curl -X PUT https://coreapi.pexcard.com/v4/Card/SetPin/{Id} \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
PUT https://coreapi.pexcard.com/v4/Card/SetPin/{Id} HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/Card/SetPin/{Id}',
  method: 'put',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');
const inputBody = '{
  "Pin": ""
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/Card/SetPin/{Id}',
{
  method: 'PUT',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.put 'https://coreapi.pexcard.com/v4/Card/SetPin/{Id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.put('https://coreapi.pexcard.com/v4/Card/SetPin/{Id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/Card/SetPin/{Id}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("PUT");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Content-Type": []string{"application/json"},
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("PUT", "https://coreapi.pexcard.com/v4/Card/SetPin/{Id}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

> Body parameter

```json
{
  "Pin": ""
}
```

> Example responses

> 200 Response

```json
{}
```

**Summary:** Create a 4-digit PIN and associate it with a card accountID

**Description:** Create a 4-digit PIN and associate it with a card accountID.<br/>
            <br/>
            There is no cash access and a PEX card cannot be used to obtain cash from an ATM, POS or by any other means.<br/>
            <br/>
            You can set a PIN to allow your cardholder to shop at some stores that require PINs, e.g. Sam's Club and Costco.<br/>
            <br/>
            The PIN is secure and cannot be viewed online or by customer service. If the cardholder forgets the PIN, a new PIN must be created.<br/>
            <br/>
            If the cardholder uses an incorrect PIN five (5) times, the system will block the card for fraud. To remove the block, call customer service (1-866-685-1898) or create a new PIN - SetPIN will unblock the card and set the failure count to 0.<br/>
            <br/>
            A PIN must:<br/>
            <list type="number">
            <item><description>- be four (4) digits<br/></description></item>
            <item><description>- not be all the same digit, ex. 1111<br/></description></item>
            <item><description>- not be digits in sequence, ex. 1234<br/></description></item>
            <item><description>- not match the last four (4) digits of the card number.<br/></description></item>
            </list>
            <br/>

**HTTP Request**
`***PUT*** /Card/SetPin/{Id}` 


**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| Id | path | Card account ID | Yes | integer |
| UserRequest | body | 4 digit PIN | Yes |  |
| Authorization | header | token {USERTOKEN} | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Success |
| 403 | <list type="number">    <item>      <description>- Invalid card account ID<br /></description>    </item>    <item>      <description>- Must be card account ID</description>    </item>  </list> |


##Card Profile
###GET Card Profile 
```shell
# You can also use wget
curl -X GET https://coreapi.pexcard.com/v4/Card/Profile/{Id} \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
GET https://coreapi.pexcard.com/v4/Card/Profile/{Id} HTTP/1.1
Host: coreapi.pexcard.com

Accept: application/json
Authorization: string

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/Card/Profile/{Id}',
  method: 'get',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');

const headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/Card/Profile/{Id}',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.get 'https://coreapi.pexcard.com/v4/Card/Profile/{Id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.get('https://coreapi.pexcard.com/v4/Card/Profile/{Id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/Card/Profile/{Id}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "https://coreapi.pexcard.com/v4/Card/Profile/{Id}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```
> Example responses

> 200 Response

```json
{
  "AccountId": 0,
  "AccountStatus": "",
  "FirstName": "",
  "LastName": "",
  "CardholderGroupId": 0,
  "SpendRulesetId": 0,
  "ProfileAddress": {
    "ContactName": "",
    "AddressLine1": "",
    "AddressLine2": "",
    "City": "",
    "State": "",
    "PostalCode": "",
    "Country": ""
  },
  "Phone": "",
  "ShippingAddress": {
    "ContactName": "",
    "AddressLine1": "",
    "AddressLine2": "",
    "City": "",
    "State": "",
    "PostalCode": "",
    "Country": ""
  },
  "ShippingPhone": "",
  "DateOfBirth": "",
  "Email": "",
  "IsVirtual": false,
  "CustomId": ""
}
```

**Summary:** Return profile data associated with a single card accountID

**Description:** Return profile data associated with a single card accountID.<br/>
            <br/>
            Definition of some of the returned fields and how the PEX system uses them:<br/>
            <list type="number">
            <item><description>- AccountId: Card account ID. 0 will be returned as the Account ID for cards that are pending.<br/></description></item>
            <item><description>- CardholderGroupID: Unique identifier for the group (for a definition of group see POST /Group/Group.)<br/></description></item>
            <item><description>- Profile address: The cardholder billing address.<br/></description></item>
            <item><description>- Shipping address: Used for card mailing. PEX uses this address for all future card replacements including: lost, stolen, compromised and renewal.<br/></description></item>
            <item><description>- SpendRulestId in the response lets user know the associated SpendingRuleset with the card account specified in the request.<br/></description></item>
            <item><description>- IsVirtual: If this is connected to a virtual card order then the value is: true, otherwise, false.<br/></description></item>
            <item><description>- CustomId: User defined Id which can be assigned to Card holder profile (alphanumeric up to 50 characters). This is optional field.<br/></description></item>
            </list>
            <br/>
            To retrieve all information stored against a card accountID, including spend and funding rules, use GET /Details/AccountDetails/{Id}.

**HTTP Request**
`***GET*** /Card/Profile/{Id}` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| Id | path | Card account ID | Yes | integer |
| Authorization | header | token {USERTOKEN} | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Success |
| 401 | Must be card account ID |
| 403 | Invalid card account ID |

###Update Card Profile 
```shell
# You can also use wget
curl -X PUT https://coreapi.pexcard.com/v4/Card/Profile/{Id} \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
PUT https://coreapi.pexcard.com/v4/Card/Profile/{Id} HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/Card/Profile/{Id}',
  method: 'put',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');
const inputBody = '{
  "CardholderGroupId": 0,
  "SpendRulesetId": 0,
  "Phone": "",
  "ShippingPhone": "",
  "DateOfBirth": "",
  "Email": "",
  "CustomId": "",
  "FirstName": "",
  "LastName": "",
  "NormalizeProfileAddress": false,
  "ProfileAddress": {
    "AddressLine1": "",
    "AddressLine2": "",
    "City": "",
    "State": "",
    "PostalCode": ""
  },
  "NormalizeShippingAddress": false,
  "ShippingAddress": {
    "ContactName": "",
    "AddressLine1": "",
    "AddressLine2": "",
    "City": "",
    "State": "",
    "PostalCode": ""
  }
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/Card/Profile/{Id}',
{
  method: 'PUT',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.put 'https://coreapi.pexcard.com/v4/Card/Profile/{Id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.put('https://coreapi.pexcard.com/v4/Card/Profile/{Id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/Card/Profile/{Id}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("PUT");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Content-Type": []string{"application/json"},
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("PUT", "https://coreapi.pexcard.com/v4/Card/Profile/{Id}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

> Body parameter

```json
{
  "CardholderGroupId": 0,
  "SpendRulesetId": 0,
  "Phone": "",
  "ShippingPhone": "",
  "DateOfBirth": "",
  "Email": "",
  "CustomId": "",
  "FirstName": "",
  "LastName": "",
  "NormalizeProfileAddress": false,
  "ProfileAddress": {
    "AddressLine1": "",
    "AddressLine2": "",
    "City": "",
    "State": "",
    "PostalCode": ""
  },
  "NormalizeShippingAddress": false,
  "ShippingAddress": {
    "ContactName": "",
    "AddressLine1": "",
    "AddressLine2": "",
    "City": "",
    "State": "",
    "PostalCode": ""
  }
}
```

> Example responses

> 200 Response

```json
{}
```
**Summary:** Update profile data for a specified card accountID.

**Description:** All fields are optional for update, however, some profile fields are required in the system and cannot be replaced by null or empty strings. The API user must have AddEditTerminateCard = true.<br/>
            <br/>
            Required profile fields:<br/>
            <list type="number">
            <item><description>- First Name<br/></description></item>
            <item><description>- Last Name<br/></description></item>
            <item><description>- Profile Address Line 1<br/></description></item>
            <item><description>- Profile City<br/></description></item>
            <item><description>- Profile State<br/></description></item>
            <item><description>- Profile Zip<br/></description></item>
            <item><description>- Shipping Address Line 1<br/></description></item>
            <item><description>- Shipping City<br/></description></item>
            <item><description>- Shipping Status<br/></description></item>
            <item><description>- Shipping Zip<br/></description></item>
            <item><description>- Phone<br/></description></item>
            <item><description>- Email<br/></description></item>
            <item><description>- Date of Birth.<br/></description></item>
            </list>
            <br/>
            To find the group name associated with a  CardholderGroupId , use GET /Details/AccountDetails.<br/>
            CustomId: User defined Id which can be assigned to Card holder profile (alphanumeric up to 50 characters). This is optional field. <br/>
            <br/>
            User can specify SpendRulesetId in the request to associate an account with SpendingRuleset. <br/>
            If SpendRulesetId value in request is null, account will be disassociated from a SpendingRuleset.<br/>
            <br/>
            If PEX card is used for fuel authorizations, transit passes or online purchases, there will be times where the cardholder will have to key in the billing zip code as it appears on the cardholder profile. To avoid issues at the time of purchase, let the cardholder know what their billing (i.e. profile) address is.<br/>
            <br/>
            If the cardholder enters an invalid Zip Code 2 times, the merchant may refuse to accept additional card swipes. If this occurs, cardholders will have to see the attendant to complete a gas transaction, or use another form of payment.<br/>
            <br/>
            If the cardholder should have access to ch.pexcard.com to review their transaction history, etc., they will need the four (4) digit year of birth from their profile. If you are using a generic value, you will need to convey that to the cardholder.

**HTTP Request**
`***PUT*** /Card/Profile/{Id}` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| Id | path | Card account ID | Yes | integer |
| UserRequest | body | Profile data | Yes |  |
| Authorization | header | token {USERTOKEN} | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Success |
| 403 | <list type="number">    <item>      <description>- Invalid card account ID<br /></description>    </item>    <item>      <description>- Must be card account ID<br /></description>    </item>    <item>      <description>- Card group not found</description>    </item>  </list> |

##Close Card 
```shell
# You can also use wget
curl -X POST https://coreapi.pexcard.com/v4/Card/Terminate/{Id} \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
POST https://coreapi.pexcard.com/v4/Card/Terminate/{Id} HTTP/1.1
Host: coreapi.pexcard.com

Accept: application/json
Authorization: string

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/Card/Terminate/{Id}',
  method: 'post',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');

const headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/Card/Terminate/{Id}',
{
  method: 'POST',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.post 'https://coreapi.pexcard.com/v4/Card/Terminate/{Id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.post('https://coreapi.pexcard.com/v4/Card/Terminate/{Id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/Card/Terminate/{Id}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("POST");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("POST", "https://coreapi.pexcard.com/v4/Card/Terminate/{Id}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

> Example responses

> 200 Response

```json
{}
```
**Summary:** Close a specified card accountId

**Description:** Close a specified card accountId.<br/>
            <br/>
            Card/Terminate completely closes the card account. Any remaining funds on the card account are returned to the main PEX business account. This action is immediate and NOT reversible.<br/>

**HTTP Request**
`***POST*** /Card/Terminate/{Id}` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| Id | path | Card account ID | Yes | integer |
| Authorization | header | token {USERTOKEN} | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Success |
| 403 | <list type="number">    <item>      <description>- Invalid card account ID<br /></description>    </item>    <item>      <description>- Must be card account ID<br /></description>    </item>    <item>      <description>- Cannot change status</description>    </item>  </list> |

##Fund Card

```shell
# You can also use wget
curl -X POST https://coreapi.pexcard.com/v4/Card/Fund/{Id} \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
POST https://coreapi.pexcard.com/v4/Card/Fund/{Id} HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/Card/Fund/{Id}',
  method: 'post',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');
const inputBody = '{
  "Amount": 0
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/Card/Fund/{Id}',
{
  method: 'POST',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.post 'https://coreapi.pexcard.com/v4/Card/Fund/{Id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.post('https://coreapi.pexcard.com/v4/Card/Fund/{Id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/Card/Fund/{Id}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("POST");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Content-Type": []string{"application/json"},
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("POST", "https://coreapi.pexcard.com/v4/Card/Fund/{Id}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

> Body parameter

```json
{
  "Amount": 0
}
```

> Example responses

> 200 Response

```json
{
  "AccountId": 0,
  "AvailableBalance": 0,
  "LedgerBalance": 0
}
```
**Summary:** Add or remove funds to/from a card accountID

**Description:** Add or remove funds to/from a card accountID.<br/>
            <br/>
            Card funding is in real-time and will change the cardholder's available balance immediately.<br/>  
            <br/> 
            To remove funds from the card balance, enter a negative number, for example: -10.00 will remove $10.00 from the card available balance.<br/> 
            <br/>
            Padding for Restaurant: At non-fast food locations, card authorization is (typically) for total plus 20&#37; of total (ex. bill total $56.00 + $11.20 (20&#37;) = $67.20 authorization amount). If the cardholder spends at restaurants, please be sure to allow for the additional 20&#37;.<br/>
            <br/>
            Gas Purchases at Automated Fuel Dispensers (AFDs): AFDs  will authorize for a minimum $50.00 and settle for the amount of gas pumped (whether the purchase is above or below $50.00).<br/>
            <br/>
            To retrieve the card accountID, use GET /Details/AccountDetails.

**HTTP Request**
`***POST*** /Card/Fund/{Id}` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| Id | path | Card account ID | Yes | integer |
| UserRequest | body | Details required for funding a card | Yes |  |
| Authorization | header | token {USERTOKEN} | Yes | string |


**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Success |
| 403 | <list type="number">    <item>      <description>- Invalid card account ID<br /></description>    </item>    <item>      <description>- Must be card account ID<br /></description>    </item>    <item>      <description>- Insufficient funds on business<br /></description>    </item>    <item>      <description>- Insufficient funds on card account<br /></description>    </item>    <item>      <description>- Card available balance will exceed card limit<br /></description>    </item>    <item>      <description>- Use Business Balance is enabled for card account</description>    </item>    <item>      <description>- Invalid amount</description>    </item>  </list> |

##Remove Card Funds 

```shell
# You can also use wget
curl -X POST https://coreapi.pexcard.com/v4/Card/Zero/{Id} \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
POST https://coreapi.pexcard.com/v4/Card/Zero/{Id} HTTP/1.1
Host: coreapi.pexcard.com

Accept: application/json
Authorization: string

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/Card/Zero/{Id}',
  method: 'post',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');

const headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/Card/Zero/{Id}',
{
  method: 'POST',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.post 'https://coreapi.pexcard.com/v4/Card/Zero/{Id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.post('https://coreapi.pexcard.com/v4/Card/Zero/{Id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/Card/Zero/{Id}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("POST");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("POST", "https://coreapi.pexcard.com/v4/Card/Zero/{Id}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

> Example responses

> 200 Response

```json
{
  "AccountId": 0,
  "AvailableBalance": 0,
  "LedgerBalance": 0
}
```
**Summary:** Fund a specified card accountID to zero ($0)

**Description:** Fund a specified card accountID to zero ($0).<br/>
            <br/>
            Specify a card accountID and funds from the business account will be added/removed so that the card account (available) balance = $0.00.

**HTTP Request**
`***POST*** /Card/Zero/{Id}` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| Id | path | Card account ID | Yes | integer |
| Authorization | header | token {USERTOKEN} | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Success |
| 403 | <list type="number">    <item>      <description>- Card Account ID does not exist<br /></description>    </item>    <item>      <description>- Must be card account ID<br /></description>    </item>    <item>      <description>- Insufficient funds on business<br /></description>    </item>    <item>      <description>- Invalid amount</description>    </item>  </list> |

##Assign Group to card 
```shell
# You can also use wget
curl -X PUT https://coreapi.pexcard.com/v4/Card/SetGroup \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
PUT https://coreapi.pexcard.com/v4/Card/SetGroup HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/Card/SetGroup',
  method: 'put',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');
const inputBody = '{
  "GroupId": 0,
  "AcctId": 0
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/Card/SetGroup',
{
  method: 'PUT',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.put 'https://coreapi.pexcard.com/v4/Card/SetGroup',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.put('https://coreapi.pexcard.com/v4/Card/SetGroup', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/Card/SetGroup");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("PUT");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Content-Type": []string{"application/json"},
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("PUT", "https://coreapi.pexcard.com/v4/Card/SetGroup", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```
> Body parameter

```json
{
  "GroupId": 0,
  "AcctId": 0
}
```

> Example responses

> 200 Response

```json
{}
```
**Summary:** Set a group for the card account

**Description:** Insert a card accountID into a specified group.<br/>
            <br/>
            For a definition of group see POST /Group/Group.

**HTTP Request**
`***PUT*** /Card/SetGroup` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| GroupRequest | body | Group ID and Account ID | Yes |  |
| Authorization | header | token {USERTOKEN} | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Success |
| 403 | <list type="number">    <item>      <description>- Invalid card account ID<br /></description>    </item>    <item>      <description>- Invalid group ID</description>    </item>  </list> |




##Multiple Card Operations 
###Fund All Cards 

```shell
# You can also use wget
curl -X PUT https://coreapi.pexcard.com/v4/Bulk/FundAllCards \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
PUT https://coreapi.pexcard.com/v4/Bulk/FundAllCards HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/Bulk/FundAllCards',
  method: 'put',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');
const inputBody = '{
  "Amount": 0
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/Bulk/FundAllCards',
{
  method: 'PUT',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.put 'https://coreapi.pexcard.com/v4/Bulk/FundAllCards',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.put('https://coreapi.pexcard.com/v4/Bulk/FundAllCards', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/Bulk/FundAllCards");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("PUT");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Content-Type": []string{"application/json"},
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("PUT", "https://coreapi.pexcard.com/v4/Bulk/FundAllCards", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

> Example request

```json
{
  "Amount": 0
}
```

> Example responses

> 200 Response

```json
{
  "TotalNumberOfCards": 0
}
```
**Summary:** Fund all cards for the business

**Description:** This is an offline process to add funds to all cards in the business for a specified amount.<br/>
            <br/>
            Cards with status Inactive, Active and Blocked will be funded. Cards with status Closed will not be funded.

**HTTP Request**
`***PUT*** /Bulk/FundAllCards` 


**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| req | body |  | Yes |  |
| Authorization | header | token {USERTOKEN} | Yes | string |



**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Success |
| 400 | Invalid request |


###Fund Multiple cards 
```shell
# You can also use wget
curl -X PUT https://coreapi.pexcard.com/v4/Bulk/FundMultipleCards \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
PUT https://coreapi.pexcard.com/v4/Bulk/FundMultipleCards HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/Bulk/FundMultipleCards',
  method: 'put',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');
const inputBody = '{
  "Cards": [
    {
      "AccountId": 0,
      "Amount": 0
    }
  ],
  "TransferType": ""
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/Bulk/FundMultipleCards',
{
  method: 'PUT',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.put 'https://coreapi.pexcard.com/v4/Bulk/FundMultipleCards',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.put('https://coreapi.pexcard.com/v4/Bulk/FundMultipleCards', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/Bulk/FundMultipleCards");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("PUT");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Content-Type": []string{"application/json"},
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("PUT", "https://coreapi.pexcard.com/v4/Bulk/FundMultipleCards", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

> Example Request

```json
{
  "Cards": [
    {
      "AccountId": 0,
      "Amount": 0
    }
  ],
  "TransferType": ""
}
```

> Example responses

> 200 Response

```json
{
  "Success": false,
  "Results": [
    {
      "BusinessTransactionId": 0,
      "BusinessCurrentBalance": 0,
      "AccountId": 0,
      "TransactionId": 0,
      "CurrentBalance": 0,
      "ResponseCode": 0,
      "Message": ""
    }
  ],
  "Errors": [
    {
      "AccountId": 0,
      "ResponseCode": 0,
      "Message": ""
    }
  ]
}
```
**Summary:** Bulk fund on batches of cards in the business.

**Description:** <b>This endpoint is not part of our standard API offering. To access the FundMultipleCards endpoint please send an email with your request to apisupport@pexcard.com.</b>  This is a bulk process to execute balance adjustments on multiple cards in the business.<br/>
            <br/>
            Funding of up to 25 cards per batch are allowed.  Cards with status of Active, Inactive and Blocked will be funded. Cards with status Closed will not be funded.

**HTTP Request**
`***PUT*** /Bulk/FundMultipleCards` 



**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| req | body |  | Yes |  |
| Authorization | header | token {USERTOKEN} | Yes | string |



**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Success |
| 206 | Partial Success |
| 400 | Failed Request |


###Remove All Card's Funds 

```shell
# You can also use wget
curl -X POST https://coreapi.pexcard.com/v4/Bulk/Zero \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
POST https://coreapi.pexcard.com/v4/Bulk/Zero HTTP/1.1
Host: coreapi.pexcard.com

Accept: application/json
Authorization: string

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/Bulk/Zero',
  method: 'post',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');

const headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/Bulk/Zero',
{
  method: 'POST',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.post 'https://coreapi.pexcard.com/v4/Bulk/Zero',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.post('https://coreapi.pexcard.com/v4/Bulk/Zero', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/Bulk/Zero");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("POST");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("POST", "https://coreapi.pexcard.com/v4/Bulk/Zero", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

> Example responses

> 200 Response

```json
{
  "TotalNumberOfCards": 0
}
```


**Summary:** Adjust all card available balances to $0.00 for the business

**Description:** This is an offline process to add or remove available funds from every card account for the business. The system will query all card available balances and add or remove that dollar value so that the available balance is $0.00.<br/>
            <br/>
            This call can take the place of individually retrieving all card balances and calling card fund for each account individually.<br/>
            <br/>
            If you fund the card account while this job is running, those funds will be reflected in the available balance. However, the job will not drive the account negative if funds are no longer in the account.<br/>

**HTTP Request**
`***POST*** /Bulk/Zero` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| Authorization | header | token {USERTOKEN} | Yes | string |


**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Success |



###Update Low Balance Funding 

```shell
# You can also use wget
curl -X PUT https://coreapi.pexcard.com/v4/Bulk/SetAllCardsLowBalanceFunding \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
PUT https://coreapi.pexcard.com/v4/Bulk/SetAllCardsLowBalanceFunding HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/Bulk/SetAllCardsLowBalanceFunding',
  method: 'put',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');
const inputBody = '{
  "ThresholdAmount": 0,
  "Amount": 0
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/Bulk/SetAllCardsLowBalanceFunding',
{
  method: 'PUT',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.put 'https://coreapi.pexcard.com/v4/Bulk/SetAllCardsLowBalanceFunding',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.put('https://coreapi.pexcard.com/v4/Bulk/SetAllCardsLowBalanceFunding', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/Bulk/SetAllCardsLowBalanceFunding");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("PUT");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Content-Type": []string{"application/json"},
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("PUT", "https://coreapi.pexcard.com/v4/Bulk/SetAllCardsLowBalanceFunding", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

> Body parameter

```json
{
  "ThresholdAmount": 0,
  "Amount": 0
}
```

> Example responses

> 200 Response

```json
{
  "TotalNumberOfCards": 0
}
```

**Summary:** Update low-balance funding rule for all cards in the business

**Description:** Update a low balance rule for all cards in the business to the Amount and/or ThresholdAmount values specified.

**HTTP Request**
`***PUT*** /Bulk/SetAllCardsLowBalanceFunding` 




**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| req | body |  | Yes |  |
| Authorization | header | token {USERTOKEN} | Yes | string |


**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Success |
| 400 | Invalid request |


###Remove Low balance funding
```shell
# You can also use wget
curl -X DELETE https://coreapi.pexcard.com/v4/Bulk/RemoveAllCardsLowBalanceFunding \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
DELETE https://coreapi.pexcard.com/v4/Bulk/RemoveAllCardsLowBalanceFunding HTTP/1.1
Host: coreapi.pexcard.com

Accept: application/json
Authorization: string

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/Bulk/RemoveAllCardsLowBalanceFunding',
  method: 'delete',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');

const headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/Bulk/RemoveAllCardsLowBalanceFunding',
{
  method: 'DELETE',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.delete 'https://coreapi.pexcard.com/v4/Bulk/RemoveAllCardsLowBalanceFunding',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.delete('https://coreapi.pexcard.com/v4/Bulk/RemoveAllCardsLowBalanceFunding', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/Bulk/RemoveAllCardsLowBalanceFunding");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("DELETE");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("DELETE", "https://coreapi.pexcard.com/v4/Bulk/RemoveAllCardsLowBalanceFunding", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

**Summary:** Remove low-balance funding rule for all cards in the business

**Description:** Remove a low balance funding rule for all cards in the business. Once the funding rule is deleted, the system will no longer add funds to any card balance.

**HTTP Request**
`***DELETE*** /Bulk/RemoveAllCardsLowBalanceFunding` 


**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| Authorization | header | token {USERTOKEN} | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Success |


###Update Scheduled Funding 

```shell
# You can also use wget
curl -X PUT https://coreapi.pexcard.com/v4/Bulk/SetAllCardsScheduledFunding \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
PUT https://coreapi.pexcard.com/v4/Bulk/SetAllCardsScheduledFunding HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/Bulk/SetAllCardsScheduledFunding',
  method: 'put',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');
const inputBody = '{
  "Frequency": 0,
  "Amount": 0
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/Bulk/SetAllCardsScheduledFunding',
{
  method: 'PUT',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.put 'https://coreapi.pexcard.com/v4/Bulk/SetAllCardsScheduledFunding',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.put('https://coreapi.pexcard.com/v4/Bulk/SetAllCardsScheduledFunding', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/Bulk/SetAllCardsScheduledFunding");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("PUT");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Content-Type": []string{"application/json"},
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("PUT", "https://coreapi.pexcard.com/v4/Bulk/SetAllCardsScheduledFunding", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

> Body parameter

```json
{
  "Frequency": 0,
  "Amount": 0
}
```

> Example responses

> 200 Response

```json
{
  "TotalNumberOfCards": 0
}
```
**Summary:** Update scheduled funding rule for all cards in the business

**Description:** Update a scheduled funding rule for all cards in the business to the Amount and Frequency values specified.<br/>
            <br/>
            Valid scheduled funding frequencies are:<br/>
            <list type="number">
            <item><description>0 - Daily<br/></description></item>
            <item><description>1 - Monday<br/></description></item>
            <item><description>2 - Tuesday<br/></description></item>
            <item><description>3 - Wednesday<br/></description></item>
            <item><description>4 - Thursday<br/></description></item>
            <item><description>5 - Friday<br/></description></item>
            <item><description>6 - Saturday<br/></description></item>
            <item><description>7 - Sunday<br/></description></item>
            <item><description>8 - First of each month<br/></description></item>
            </list>

**HTTP Request**
`***PUT*** /Bulk/SetAllCardsScheduledFunding` 



**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| req | body |  | Yes |  |
| Authorization | header | token {USERTOKEN} | Yes | string |


**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Success |
| 400 | Invalid request |


###Remove Scheduled Funding 

```shell
# You can also use wget
curl -X DELETE https://coreapi.pexcard.com/v4/Bulk/RemoveAllCardsScheduledFunding \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
DELETE https://coreapi.pexcard.com/v4/Bulk/RemoveAllCardsScheduledFunding HTTP/1.1
Host: coreapi.pexcard.com

Accept: application/json
Authorization: string

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/Bulk/RemoveAllCardsScheduledFunding',
  method: 'delete',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');

const headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/Bulk/RemoveAllCardsScheduledFunding',
{
  method: 'DELETE',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.delete 'https://coreapi.pexcard.com/v4/Bulk/RemoveAllCardsScheduledFunding',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.delete('https://coreapi.pexcard.com/v4/Bulk/RemoveAllCardsScheduledFunding', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/Bulk/RemoveAllCardsScheduledFunding");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("DELETE");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("DELETE", "https://coreapi.pexcard.com/v4/Bulk/RemoveAllCardsScheduledFunding", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

> Example responses

> 200 Response

```json
{
  "TotalNumberOfCards": 0
}
```

**Summary:** Remove scheduled funding rule for all cards in the business

**Description:** Remove a scheduled funding rule for all cards in the business. Once the funding rule is deleted, the system will no longer add funds to any card balance.

**HTTP Request**
`***DELETE*** /Bulk/RemoveAllCardsScheduledFunding` 



**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| Authorization | header | token {USERTOKEN} | Yes | string |



**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Success |

###Get All Spending Rulesets 

```shell
# You can also use wget
curl -X GET https://coreapi.pexcard.com/v4/Bulk/GetSpendingRulesets \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
GET https://coreapi.pexcard.com/v4/Bulk/GetSpendingRulesets HTTP/1.1
Host: coreapi.pexcard.com

Accept: application/json
Authorization: string

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/Bulk/GetSpendingRulesets',
  method: 'get',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');

const headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/Bulk/GetSpendingRulesets',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.get 'https://coreapi.pexcard.com/v4/Bulk/GetSpendingRulesets',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.get('https://coreapi.pexcard.com/v4/Bulk/GetSpendingRulesets', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/Bulk/GetSpendingRulesets");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "https://coreapi.pexcard.com/v4/Bulk/GetSpendingRulesets", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```


> Example responses

> 200 Response

```json
[
  {
    "RulesetId": 0,
    "SpendingRulesetCategories": {
      "CategoryId": 0,
      "AssociationsOrganizationsAllowed": false,
      "AutomotiveDealersAllowed": false,
      "EducationalServicesAllowed": false,
      "EntertainmentAllowed": false,
      "FuelPumpsAllowed": false,
      "GasStationsConvenienceStoresAllowed": false,
      "GroceryStoresAllowed": false,
      "HealthcareChildcareServicesAllowed": false,
      "ProfessionalServicesAllowed": false,
      "RestaurantsAllowed": false,
      "RetailStoresAllowed": false,
      "TravelTransportationAllowed": false,
      "HardwareStoresAllowed": false
    },
    "MccRestrictions": false,
    "BacctId": 0,
    "Name": "",
    "CountCardsPresent": 0,
    "DailySpendLimit": 0,
    "WeeklySpendLimit": 0,
    "MonthlySpendLimit": 0,
    "YearlySpendLimit": 0,
    "LifetimeSpendLimit": 0,
    "InternationalAllowed": false,
    "CardNotPresentAllowed": false,
    "UsePexAccountBalanceForAuths": false,
    "UseCustomerAuthDecision": false
  }
]
```
**Summary:** Return all spending rulesets for the business

**Description:** Return all spending rulesets for the business.<br/>
            <br/>
            A spending ruleset is a group of spend rules that can be applied to multiple card accounts. For example, if all cardholders should be allowed to spend funds at restaurants and fuel pumps, the administrator can create a spending ruleset that has only those merchant categories 'checked'. Every card with that ruleset applied can only spend at restaurants and fuel pumps.<br/>
            <br/>
            Spending rulesets must be created in the administration website.

**HTTP Request**
`***GET*** /Bulk/GetSpendingRulesets` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| Authorization | header | token {USERTOKEN} | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |


###Update Spending Ruleset
```shell
# You can also use wget
curl -X PUT https://coreapi.pexcard.com/v4/Bulk/SetAllCardsSpendingRuleset \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
PUT https://coreapi.pexcard.com/v4/Bulk/SetAllCardsSpendingRuleset HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/Bulk/SetAllCardsSpendingRuleset',
  method: 'put',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');
const inputBody = '{
  "RulesetId": 0
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/Bulk/SetAllCardsSpendingRuleset',
{
  method: 'PUT',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.put 'https://coreapi.pexcard.com/v4/Bulk/SetAllCardsSpendingRuleset',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.put('https://coreapi.pexcard.com/v4/Bulk/SetAllCardsSpendingRuleset', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/Bulk/SetAllCardsSpendingRuleset");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("PUT");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Content-Type": []string{"application/json"},
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("PUT", "https://coreapi.pexcard.com/v4/Bulk/SetAllCardsSpendingRuleset", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

> Body parameter

```json
{
  "RulesetId": 0
}
```

> Example responses

> 200 Response

```json
{
  "TotalNumberOfCards": 0
}
```

**Summary:** Update spend rules for all cards in the business

**Description:** To retrieve the RulesetId, use Get /Bulk/GetSpendingRulesets and apply that RulesetId to all cards.<br/>
            <br/>
            Changes to spend rules happen in real-time. Be sure the cardholder is aware of the limitations being set.<br/>
            <br/>
            Cardholders using PEX card do not have cash access. ATMs, Money Orders, Money Remittance (e.g. MoneyGram) and other cash transactions, such as purchasing casino chips, will be declined at all times.<br/>
            <br/>
            Spending rulesets must be created in the administration website.

**HTTP Request**
`***PUT*** /Bulk/SetAllCardsSpendingRuleset` 


**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| req | body |  | Yes |  |
| Authorization | header | token {USERTOKEN} | Yes | string |


**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Success |
| 400 | Invalid request |


##Card Low Balance Funding 
###Get Low Balance Funding  

```shell
# You can also use wget
curl -X GET https://coreapi.pexcard.com/v4/Card/LowBalanceFundingRules/{Id} \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
GET https://coreapi.pexcard.com/v4/Card/LowBalanceFundingRules/{Id} HTTP/1.1
Host: coreapi.pexcard.com

Accept: application/json
Authorization: string

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/Card/LowBalanceFundingRules/{Id}',
  method: 'get',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');

const headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/Card/LowBalanceFundingRules/{Id}',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.get 'https://coreapi.pexcard.com/v4/Card/LowBalanceFundingRules/{Id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.get('https://coreapi.pexcard.com/v4/Card/LowBalanceFundingRules/{Id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/Card/LowBalanceFundingRules/{Id}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "https://coreapi.pexcard.com/v4/Card/LowBalanceFundingRules/{Id}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```
> Example responses

> 200 Response

```json
{
  "LowBalanceFunding": {
    "ThresholdAmount": 0,
    "AmountToFund": 0
  }
}
```
**Summary:** Return funding rules for a specified card accountID

**Description:** Return funding rules for a specified card accountID.<br/>
            <br/>
            If no funding rule is set, PEX system will return a null response.<br/>
            <br/>
            To retrieve the card accountID, use GET /Details/AccountDetails.

**HTTP Request**
`***GET*** /Card/LowBalanceFundingRules/{Id}` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| Id | path | Card account ID | Yes | integer |
| Authorization | header | token {USERTOKEN} | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Success |
| 403 | <list type="number">    <item>      <description>- Invalid card account ID<br /></description>    </item>    <item>      <description>- Must be card account ID</description>    </item>  </list> |

###Update Low Balance Funding  

```shell
# You can also use wget
curl -X PUT https://coreapi.pexcard.com/v4/Card/LowBalanceFundingRules/{Id} \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
PUT https://coreapi.pexcard.com/v4/Card/LowBalanceFundingRules/{Id} HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/Card/LowBalanceFundingRules/{Id}',
  method: 'put',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');
const inputBody = '{
  "ThresholdAmount": 0,
  "AmountToFund": 0
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/Card/LowBalanceFundingRules/{Id}',
{
  method: 'PUT',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.put 'https://coreapi.pexcard.com/v4/Card/LowBalanceFundingRules/{Id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.put('https://coreapi.pexcard.com/v4/Card/LowBalanceFundingRules/{Id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/Card/LowBalanceFundingRules/{Id}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("PUT");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Content-Type": []string{"application/json"},
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("PUT", "https://coreapi.pexcard.com/v4/Card/LowBalanceFundingRules/{Id}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

> Body parameter

```json
{
  "ThresholdAmount": 0,
  "AmountToFund": 0
}
```

> Example responses

> 200 Response

```json
{}
```

**Summary:** Create a low balance funding rule for a specified card accountID

**Description:** Create a low balance funding rule for a specified card accountID.<br/>
            <br/>
            Example of the low balance funding rule logic: I would like to add $50.00 whenever this card's balance is less than or equal to $50.00.<br/>
            <br/>
            You may have cardholders who should never run out of funds. For those employees, set a funding rule on the card.<br/>  
            <br/>
            The low balance rule is trigger based. When a transaction posts against the account, the system will check to see if the available balance falls below the set threshold amount. If it does, the system will add the specified amount to the card balance. In the above example, the system will add $50.00 every time a transaction causes the card available balance to be less than or equal to $50.00.<br/>
            <br/>
            The system does not make a periodic check of the balance, it is triggered based upon transactions. If there are no transactions, the card will not 'top up'.<br/>
            <br/>
            To change the existing rule, post new values in the fields.<br/>
            <br/>
            To retrieve the card accountID, use GET /Details/AccountDetails.

**HTTP Request**
`***PUT*** /Card/LowBalanceFundingRules/{Id}` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| Id | path | Card account ID | Yes | integer |
| UserRequest | body | Rule parameters | Yes |  |
| Authorization | header | token {USERTOKEN} | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Success |
| 403 | <list type="number">    <item>      <description>- Invalid card account ID<br /></description>    </item>    <item>      <description>- Must be card account ID<br /></description>    </item>    <item>      <description>- Invalid amount</description>    </item>  </list> |

###Delete Low Balance Funding 

```shell
# You can also use wget
curl -X DELETE https://coreapi.pexcard.com/v4/Card/LowBalanceFundingRules/{Id} \
  -H 'Authorization: string'

```

```http
DELETE https://coreapi.pexcard.com/v4/Card/LowBalanceFundingRules/{Id} HTTP/1.1
Host: coreapi.pexcard.com

Authorization: string

```

```javascript
var headers = {
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/Card/LowBalanceFundingRules/{Id}',
  method: 'delete',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');

const headers = {
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/Card/LowBalanceFundingRules/{Id}',
{
  method: 'DELETE',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Authorization' => 'string'
}

result = RestClient.delete 'https://coreapi.pexcard.com/v4/Card/LowBalanceFundingRules/{Id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Authorization': 'string'
}

r = requests.delete('https://coreapi.pexcard.com/v4/Card/LowBalanceFundingRules/{Id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/Card/LowBalanceFundingRules/{Id}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("DELETE");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("DELETE", "https://coreapi.pexcard.com/v4/Card/LowBalanceFundingRules/{Id}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

**Summary:** Remove a low balance funding rule from the specified card accountID

**Description:** Remove a low balance funding rule from the specified card accountID.<br/>
            <br/>
            Once the rule is deleted, the system will no longer add funds to the card balance.<br/>
            <br/>
            To retrieve the card accountID, use GET /Details/AccountDetails.

**HTTP Request**
`***DELETE*** /Card/LowBalanceFundingRules/{Id}` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| Id | path | Card account ID | Yes | integer |
| Authorization | header | token {USERTOKEN} | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 403 | <list type="number">    <item>      <description>- Invalid card account ID<br /></description>    </item>    <item>      <description>- Must be card account ID</description>    </item>  </list> |


##Card Scheduled Funding 
###Get Card Scheduled Funding 
```shell
# You can also use wget
curl -X GET https://coreapi.pexcard.com/v4/Card/ScheduledFundingRules/{Id} \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
GET https://coreapi.pexcard.com/v4/Card/ScheduledFundingRules/{Id} HTTP/1.1
Host: coreapi.pexcard.com

Accept: application/json
Authorization: string

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/Card/ScheduledFundingRules/{Id}',
  method: 'get',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');

const headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/Card/ScheduledFundingRules/{Id}',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.get 'https://coreapi.pexcard.com/v4/Card/ScheduledFundingRules/{Id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.get('https://coreapi.pexcard.com/v4/Card/ScheduledFundingRules/{Id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/Card/ScheduledFundingRules/{Id}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "https://coreapi.pexcard.com/v4/Card/ScheduledFundingRules/{Id}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

> Example responses

> 200 Response

```json
{
  "ScheduledFunding": {
    "Amount": 0,
    "Frequency": 0
  }
}
```
**Summary:** Return scheduled funding rules for a specified card accountID

**Description:** Return scheduled funding rules for a specified card accountID.<br/>
            <br/>
            If no funding rule is set, PEX system will return a null response.<br/>
            <br/>
            To retrieve the card accountID, use GET /Details/AccountDetails.

**HTTP Request**
`***GET*** /Card/ScheduledFundingRules/{Id}` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| Id | path | Card account ID | Yes | integer |
| Authorization | header | token {USERTOKEN} | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Success |
| 403 | <list type="number">    <item>      <description>- Invalid card account ID<br /></description>    </item>    <item>      <description>- Must be card account ID</description>    </item>  </list> |

###Update Scheduled Funding

```shell
# You can also use wget
curl -X PUT https://coreapi.pexcard.com/v4/Card/ScheduledFundingRules/{Id} \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
PUT https://coreapi.pexcard.com/v4/Card/ScheduledFundingRules/{Id} HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/Card/ScheduledFundingRules/{Id}',
  method: 'put',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');
const inputBody = '{
  "Amount": 0,
  "Frequency": 0
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/Card/ScheduledFundingRules/{Id}',
{
  method: 'PUT',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.put 'https://coreapi.pexcard.com/v4/Card/ScheduledFundingRules/{Id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.put('https://coreapi.pexcard.com/v4/Card/ScheduledFundingRules/{Id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/Card/ScheduledFundingRules/{Id}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("PUT");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Content-Type": []string{"application/json"},
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("PUT", "https://coreapi.pexcard.com/v4/Card/ScheduledFundingRules/{Id}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

> Body parameter

```json
{
  "Amount": 0,
  "Frequency": 0
}
```
> Example responses

> 200 Response

```json
{}
```

**Summary:** Create a scheduled funding rule for the specified card accountID

**Description:** Create a scheduled funding rule for the specified card accountID.<br/>
            <br/>
            Example of a scheduled funding rule logic: I would like this card balance to equal $500.00 every Monday.<br/>
            <br/>
            You may have cardholders who should have a set balance every day or once a week. For those employees, set a funding rule on the card.<br/>
            The scheduled rule is time based. At midnight ET, the system checks to see if the card balance should be changed. If the balance is below the threshold, the system will add funds to equal the amount specified in the rule.<br/>
            <br/>
            To change the existing rule, post new values in the input fields.<br/>
            <br/>
            To retrieve the card accountID, use GET /Details/AccountDetails.

**HTTP Request**
`***PUT*** /Card/ScheduledFundingRules/{Id}` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| Id | path | Card account ID | Yes | integer |
| UserRequest | body | Rule parameters | Yes |  |
| Authorization | header | token {USERTOKEN} | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Success |
| 403 | <list type="number">    <item>      <description>- Invalid card account ID<br /></description>    </item>    <item>      <description>- Must be card account ID<br /></description>    </item>    <item>      <description>- Invalid amount</description>    </item>  </list> |


##Virtual Card
###Create Virtual Card
```shell
# You can also use wget
curl -X POST https://coreapi.pexcard.com/v4/VirtualCard/Order \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
POST https://coreapi.pexcard.com/v4/VirtualCard/Order HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/VirtualCard/Order',
  method: 'post',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');
const inputBody = '{
  "VirtualCards": [
    {
      "FirstName": "",
      "LastName": "",
      "DateOfBirth": "",
      "Phone": "",
      "Email": "",
      "ProfileAddress": {
        "AddressLine1": "",
        "AddressLine2": "",
        "City": "",
        "State": "",
        "PostalCode": ""
      },
      "GroupId": 0,
      "RulesetId": 0,
      "AutoActivation": false,
      "FundCardAmount": 0,
      "CardDataWebhookURL": ""
    }
  ]
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/VirtualCard/Order',
{
  method: 'POST',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.post 'https://coreapi.pexcard.com/v4/VirtualCard/Order',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.post('https://coreapi.pexcard.com/v4/VirtualCard/Order', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/VirtualCard/Order");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("POST");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Content-Type": []string{"application/json"},
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("POST", "https://coreapi.pexcard.com/v4/VirtualCard/Order", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

> Body parameter

```json
{
  "VirtualCards": [
    {
      "FirstName": "",
      "LastName": "",
      "DateOfBirth": "",
      "Phone": "",
      "Email": "",
      "ProfileAddress": {
        "AddressLine1": "",
        "AddressLine2": "",
        "City": "",
        "State": "",
        "PostalCode": ""
      },
      "GroupId": 0,
      "RulesetId": 0,
      "AutoActivation": false,
      "FundCardAmount": 0,
      "CardDataWebhookURL": ""
    }
  ]
}
```

> Example responses

> 200 Response

```json
{
  "VirtualCardOrderId": 0,
  "NumberOfCardsRequested": 0
}
```
**Summary:** Create virtual cards for the business

**Description:** Create virtual cards for the business. The response to this call is a VirtualCardOrderId and NumberOfCardsRequested. <br/>
            <br/>
            To retrieve card order details (without sensitive data), including the card AcctId, use GET /VirtualCard/Order/{Id} <br/>
            <br/>
            Cards have an expiration date of 3 years and will renew automatically 60 days prior to expiration. 
            If the card expiration is 01/20, the card will expire on the last day of the month, January 31, 2020. <br/>
            <br/>
            non-ASCII characters. Ex: " " not allowed <br/>
            Cardholder name may only include letters, numbers and the following punctuation symbols: , . - & ' <br/>
            Cardholder first + last names must be no more than 23 characters <br/>
            Email format: name@domain.com <br/>
            Date format: MM-DD-YYYY, ex. 01-31-1970 <br/>
            Phone format: 2125551212 or 212-555-1212, 10 digits can not begin with 1 <br/>
            Zip Code should be 5 digits: 10018 <br/>
            Country is always "US" <br/>
            Address format: letters, numbers and the following punctuation symbols: . ' () , # - / <br/>
            City format: letters, numbers and the following punctuation symbols: . ' () , # - / <br/>
            State format: two letter format ex. "CA" <br/>
            Max AddressLine1 field length: 26 characters <br/>
            Max AddressLine2 field length: 26 characters <br/>
            Max City field length: 25 characters <br/>
            <br/>
            To add a card to a group, use GroupId, otherwise there will be no group applied. 
            To add a card to a group after the card order has been created, use PUT/Card/SetGroup. <br/>
            To add spend rules to a card accountID, use RulesetId, otherwise there will be no spend rulesets applied. 
            To add spend rules to a card after the card order has been created, use PUT/Card/SpendRules/{Id} <br/>
            AutoActivation by default is set to true, if you want to activate your card(s) later it can be set to false. <br/>
            FundCardAmount is optional from 0 - 50,000 (if $50,000 that is the maximum card balance). 
            We allow for up to 2 decimal places, so 40.55. <br/>
            CardDataWebhookURL requires https and the max length is 500 characters, so "https://myapp.awesome.pexcustomer.com" will suffice. 
            You can add your own custom parameters in your webhook i.e. "https://myapp.awesome.pexcustomer.com?id=123&orderid=1234". <br/>
            <br/>
            If PEX is used for fuel authorizations, transit passes or online purchases, 
            there will be times where the cardholder will have to key in the billing zip code as it appears on the cardholder profile. 
            To avoid issues at the time of purchase, let the cardholder know what their billing (i.e. profile) address is. <br/>
            <br/>
            If the cardholder enters an invalid Zip Code 2 times, the merchant may refuse to accept additional card swipes. 
            If this occurs, cardholders will have to see the attendant to complete a gas transaction, or use another form of payment. <br/>
            <br/>
            If the cardholder should have access to ch.pexcard.com to review their transaction history, etc., 
            they will need the four (4) digit year of birth from their profile. 
            If you are using a generic value, you will need to convey that to the cardholder. <br/>
            <br/>
            At card creation, the spend rule defaults are: <br/>
            <list type="number">
              <item><description> - Daily spend limit is NONE <br/></description></item>
              <item><description> - International spending is OFF <br/></description></item>
              <item><description> - Card-not-present spending is ON <br/></description></item>
              <item><description> - All merchant categories are ON <br/></description></item>
            </list>

**HTTP Request**
`***POST*** /VirtualCard/Order` 


**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| orderRequest | body |  | Yes |  |
| Authorization | header | token {USERTOKEN} | Yes | string |


**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Success |
| 400 | <list type="number">    <item>      <description> - The GroupId does not exist <br /></description>    </item>    <item>      <description> - The RulesetId does not exist <br /></description>    </item>    <item>      <description> - Funding Card Amount you entered (X) is greater than the Maximum Card Balance (Y) <br /></description>    </item>    <item>      <description> - Webhook host request is different than one registered with PEX </description>    </item>  </list> |
| 403 | <list type="number">    <item>      <description> - The business does not support Virtual Card feature <br /></description>    </item>    <item>      <description> - Administrator lacking proper permissions to 'Add/Edit/Terminate Card' <br /></description>    </item>    <item>      <description> - Administrator lacking proper permissions for 'Funding' of Card <br /></description>    </item>    <item>      <description> - Card limit exceeded <br /></description>    </item>    <item>      <description> - Balance on cards greater than business balance <br /></description>    </item>    <item>      <description> - Webhook is not properly registered with PEX </description>    </item>  </list> |

###GET Virtual Card details 

```shell
# You can also use wget
curl -X GET https://coreapi.pexcard.com/v4/VirtualCard/Order/{id} \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
GET https://coreapi.pexcard.com/v4/VirtualCard/Order/{id} HTTP/1.1
Host: coreapi.pexcard.com

Accept: application/json
Authorization: string

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/VirtualCard/Order/{id}',
  method: 'get',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');

const headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/VirtualCard/Order/{id}',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.get 'https://coreapi.pexcard.com/v4/VirtualCard/Order/{id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.get('https://coreapi.pexcard.com/v4/VirtualCard/Order/{id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/VirtualCard/Order/{id}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "https://coreapi.pexcard.com/v4/VirtualCard/Order/{id}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```
**Summary:** Return details for all virtual cards included in a virtual card order (note: will not return sensitive card data)

**Description:** After using POST /VirtualCard/Order to create one or more cards, you can use this call to retrieve the card order information, 
            including the virtual card Account Id ("AcctId"). 
            Note the response will not include any sensitive card data.

**HTTP Request**
`***GET*** /VirtualCard/Order/{id}` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| Id | path | Virtual Card Order Id | Yes | integer |
| Authorization | header | token {USERTOKEN} | Yes | string |
> Example responses

> 200 Response

```json
{
  "CardOrderId": 0,
  "OrderDateTime": "",
  "UserName": "",
  "Cards": [
    {
      "RequestId": 0,
      "AcctId": 0,
      "AccountNumber": "",
      "FirstName": "",
      "LastName": "",
      "DateOfBirth": "",
      "Phone": "",
      "Email": "",
      "HomeAddress": {
        "AddressLine1": "",
        "AddressLine2": "",
        "City": "",
        "State": "",
        "PostalCode": "",
        "Country": ""
      },
      "GroupId": 0,
      "SpendingRulesetsId": 0,
      "AutoActivation": false,
      "FundCardAmount": 0,
      "CardDataWebhookURL": "",
      "Status": "",
      "Errors": [
        "string"
      ],
      "ErrorMessage": ""
    }
  ]
}
```
**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Success |
| 403 | Virtual Card Order is not available (may belong to another business) |
| 404 | Virtual Card Order does not exist |

###Resend Virtual Card Data
```shell
# You can also use wget
curl -X POST https://coreapi.pexcard.com/v4/VirtualCard/Data \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
POST https://coreapi.pexcard.com/v4/VirtualCard/Data HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/VirtualCard/Data',
  method: 'post',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');
const inputBody = '{
  "AcctId": 0,
  "CardDataWebhookURL": ""
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/VirtualCard/Data',
{
  method: 'POST',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.post 'https://coreapi.pexcard.com/v4/VirtualCard/Data',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.post('https://coreapi.pexcard.com/v4/VirtualCard/Data', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/VirtualCard/Data");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("POST");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Content-Type": []string{"application/json"},
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("POST", "https://coreapi.pexcard.com/v4/VirtualCard/Data", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

> Body parameter

```json
{
  "AcctId": 0,
  "CardDataWebhookURL": ""
}
```

> Example responses

> 200 Response

```json
{}
```

**Summary:** Request to resend callback with sensitive card data

**Description:** Request to resend webhook/callback with sensitive card data for a single AcctId. 
            This should only be used if the webhook from POST/VirtualCard/Order is not delivered. 
            If successful, you receive no response, just the webhook. <br/>
            <br/>
            To retrieve card order details (without sensitive data), including the card AcctId, use GET /VirtualCard/Order/{Id}.

**HTTP Request**
`***POST*** /VirtualCard/Data` 


**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| dataRequest | body | Account ID and webhook URL | Yes |  |
| Authorization | header | token {USERTOKEN} | Yes | string |


**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Success |
| 400 | <list type="number">    <item>      <description> - AccountId is not found or is not associated with a Virtual Card Order<br /></description>    </item>    <item>      <description> - Webhook host request is different than one registered with PEX</description>    </item>  </list> |
| 403 | <list type="number">    <item>      <description> - Cardholder does not belong to this business<br /></description>    </item>    <item>      <description> - Webhook is not properly registered with PEX</description>    </item>  </list> |


#Transaction Management 
##Transaction Details
###Retrieve All transactions 
```shell
# You can also use wget
curl -X GET https://coreapi.pexcard.com/v4/Details/AllCardholderTransactions?StartDate=2018-09-05T19%3A02%3A19Z&EndDate=2018-09-05T19%3A02%3A19Z \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
GET https://coreapi.pexcard.com/v4/Details/AllCardholderTransactions?StartDate=2018-09-05T19%3A02%3A19Z&EndDate=2018-09-05T19%3A02%3A19Z HTTP/1.1
Host: coreapi.pexcard.com

Accept: application/json
Authorization: string

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/Details/AllCardholderTransactions',
  method: 'get',
  data: '?StartDate=2018-09-05T19%3A02%3A19Z&EndDate=2018-09-05T19%3A02%3A19Z',
  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');

const headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/Details/AllCardholderTransactions?StartDate=2018-09-05T19%3A02%3A19Z&EndDate=2018-09-05T19%3A02%3A19Z',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.get 'https://coreapi.pexcard.com/v4/Details/AllCardholderTransactions',
  params: {
  'StartDate' => 'string(date-time)',
'EndDate' => 'string(date-time)'
}, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.get('https://coreapi.pexcard.com/v4/Details/AllCardholderTransactions', params={
  'StartDate': '2018-09-05T19:02:19Z',  'EndDate': '2018-09-05T19:02:19Z'
}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/Details/AllCardholderTransactions?StartDate=2018-09-05T19%3A02%3A19Z&EndDate=2018-09-05T19%3A02%3A19Z");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "https://coreapi.pexcard.com/v4/Details/AllCardholderTransactions", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

> Example responses

> 200 Response

```json
{
  "TransactionList": [
    {
      "TransactionId": 0,
      "AcctId": 0,
      "TransactionTime": "",
      "MerchantLocalTime": "",
      "HoldTime": "",
      "SettlementTime": "",
      "AuthTransactionId": 0,
      "TransactionAmount": 0,
      "PaddingAmount": 0,
      "TransactionType": 1,
      "Description": "",
      "TransactionNotes": [
        {
          "NoteId": 0,
          "UserName": "",
          "NoteText": "",
          "NoteDate": ""
        }
      ],
      "IsPending": false,
      "IsDecline": false,
      "MerchantName": "",
      "MerchantCity": "",
      "MerchantState": "",
      "MerchantZip": "",
      "MerchantCountry": "",
      "MCCCode": "",
      "TransferToOrFromAccountId": 0,
      "AuthIdentityResponseCode": "",
      "MerchantId": "",
      "TerminalId": "",
      "NetworkTransactionId": 0,
      "SourceCurrencyCodeDescription": "",
      "SourceCurrencyNumericCode": "",
      "SourceAmount": 0,
      "TransactionTags": {
        "Tags": [
          {
            "FieldId": "",
            "Value": {},
            "Name": ""
          }
        ],
        "State": 0,
        "FieldsVersion": ""
      },
      "MetadataApprovalStatus": "",
      "TransactionTypeCategory": ""
    }
  ],
  "Pages": {
    "PageSize": 0,
    "TotalRecords": 0,
    "NumberOfPages": 0,
    "LastTimeRetrieved": ""
  }
}
```

**Summary:** Return a list of all card transactions for the business

**Description:** Please make sure time frame selected between StartDate and EndDate is no more than last 12 months.<br/>
            <br/>
            Return a list of transaction details, within a specified start and end date, for all card accounts associated with the business of the authenticated user. Fields IsPending and IsDecline can be set to true or false as required.<br/>
            <br/>
            If, for the time-frame selected, over 30,000 transactions are returned then the results will be paginated. To retrieve more data, use the  LastTimeRetrieved  field returned in the StartDate parameter and repeat the call until the NumberOfPages field = 1. (Note: the last transaction for the page will be the first transaction retrieved in the next call, use the TransactionId to eliminate duplicate records.)<br/>
            <br/>
            Definition of some of the transaction detail fields:<br/>
            <list type="number">
            <item><description>- TransactionTime: Eastern time. The date/time when authorization was received from the Network.<br/></description></item>
            <item><description>- SettlementTime: Eastern time. Funds have been transferred to the merchant and the transaction is final. Use this for reconciliation purposes. Null for Pendings and Declines.<br/></description></item>
            <item><description>- HoldTime: Eastern time. Date/time a hold was placed on the card account balance. Null for Declines.<br/></description></item>
            <item><description>- MerchantLocalTime: Local time. Date/time provided by the merchant for the transaction. This is controlled by the merchant and may not be accurate.<br/></description></item>
            <item><description>- AuthTransactionId: If PEX was able to match a settlement to an authorization, the matched ID will be in this field.<br/></description></item>
            <item><description>- TransactionAmount: Received from the merchant as the total of the transaction.<br/></description></item>
            <item><description>- PaddingAmount: Added to fuel purchases ($49.00).<br/></description></item>
            <item><description>- TransactionType: Network (purchase or return) or Transfer (funding from business PEX Account).<br/></description></item>
            <item><description>- TransactionNotes: Text notes added by the cardholder or PEX administrator for accounting purposes.<br/></description></item>
            <item><description>- IsPending: If true, the merchant has not settled the transaction. PEX is holding the funds.<br/></description></item>
            <item><description>- IsDecline: The authorization was not successful.<br/></description></item>
            <item><description>- MerchantName: The merchant name provided in the Visa transaction.<br/></description></item>
            <item><description>- MCCCode: The 4 digit code assigned by Visa to categorize the type of merchant.<br/></description></item>
            <item><description>- TransferToOrFromAccountId: If a funding transaction, this will be the PEX account ID.<br/></description></item>
            <item><description>- PageSize: Total page size, 30,000.<br/></description></item>
            <item><description>- TotalRecords: Number of transactions returned for the time period.<br/></description></item>
            <item><description>- NumberofPages: Indicator of how many calls must be made to return all the records for the time period.<br/></description></item>
            <item><description>- LastTimeRetrieved: The date/time of the last record returned.<br/></description></item>
            <item><description>- TransactionTags: Transaction tags.<br/></description></item>
            <item><description>- SourceCurrencyCodeDescription : Currency code description of the amount spent, in local currency.  E.g. if a PEX card is used to make a purchase in Canada this field will have the value = Canadian Dollar. For an exhaustive list of ISO standard currency, please refer to https://www.iso.org/iso-4217-currency-codes.html <br/></description></item>
            <item><description>- SourceCurrencyNumericCode : Currency numeric code of the amount spent, in local currency. E.g. if a PEX card is used to make a purchase in Canada this field will have the value = 124. For an exhaustive list of ISO standard currency numeric code, please refer to https://www.iso.org/iso-4217-currency-codes.html   <br/></description></item>
            <item><description>- SourceAmount : Amount spent in local currency where transaction took place.<br/></description></item>
            <item><description>- TransactionTypeCategory : This gives more information about TransactionType. For TransactionType = Transfer there could be multiple TransactionTypeCatagory such as Business account fee or Card account fee etc.<br/></description></item>
            <item><description>- MetadataApprovalStatus : Specifies the status of the metadata (Tags, receipt image file) associated with transaction. Possible values Approved, Rejected, Ignored, Not Reviewed.<br/></description></item>
            </list>
            <br/>
            Details about why a transaction was declined is provided in the "Description" field. Potential values for the message include:<br/>
            <list type="number">
            <item><description>- Transaction exceeded current card balance<br/></description></item>
            <item><description>- Transaction exceeded daily spend limit<br/></description></item>
            <item><description>- International transactions not allowed<br/></description></item>
            <item><description>- Expired card<br/></description></item>
            <item><description>- Address does not match<br/></description></item>
            <item><description>- Unauthorized merchant<br/></description></item>
            <item><description>- Card not present<br/></description></item>
            <item><description>- Unauthorized geographic location<br/></description></item>
            <item><description>- Unauthorized merchant category: &lt;category&gt;<br/></description></item>
            <item><description>- Insufficient balance in PEX Account<br/></description></item>
            <item><description>- Remote service decline<br/></description></item>
            <item><description>- Do not honor<br/></description></item>
            </list>

*HTTP Request*
`***GET*** /Details/AllCardholderTransactions` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| IncludePendings | query | 1 to include pending transactions and 0 to exclude | No | boolean |
| IncludeDeclines | query | 1 to include decline transactions and 0 to exclude | No | boolean |
| StartDate | query | YYYY-MM-DDThh:mm:ss | Yes | dateTime |
| EndDate | query | YYYY-MM-DDThh:mm:ss | Yes | dateTime |
| Authorization | header | token {USERTOKEN} | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |

##Network Transaction Details
### GET Details For All Cards 
```shell
# You can also use wget
curl -X GET https://coreapi.pexcard.com/v4/Details/{Id}/NetworkTransactions?StartDate=2018-09-05T19%3A02%3A19Z&EndDate=2018-09-05T19%3A02%3A19Z \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
GET https://coreapi.pexcard.com/v4/Details/{Id}/NetworkTransactions?StartDate=2018-09-05T19%3A02%3A19Z&EndDate=2018-09-05T19%3A02%3A19Z HTTP/1.1
Host: coreapi.pexcard.com

Accept: application/json
Authorization: string

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/Details/{Id}/NetworkTransactions',
  method: 'get',
  data: '?StartDate=2018-09-05T19%3A02%3A19Z&EndDate=2018-09-05T19%3A02%3A19Z',
  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');

const headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/Details/{Id}/NetworkTransactions?StartDate=2018-09-05T19%3A02%3A19Z&EndDate=2018-09-05T19%3A02%3A19Z',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.get 'https://coreapi.pexcard.com/v4/Details/{Id}/NetworkTransactions',
  params: {
  'StartDate' => 'string(date-time)',
'EndDate' => 'string(date-time)'
}, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.get('https://coreapi.pexcard.com/v4/Details/{Id}/NetworkTransactions', params={
  'StartDate': '2018-09-05T19:02:19Z',  'EndDate': '2018-09-05T19:02:19Z'
}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/Details/{Id}/NetworkTransactions?StartDate=2018-09-05T19%3A02%3A19Z&EndDate=2018-09-05T19%3A02%3A19Z");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "https://coreapi.pexcard.com/v4/Details/{Id}/NetworkTransactions", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

> Example responses

> 200 Response

```json
{
  "TransactionList": [
    {
      "NetworkTransactionId": 0,
      "TransactionId": 0,
      "AcctId": 0,
      "TransactionTime": "",
      "HoldTime": "",
      "SettlementTime": "",
      "MerchantLocalTime": "",
      "AuthTransactionId": 0,
      "TransactionAmount": 0,
      "PaddingAmount": 0,
      "AvailableBalance": 0,
      "LedgerBalance": 0,
      "TransactionType": "",
      "Description": "",
      "TransactionNotes": [
        {
          "NoteId": 0,
          "UserName": "",
          "NoteText": "",
          "NoteDate": ""
        }
      ],
      "ReferencedTranId": 0,
      "ReferencedTransactionTime": "",
      "MerchantName": "",
      "MerchantCity": "",
      "MerchantState": "",
      "MerchantZip": "",
      "MerchantCountry": "",
      "MCCCode": "",
      "AuthIdentityResponseCode": "",
      "MerchantId": "",
      "TerminalId": "",
      "NetworkType": "",
      "NetworkStatus": "",
      "IsCardPresent": false,
      "Message": "",
      "MessageCode": "",
      "MerchantRequestedAmount": 0
    }
  ]
}
```
**Summary:** Returns all network transaction for specified card account ID. Examples: Authorization, Settlement, Reversal, PIN transaction, Decline.

**Description:** This call is only for network transactions. Card funding transactions are not included. In case you miss webhook call  for any reason, you can use this endpoint to retrieve same information.<br/>
            <br/>
            Please make sure time frame selected between StartDate and EndDate is no more than last 12 months.<br/>
            <br/>
            Return a list of network transaction details, within a specified start and end date, for the given card account ID.<br/>
            <br/>
            Definition of some of the network transaction detail fields:<br/>
            <list type="number">
            <item><description>- NetworkTransactionId: Unique Id for all the related network transactions (e.g. chain of authorization, settlement, etc).<br/></description></item>
            <item><description>- TransactionId: Unique Id for transaction.<br/></description></item>
            <item><description>- AcctId: Unique Id for cardholder account Id.<br/></description></item>
            <item><description>- TransactionTime: Eastern time. The date/time when authorization was received from the Network.<br/></description></item>
            <item><description>- HoldTime: Eastern time. Date/time a hold was placed on the card account balance. Null for Declines.<br/></description></item>
            <item><description>- SettlementTime: Eastern time. Funds have been transferred to the merchant and the transaction is final. Use this for reconciliation purposes. Null for Pendings and Declines.<br/></description></item>
            <item><description>- MerchantLocalTime: Local time. Date/time provided by the merchant for the transaction. This is controlled by the merchant and may not be accurate.<br/></description></item>
            <item><description>- AuthTransactionId: If PEX was able to match a settlement to an authorization, the matched ID will be in this field.<br/></description></item>
            <item><description>- TransactionAmount: Received from the merchant as the total of the transaction.<br/></description></item>
            <item><description>- PaddingAmount: Added to restaurant (20%) and fuel ($49.00) purchases.<br/></description></item>
            <item><description>- AvailableBalance: What the cardholder has access to spend. It is the ledger balance minus pending transactions.<br/></description></item>
            <item><description>- LedgerBalance: The total funds allocated to the card.<br/></description></item>
            <item><description>- TransactionType: Network (purchase or return) or Transfer (funding from business PEX Account).<br/></description></item>
            <item><description>- Description: More information about the transaction.<br/></description></item>
            <item><description>- TransactionNotes: Text notes added by the cardholder or PEX administrator for accounting purposes.<br/></description></item>
            <item><description>- ReferencedTranId: Unique Id which refers back to network transaction that precedes to the current one (e.g. ReferenceTranId on Settlement transaction refers to id on predecessor network transaction i.e. Authorization transaction).<br/></description></item>
            <item><description>- ReferencedTransactionTime: The date/time when referenced transaction was received from the Network. Eastern Standard time.<br/></description></item>
            <item><description>- MerchantName: The merchant name provided in the Visa transaction.<br/></description></item>
            <item><description>- MerchantCity: The merchant city provided in the Visa transaction.<br/></description></item>
            <item><description>- MerchantState: The merchant state provided in the Visa transaction.<br/></description></item>
            <item><description>- MerchantZip: The merchant address zip code provided in the Visa transaction.<br/></description></item>
            <item><description>- MerchantCountry: The merchant country provided in the Visa transaction.<br/></description></item>
            <item><description>- MCCCode: The 4 digit code assigned by Visa to categorize the type of merchant.<br/></description></item>
            <item><description>- AuthIdentityResponseCode: Authorization Identification Response code from Star data element 38 in Auth Response message.<br/></description></item>
            <item><description>- MerchantId: Unique Id for merchant provided in Visa transaction.<br/></description></item>
            <item><description>- TerminalId: Unique Id for POS terminal.<br/></description></item>
            <item><description>- NetworkType: Specify the type of event.<br/></description></item>
            <item><description>- NetworkStatus: Specify the status of the network event, Approved/Declined.<br/></description></item>
            <item><description>- IsCardPresent: Boolean parameter, indicates if card was actually physically swiped at POS or used other way e.g over internet or phone etc.<br/></description></item>
            <item><description>- Message: In case of declined transaction, Transaction Decline reason can be found here.<br/></description></item>
            <item><description>- MessageCode: Codes for decline reason.<br/></description></item>
            <item><description>- MerchantRequestedAmount: The amount which merchant requests at the POS to complete the transaction.<br/></description></item>
            </list>
            <br/>
            Details about why a transaction was declined is provided in the "Message" field.<br/>
            You can find list of message codes and corresponding messages <a href="https://developer.pexcard.com/documentation/web-hooks/message-codes" target="_blank">here</a>

*HTTP Request*
`***GET*** /Details/{Id}/NetworkTransactions` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| Id | path | Unique Id for cardholder account Id | Yes | integer |
| StartDate | query | YYYY-MM-DDThh:mm:ss | Yes | dateTime |
| EndDate | query | YYYY-MM-DDThh:mm:ss | Yes | dateTime |
| Authorization | header | token {USERTOKEN} | Yes | string |



**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Success |
| 403 | Invalid card account ID |


### GET Details for Card Account
```shell
# You can also use wget
curl -X GET https://coreapi.pexcard.com/v4/Details/{Id}/NetworkTransactions?StartDate=2018-09-05T19%3A02%3A19Z&EndDate=2018-09-05T19%3A02%3A19Z \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
GET https://coreapi.pexcard.com/v4/Details/{Id}/NetworkTransactions?StartDate=2018-09-05T19%3A02%3A19Z&EndDate=2018-09-05T19%3A02%3A19Z HTTP/1.1
Host: coreapi.pexcard.com

Accept: application/json
Authorization: string

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/Details/{Id}/NetworkTransactions',
  method: 'get',
  data: '?StartDate=2018-09-05T19%3A02%3A19Z&EndDate=2018-09-05T19%3A02%3A19Z',
  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');

const headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/Details/{Id}/NetworkTransactions?StartDate=2018-09-05T19%3A02%3A19Z&EndDate=2018-09-05T19%3A02%3A19Z',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.get 'https://coreapi.pexcard.com/v4/Details/{Id}/NetworkTransactions',
  params: {
  'StartDate' => 'string(date-time)',
'EndDate' => 'string(date-time)'
}, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.get('https://coreapi.pexcard.com/v4/Details/{Id}/NetworkTransactions', params={
  'StartDate': '2018-09-05T19:02:19Z',  'EndDate': '2018-09-05T19:02:19Z'
}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/Details/{Id}/NetworkTransactions?StartDate=2018-09-05T19%3A02%3A19Z&EndDate=2018-09-05T19%3A02%3A19Z");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "https://coreapi.pexcard.com/v4/Details/{Id}/NetworkTransactions", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

> Example responses

> 200 Response

```json
{
  "TransactionList": [
    {
      "NetworkTransactionId": 0,
      "TransactionId": 0,
      "AcctId": 0,
      "TransactionTime": "",
      "HoldTime": "",
      "SettlementTime": "",
      "MerchantLocalTime": "",
      "AuthTransactionId": 0,
      "TransactionAmount": 0,
      "PaddingAmount": 0,
      "AvailableBalance": 0,
      "LedgerBalance": 0,
      "TransactionType": "",
      "Description": "",
      "TransactionNotes": [
        {
          "NoteId": 0,
          "UserName": "",
          "NoteText": "",
          "NoteDate": ""
        }
      ],
      "ReferencedTranId": 0,
      "ReferencedTransactionTime": "",
      "MerchantName": "",
      "MerchantCity": "",
      "MerchantState": "",
      "MerchantZip": "",
      "MerchantCountry": "",
      "MCCCode": "",
      "AuthIdentityResponseCode": "",
      "MerchantId": "",
      "TerminalId": "",
      "NetworkType": "",
      "NetworkStatus": "",
      "IsCardPresent": false,
      "Message": "",
      "MessageCode": "",
      "MerchantRequestedAmount": 0
    }
  ]
}
```
**Summary:** Returns all network transaction for specified card account ID. Examples: Authorization, Settlement, Reversal, PIN transaction, Decline.

**Description:** This call is only for network transactions. Card funding transactions are not included. In case you miss webhook call  for any reason, you can use this endpoint to retrieve same information.<br/>
            <br/>
            Please make sure time frame selected between StartDate and EndDate is no more than last 12 months.<br/>
            <br/>
            Return a list of network transaction details, within a specified start and end date, for the given card account ID.<br/>
            <br/>
            Definition of some of the network transaction detail fields:<br/>
            <list type="number">
            <item><description>- NetworkTransactionId: Unique Id for all the related network transactions (e.g. chain of authorization, settlement, etc).<br/></description></item>
            <item><description>- TransactionId: Unique Id for transaction.<br/></description></item>
            <item><description>- AcctId: Unique Id for cardholder account Id.<br/></description></item>
            <item><description>- TransactionTime: Eastern time. The date/time when authorization was received from the Network.<br/></description></item>
            <item><description>- HoldTime: Eastern time. Date/time a hold was placed on the card account balance. Null for Declines.<br/></description></item>
            <item><description>- SettlementTime: Eastern time. Funds have been transferred to the merchant and the transaction is final. Use this for reconciliation purposes. Null for Pendings and Declines.<br/></description></item>
            <item><description>- MerchantLocalTime: Local time. Date/time provided by the merchant for the transaction. This is controlled by the merchant and may not be accurate.<br/></description></item>
            <item><description>- AuthTransactionId: If PEX was able to match a settlement to an authorization, the matched ID will be in this field.<br/></description></item>
            <item><description>- TransactionAmount: Received from the merchant as the total of the transaction.<br/></description></item>
            <item><description>- PaddingAmount: Added to restaurant (20%) and fuel ($49.00) purchases.<br/></description></item>
            <item><description>- AvailableBalance: What the cardholder has access to spend. It is the ledger balance minus pending transactions.<br/></description></item>
            <item><description>- LedgerBalance: The total funds allocated to the card.<br/></description></item>
            <item><description>- TransactionType: Network (purchase or return) or Transfer (funding from business PEX Account).<br/></description></item>
            <item><description>- Description: More information about the transaction.<br/></description></item>
            <item><description>- TransactionNotes: Text notes added by the cardholder or PEX administrator for accounting purposes.<br/></description></item>
            <item><description>- ReferencedTranId: Unique Id which refers back to network transaction that precedes to the current one (e.g. ReferenceTranId on Settlement transaction refers to id on predecessor network transaction i.e. Authorization transaction).<br/></description></item>
            <item><description>- ReferencedTransactionTime: The date/time when referenced transaction was received from the Network. Eastern Standard time.<br/></description></item>
            <item><description>- MerchantName: The merchant name provided in the Visa transaction.<br/></description></item>
            <item><description>- MerchantCity: The merchant city provided in the Visa transaction.<br/></description></item>
            <item><description>- MerchantState: The merchant state provided in the Visa transaction.<br/></description></item>
            <item><description>- MerchantZip: The merchant address zip code provided in the Visa transaction.<br/></description></item>
            <item><description>- MerchantCountry: The merchant country provided in the Visa transaction.<br/></description></item>
            <item><description>- MCCCode: The 4 digit code assigned by Visa to categorize the type of merchant.<br/></description></item>
            <item><description>- AuthIdentityResponseCode: Authorization Identification Response code from Star data element 38 in Auth Response message.<br/></description></item>
            <item><description>- MerchantId: Unique Id for merchant provided in Visa transaction.<br/></description></item>
            <item><description>- TerminalId: Unique Id for POS terminal.<br/></description></item>
            <item><description>- NetworkType: Specify the type of event.<br/></description></item>
            <item><description>- NetworkStatus: Specify the status of the network event, Approved/Declined.<br/></description></item>
            <item><description>- IsCardPresent: Boolean parameter, indicates if card was actually physically swiped at POS or used other way e.g over internet or phone etc.<br/></description></item>
            <item><description>- Message: In case of declined transaction, Transaction Decline reason can be found here.<br/></description></item>
            <item><description>- MessageCode: Codes for decline reason.<br/></description></item>
            <item><description>- MerchantRequestedAmount: The amount which merchant requests at the POS to complete the transaction.<br/></description></item>
            </list>
            <br/>
            Details about why a transaction was declined is provided in the "Message" field.<br/>
            You can find list of message codes and corresponding messages <a href="https://developer.pexcard.com/documentation/web-hooks/message-codes" target="_blank">here</a>

**HTTP Request**
`***GET*** /Details/{Id}/NetworkTransactions` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| Id | path | Unique Id for cardholder account Id | Yes | integer |
| StartDate | query | YYYY-MM-DDThh:mm:ss | Yes | dateTime |
| EndDate | query | YYYY-MM-DDThh:mm:ss | Yes | dateTime |
| Authorization | header | token {USERTOKEN} | Yes | string |



**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Success |
| 403 | Invalid card account ID |



## Account Details
### GET All Card Account Data 
```shell
# You can also use wget
curl -X GET https://coreapi.pexcard.com/v4/Details/AccountDetails \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
GET https://coreapi.pexcard.com/v4/Details/AccountDetails HTTP/1.1
Host: coreapi.pexcard.com

Accept: application/json
Authorization: string

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/Details/AccountDetails',
  method: 'get',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');

const headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/Details/AccountDetails',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.get 'https://coreapi.pexcard.com/v4/Details/AccountDetails',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.get('https://coreapi.pexcard.com/v4/Details/AccountDetails', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/Details/AccountDetails");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "https://coreapi.pexcard.com/v4/Details/AccountDetails", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

> Example responses

> 200 Response

```json
{
  "BusinessAccountId": 0,
  "BusinessName": "",
  "BusinessAccountStatus": "",
  "BusinessAccountBalance": 0,
  "PendingTransferAmount": 0,
  "BankAccountList": [
    {
      "ExternalBankAcctId": 0,
      "RoutingNumber": "",
      "BankAccountNumber": "",
      "BankName": "",
      "BankAccountType": "",
      "IsActive": false
    }
  ],
  "CHAccountList": [
    {
      "AccountId": 0,
      "FirstName": "",
      "LastName": "",
      "LedgerBalance": 0,
      "AvailableBalance": 0,
      "AccountStatus": "",
      "IsVirtual": false,
      "CustomId": ""
    }
  ],
  "CardholderGroups": [
    {
      "Id": 0,
      "Name": ""
    }
  ]
}
```
**Summary:** Return all accounts associated with your business

**Description:** Return all accounts associated with your business, including registered external business checking accounts and all PEX business accounts.<br/>
            <br/>
            Reasons you will use this call:<br/>
            <list type="number">
            <item><description>- One-time transfer: To retrieve or create a one-time transfer requires an ExternalBankAcctId<br/></description></item>
            <item><description>- Business: Use field  BusinessAccountBalance to monitor the available balance in your PEX business account for fund disbursement. You must have a minimum of $50.00 in your PEX Card business account at all times. The system will not allow you to allocate the last $50.00 to cards.<br/></description></item>
            <item><description>- Cards: To edit, fund, delete or create funding and spend rules, you will need the AccountID for the card. Also, this call will give you the available balance and status on all card accounts.<br/></description></item>
            <item><description>- Groups: To find the group name associated with each unique GroupID.<br/></description></item>
            <item><description>- IsVirtual: If this is connected to a virtual card order then the value is: true, otherwise, false.<br/></description></item>
            <item><description>- CustomId: User defined Id which can be assigned to Card holder profile (alphanumeric up to 50 characters). This is optional field. <br/></description></item>
            </list>

*HTTP Request*
`***GET*** /Details/AccountDetails` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| Authorization | header | token {USERTOKEN} | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Success |


###GET Card Account Data
```shell
# You can also use wget
curl -X GET https://coreapi.pexcard.com/v4/Details/AccountDetails/{Id} \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
GET https://coreapi.pexcard.com/v4/Details/AccountDetails/{Id} HTTP/1.1
Host: coreapi.pexcard.com

Accept: application/json
Authorization: string

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/Details/AccountDetails/{Id}',
  method: 'get',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');

const headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/Details/AccountDetails/{Id}',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.get 'https://coreapi.pexcard.com/v4/Details/AccountDetails/{Id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.get('https://coreapi.pexcard.com/v4/Details/AccountDetails/{Id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/Details/AccountDetails/{Id}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "https://coreapi.pexcard.com/v4/Details/AccountDetails/{Id}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

> Example responses

> 200 Response

```json
{
  "AccountId": 0,
  "Group": {
    "Id": 0,
    "GroupName": ""
  },
  "AccountStatus": "",
  "LedgerBalance": 0,
  "AvailableBalance": 0,
  "ProfileAddress": {
    "ContactName": "",
    "AddressLine1": "",
    "AddressLine2": "",
    "City": "",
    "State": "",
    "PostalCode": "",
    "Country": ""
  },
  "Phone": "",
  "ShippingAddress": {
    "ContactName": "",
    "AddressLine1": "",
    "AddressLine2": "",
    "City": "",
    "State": "",
    "PostalCode": "",
    "Country": ""
  },
  "ShippingPhone": "",
  "DateOfBirth": "",
  "Email": "",
  "IsVirtual": false,
  "CardList": [
    {
      "CardId": 0,
      "IssuedDate": "",
      "ExpirationDate": "",
      "Last4CardNumber": "",
      "CardStatus": ""
    }
  ],
  "SpendingRulesetId": 0,
  "SpendRules": {
    "UseMerchantCategory": false,
    "MerchantCategories": {
      "AssociationsAndOrganizations": false,
      "AutomotiveDealers": false,
      "EducationalServices": false,
      "Entertainment": false,
      "FuelAndConvenienceStores": false,
      "GroceryStores": false,
      "HealthcareAndChildcareServices": false,
      "ProfessionalServices": false,
      "Restaurants": false,
      "RetailStores": false,
      "TravelAndTransportation": false,
      "FuelPumpOnly": false,
      "HardwareStores": false
    },
    "InternationalSpendEnabled": false,
    "IsDailySpendLimitEnabled": false,
    "DailySpendLimit": 0,
    "CardNotPresentUse": false,
    "UsePexAccountBalanceForAuths": false,
    "UseCustomerAuthDecision": false
  },
  "ScheduledFunding": {
    "Amount": 0,
    "Frequency": 0
  },
  "LowBalanceFunding": {
    "ThresholdAmount": 0,
    "AmountToFund": 0
  },
  "CustomId": ""
}
```
**Summary:** Return all data associated with a single card account

**Description:** Return all data associated with a single card account.<br/>
            <br/>
            Definition of some of the returned fields and how the PEX system uses them:<br/>
            <list type="number">
            <item><description>- Group: An administrator defined category that can be used for sorting and reporting.<br/> </description></item>
            <item><description>- Account Status: Either open or closed. A closed account cannot be reopened.<br/></description></item>
            <item><description>- Ledger balance: The total funds allocated to the card.<br/></description></item>
            <item><description>- Available balance: What the cardholder has access to spend. It is the ledger balance minus pending transactions.<br/></description></item>
            <item><description>- Profile address: The cardholder's billing address. This address may be validated by merchants in a card not present transaction (online and phone) or at a fuel pump. It is important that your cardholders know what their billing address is.<br/></description></item>
            <item><description>- Shipping address:  used for card mailing. PEX uses this address for all future card replacements including: lost, stolen, compromised and renewal.<br/></description></item>
            <item><description>- Card list: Contains all card numbers that have been issued to this account.<br/></description></item>
            <item><description>- Spend rules: Controls where and how much a card can be used. You can set limitations on international spending, merchant categories (MCCs) and the dollar amount spent per day. A definition of spend rules can be found under GET /Card/SpendRules/{Id}.<br/></description></item>
            <item><description>- Funding rules allow you to systematically add funds to a card balance.<br/></description></item>
            <item><description>- IsVirtual: If this is connected to a virtual card order then the value is: true, otherwise, false.<br/></description></item>
            <item><description>- CustomId: User defined Id which can be assigned to Card holder profile (alphanumeric up to 50 characters). This is optional field. <br/></description></item>
            </list>

**HTTP Request**
`***GET*** /Details/AccountDetails/{Id}` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| Id | path | Card account ID | Yes | integer |
| Authorization | header | token {USERTOKEN} | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Success |
| 403 | <list type="number">    <item>      <description>- Invalid card account ID<br /></description>    </item>    <item>      <description>- Must be card account ID</description>    </item>  </list> |



###GET Card Account Data Advanced
```shell
# You can also use wget
curl -X GET https://coreapi.pexcard.com/v4/Details/AccountDetails/{Id}/Advanced \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
GET https://coreapi.pexcard.com/v4/Details/AccountDetails/{Id}/Advanced HTTP/1.1
Host: coreapi.pexcard.com

Accept: application/json
Authorization: string

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/Details/AccountDetails/{Id}/Advanced',
  method: 'get',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');

const headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/Details/AccountDetails/{Id}/Advanced',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.get 'https://coreapi.pexcard.com/v4/Details/AccountDetails/{Id}/Advanced',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.get('https://coreapi.pexcard.com/v4/Details/AccountDetails/{Id}/Advanced', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/Details/AccountDetails/{Id}/Advanced");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "https://coreapi.pexcard.com/v4/Details/AccountDetails/{Id}/Advanced", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

> Example responses

> 200 Response

```json
{
  "AccountId": 0,
  "Group": {
    "Id": 0,
    "GroupName": ""
  },
  "AccountStatus": "",
  "LedgerBalance": 0,
  "AvailableBalance": 0,
  "ProfileAddress": {
    "ContactName": "",
    "AddressLine1": "",
    "AddressLine2": "",
    "City": "",
    "State": "",
    "PostalCode": "",
    "Country": ""
  },
  "Phone": "",
  "ShippingAddress": {
    "ContactName": "",
    "AddressLine1": "",
    "AddressLine2": "",
    "City": "",
    "State": "",
    "PostalCode": "",
    "Country": ""
  },
  "ShippingPhone": "",
  "DateOfBirth": "",
  "Email": "",
  "IsVirtual": false,
  "CardList": [
    {
      "CardId": 0,
      "IssuedDate": "",
      "ExpirationDate": "",
      "Last4CardNumber": "",
      "CardStatus": ""
    }
  ],
  "SpendingRulesetId": 0,
  "SpendRules": {
    "MerchantCategories": [
      {
        "Id": 0,
        "Name": "",
        "Description": "",
        "TransactionLimit": 0,
        "DailySpendLimit": 0,
        "WeeklySpendLimit": 0,
        "MonthlySpendLimit": 0,
        "YearlySpendLimit": 0,
        "LifetimeSpendLimit": 0
      }
    ],
    "InternationalSpendEnabled": false,
    "IsDailySpendLimitEnabled": false,
    "DailySpendLimit": 0,
    "WeeklySpendLimit": 0,
    "MonthlySpendLimit": 0,
    "YearlySpendLimit": 0,
    "LifetimeSpendLimit": 0,
    "CardNotPresentUse": false,
    "UsePexAccountBalanceForAuths": false,
    "UseCustomerAuthDecision": false
  },
  "ScheduledFunding": {
    "Amount": 0,
    "Frequency": 0
  },
  "LowBalanceFunding": {
    "ThresholdAmount": 0,
    "AmountToFund": 0
  },
  "CustomId": ""
}
```
**Summary:** Return all data associated with a single card account

**Description:** Return all data associated with a single card account.<br/>
            <br/>
            Definition of some of the returned fields and how the PEX system uses them:<br/>
            <list type="number">
            <item><description>- Group: An administrator defined category that can be used for sorting and reporting.<br/> </description></item>
            <item><description>- Account Status: Either open or closed. A closed account cannot be reopened.<br/></description></item>
            <item><description>- Ledger balance: The total funds allocated to the card.<br/></description></item>
            <item><description>- Available balance: What the cardholder has access to spend. It is the ledger balance minus pending transactions.<br/></description></item>
            <item><description>- Profile address: The cardholder's billing address. This address may be validated by merchants in a card not present transaction (online and phone) or at a fuel pump. It is important that your cardholders know what their billing address is.<br/></description></item>
            <item><description>- Shipping address:  used for card mailing. PEX uses this address for all future card replacements including: lost, stolen, compromised and renewal.<br/></description></item>
            <item><description>- Card list: Contains all card numbers that have been issued to this account.<br/></description></item>
            <item><description>- Spend rules: Controls where and how much a card can be used. You can set limitations on international spending, merchant categories (MCCs) and the dollar amount spent per day. A definition of spend rules can be found under GET /Card/SpendRules/{Id}.<br/></description></item>
            <item><description>- Funding rules allow you to systematically add funds to a card balance.<br/></description></item>
            <item><description>- IsVirtual: If this is connected to a virtual card order then the value is: true, otherwise, false.<br/></description></item>
            <item><description>- CustomId: User defined Id which can be assigned to Card holder profile (alphanumeric up to 50 characters). This is optional field. <br/></description></item>
            </list>

**HTTP Request**
`***GET*** /Details/AccountDetails/{Id}/Advanced` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| Id | path | Card account ID | Yes | integer |
| Authorization | header | token {USERTOKEN} | Yes | string |


**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Success |
| 403 | <list type="number">    <item>      <description>- Invalid card account ID<br /></description>    </item>    <item>      <description>- Must be card account ID</description>    </item>  </list> |


##All Cardholder
###Transaction Count 
```shell
# You can also use wget
curl -X GET https://coreapi.pexcard.com/v4/Details/AllCardholderTransactionCount?StartDate=2018-09-05T19%3A02%3A19Z&EndDate=2018-09-05T19%3A02%3A19Z \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
GET https://coreapi.pexcard.com/v4/Details/AllCardholderTransactionCount?StartDate=2018-09-05T19%3A02%3A19Z&EndDate=2018-09-05T19%3A02%3A19Z HTTP/1.1
Host: coreapi.pexcard.com

Accept: application/json
Authorization: string

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/Details/AllCardholderTransactionCount',
  method: 'get',
  data: '?StartDate=2018-09-05T19%3A02%3A19Z&EndDate=2018-09-05T19%3A02%3A19Z',
  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');

const headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/Details/AllCardholderTransactionCount?StartDate=2018-09-05T19%3A02%3A19Z&EndDate=2018-09-05T19%3A02%3A19Z',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.get 'https://coreapi.pexcard.com/v4/Details/AllCardholderTransactionCount',
  params: {
  'StartDate' => 'string(date-time)',
'EndDate' => 'string(date-time)'
}, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.get('https://coreapi.pexcard.com/v4/Details/AllCardholderTransactionCount', params={
  'StartDate': '2018-09-05T19:02:19Z',  'EndDate': '2018-09-05T19:02:19Z'
}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/Details/AllCardholderTransactionCount?StartDate=2018-09-05T19%3A02%3A19Z&EndDate=2018-09-05T19%3A02%3A19Z");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "https://coreapi.pexcard.com/v4/Details/AllCardholderTransactionCount", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

> Example responses

> 200 Response

```json
0
```
**Summary:** Return a count of transactions for the authenticated user

**Description:** Please make sure time frame selected between StartDate and EndDate is no more than last 12 months.<br/>
            <br/>
            Return a count of transactions, within a specified start and end date, for all card accounts associated with the business of the authenticated user. Fields  IsPending  and  IsDecline  can be set to true or false as required.

**HTTP Request**
`***GET*** /Details/AllCardholderTransactionCount` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| IncludePendings | query | 1 to include pending transactions and 0 to exclude | No | boolean |
| IncludeDeclines | query | 1 to include decline transactions and 0 to exclude | No | boolean |
| StartDate | query | YYYY-MM-DDThh:mm:ss | Yes | dateTime |
| EndDate | query | YYYY-MM-DDThh:mm:ss | Yes | dateTime |
| Authorization | header | token {USERTOKEN} | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Success |

###Transaction Details 

```shell
# You can also use wget
curl -X GET https://coreapi.pexcard.com/v4/Details/AllCardholderTransactions?StartDate=2018-09-05T19%3A02%3A19Z&EndDate=2018-09-05T19%3A02%3A19Z \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
GET https://coreapi.pexcard.com/v4/Details/AllCardholderTransactions?StartDate=2018-09-05T19%3A02%3A19Z&EndDate=2018-09-05T19%3A02%3A19Z HTTP/1.1
Host: coreapi.pexcard.com

Accept: application/json
Authorization: string

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/Details/AllCardholderTransactions',
  method: 'get',
  data: '?StartDate=2018-09-05T19%3A02%3A19Z&EndDate=2018-09-05T19%3A02%3A19Z',
  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');

const headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/Details/AllCardholderTransactions?StartDate=2018-09-05T19%3A02%3A19Z&EndDate=2018-09-05T19%3A02%3A19Z',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.get 'https://coreapi.pexcard.com/v4/Details/AllCardholderTransactions',
  params: {
  'StartDate' => 'string(date-time)',
'EndDate' => 'string(date-time)'
}, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.get('https://coreapi.pexcard.com/v4/Details/AllCardholderTransactions', params={
  'StartDate': '2018-09-05T19:02:19Z',  'EndDate': '2018-09-05T19:02:19Z'
}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/Details/AllCardholderTransactions?StartDate=2018-09-05T19%3A02%3A19Z&EndDate=2018-09-05T19%3A02%3A19Z");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "https://coreapi.pexcard.com/v4/Details/AllCardholderTransactions", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

> Example responses

> 200 Response

```json
{
  "TransactionList": [
    {
      "TransactionId": 0,
      "AcctId": 0,
      "TransactionTime": "",
      "MerchantLocalTime": "",
      "HoldTime": "",
      "SettlementTime": "",
      "AuthTransactionId": 0,
      "TransactionAmount": 0,
      "PaddingAmount": 0,
      "TransactionType": 1,
      "Description": "",
      "TransactionNotes": [
        {
          "NoteId": 0,
          "UserName": "",
          "NoteText": "",
          "NoteDate": ""
        }
      ],
      "IsPending": false,
      "IsDecline": false,
      "MerchantName": "",
      "MerchantCity": "",
      "MerchantState": "",
      "MerchantZip": "",
      "MerchantCountry": "",
      "MCCCode": "",
      "TransferToOrFromAccountId": 0,
      "AuthIdentityResponseCode": "",
      "MerchantId": "",
      "TerminalId": "",
      "NetworkTransactionId": 0,
      "SourceCurrencyCodeDescription": "",
      "SourceCurrencyNumericCode": "",
      "SourceAmount": 0,
      "TransactionTags": {
        "Tags": [
          {
            "FieldId": "",
            "Value": {},
            "Name": ""
          }
        ],
        "State": 0,
        "FieldsVersion": ""
      },
      "MetadataApprovalStatus": "",
      "TransactionTypeCategory": ""
    }
  ],
  "Pages": {
    "PageSize": 0,
    "TotalRecords": 0,
    "NumberOfPages": 0,
    "LastTimeRetrieved": ""
  }
}
```

**Summary:** Return a list of all card transactions for the business

**Description:** Please make sure time frame selected between StartDate and EndDate is no more than last 12 months.<br/>
            <br/>
            Return a list of transaction details, within a specified start and end date, for all card accounts associated with the business of the authenticated user. Fields IsPending and IsDecline can be set to true or false as required.<br/>
            <br/>
            If, for the time-frame selected, over 30,000 transactions are returned then the results will be paginated. To retrieve more data, use the  LastTimeRetrieved  field returned in the StartDate parameter and repeat the call until the NumberOfPages field = 1. (Note: the last transaction for the page will be the first transaction retrieved in the next call, use the TransactionId to eliminate duplicate records.)<br/>
            <br/>
            Definition of some of the transaction detail fields:<br/>
            <list type="number">
            <item><description>- TransactionTime: Eastern time. The date/time when authorization was received from the Network.<br/></description></item>
            <item><description>- SettlementTime: Eastern time. Funds have been transferred to the merchant and the transaction is final. Use this for reconciliation purposes. Null for Pendings and Declines.<br/></description></item>
            <item><description>- HoldTime: Eastern time. Date/time a hold was placed on the card account balance. Null for Declines.<br/></description></item>
            <item><description>- MerchantLocalTime: Local time. Date/time provided by the merchant for the transaction. This is controlled by the merchant and may not be accurate.<br/></description></item>
            <item><description>- AuthTransactionId: If PEX was able to match a settlement to an authorization, the matched ID will be in this field.<br/></description></item>
            <item><description>- TransactionAmount: Received from the merchant as the total of the transaction.<br/></description></item>
            <item><description>- PaddingAmount: Added to fuel purchases ($49.00).<br/></description></item>
            <item><description>- TransactionType: Network (purchase or return) or Transfer (funding from business PEX Account).<br/></description></item>
            <item><description>- TransactionNotes: Text notes added by the cardholder or PEX administrator for accounting purposes.<br/></description></item>
            <item><description>- IsPending: If true, the merchant has not settled the transaction. PEX is holding the funds.<br/></description></item>
            <item><description>- IsDecline: The authorization was not successful.<br/></description></item>
            <item><description>- MerchantName: The merchant name provided in the Visa transaction.<br/></description></item>
            <item><description>- MCCCode: The 4 digit code assigned by Visa to categorize the type of merchant.<br/></description></item>
            <item><description>- TransferToOrFromAccountId: If a funding transaction, this will be the PEX account ID.<br/></description></item>
            <item><description>- PageSize: Total page size, 30,000.<br/></description></item>
            <item><description>- TotalRecords: Number of transactions returned for the time period.<br/></description></item>
            <item><description>- NumberofPages: Indicator of how many calls must be made to return all the records for the time period.<br/></description></item>
            <item><description>- LastTimeRetrieved: The date/time of the last record returned.<br/></description></item>
            <item><description>- TransactionTags: Transaction tags.<br/></description></item>
            <item><description>- SourceCurrencyCodeDescription : Currency code description of the amount spent, in local currency.  E.g. if a PEX card is used to make a purchase in Canada this field will have the value = Canadian Dollar. For an exhaustive list of ISO standard currency, please refer to https://www.iso.org/iso-4217-currency-codes.html <br/></description></item>
            <item><description>- SourceCurrencyNumericCode : Currency numeric code of the amount spent, in local currency. E.g. if a PEX card is used to make a purchase in Canada this field will have the value = 124. For an exhaustive list of ISO standard currency numeric code, please refer to https://www.iso.org/iso-4217-currency-codes.html   <br/></description></item>
            <item><description>- SourceAmount : Amount spent in local currency where transaction took place.<br/></description></item>
            <item><description>- TransactionTypeCategory : This gives more information about TransactionType. For TransactionType = Transfer there could be multiple TransactionTypeCatagory such as Business account fee or Card account fee etc.<br/></description></item>
            <item><description>- MetadataApprovalStatus : Specifies the status of the metadata (Tags, receipt image file) associated with transaction. Possible values Approved, Rejected, Ignored, Not Reviewed.<br/></description></item>
            </list>
            <br/>
            Details about why a transaction was declined is provided in the "Description" field. Potential values for the message include:<br/>
            <list type="number">
            <item><description>- Transaction exceeded current card balance<br/></description></item>
            <item><description>- Transaction exceeded daily spend limit<br/></description></item>
            <item><description>- International transactions not allowed<br/></description></item>
            <item><description>- Expired card<br/></description></item>
            <item><description>- Address does not match<br/></description></item>
            <item><description>- Unauthorized merchant<br/></description></item>
            <item><description>- Card not present<br/></description></item>
            <item><description>- Unauthorized geographic location<br/></description></item>
            <item><description>- Unauthorized merchant category: &lt;category&gt;<br/></description></item>
            <item><description>- Insufficient balance in PEX Account<br/></description></item>
            <item><description>- Remote service decline<br/></description></item>
            <item><description>- Do not honor<br/></description></item>
            </list>

**HTTP Request**
`***GET*** /Details/AllCardholderTransactions` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| IncludePendings | query | 1 to include pending transactions and 0 to exclude | No | boolean |
| IncludeDeclines | query | 1 to include decline transactions and 0 to exclude | No | boolean |
| StartDate | query | YYYY-MM-DDThh:mm:ss | Yes | dateTime |
| EndDate | query | YYYY-MM-DDThh:mm:ss | Yes | dateTime |
| Authorization | header | token {USERTOKEN} | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |


##Transaction Details 
###Transaction Details 
```shell
# You can also use wget
curl -X GET https://coreapi.pexcard.com/v4/Details/TransactionDetails?StartDate=2018-09-05T19%3A02%3A19Z&EndDate=2018-09-05T19%3A02%3A19Z \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
GET https://coreapi.pexcard.com/v4/Details/TransactionDetails?StartDate=2018-09-05T19%3A02%3A19Z&EndDate=2018-09-05T19%3A02%3A19Z HTTP/1.1
Host: coreapi.pexcard.com

Accept: application/json
Authorization: string

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/Details/TransactionDetails',
  method: 'get',
  data: '?StartDate=2018-09-05T19%3A02%3A19Z&EndDate=2018-09-05T19%3A02%3A19Z',
  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');

const headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/Details/TransactionDetails?StartDate=2018-09-05T19%3A02%3A19Z&EndDate=2018-09-05T19%3A02%3A19Z',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.get 'https://coreapi.pexcard.com/v4/Details/TransactionDetails',
  params: {
  'StartDate' => 'string(date-time)',
'EndDate' => 'string(date-time)'
}, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.get('https://coreapi.pexcard.com/v4/Details/TransactionDetails', params={
  'StartDate': '2018-09-05T19:02:19Z',  'EndDate': '2018-09-05T19:02:19Z'
}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/Details/TransactionDetails?StartDate=2018-09-05T19%3A02%3A19Z&EndDate=2018-09-05T19%3A02%3A19Z");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "https://coreapi.pexcard.com/v4/Details/TransactionDetails", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

> Example responses

> 200 Response

```json
{
  "TransactionList": [
    {
      "TransactionId": 0,
      "AcctId": 0,
      "TransactionTime": "",
      "MerchantLocalTime": "",
      "HoldTime": "",
      "SettlementTime": "",
      "AuthTransactionId": 0,
      "TransactionAmount": 0,
      "PaddingAmount": 0,
      "TransactionType": 1,
      "Description": "",
      "TransactionNotes": [
        {
          "NoteId": 0,
          "UserName": "",
          "NoteText": "",
          "NoteDate": ""
        }
      ],
      "IsPending": false,
      "IsDecline": false,
      "MerchantName": "",
      "MerchantCity": "",
      "MerchantState": "",
      "MerchantZip": "",
      "MerchantCountry": "",
      "MCCCode": "",
      "TransferToOrFromAccountId": 0,
      "AuthIdentityResponseCode": "",
      "MerchantId": "",
      "TerminalId": "",
      "NetworkTransactionId": 0,
      "SourceCurrencyCodeDescription": "",
      "SourceCurrencyNumericCode": "",
      "SourceAmount": 0,
      "TransactionTags": {
        "Tags": [
          {
            "FieldId": "",
            "Value": {},
            "Name": ""
          }
        ],
        "State": 0,
        "FieldsVersion": ""
      },
      "MetadataApprovalStatus": "",
      "TransactionTypeCategory": ""
    }
  ],
  "Pages": {
    "PageSize": 0,
    "TotalRecords": 0,
    "NumberOfPages": 0,
    "LastTimeRetrieved": ""
  }
}
```
**Summary:** Return a list of transaction details for the authenticated user

**Description:** Please make sure time frame selected between StartDate and EndDate is no more than last 12 months.<br/>
            <br/>
            Return a list of transaction details, within a specified start and end date, for the authenticated user.<br/>
            <br/>
            If the token user is a PEX administrator, the transactions returned will be for the PEX business account. (Note: input fields IsPending and IsDecline should be false, as they don't apply to transactions on the business account.)<br/>
            <br/>
            If the token user is a cardholder (and you are a partner), the transactions returned will be for that card account. Fields IsPending and IsDecline can be set to true or false as required.<br/>
            <br/>
            If, for the time-frame selected, over 30,000 transactions are returned then the results will be paginated. To retrieve more data, use the LastTimeRetrieved field returned in the StartDate parameter and repeat the call until the NumberOfPages field = 1. (Note: the last transaction for the page will be the first transaction retrieved in the next call, use the TransactionId to eliminate duplicate records.)<br/>
            <br/>
            Definition of some of the transaction detail fields:<br/>
            <list type="number">
            <item><description>- TransactionTime: Eastern time. The date/time when authorization was received from the Network.<br/></description></item>
            <item><description>- SettlementTime: Eastern time. Funds have been transferred to the merchant and the transaction is final. Use this for reconciliation purposes. Null for Pendings and Declines.<br/></description></item>
            <item><description>- HoldTime: Eastern time. Date/time a hold was placed on the card account balance. Null for Declines.<br/></description></item>
            <item><description>- MerchantLocalTime: Local time. Date/time provided by the merchant for the transaction. This is controlled by the merchant and may not be accurate.<br/></description></item>
            <item><description>- AuthTransactionId: If PEX was able to match a settlement to an authorization, the matched ID will be in this field.<br/></description></item>
            <item><description>- TransactionAmount: Received from the merchant as the total of the transaction.<br/></description></item>
            <item><description>- PaddingAmount: Added to restaurant (20&#37;) and fuel ($49.00) purchases.<br/></description></item>
            <item><description>- TransactionType: Network (purchase or return) or Transfer (funding from business PEX Account).<br/></description></item>
            <item><description>- TransactionNotes: Text notes added by the cardholder or PEX administrator for accounting purposes.<br/></description></item>
            <item><description>- IsPending: If true, the merchant has not settled the transaction. PEX is holding the funds.<br/></description></item>
            <item><description>- IsDecline: The authorization was not successful.<br/></description></item>
            <item><description>- MerchantName: The merchant name provided in the Visa transaction.<br/></description></item>
            <item><description>- MCCCode: The 4 digit code assigned by Visa to categorize the type of merchant.<br/></description></item>
            <item><description>- TransferToOrFromAccountId: If a funding transaction, this will be the PEX account ID.<br/></description></item>
            <item><description>- PageSize: Total page size, 30,000.<br/></description></item>
            <item><description>- TotalRecords: Number of transactions returned for the time period.<br/></description></item>
            <item><description>- NumberofPages: Indicator of how many calls must be made to return all the records for the time period.<br/></description></item>
            <item><description>- LastTimeRetrieved: The date/time of the last record returned.<br/></description></item>
            <item><description>- TransactionTags: Transaction tags.<br/></description></item>
            <item><description>- SourceCurrencyCodeDescription : Currency code description of the amount spent, in local currency.  E.g. if a PEX card is used to make a purchase in Canada this field will have the value = Canadian Dollar. For an exhaustive list of ISO standard currency, please refer to https://www.iso.org/iso-4217-currency-codes.html <br/></description></item>
            <item><description>- SourceCurrencyNumericCode : Currency numeric code of the amount spent, in local currency. E.g. if a PEX card is used to make a purchase in Canada this field will have the value = 124. For an exhaustive list of ISO standard currency numeric code, please refer to https://www.iso.org/iso-4217-currency-codes.html   <br/></description></item>
            <item><description>- SourceAmount : Amount spent in local currency where transaction took place.<br/></description></item>
            <item><description>- TransactionTypeCategory : This gives more information about TransactionType. For TransactionType = Transfer there could be multiple TransactionTypeCatagory such as Business account fee or Card account fee etc.<br/></description></item>
            <item><description>- MetadataApprovalStatus : Specifies the status of the metadata (Tags, receipt image file) associated with transaction. Possible values Approved, Rejected, Ignored, Not Reviewed.<br/></description></item>
            </list>
            <br/>
            Details about why a transaction was declined is provided in the "Description" field. Potential values for the message include:<br/>
            <list type="number">
            <item><description>- Transaction exceeded current card balance<br/></description></item>
            <item><description>- Transaction exceeded daily spend limit<br/></description></item>
            <item><description>- International transactions not allowed<br/></description></item>
            <item><description>- Expired card<br/></description></item>
            <item><description>- Address does not match<br/></description></item>
            <item><description>- Unauthorized merchant<br/></description></item>
            <item><description>- Card not present<br/></description></item>
            <item><description>- Unauthorized geographic location<br/></description></item>
            <item><description>- Unauthorized merchant category: &lt;category&gt;<br/></description></item>
            <item><description>- Insufficient balance in PEX Account<br/></description></item>
            <item><description>- Remote service decline<br/></description></item>
            <item><description>- Do not honor<br/></description></item>
            </list>

**HTTP Request**
`***GET*** /Details/TransactionDetails` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| IncludePendings | query | 1 to include pending transactions and 0 to exclude | No | boolean |
| IncludeDeclines | query | 1 to include decline transactions and 0 to exclude | No | boolean |
| StartDate | query | YYYY-MM-DDThh:mm:ss | Yes | dateTime |
| EndDate | query | YYYY-MM-DDThh:mm:ss | Yes | dateTime |
| Authorization | header | token {USERTOKEN} | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |


###Transaction Details {ID}
```shell
# You can also use wget
curl -X GET https://coreapi.pexcard.com/v4/Details/TransactionDetails/{Id}?StartDate=2018-09-05T19%3A02%3A19Z&EndDate=2018-09-05T19%3A02%3A19Z \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
GET https://coreapi.pexcard.com/v4/Details/TransactionDetails/{Id}?StartDate=2018-09-05T19%3A02%3A19Z&EndDate=2018-09-05T19%3A02%3A19Z HTTP/1.1
Host: coreapi.pexcard.com

Accept: application/json
Authorization: string

```

```javascript
var headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/Details/TransactionDetails/{Id}',
  method: 'get',
  data: '?StartDate=2018-09-05T19%3A02%3A19Z&EndDate=2018-09-05T19%3A02%3A19Z',
  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');

const headers = {
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/Details/TransactionDetails/{Id}?StartDate=2018-09-05T19%3A02%3A19Z&EndDate=2018-09-05T19%3A02%3A19Z',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.get 'https://coreapi.pexcard.com/v4/Details/TransactionDetails/{Id}',
  params: {
  'StartDate' => 'string(date-time)',
'EndDate' => 'string(date-time)'
}, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.get('https://coreapi.pexcard.com/v4/Details/TransactionDetails/{Id}', params={
  'StartDate': '2018-09-05T19:02:19Z',  'EndDate': '2018-09-05T19:02:19Z'
}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/Details/TransactionDetails/{Id}?StartDate=2018-09-05T19%3A02%3A19Z&EndDate=2018-09-05T19%3A02%3A19Z");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "https://coreapi.pexcard.com/v4/Details/TransactionDetails/{Id}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

> Example responses

> 200 Response

```json
{
  "TransactionList": [
    {
      "TransactionId": 0,
      "AcctId": 0,
      "TransactionTime": "",
      "MerchantLocalTime": "",
      "HoldTime": "",
      "SettlementTime": "",
      "AuthTransactionId": 0,
      "TransactionAmount": 0,
      "PaddingAmount": 0,
      "TransactionType": 1,
      "Description": "",
      "TransactionNotes": [
        {
          "NoteId": 0,
          "UserName": "",
          "NoteText": "",
          "NoteDate": ""
        }
      ],
      "IsPending": false,
      "IsDecline": false,
      "MerchantName": "",
      "MerchantCity": "",
      "MerchantState": "",
      "MerchantZip": "",
      "MerchantCountry": "",
      "MCCCode": "",
      "TransferToOrFromAccountId": 0,
      "AuthIdentityResponseCode": "",
      "MerchantId": "",
      "TerminalId": "",
      "NetworkTransactionId": 0,
      "SourceCurrencyCodeDescription": "",
      "SourceCurrencyNumericCode": "",
      "SourceAmount": 0,
      "TransactionTags": {
        "Tags": [
          {
            "FieldId": "",
            "Value": {},
            "Name": ""
          }
        ],
        "State": 0,
        "FieldsVersion": ""
      },
      "MetadataApprovalStatus": "",
      "TransactionTypeCategory": ""
    }
  ],
  "Pages": {
    "PageSize": 0,
    "TotalRecords": 0,
    "NumberOfPages": 0,
    "LastTimeRetrieved": ""
  }
}
```
**Summary:** Return a list of transaction details for the account

**Description:** Please make sure time frame selected between StartDate and EndDate is no more than last 12 months.<br/>
            <br/>
            Return a list of transaction details for PEX business account ID or card account ID provided.<br/>
            <br/>
            If a business account ID is provided, the transactions returned will be for the PEX business account. (Note: input fields  IsPending  and  IsDecline  should be false, as they don't apply to transactions on the business account.)<br/>
            <br/>
            If a card account ID is provided (and you are a partner), the transactions returned will be for that card account. Fields  IsPending  and  IsDecline  can be set to true or false as required.<br/>
            <br/>
            If, for the time-frame selected, over 30,000 transactions are returned then the results will be paginated. To retrieve more data, use the  LastTimeRetrieved  field returned in the StartDate parameter and repeat the call until the  NumberOfPages  field = 1. (Note: the last transaction for the page will be the first transaction retrieved in the next call, use the TransactionId to eliminate duplicate records.)<br/>
            <br/>
            Definition of some of the transaction detail fields:<br/>
            <list type="number">
            <item><description>- TransactionTime: Eastern time. The date/time when authorization was received from the Network.<br/></description></item>
            <item><description>- SettlementTime: Eastern time. Funds have been transferred to the merchant and the transaction is final. Use this for reconciliation purposes. Null for Pendings and Declines.<br/></description></item>
            <item><description>- HoldTime: Eastern time. Date/time a hold was placed on the card account balance. Null for Declines.<br/></description></item>
            <item><description>- MerchantLocalTime: Local time. Date/time provided by the merchant for the transaction. This is controlled by the merchant and may not be accurate.<br/></description></item>
            <item><description>- AuthTransactionId: If PEX was able to match a settlement to an authorization, the matched ID will be in this field.<br/></description></item>
            <item><description>- TransactionAmount: Received from the merchant as the total of the transaction.<br/></description></item>
            <item><description>- PaddingAmount: Added to fuel purchases ($49.00).<br/></description></item>
            <item><description>- TransactionType: Network (purchase or return) or Transfer (funding from business PEX Account).<br/></description></item>
            <item><description>- TransactionNotes: Text notes added by the cardholder or PEX administrator for accounting purposes.<br/></description></item>
            <item><description>- IsPending: If true, the merchant has not settled the transaction. PEX is holding the funds.<br/></description></item>
            <item><description>- IsDecline: The authorization was not successful.<br/></description></item>
            <item><description>- MerchantName: The merchant name provided in the Visa transaction.<br/></description></item>
            <item><description>- MCCCode: The 4 digit code assigned by Visa to categorize the type of merchant.<br/></description></item>
            <item><description>- TransferToOrFromAccountId: If a funding transaction, this will be the PEX account ID.<br/></description></item>
            <item><description>- PageSize: Total page size, 30,000.<br/></description></item>
            <item><description>- TotalRecords: Number of transactions returned for the time period.<br/></description></item>
            <item><description>- NumberofPages: Indicator of how many calls must be made to return all the records for the time period.<br/></description></item>
            <item><description>- LastTimeRetrieved: The date/time of the last record returned.<br/></description></item>
            <item><description>- TransactionTags: Transaction tags.<br/></description></item>
            <item><description>- SourceCurrencyCodeDescription : Currency code description of the amount spent, in local currency.  E.g. if a PEX card is used to make a purchase in Canada this field will have the value = Canadian Dollar. For an exhaustive list of ISO standard currency, please refer to https://www.iso.org/iso-4217-currency-codes.html <br/></description></item>
            <item><description>- SourceCurrencyNumericCode : Currency numeric code of the amount spent, in local currency. E.g. if a PEX card is used to make a purchase in Canada this field will have the value = 124. For an exhaustive list of ISO standard currency numeric code, please refer to https://www.iso.org/iso-4217-currency-codes.html   <br/></description></item>
            <item><description>- SourceAmount : Amount spent in local currency where transaction took place.<br/></description></item>
            <item><description>- TransactionTypeCategory : This gives more information about TransactionType. For TransactionType = Transfer there could be multiple TransactionTypeCatagory such as Business account fee or Card account fee etc.<br/></description></item>
            <item><description>- MetadataApprovalStatus : Specifies the status of the metadata (Tags, receipt image file) associated with transaction. Possible values Approved, Rejected, Ignored, Not Reviewed.<br/></description></item>
            </list>
            <br/>
            Details about why a transaction was declined is provided in the "Description" field. Potential values for the message include:<br/>
            <list type="number">
            <item><description>- Transaction exceeded current card balance<br/></description></item>
            <item><description>- Transaction exceeded daily spend limit<br/></description></item>
            <item><description>- International transactions not allowed<br/></description></item>
            <item><description>- Expired card<br/></description></item>
            <item><description>- Address does not match<br/></description></item>
            <item><description>- Unauthorized merchant<br/></description></item>
            <item><description>- Card not present<br/></description></item>
            <item><description>- Unauthorized geographic location<br/></description></item>
            <item><description>- Unauthorized merchant category: &lt;category&gt;<br/></description></item>
            <item><description>- Insufficient balance in PEX Account<br/></description></item>
            <item><description>- Remote service decline<br/></description></item>
            <item><description>- Do not honor<br/></description></item>
            </list>

**HTTP Request**
`***GET*** /Details/TransactionDetails/{Id}` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| Id | path | Card account ID or Business account ID | Yes | integer |
| IncludePendings | query | 1 to include pending transactions and 0 to exclude | No | boolean |
| IncludeDeclines | query | 1 to include decline transactions and 0 to exclude | No | boolean |
| StartDate | query | YYYY-MM-DDThh:mm:ss | Yes | dateTime |
| EndDate | query | YYYY-MM-DDThh:mm:ss | Yes | dateTime |
| Authorization | header | token {USERTOKEN} | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Success |
| 403 | Invalid card account ID |

##Transaction Notes
###Create Note 
```shell
# You can also use wget
curl -X POST https://coreapi.pexcard.com/v4/Note \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
POST https://coreapi.pexcard.com/v4/Note HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/Note',
  method: 'post',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');
const inputBody = '{
  "TransactionId": 0,
  "NoteText": "",
  "Pending": false
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/Note',
{
  method: 'POST',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.post 'https://coreapi.pexcard.com/v4/Note',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.post('https://coreapi.pexcard.com/v4/Note', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/Note");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("POST");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Content-Type": []string{"application/json"},
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("POST", "https://coreapi.pexcard.com/v4/Note", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

> Body parameter

```json
{
  "TransactionId": 0,
  "NoteText": "",
  "Pending": false
}
```

> Example responses

> 200 Response

```json
{
  "Id": 0
}
```
**Summary:** Create a transaction note

**Description:** You may want to add a transaction note to track a PO or invoice number.<br/>
             <br/>
            Transaction notes are alpha/numeric and can be added to cardholder funding, pending and settlement transactions.  Notes can be viewed on the administration website in transaction details and on reports.<br/>
            <br/>
            To add a note to a funding or settlement transaction, set Pending to false.  For authorization/hold transactions, set Pending to true.<br/>
            <br/>
            To retrieve the TransactionId, get a card transaction list using <br/>
            GET /Details/AllCardholderTransactions<br/>
            GET /Details/TransactionDetails<br/>
            GET /Details/TransactionDetails/{Id}

**HTTP Request**
`***POST*** /Note` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| createRequest | body |  | Yes |  |
| Authorization | header | token {USERTOKEN} | Yes | string |


**Responses**

| Code | Description |
| ---- | ----------- |

###Network Transaction Note
```shell
# You can also use wget
curl -X POST https://coreapi.pexcard.com/v4/Note/NetworkTransactionNote \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
POST https://coreapi.pexcard.com/v4/Note/NetworkTransactionNote HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/Note/NetworkTransactionNote',
  method: 'post',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');
const inputBody = '{
  "NoteText": "",
  "NetworkTransactionId": 0
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/Note/NetworkTransactionNote',
{
  method: 'POST',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.post 'https://coreapi.pexcard.com/v4/Note/NetworkTransactionNote',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.post('https://coreapi.pexcard.com/v4/Note/NetworkTransactionNote', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/Note/NetworkTransactionNote");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("POST");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Content-Type": []string{"application/json"},
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("POST", "https://coreapi.pexcard.com/v4/Note/NetworkTransactionNote", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

> Body parameter

```json
{
  "NoteText": "",
  "NetworkTransactionId": 0
}
```

> Example responses

> 200 Response

```json
{
  "Id": 0
}
```
**Summary:** Create a network transaction note

**Description:** You may want to add a network transaction note to track a PO or invoice number.<br/>
             <br/>
            Network transaction notes are alpha/numeric and can be added to cardholder funding, pending and settlement transactions.  Notes can be viewed on the administration website in transaction details and on reports.<br/>
            <br/>
            To add a note to a funding or settlement transaction, set Pending to false.  For authorization/hold transactions, set Pending to true.<br/>
            <br/>
            To retrieve the TransactionId, get a card transaction list using <br/>
            GET /Details/AllCardholderTransactions<br/>
            GET /Details/TransactionDetails<br/>
            GET /Details/TransactionDetails/{Id}

**HTTP Request**
`***POST*** /Note/NetworkTransactionNote` 


**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| createRequest | body |  | Yes |  |
| Authorization | header | token {USERTOKEN} | Yes | string |


**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | OK |


###Update Note 
```shell
# You can also use wget
curl -X PUT https://coreapi.pexcard.com/v4/Note/{id} \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
PUT https://coreapi.pexcard.com/v4/Note/{id} HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/Note/{id}',
  method: 'put',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');
const inputBody = '{
  "NoteText": "",
  "Pending": false
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/Note/{id}',
{
  method: 'PUT',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.put 'https://coreapi.pexcard.com/v4/Note/{id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.put('https://coreapi.pexcard.com/v4/Note/{id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/Note/{id}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("PUT");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Content-Type": []string{"application/json"},
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("PUT", "https://coreapi.pexcard.com/v4/Note/{id}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

> Body parameter

```json
{
  "NoteText": "",
  "Pending": false
}
```

> Example responses

> 200 Response

```json
{
  "Id": 0
}
```
**Summary:** Update a transaction note

**Description:** To retrieve the NoteId, get a card transaction list using <br/>
            GET /Details/AllCardholderTransactions<br/>
            GET /Details/TransactionDetails<br/>
            GET /Details/TransactionDetails/{Id}<br/>
            <br/>
            To edit a note on a funding or settlement transaction, set Pending to false. For authorization/hold transactions, set Pending to true.<br/>
            <br/>
            Transaction notes can also be edited from the administration website in transaction detail.

**HTTP Request**
`***PUT*** /Note/{id}` 


**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| id | path | Note Ic | Yes | long |
| updateRequest | body | Details required to update note | Yes |  |
| Authorization | header | token {USERTOKEN} | Yes | string |


**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Success |
| 403 | Note not found |



###Delete Note 
```shell
# You can also use wget
curl -X DELETE https://coreapi.pexcard.com/v4/Note/{id} \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: string'

```

```http
DELETE https://coreapi.pexcard.com/v4/Note/{id} HTTP/1.1
Host: coreapi.pexcard.com
Content-Type: application/json
Accept: application/json
Authorization: string

```

```javascript
var headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'

};

$.ajax({
  url: 'https://coreapi.pexcard.com/v4/Note/{id}',
  method: 'delete',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const request = require('node-fetch');
const inputBody = '{
  "Pending": false
}';
const headers = {
  'Content-Type':'application/json',
  'Accept':'application/json',
  'Authorization':'string'

};

fetch('https://coreapi.pexcard.com/v4/Note/{id}',
{
  method: 'DELETE',
  body: inputBody,
  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Content-Type' => 'application/json',
  'Accept' => 'application/json',
  'Authorization' => 'string'
}

result = RestClient.delete 'https://coreapi.pexcard.com/v4/Note/{id}',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Content-Type': 'application/json',
  'Accept': 'application/json',
  'Authorization': 'string'
}

r = requests.delete('https://coreapi.pexcard.com/v4/Note/{id}', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("https://coreapi.pexcard.com/v4/Note/{id}");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("DELETE");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Content-Type": []string{"application/json"},
        "Accept": []string{"application/json"},
        "Authorization": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("DELETE", "https://coreapi.pexcard.com/v4/Note/{id}", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

> Body parameter

```json
{
  "Pending": false
}
```

> Example responses

> 200 Response

```json
{
  "Id": 0
}
```
**Summary:** Delete a transaction note

**Description:** To retrieve the NoteId, get a card transaction list using <br/>
            GET /Details/AllCardholderTransactions<br/>
            GET /Details/TransactionDetails<br/>
            GET /Details/TransactionDetails/{Id}<br/>
            <br/>
            To delete a note on a funding or settlement transaction, set Pending to false. For authorization/hold transactions, set Pending to true.<br/>
            <br/>
            Transaction notes can also be deleted from the administration website in transaction detail.

**HTTP Request**
`***DELETE*** /Note/{id}` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| id | path |  | Yes | long |
| deleteRequest | body |  | Yes |  |
| Authorization | header | token {USERTOKEN} | Yes | string |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | Success |
| 403 | Note not found |


#Webhooks
##Introduction
PEX can send webhook notifications to customers in response to a variety of events.  An event is an activity, such as a card transaction at a point-of-sale (POS) terminal or a card status change. Webhooks provide more details about the event. For example, a notification might alert a customer that a card was used and include details regarding the outcome of the attempted transaction. 

To receive webhook notifications, you will need to pre-configure and host endpoints for each of the webhooks you wish to receive. After setting up the endpoints, contact API Support or your client success manager with details of the endpoints and the events you wish to receive. PEX will then begin issuing HTTPS POST requests to your endpoints with information about the event. 

PEX support TLS 1.1 and higher versions. PEX does NOT support TLS 1.0

PEX sends 3 types of webhooks:

1. Card Network Transaction

2. Card Status Change

3. Card Shipment
    

  
**Webhook headers**

```json
HTTP POST
Connection: Keep-Alive
Content-Length: 761 
Content-Type: application/json; charset=utf-8
Authorization: Basic QTM1Q0JENkE2Mzc1NDYxQThFQzE0MUZBQTk1QzI1MEY=
X-PEX-Version: 2.0.1.1
Expect: 100-continue 
Host: coreapi.pexcard.com  
Request-Context: appId=cid-v1:894ea26b-2fc9-45f1-ac12-e0c7d4083452
x-ms-request-root-id: 5240accf-42dfdcaf1157b7f7
x-ms-request-id: |5240accf-42dfdcaf1157b7f7.
Request-Id: |5240accf-42dfdcaf1157b7f7.
```
PEX takes security and scalability seriously. To allow our customers to authenticate webhook calls, all webhooks include an authentication header. 

PEX uses **HTTP Basic Authentication** (HTTPS) in order to securely authenticate webhooks calls. With HTTP Basic Authentication, a shared secred key is base64 encoded and passed in header. Customers can compare a decoded copy of this value against the shared secret to authenticate the webhook call.

Customers should contact API Support to receive their shared secret. Please store your shared secret in a secure location and do not share it.





**Card Network Transactions**

Transaction events are generated when a network transaction occurs. There are several types of network transaction events. You can subscribe to receive a webhook for each type of network event independently:

**Types of Network Transactions**
PEX currently provides webhooks for 5 types of network transaction events. Network transaction events are identified by "TransactionType": "NETWORK". The type of transaction can be identified by using the NetworkType and NetworkStatus fields. NetworkType can be one of four values: Auth, Pin, Settlement, Reversal. NetworkStatus can be one of two values: Approved, Declined. All Reversal events will have a default NetworkStatus value of "Approved".

You can subscribe to receive each type of event on separate endpoints: Authorization (Signature Transactions;Type 0100), Reversal (Type 0420), Settlement (Type 0220), PIN Transaction (Type 0200), Decline (Note the decline endpoint will receive both declined (signature) Authorization Transaction decline events and PIN Transaction decline events.)

Although the "Description" field may contain information about the kind of transaction, this field should not be relied upon to identify the type of transaction.


* [Authorization](#authentication) (Signature Transactions;Type 0100) 

* [Reversal](#reversal) (Type 0420)
    
* [Settlement](#settlement) (Type 0220)

* [PIN Transaction](#pin-transaction) (Type 0200)

* [Decline](#transaction-decline)
        

**[Card Status Change](#card-status-change)**: This event is generated when the status of a card changes. Activating a card, blocking a card, and closing a card will all generate card status change events.

**[Card Shipping Information](#card-shipping-information)**:  After placing an order for new cards, a card shipping information event is generated when the card order is shipped to the cardholder.
               
**[Virtual Card Sensitive Data](#virtual-card-sensitive-data)**: After placing an order for a virtual card(s), the sensitive card data data, such as the 16 digit card number, expiration date, and security code (CVV), are sent via a webhook.

  
If you are ready to start using PEX webhooks, please send your request, along with your endpoint URLs, to API Support or your client success manager. The URL endpoints should adheres to the following
*  HTTPS URL (ie. https://)  

* URL endpoint for Auth Transaction Message

* URL endpoint for PIN Transaction Message

* URL endpoint for Settlement Transaction Message

* URL endpoint for Reversal Transaction Message

* URL endpoint for Card Status Change Message

* URL endpoint for Card Shipping Information Message

* URL endpoint for Virtual Card Sensitive Data Message
 
Note that

1. if a URL endpoint is not provided for a particular transaction type, then notifications will not be sent for that particular transaction type.

2. for the Card Status Change webhook, you will receive a webhook for each status change regardless of the method used to change the status (API, Admin web portal, Mobile)

3. If PEX does not receive a 200 or 201 response from you within 20 seconds after sending a webhook, retry attempts will be made 15, 30, 60 and 120 seconds later. One final retry attempt will be made 3600 seconds (1 hour) later. If PEX does not receive a reply to that last attempt, that notification will be deleted from the queue. You will be responsible for proactively retrieving missed transactions via the PEX API. In the unlikely event of a PEX outage, webhooks are stored and released immediately when we come back online.

**Timestamp Fields**: All date/time values are in EST (eastern standard time) unless otherwise noted.

**TransactionTime**: The date/time when authorization request was received from the network.

**HoldTime**: Date/time a hold was placed on the card account balance. HoldTime will be "null" for Authorizations as the hold is placed concurrently with the webhook event.

**SettlementTime**: Funds have been transferred to the merchant and the transaction is final. Use this for reconciliation purposes. SettlementTime will be "null" for Authorizations and any transactions where "NetworkStatus"="Declined".

**MerchantLocalTime**: Local time for the POS used for the transaction. The date/time is provided by the merchant and does not include time zone information. As this value is set on the POS, it may not be accurate.

##Authorization 

> Sample approved authorization webhook:

```json
{ 
  "CallbackTime": "2017-09-07T04:03:36.5738865-04:00",
  "Data": {
        "NetworkTransactionId":2265018,
        "TransactionId":null,
        "AcctId":7378,
        "TransactionTime":"2017-09-07T04:03:35",
        "HoldTime":null,
        "SettlementTime":null,
        "MerchantLocalTime":"2017-09-07T04:03:35",
        "AuthTransactionId":null,
        "TransactionAmount":-2.0,
        "PaddingAmount":0.0,
        "AvailableBalance":156.0,
        "LedgerBalance":156.0,
        "TransactionType":"NETWORK",
        "Description":"Pending",
        "TransactionNotes":null,  
        "ReferencedTranId":null,
        "ReferencedTransactionTime":null,
        "MerchantName":"Merch Name",
        "MerchantCity":"Iv-Fr",
        "MerchantState":"CO",
        "MerchantZip":"760009874",
        "MerchantCountry":"US",
        "MCCCode":"5812",
        "AuthIdentityResponseCode":"529958",
        "MerchantId":"000065432112514",
        "TerminalId":"6548526 ",
        "NetworkType":"Auth",
        "NetworkStatus":"Approved",
        "IsCardPresent":true,
        "Message":null,
        "MessageCode":null,
        "MerchantRequestedAmount":-2.0      
      }
    }
```

**(Signature) Authorization**




When a PEX card is used to make a (signature) purchase, a merchant will request an authorization for a charge to the card and an authorization event is generated. The authorization request checks that the funds are available on the card and can be either Approved or Declined.

If the authorization is successful, the transaction amount will be placed on hold on the card for a period of time, reducing the amount available for other purchases. If the purchase is not settled ('captured') within this time, the hold is canceled and on-hold funds are released. This hold period is typically five days, but may vary by merchant.

Note that a transaction using a PIN will not generate an authorization event. See PIN Transaction for details on webhooks for PIN transactions.      
      

##Reversal

> Sample approved Reversal webhook:

```json
{ 
  "CallbackTime": "2017-09-07T04:05:43.4025944-04:00",
  "Data": { 
        "NetworkTransactionId":2265018,
        "TransactionId":null,
        "AcctId":7378,
        "TransactionTime":"2017-09-07T04:05:42",
        "HoldTime":null,
        "SettlementTime":null,
        "MerchantLocalTime":"2017-09-07T04:03:35",
        "AuthTransactionId":2465657071,
        "TransactionAmount":2.0,
        "PaddingAmount":0.0,
        "AvailableBalance":154.0,
        "LedgerBalance":154.0,
        "TransactionType":"NETWORK",
        "Description":"Reversal",
        "TransactionNotes":null,
        "ReferencedTranId":2465657071,
        "ReferencedTransactionTime":"2017-09-07T04:03:35",
        "MerchantName":"Merch Name",
        "MerchantCity":"Iv-Fr",
        "MerchantState":"CO",
        "MerchantZip":"760009874",
        "MerchantCountry":"US",
        "MCCCode":"5812",
        "AuthIdentityResponseCode":"529958",
        "MerchantId":"000065432112514",
        "TerminalId":"6548526 ",
        "NetworkType":"Reversal",
        "NetworkStatus":null,
        "IsCardPresent":true,
        "Message":null,
        "MessageCode":null,
        "MerchantRequestedAmount":2.0        
      }
}
```

**Transaction Reversal**
  
A merchant may decide to reverse a previous authorization and release the funds that were previously on hold for a given purchase. This will result in an increase to the available funds on the account. A merchant may also decide to reverse a PIN Transaction, in which case the funds that were debited from the account will be credited back to the account.

<aside class="notice">
If available, the AuthTransactionId can be used to find the associated authorization which is being reversed. However, the id of the associated authorization may not always be available. Visa reviewed thousands of authorization reversal transactions over a three month period and found that many merchants send incomplete or incorrect information in the reversal message. This means that the issuer is not able to properly identify and remove the matching authorization hold.
</aside>


##Settlement 

>Sample posted settlement webhook:

```json
{
   "CallbackTime": "2017-09-07T04:09:30.0986603-04:00",
   "Data": {     
    "NetworkTransactionId":2265018,
        "TransactionId":2465657073,
        "AcctId":7378,
        "TransactionTime":"2017-09-07T04:03:35",
        "HoldTime":"2017-09-07T04:03:35",
        "SettlementTime":"2017-09-07T04:03:54",
        "MerchantLocalTime":"2017-09-07T04:03:35",
        "AuthTransactionId":2465657071,
        "TransactionAmount":-2.0,
        "PaddingAmount":0.0,
        "AvailableBalance":154.0,
        "LedgerBalance":154.0,
        "TransactionType":"NETWORK",
        "Description":"Settlement",
        "TransactionNotes":null,
        "ReferencedTranId":2465657071,
        "ReferencedTransactionTime":"2017-09-07T04:03:35",
        "MerchantName":"Merch Name",
        "MerchantCity":"Iv-Fr",
        "MerchantState":"CO",
        "MerchantZip":"760009874",
        "MerchantCountry":"US",
        "MCCCode":"5812",
        "AuthIdentityResponseCode":"529958",
        "MerchantId":"000065432112514",
        "TerminalId":"6548526 ",
        "NetworkType":"Settlement",
        "NetworkStatus":null,
        "IsCardPresent":true,
        "Message":null,    
        "MessageCode":null,
        "MerchantRequestedAmount":-2.0
      
      }
}
```      

**Posted Signature Settlement**
    
A settlement event is generated when the merchant 'captures' the funds previously authorized as part of a signature transaction. Note that NetworkStatus is null for all settlement events.

  
##PIN Transaction

>Sample PIN transaction webhook:

```json
{    
  "CallbackTime": "2017-09-07T05:19:47.1675395-04:00",
  "Data": {      
    "NetworkTransactionId":2265021,
        "TransactionId":null,
        "AcctId":7378,
        "TransactionTime":"2017-09-07T05:19:46",
        "HoldTime":null,
        "SettlementTime":null,
        "MerchantLocalTime":"2017-09-07T05:19:45",
        "AuthTransactionId":null,
        "TransactionAmount":-15.0,
        "PaddingAmount":0.0,
        "AvailableBalance":156.0,
        "LedgerBalance":156.0,
        "TransactionType":"NETWORK",
        "Description":"Settlement",
        "TransactionNotes":null,      
        "ReferencedTranId":null,
        "ReferencedTransactionTime":null,
        "MerchantName":"Merch N",
        "MerchantCity":"",
        "MerchantState":"",
        "MerchantZip":"760009874",
        "MerchantCountry":"",
        "MCCCode":"5812",
        "AuthIdentityResponseCode":"394297",
        "MerchantId":"000065432112514",
        "TerminalId":"12313123",
        "NetworkType":"Pin",
        "NetworkStatus":"Approved",
        "IsCardPresent":true,
        "Message":null,
        "MessageCode":null,
        "MerchantRequestedAmount":-15.0
      }
}
```

**PIN Transaction**
    
When a PEX card is used for transaction that is completed with a PIN (Personal Identification Number), a PIN transaction event is generated. In a PIN transaction, funds are immediately debited from the card account. Note that the "Description" field will read "Settlement as the funds have been debited.
      
##Transaction Decline

>Sample transaction decline webhook:

```json       

{
   "CallbackTime": "2017-09-07T03:36:19.0333786-04:00",
  "Data": {       
        "NetworkTransactionId":2265017,
        "TransactionId":null,
        "AcctId":7378,
        "TransactionTime":"2017-09-07T03:32:11",
        "HoldTime":null,
        "SettlementTime":null,
        "MerchantLocalTime":"2017-09-07T03:32:11",
        "AuthTransactionId":null,
        "TransactionAmount":-15.0,
        "PaddingAmount":0.0,
        "AvailableBalance":156.0,
        "LedgerBalance":156.0,
        "TransactionType":"NETWORK",
        "Description":"Declined",
        "TransactionNotes":null,
        "ReferencedTranId":null,
        "ReferencedTransactionTime":null,
        "MerchantName":"Merch N",
        "MerchantCity":"",
        "MerchantState":"",
        "MerchantZip":"760009874",
        "MerchantCountry":"",
        "MCCCode":"5812",
        "AuthIdentityResponseCode":"",
        "MerchantId":"000065432112514",
        "TerminalId":"12313123",
        "NetworkType":"Pin",
        "NetworkStatus":"Declined",
        "IsCardPresent":true,
        "Message": "Unauthorized merchant category: Hardware Stores",
        "MessageCode":"decline.rule.mcc",
        "MerchantRequestedAmount":-15.0      
      }
}
```

PEX may determine that a transaction should not be honored, based on various criteria. For example, the transaction may not comply with the restrictions ('rules') placed on the card or sufficient funds are not available. In this situation, a decline event is generated. The decline webhook includes details about the transaction and the reason for the decline.
      
A declined transaction can be identified by having "NetworkStatus":"Declined"
      

Decline reasons
Details about why a transaction was declined is provided in the "Message" field.
Transaction decline reasons are categorized by a unique and self describing "MessageCode" identifying either a single decline reason or a category of decline reasons.
You can find list of message codes and corresponding messages here

Additional information about declined transactions can be found in the <a href="https://pexcard.zendesk.com/hc/en-us/articles/221392207-What-is-the-Reason-for-Card-Declines">Knowledge Base</a>.


##Card Status Change 

>Sample card status change webhook:

```json
{  
  "CallbackTime": "2016-08-22T12:20:53.7335395+03:00",<br>
  "Data": {       
    "AcctId": 123213234,
    "TransactionType": "CARD",
    "Description": "Status Change",
    "CardList":[ 
     { 
      "CardId": 6231,
      "IssueDate": "2014-11-26T00:00:00",
      "ExpirationDate": "2017-11-30T00:00:00",
      "Last4CardNumber": "1212",
      "CardStatus": "CLOSED"
       
      }
   ]
  }
}
```
    
You can subscribe to the Card Status Change webhook to receive a callback when there is a change in the status of a card. A card can be one of the following statuses: ACTIVE, BLOCKED, CLOSED or INACTIVE:<br>
In most cases you will receive webhook call as soon as card status is changed, but in some cases there could be delays depending upon the processing queue</p>


**Card Status Definitions**

* INACTIV: Card account and plastic have been created, but the card has not been activated and is not ready for use. Note that you will receive a webhook with CardStatus=INACTIVE for each card created using the  [/Card/CreateAsync](#create-card) endpoints, as well as any cards created using the Admin portal or via a file upload.

* ACTIVE: Card is active and ready to use.

* BLOCKED: Card is set to decline all authorization attempts. Note that a change from INACTIVE status to BLOCKED status results in the card first being activated and then immediately being set to BLOCKED status and will generate 2 webhooks - ACTIVE and BLOCKED.

* CLOSED: Card has been terminated and can no longer be used. This status is permanent and cannot be reversed.


##Card Shipping Information

>Sample card shipping information webhook:

```json   
{
  "CallbackTime": "2016-08-22T12:20:53.7335395+03:00",<br>
  "Data": {        
    "AcctId": 11111,
    "TransactionType": "CARDORDER",
    "Description": "Shipped",
    "TrackingNumber": "9400015001052000000000",
    "ShippingMethod": "USPS",
    "Last4CardNumber": "1234",
    "CardOrderId": 1221
      
      }
}
```
    
You can subscribe to the Card Shipping Information webhook to receive a message when the cards you ordered are embossed and shipped. This webhook will contain the shipping provider and tracking number so you can track the shipment.


##Virtual Card Sensitive Data

>Sample Response:

```json
{
    "CallbackTime": "2017-12-27T05:35:52.4142456-05:00",<br>
    "Data": {
        "AccountId": 12343,
        "AccountNumber": "10000000353902",
        "FirstName": "Jon",
        "LastName": "Snow",
        "CardNumber": "4111123412341234",
        "ExpirationDate": "2020-12-31T00:00:00",
        "CVV2": "123",
        "Status": "ACTIVE",
        "Balance": 400.0,
        "VirtualCardOrderId": 13232,
        "OrderDateTime": "2017-12-27T05:35:25.847",
        "Errors": [],
        "Message": "Account Creation Successful"
    }
}
```

You can subscribe to the Virtual Card Sensitive Data webhook to receive details your newly created virtual cards. Card data, including the 16 digit PAN and CVV2, is sensitive data. Do not store the data contained in this webook. You can retrieve the card data at any point by using POST /VirtualCard/Data to request a resend of the webhook. Note that when using the /VirtualCard/Data endpoint, you can only request webhook data for one virtual card at a time.


* CardNumber is 16 digits without dashes

* ExpirationDate is in a Date and Time format, you can convert 2020-01-31T00:00:00.00 Into January 2020

* Security Code or CVV or CVV2 is 3 digits

* Status is either active or inactive and reflects the current state of the card

* Balance reflects the current balance on the card. If card has not been used, then it reflects the funding amount initially placed on the card



  
"Errors" and "Message" are only present for the webhook associated with the original order  (POST/VirtualCard/Order).  In the re-sent callback message (i.e. POST/VirtualCard/Data) they are always empty. This is so because, funding, activation or any other successful or failed event associated with a virtual card order can be updated manually via other API calls.

>Within the “Errors” array are the following values:
```json
"Card"
"Group"
"Ruleset"
"Activation"
"Funding"
```

The virtual card order process is asynchronous so theoretically a variety of errors could occur. Below are a few examples and how “Errors” and “Messages” would appear in the original callback:
  
> completely successful, no errors

```json
{
    "Errors": [],<br>
    "Message": "Account Creation Successful"<br>
}
```
 
>completely failed - card was not created

```json
{
    "Errors": [ "Card" ],<br>
    "Message": "Failed: Card Creation"<br>
}
```

> partial fail of some post card creation actions (group or ruleset or activation or funding)

```json
{
    "Errors": [ "Group", "Ruleset", "Activation", "Funding" ],<br>
    "Message": "Failed: Set Group, Set Ruleset, Activation, Funding"<br>
}
```
