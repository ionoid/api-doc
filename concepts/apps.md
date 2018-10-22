# Ionoid IoT Apps

A project is a way to organize users, end-users and devices into a
logical entity.


## 1. The Project Object

The Project Object can be accessed at:
```
https://api.ionoid.io/api/project/v1.0/
```

The Project Object is a `Json` Object

```json
{
        "API_PROJECT_NAME":             "IoT-Blockchain",
        "API_PROJECT_TYPE":             "Blockchain",
        "API_PROJECT_DEVICE_TYPE":      "CPU Architecture",
        "API_PROJECT_ORGANIZATION":     "My Project Organization",
        "API_PROJECT_AGE":              1526113719,

        "API_USER_ID":                  "3b36e0e2-5572-443d-bb04-7b3fb596c7fe",
        "API_PROJECT_ID":               "b504eae1-a2cc-4e56-a309-6d6dbdbba977",
        "API_PROJECT_DEVICES_STATUS":   "OK",
        "API_PROJECT_DEVICES_COUNT":    200,

        "API_PROJECT_ACTION":           "Action to Perform"
}
```

Summary of each field:

* **API_PROJECT_NAME**: The project name as set by user

* **API_PROJECT_TYPE**: The project or product segment type as set by user

* **API_PROJECT_DEVICE_TYPE**: The Device type used by this Project

* **API_PROJECT_ORGANIZATION**: The organization of this project as set by the
user.

* **API_PROJECT_AGE**: The Project age in Unix time, represented by the
number of seconds elapsed since January 1, 1970 UTC.

* **API_PROJECT_ACTION**: The Action to perform on the project.

* **API_USER_ID**: The owner or creator of the project, used for API
Calls.

* **API_PROJECT_ID**: The Project ID, set internally and used for API
Calls.

* **API_PROJECT_DEVICES_STATUS**: The Status of Devices in this Project.

* **API_PROJECT_DEVICES_COUNT**: The number of Devices in this Project.


## 2. Interact with Projects

### 2.1 List All Projects

To list your projects with your `jwt` token:

Request:
```
GET https://api.ionoid.io/api/project/v1.0/

Headers:

x-api-key: secret_key
API_USER_EMAIL: email@example.com
content-type: application/json
idToken: ID Token
accessToken: Access Token
```

Response:
```json
{
        "statuscode": 200,
        "body": {
                "message": "OK",
                "errormsg": "",
                "projects": [
                {
                        "API_USER_ID": "3b36e0e2-5572-443d-bb04-7b3fb596c7fe",
                        "API_PROJECT_ID": "b504eae1-a2cc-4e56-a309-6d6dbdbba977",
                        "API_PROJECT_NAME": "ProjectBlockchainX",
                        "API_PROJECT_ORGANIZATION": "My Project Organization",
                        "API_PROJECT_DEVICE_TYPE": "Raspberry PI 3",
                        "API_PROJECT_DEVICES_STATUS": "OK"
                },
                {
                        "API_USER_ID": "3b36e0e2-5572-443d-bb04-7b3fb596c7fe",
                        "API_PROJECT_ID": "109732a1-a2cd-4e56-a621-6d6dbccba319",
                        "API_PROJECT_NAME": "projectX",
                        "API_PROJECT_ORGANIZATION": "My Project Organization",
                        "API_PROJECT_DEVICE_TYPE": "BeagleBone Black",
                        "API_PROJECT_DEVICES_STATUS": "ERRORS"
                }
                ]
        }
}
```

Curl Example:
```bash
$ curl --verbose \
        -H "x-api-key: secret_key" \
        -H "API_USER_NAME: user.name" \
        -X GET https://api.ionoid.io/project/v1.0/
```


### 2.2 Create a New Project

To create a new Project use the following request.

