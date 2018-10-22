# Ionoid IoT API Responses

Ionoid IoT API Responses are HTTP Responses that may contain Json
data.

The API Requests and responses represent objects that may refence a
User, Projects or Devices. Each Object is represented as a `Json` Object.

The following doc references objects as entities.


## API Response format

An API Response to a previous API Call is an HTTP Response that may
contain `Json` data. In this case the API Response is formatted as:

```json
{
        "statuscode":   200,
        "body": {
                "message":      "OK",
                "errormsg":     "",
                "data": { }
        }
}
```


## API Response Examples:

### HTTP GET

An example of an HTTP GET to list Your IoT Projects

Request:
```
GET https://api.ionoid.io/project/v1.0/list

Headers:
API_TOKEN: token header example
```

Curl example
```bash
$ curl --verbose \
        -H "API_TOKEN: token_key" \
        -X GET https://api.ionoid.io/project/v1.0/list
```

Response:
HTTP/1.1 200 OK
```json
{
        "statuscode": 200,
        "body": {
                "message": "OK",
                "errormsg": "",
                "projects": [
                {
                        "API_USER_ID": "3b36e0e2-5572-443d-bb04-7b3fb596c7fe",
                        "API_PROJECT_ID": "56542defawc542081",
                        "API_PROJECT_NAME": "ProjectBlockchainX",
                        "API_PROJECT_ORGANIZATION": "My Project Organization",
                        "API_PROJECT_DEVICE_TYPE": "Raspberry PI 3",
                        "API_PROJECT_DEVICES_STATUS": "OK"
                },
                {
                        "API_USER_ID": "3b36e0e2-5572-443d-bb04-7b3fb596c7fe",
                        "API_PROJECT_ID": "109732zwq",
                        "API_PROJECT_NAME": "projectX",
                        "API_PROJECT_ORGANIZATION": "My Project Organization",
                        "API_PROJECT_DEVICE_TYPE": "BeagleBone Black",
                        "API_PROJECT_DEVICES_STATUS": "ERRORS"
                }
                ]
        }
}
```

### HTTP POST

An example of an HTTP Post to create a new project

Request:
```
POST https://api.ionoid.io/project/v1.0/new

Headers:
API_TOKEN: token header example
content-type: application/json

Body:
{
        "API_PROJECT_NAME":             "ProjectBlockchainX",
        "API_PROJECT_TYPE":             "Blockchain",
        "API_PROJECT_ORGANIZATION":     "My Project Organization",
        "API_PROJECT_DEVICE_TYPE":      "Raspberry PI 3"
}
```

Curl Example:
```
$ curl --verbose \
        -H "API_TOKEN: token_key" \
        -H 'content-type: application/json' \
        -X POST -d '{"API_PROJECT_NAME": "ProjectBlockchainX", \
                "API_PROJECT_TYPE": "Blockchain", \
                "API_PROJECT_ORGANIZATION": "My Project Organization", \
                "API_PROJECT_DEVICE_TYPE": "Raspberry PI 3"}' \
        https://api.ionoid.io/project/v1.0/new
```

Response:
HTTP/1.1 201 Created
```json
{
        "statuscode": 201,
        "body": {
                "message": "Created",
                "project": {
                        "API_PROJECT_ID": "56542defawc542081",
                        "API_PROJECT_NAME": "IoT-Blockchain",
                        "API_PROJECT_TYPE": "Blockchain",
                        "API_PROJECT_ORGANIZATION": "My Project Organization",
                        "API_PROJECT_DEVICE_TYPE": "Raspberry PI 3",
                        "API_PROJECT_DEVICES_STATUS": "Empty",
                        "API_PROJECT_DEVICES_COUNT": 0
                }
        }
}
```
