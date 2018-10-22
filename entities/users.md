# Ionoid IoT Users

A user is a person or a program that interacts with projects and devices,
it can use the dashboard or the API to talk to devices directly.


## 1. The User Object

The User Object can be accessed at:
```
https://api.ionoid.io/api/user/v1.0/
```

The User Object is a `Json` Object

```json
{
        "API_USER_NAME":        "user",
        "API_USER_EMAIL":       "test@example.com",
        "API_USER_ID":          "3b36e0e2-5572-443d-bb04-7b3fb596c7fe",
        "API_KEY":              "5YxfPuGBSTPDasoQ8mlGfbvKZBRAGisCQhVZUTdcD",
        "API_KEY_DEVICES":       "rOPbiTeEfsdu8A8Sz9aZFDRMbqwGKqLrGKS4GWbDx",
        "API_KEY_PUBLISH_EVENTS": "secretkey",
        "API_KEY_SUBSCRIBE_EVENTS":     "secretkey",
        "API_KEY_PUBLISH_RESPONSES":    "secretkey",
        "API_KEY_SUBSCRIBE_RESPONSES":  "secretkey",
        "API_ORGANIZATION":             "My Organization",
        "API_ORGANIZATION_ID":          "a09539d3-be02-4782-8213-11b60d3d20e1",
        "API_ACCOUNT_PLAN":     "Developer",
        "API_ENDPOINT":         "https://endpoint.example.com",
        "API_ENDPOINT_DEVICES": "https://endpoint.example.com",
        "API_USAGE_EPOCH_MONTH":        1527811200,
        "API_USAGE_KEY":        1000,
        "API_USAGE_KEY_PREVIOUS":       100000,
        "API_USAGE_KEY_DEVICES":        10000,
        "API_USAGE_KEY_PREVIOUS_DEVICES": 1000000,
        "API_USAGE_TOTAL_DEVICES":     200
}
```

Summary of each field:

* **API_USER_NAME**:            The user name

* **API_USER_EMAIL**:           The user email

* **API_USER_PASSWORD**:        The user bcrypt hashed password

* **API_USER_ID**:              The unique User ID

* **API_KEY**:                  The user API Key used to send actions and events
to devices.

* **API_KEY_DEVICES**:          The devices API Key used to update their status.

* **API_KEY_PUBLISH_EVENTS**:   The publish key for the events channel.

* **API_KEY_SUBSCRIBE_EVENTS**: The subscribe key for the events
channel, used by devices to receive events and actions.

* **API_KEY_PUBLISH_RESPONSES**: The publish key used by devices to
publish messages.

* **API_KEY_SUBSCRIBE_RESPONSES**: The subscribe key used to receive
devices messages.

* **API_ORGANIZATION**:         The user organization name

* **API_ORGANIZATION_ID**:      The user organization unique ID

* **API_ACCOUNT_PLAN**:         The user subscription plan

* **API_ENDPOINT**:             Endpoint URL for API Access

* **API_ENDPOINT_DEVICES**:     Endpoint URL for Devices API Access


## 2. Interact with Users Objects

### 2.1 Register new User object


TODO


**Important Note**: Users must register and confirm their email address
before they are allowed to interact with the API.



### 2.2 Log in as User

To log in:

Request:
```
POST https://api.ionoid.io/api/user/v1.0/login

Headers:
content-type: application/json

body:
{
        "API_USER_EMAIL":       "email@example.com",
        "API_KEY":              "api_key"
}
```

Response:
```json
{
        "statuscode": 200,
        "body": {
                "message": "OK",
                "authenticateuser": {
                        "API_USER_EMAIL":       "email@example.com",
                        "API_KEY":              "api_key",
                        "accessToken":          "..."
                },
        }
}
```


Curl Request:
```json
$ curl --verbose \
        -H 'content-type: application/json' \
        -X POST -d '{ "API_USER_NAME": "username", \
                "API_USER_PASSWORD": "bcrypt_hashed(pass)"}' \
        https://api.ionoid.io/api/user/v1/login
```


### 2.3 Log out

To logout from the session, use the logout API Call.

Request:
```
POST https://api.ionoid.io/api/user/v1.0/sessions/logout

Headers:
content-type: application/json
authorization: JWT token
```

Response:
```json
{
        "statuscode": 200,
        "body": {
                "message": "OK"
        }
}
```


Curl Example:
```json
$ curl --verbose \
        --request POST \
        --url https://api.ionoid.io/api/user/v1/sessions/logout \
        --header 'authorization: JWT token'
```


### 2.4 Validate JWT Token

To check if the JWT Token is valid, please use the following:

Request:
```
POST https://api.ionoid.io/api/user/v1.0/sessions/validate

Headers:
content-type: application/json
API_USER_EMAIL: myemail@example.com
x-api-key: api_key

body:
{
        "API_USER_EMAIL":       "email@example.com",
        "idToken":              "JwtToken",
        "accessToken":          "JwtToken"
}
```


Response:
```json
{
        "statuscode": 200,
        "body": {
                "message": "OK"
        }
}
```


### 2.5 Query Account Information

To query your account information, please use the following:

Request:
```
POST https://api.ionoid.io/api/user/v1.0/info

Headers:
content-type: application/json

API_USER_EMAIL: myemail@example.com
x-api-key: api_key
or
idToken: ID Token
accessToken: Access Token

body:
{
        "API_USER_EMAIL": "email@example.com"
}
```


Response:
```json
{
        "statuscode": 200,
        "body": {
                "message": "OK",
                'user": {

                }
        }
}
```


### 2.6 Update Account Information

To update account information, please use the following:

Request:
```
POST https://api.ionoid.io/api/user/v1.0/update

Headers:

API_USER_EMAIL: myemail@example.com
x-api-key: api_key
content-type: application/json
or
idToken: ID Token
accessToken: Access Token

body:
{
        "API_USER_EMAIL": "myemail@example.com",
        "API_USER_NEW_FIELD": "NEW_VALUE"
}
```


Response:
```json
{
        "statuscode": 200,
        "body": {
                "message": "OK",
                "user": {
                        "API_USER_EMAIL": "myemail@example.com",
                        "API_USER_NEW_FIELD": "NEW_VALUE"
                }
        }
}
```