Request:
```
POST https://api.ionoid.io/api/project/v1.0/new

Headers:
        "x-api-key": "secret_key"
        "API_USER_NAME": "user.name"
        'content-type: application/json'

body:
{
        "API_PROJECT_NAME":             "IoT-Blockchain",
        "API_PROJECT_TYPE":             "Blockchain",
        "API_PROJECT_ORGANIZATION":     "My Project Organization",
        "API_PROJECT_DEVICE_TYPE":      "Raspberry PI 3"
}
```

Response:
```json
{
        "statuscode": 201,
        "body": {
                "message": "Created",
                "project": {
                        "API_USER_ID": "3b36e0e2-5572-443d-bb04-7b3fb596c7fe",
                        "API_PROJECT_ID": "b504eae1-a2cc-4e56-a309-6d6dbdbba977",
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

Curl Example:
```
$ curl --verbose \
        -H "API_KEY: secret_key" \
        -H 'content-type: application/json' \
        -X POST -d '{"API_PROJECT_NAME": "ProjectBlockchainX", \
                "API_PROJECT_TYPE": "Blockchain", \
                "API_PROJECT_ORGANIZATION": "My Project Organization", \
                "API_PROJECT_DEVICE_TYPE": "Raspberry PI 3"}' \
        https://api.ionoid.io/api/project/v1.0/new
```

### 2.3. Information about Project X and List All its Devices

Retrieve detailed information about a Project and list all its devices.

Request:
```
GET https://api.ionoid.io/api/project/v1.0/{project_id}

GET https://api.ionoid.io/api/project/v1.0/b504eae1-a2cc-4e56-a309-6d6dbdbba977

Headers:
"x-api-key": "secret_key"
"API_USER_NAME": "user.name"
```

Response:
```json
{
        "statuscode": 200,
        "body": {
                "message": "OK",
                "project": {
                        "API_USER_ID": "3b36e0e2-5572-443d-bb04-7b3fb596c7fe",
                        "API_PROJECT_ID": "b504eae1-a2cc-4e56-a309-6d6dbdbba977",
                        "API_PROJECT_NAME": "IoT-Blockchain",
                        "API_PROJECT_TYPE": "Blockchain",
                        "API_PROJECT_ORGANIZATION": "My Project Organization",
                        "API_PROJECT_DEVICE_TYPE": "Raspberry PI 3",
                        "API_PROJECT_DEVICES_STATUS": "OK",
                        "API_PROJECT_DEVICES_COUNT": 2
                },
                "devices": [
                {
                        "API_USER_ID": "3b36e0e2-5572-443d-bb04-7b3fb596c7fe",
                        "API_PROJECT_ID": "b504eae1-a2cc-4e56-a309-6d6dbdbba977",
                        "API_DEVICE_UUID": "a61f2b04-e61f-42e1-9e6f-77301d4b8ee2",
                        "API_PROJECT_DEVICE_TYPE": "Raspberry PI 3",
                        "API_DEVICE_NAME": "Network:10:Node:32:x",
                        "API_DEVICE_STATUS": "ONLINE",
                        "API_DEVICE_OS_RELEASE": "v0.1",
                        "API_DEVICE_IS_LOCKED": false,
                        "API_DEVICE_ERRORS": 0
                },
                {
                        "API_USER_ID": "3b36e0e2-5572-443d-bb04-7b3fb596c7fe",
                        "API_PROJECT_ID": "b504eae1-a2cc-4e56-a309-6d6dbdbba977",
                        "API_DEVICE_UUID": "173782a9-221b-497c-b377-63191f8da497",
                        "API_PROJECT_DEVICE_TYPE": "Raspberry PI 3",
                        "API_DEVICE_NAME": "Network:10:Node:12:x",
                        "API_DEVICE_STATUS": "ONLINE",
                        "API_DEVICE_OS_RELEASE": "v0.1",
                        "API_DEVICE_IS_LOCKED": false,
                        "API_DEVICE_ERRORS": 0
                }
                ]
        }
}
```

Curl Example:
```bash
$ curl --verbose \
        -H "x-api-key: secret_key" \
        -H "API_USER_NAME: user.name" \
        -X GET https://api.ionoid.io/api/project/v1.0/b504eae1-a2cc-4e56-a309-6d6dbdbba977
