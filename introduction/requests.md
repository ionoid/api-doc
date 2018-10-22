# Ionoid IoT API Requests

Ionoid IoT API Requests are HTTP Requests. That is the main
interface to interact with IoT Projects and Devices.

The API Requests and responses represent objects that may refence a
User, Projects or Devices.

Each Object is represented as a `Json` Object.

The following doc references objects as entities.


## API Requests format

An API Call is formatted as:

```
Method https://api.ionoid.io/object/v1.0/call
```

* Method: is an HTTP Method that the target object support.
* URL: is the endpoint of the API to the object and the requested
resouce.


## Version Prefix

All API Calls include a version number. The Version number comes after
the requested object. This is by design, since we will support self
hosted solutions where our users should be able internally to migrate
an old version to a new version of microservice easily.

Format:
```
https://api.ionoid.io/object/vX.0/call
```

**Important Note:**
At the moment we do not yet promise backwards compatibility.


## API Request Examples:

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