```


### 2.4. Delete a Project

To Delete a project.

Request:
```
POST https://api.ionoid.io/api/project/v1.0/{project_id}

POST https://api.ionoid.io/api/project/v1.0/b504eae1-a2cc-4e56-a309-6d6dbdbba977

Headers:
"x-api-key": "secret_key"
"API_USER_NAME": "user.name"
'content-type: application/json'

body:
{
        "API_PROJECT_ACTION":   "delete"
}
```


## 3. Actions on Project X

Each Project supports a number of actions based on the device type and
the version of the Operating System.


### 3.1. Ping Devices of Project X

Ping all devices of a Project and get their status on the appropriate
Project channel.


#### 3.1.1 Ping Project and Devices

Request:
```
POST https://api.ionoid.io/api/project/v1.0/{project_id}

POST https://api.ionoid.io/api/project/v1.0/b504eae1-a2cc-4e56-a309-6d6dbdbba977

Headers:
"x-api-key": "secret_key"
"API_USER_NAME": "user.name"
'content-type: application/json'

body:
{
        "API_PROJECT_ACTION":   "ping"
}
```


To ping a specific Device, perform a POST request with same headers but
speficy the device UUID like:

```
POST https://api.ionoid.io/api/project/v1.0/b504eae1-a2cc-4e56-a309-6d6dbdbba977

Headers:
"x-api-key": "secret_key"
"API_USER_NAME": "user.name"
'content-type: application/json'

body:
{
        "API_DEVICE_UUID": "173782a9-221b-497c-b377-63191f8da497",
        "API_PROJECT_ACTION":   "ping"
}
```

#### 3.1.2 Subscribe to Ping Responses from Devices

After successfully sending a Ping Request, the client or reader should
subscribe automatically to the appropriate Project channel to not miss
any results from Devices.

Devices will start sending their status on the channel name:
`od_iot_channel_project_${project_id}_status`

The `${project_id}` is the **API Project ID**. In this example, the channel
name is:
`od_iot_channel_project_b504eae1-a2cc-4e56-a309-6d6dbdbba977_status`

Please check our [Ionoid IoT PUB/SUB API documentation](https://github.com/ionoid.io.opendevices.pubsub.api)
for more details.

Each device will send a response as a json object including its own
Device UUID as shown in this example:
```json
{
        "API_DEVICE_UUID": "173782a9-221b-497c-b377-63191f8da497",
        "API_DEVICE_NAME": "Network:10:Node:12:x",
        "API_DEVICE_STATUS": "ONLINE"
}
```

If there is no response device is assumed to be offline. Possible values
for `"API_DEVICE_STATUS": "ONLINE"`


#### 3.1.3 Response

The returned HTTP Response means that the request was processed
successfully. It does not mean that Devices are alive, only packets
published on the Project Channel will inform about the devices status.

Response on success:
```json
{
        "statuscode": 200,
        "body": {
                "message": "OK"
        }
}
```


### 3.2. Status of All Devices of Project X

Get status of all devices of a Project on the appropriate Project
channel.

Request:
```
POST https://api.ionoid.io/api/project/v1.0/{project_id}

Headers:
"x-api-key": "secret_key"
"API_USER_NAME": "user.name"
'content-type: application/json'

body:
{
        "API_PROJECT_ACTION":   "status"
}
```

To get status of a specific Device, perform a POST request with same
headers but specify the device UUID like:

```
POST https://api.ionoid.io/api/project/v1.0/b504eae1-a2cc-4e56-a309-6d6dbdbba977

Headers:
"x-api-key": "secret_key"
"API_USER_NAME": "user.name"
'content-type: application/json'

body:
{
        "API_DEVICE_UUID": "173782a9-221b-497c-b377-63191f8da497",
        "API_PROJECT_ACTION":   "status"
}
```

#### 3.2.2 Subscribe to Status Responses from Devices

After successfully sending a Status Request, the client or reader should
subscribe automatically to the appropriate Project channel to not miss
any results from Devices.

Devices will start sending their status on the channel name:
`od_iot_channel_project_${project_id}_status`

The `${project_id}` is the **API Project ID**. In this example, the channel
name is:
`od_iot_channel_project_b504eae1-a2cc-4e56-a309-6d6dbdbba977_status`

Please check our [Ionoid IoT PUB/SUB API documentation](https://github.com/ionoid.io.opendevices.pubsub.api)
for more details.

Each device will send a response as a json object including its own
Device UUID as shown in this example:
```json
{
        "API_DEVICE_UUID": "173782a9-221b-497c-b377-63191f8da497",
        "API_DEVICE_NAME": "Network:10:Node:12:x",
        "API_DEVICE_STATUS": "ONLINE"
}
```

If there is no response device is assumed to be offline. Possible values
for `"API_DEVICE_STATUS": "ONLINE", "OFFLINE" or "ERRORS"`

* **ONLINE**: means device is online and there are no errors.
* **OFFLINE**: means device is going offline.
* **ERRORS**: means device is online but there are errors. The status of
the Device is not clean.


#### 3.2.3 Response

The returned HTTP Response means that the request was processed
successfully. It does not mean that Devices are alive, only packets
published on the Project Channel will inform about the devices status.

Response on success:
```json
{
        "statuscode": 200,
        "body": {
                "message": "OK"
        }
}
```


### 3.3. Update Firmeware or OS of All Devices of Project X

TODO


### 3.4. Reboot All Devices of Project X

Reboot all Devices of a Project by sending an HTTP Post request to the
appropriate project.

Request:
```
POST https://api.ionoid.io/api/project/v1.0/{project_id}

POST https://api.ionoid.io/api/project/v1.0/b504eae1-a2cc-4e56-a309-6d6dbdbba977

Headers:
"x-api-key": "secret_key"
"API_USER_NAME": "user.name"
'content-type: application/json'

body:
{
        "API_PROJECT_ACTION":   "reboot"
}
```

To reboot a specific Device, perform a POST request with same headers but
speficy the device UUID like:

```
POST https://api.ionoid.io/api/project/v1.0/b504eae1-a2cc-4e56-a309-6d6dbdbba977

Headers:
"x-api-key": "secret_key"
"API_USER_NAME": "user.name"
'content-type: application/json'

body:
{
        "API_DEVICE_UUID": "173782a9-221b-497c-b377-63191f8da497",
        "API_PROJECT_ACTION":   "reboot"
}
```

#### 3.4.2 Subscribe to Reboot Responses from Devices

After successfully sending a Reboot Request, the client or reader should
subscribe automatically to the appropriate Project channel to not miss
any results from Devices.

Devices will start sending their status on the channel name:
`od_iot_channel_project_${project_id}_actions`

The `${project_id}` is the **API Project ID**. In this example, the channel
name is:
`od_iot_channel_project_b504eae1-a2cc-4e56-a309-6d6dbdbba977_actions`

Please check our [Ionoid IoT PUB/SUB API documentation](https://github.com/ionoid.io.opendevices.pubsub.api)
for more details.

Each device will send a response as a json object including its own
Device UUID as shown in this example:
```json
{
        "API_DEVICE_UUID": "173782a9-221b-497c-b377-63191f8da497",
        "API_DEVICE_NAME": "Network:10:Node:12:x",
        "API_DEVICE_STATUS": "OFFLINE",
}
```

If there is no response device is assumed to be offline. Possible values
for `"API_DEVICE_STATUS": "ONLINE", "OFFLINE" or "ERRORS"`

* **OFFLINE**: means device is going offline.
* **ERRORS**: means device has errors. The status of the Device is not clean.


#### 3.4.3 Response

The returned HTTP Response means that the request was processed
successfully. It does not mean that Devices are alive, only packets
published on the Project Channel will inform about the devices status.

Response on success:
```json
{
        "statuscode": 200,
        "body": {
                "message": "OK"
        }
}
```


### 3.5. Shutdown All Devices of Project X

Not supported for now.


### 3.6. Deploy an Application on All Devices of Project X

Deploy an application on all Devices of a Project by sending an
HTTP Post request to the appropriate project.

Request:
```
POST https://api.ionoid.io/api/project/v1.0/{project_id}

POST https://api.ionoid.io/api/project/v1.0/b504eae1-a2cc-4e56-a309-6d6dbdbba977

Headers:
"x-api-key": "secret_key"
"API_USER_NAME": "user.name"
'content-type: application/json'

body:
{
        "API_PROJECT_ACTION":   "deploy-app app-url",
        "API_APP_NAME":         "appname"
}
```

The `API_APP_NAME` field is optional. In case it is set it will be used,
otherwise the Application Name will be derivered from the Application
Url.


#### 3.6.2 Subscribe to Deploy Apps Responses from Devices

After successfully sending a Deploy App Request, the client or reader should
subscribe automatically to the appropriate Project channel to not miss
any results from Devices.

Devices will start sending their status on the channel name:
`od_iot_channel_project_${project_id}_status`

The `${project_id}` is the **API Project ID**. In this example, the channel
name is:
`od_iot_channel_project_b504eae1-a2cc-4e56-a309-6d6dbdbba977_actions`

Please check our [Ionoid IoT PUB/SUB API documentation](https://github.com/ionoid.io.opendevices.pubsub.api)
for more details.

Each device will send a response as a json object including its own
Device UUID as shown in this example:
```json
{
        "API_DEVICE_UUID": "173782a9-221b-497c-b377-63191f8da497",
        "API_DEVICE_NAME": "Network:10:Node:12:x",
        "API_PROJECT_ACTION": "OK"
}
```

If there is no response device is assumed to be offline or there was an
error.


#### 3.6.3 Response

The returned HTTP Response means that the request was processed
successfully. It does not mean that Devices are alive, only packets
published on the Project Channel will inform about the devices status.

Response on success:
```json
{
        "statuscode": 200,
        "body": {
                "message": "OK"
        }
}
```


### 3.7. Start an Application on All Devices of Project X

Start an application on all Devices of a Project by sending an
HTTP Post request to the appropriate project.

Request:
```
POST https://api.ionoid.io/api/project/v1.0/{project_id}

POST https://api.ionoid.io/api/project/v1.0/b504eae1-a2cc-4e56-a309-6d6dbdbba977

Headers:
"x-api-key": "secret_key"
"API_USER_NAME": "user.name"
'content-type: application/json'

body:
{
        "API_PROJECT_ACTION":   "start-app app-name"
}
```

To start an application on a specific Device, perform a POST request with same headers but
speficy the device UUID like:

```
POST https://api.ionoid.io/api/project/v1.0/b504eae1-a2cc-4e56-a309-6d6dbdbba977

Headers:
"x-api-key": "secret_key"
"API_USER_NAME": "user.name"
'content-type: application/json'

body:
{
        "API_DEVICE_UUID": "173782a9-221b-497c-b377-63191f8da497",
        "API_PROJECT_ACTION":   "start-app app-name"
}
```

### 3.8. Stop an Application from running on Project X

Stop an application that is running on Devices of a Project
by sending an HTTP Post request to the appropriate project.

Request:
```
POST https://api.ionoid.io/api/project/v1.0/{project_id}

POST https://api.ionoid.io/api/project/v1.0/b504eae1-a2cc-4e56-a309-6d6dbdbba977

Headers:
"x-api-key": "secret_key"
"API_USER_NAME": "user.name"
'content-type: application/json'

body:
{
        "API_PROJECT_ACTION":   "stop-app app-name"
}
```

To stop an application on a specific Device, perform a POST request with same headers but
speficy the device UUID like:

```
POST https://api.ionoid.io/api/project/v1.0/b504eae1-a2cc-4e56-a309-6d6dbdbba977

Headers:
"x-api-key": "secret_key"
"API_USER_NAME": "user.name"
'content-type: application/json'

body:
{
        "API_DEVICE_UUID": "173782a9-221b-497c-b377-63191f8da497",
        "API_PROJECT_ACTION":   "stop-app app-name"
}
```


### 3.9. Delete a Deployed Application from Project X

TODO


### 3.10. Request Logs from devices of Project X

To request the logs from devices of Project X:

* Send an HTTP API request to the appropriate project.
* Subscribe to the Project channel logs.

The logs are in `Json` Format. To stop devices from sending logs,
a `stop-logs` action is needed.


#### 3.10.1 Send HTTP Start Logs Request:

To instruct all Devices to send their logs, an HTTP request allows to do
so: 

```
POST https://api.ionoid.io/api/project/v1.0/{project_id}

POST https://api.ionoid.io/api/project/v1.0/b504eae1-a2cc-4e56-a309-6d6dbdbba977

Headers:
"x-api-key": "secret_key"
"API_USER_NAME": "user.name"
'content-type: application/json'

body:
{
        "API_PROJECT_ACTION":   "start-logs"
}
```

To get the logs of a specific Device, perform a POST request with same
headers but specify the device UUID like:

```
POST https://api.ionoid.io/api/project/v1.0/b504eae1-a2cc-4e56-a309-6d6dbdbba977

Headers:
"x-api-key": "secret_key"
"API_USER_NAME": "user.name"
'content-type: application/json'

body:
{
        "API_DEVICE_UUID": "173782a9-221b-497c-b377-63191f8da497",
        "API_PROJECT_ACTION":   "start-logs"
}
```

#### 3.9.2 Subscribe to Channel Logs results:

After successfully sending a Start Logs Request, the client or reader
should subscribe automatically to the appropriate channel logs to not
miss any results.

Devices will start sending their logs on the channel name:
`od_iot_channel_project_${project_id}_logs`

The `${project_id}` is the **API Project ID**. In this example, the channel
name is:
`od_iot_channel_project_b504eae1-a2cc-4e56-a309-6d6dbdbba977_logs`

Please check our [Ionoid IoT PUB/SUB API documentation](https://github.com/ionoid.io.opendevices.pubsub.api)
for more details.

Each device will send a response and logs as a json object including its own
Device UUID as shown in this example:
```json
{
        "API_DEVICE_UUID": "173782a9-221b-497c-b377-63191f8da497",
        "API_DEVICE_NAME": "Network:10:Node:12:x",
        "API_DEVICE_LOGS": {}
}
```

#### 3.9.3 Response

The returned HTTP Response means that the request was processed
successfully. It does not mean that Devices are alive, only packets
published on the Project Channel will inform about the devices status.

Response on success:
```json
{
        "statuscode": 200,
        "body": {
                "message": "OK"
        }
}
```


### 3.10. Stop Sending Logs from devices of Project X:

To stop devices of project X from sending their logs.

* Send an HTTP API request to the appripriate project.

Send HTTP Stop Logs Request:
```
POST https://api.ionoid.io/api/project/v1.0/{project_id}

POST https://api.ionoid.io/api/project/v1.0/b504eae1-a2cc-4e56-a309-6d6dbdbba977

Headers:
"x-api-key": "secret_key"
"API_USER_NAME": "user.name"
'content-type: application/json'

body:
{
        "API_PROJECT_ACTION":   "stop-logs"
}
```

To stop a specific device from sending its logs, perform a POST request with same
headers but specify the device UUID like:

```
POST https://api.ionoid.io/api/project/v1.0/b504eae1-a2cc-4e56-a309-6d6dbdbba977

Headers:
"x-api-key": "secret_key"
"API_USER_NAME": "user.name"
'content-type: application/json'

body:
{
        "API_DEVICE_UUID": "173782a9-221b-497c-b377-63191f8da497",
        "API_PROJECT_ACTION":   "stop-logs"
}
```

If the request is successfully received, the appropriate devices will
stop from sending their logs.
