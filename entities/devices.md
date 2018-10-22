# Ionoid IoT Devices

A device represents an IoT Connected Device that is part of a registered
project on the Ionoid IoT Platform.


## 1. The Device Object

The Device Object can be accessed at:
```
https://api.ionoid.io/api/device/v1.0/
```

The Device Object is a `Json` Object

```json
{
        "API_DEVICE_NAME":              "Network:10:Node:32:x",
        "API_DEVICE_PRODUCT":           "Raspberry Pi 3",
        "API_DEVICE_STATUS":            "ONLINE",
        "API_DEVICE_OS_RELEASE":        "v0.1",
        "API_DEVICE_IS_LOCKED":         "false",
        "API_DEVICE_ERRORS":            12,
        "API_DEVICE_AGE":               1526113719,
        "API_DEVICE_UPTIME":            3600,
        "API_DEVICE_LAST_SEEN":         60,

        "API_DEVICE_ACTION":            "Action to Perform",

        "API_USER_ID":                  "3b36e0e2-5572-443d-bb04-7b3fb596c7fe",
        "API_PROJECT_ID":               "b504eae1-a2cc-4e56-a309-6d6dbdbba977",
        "API_PROJECT_OS":               "SealOS",
        "API_DEVICE_UUID":              "a61f2b04e61f42e19e6f77301d4b8ee2",
        "API_DEVICE_NETWORK_UUID":      "abb00baac9c8fbd0b2ac918f7fc2ba7d",
        "API_PROJECT_DEVICE_ARCH":      "ARMv7",
        "API_PROJECT_TAGS":             ["tag1", "tag2"],
        "API_DEVICE_SYSTEM_SETTINGS": {

        }
}
```

Summary of each field:

* **API_DEVICE_NAME**: The device name as set by user

* **API_DEVICE_PRODUCT** The device product type.

* **API_DEVICE_STATUS**: The status of the device.

* **API_DEVICE_OS_RELEASE**: The OS Release running on the device.

* **API_DEVICE_IS_LOCKED**: If the device is locked, if so operations on
it are blocked until it is unlocked.

* **API_DEVICE_ERRORS**: The errors encountered on the device.

* **API_DEVICE_AGE**: The device age in Unix time, represented by the
number of seconds elapsed since January 1, 1970 UTC.

* **API_DEVICE_UPTIME**: The device running age in Unix time, reppresented
by number of seconds elapsed since January 1, 1970 UTC.

* **API_DEVICE_LAST_SEEN**: Last time the device has contacted servers.
Period is in seconds.

* **API_DEVICE_ACTION**: The Action to perform on the device.

* **API_USER_ID**: The owner or creator of the project, used for API
Calls.

* **API_PROJECT_ID**: The Project ID, set internally and used for API

* **API_PROJECT_OS**: The Project Operating System.

* **API_DEVICE_UUID**: The Device Unique ID, usually this is
**/etc/machine-id** and it should be private to you as a user.

* **API_DEVICE_NETWORK_UUID**: The Hashed Device Unique ID, usually this
can be used in network or untrusted communications.

* **API_PROJECT_DEVICE_ARCH**: The Device architecture used by this Project

* **API_PROJECT_TAGS**: The Device tags used by this Project

* **API_DEVICE_SYSTEM_SETTINGS**: The Device System Configuration


## 2. Interact with Devices

### 2.1 List All Devices of a project

To list devices of a Project, we interact with the
project API.

Please see documentation about [Information about
Project](../entities/projects.md)


### 2.3. Information about a Device

To retrieve detailed information about a device.

Request:
```
GET https://api.ionoid.io/api/device/v1.0/{device_uuid}

GET https://api.ionoid.io/api/device/v1.0/173782a9-221b-497c-b377-63191f8da497

Headers:
"x-api-key": "secret_key"
"API_USER_NAME": "user.name"
"API_PROJECT_ID": "b504eae1-a2cc-4e56-a309-6d6dbdbba977"
```

Response:
```json
{
        "statuscode": 200,
        "body": {
                "message": "OK",
                "device": {
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
        }
}
```

Curl Example:
```bash
$ curl --verbose \
        -H "x-api-key: secret_key" \
        -H "API_USER_NAME: user.name" \
        -H "API_PROJECT_ID: b504eae1-a2cc-4e56-a309-6d6dbdbba977" \
        -X GET https://api.ionoid.io/api/device/v1.0/173782a9-221b-497c-b377-63191f8da497
```


### 2.4. Unregister a Device

To unregister a device.

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
        "API_DEVICE_UUID": "173782a9-221b-497c-b377-63191f8da497",
        "API_PROJECT_ACTION":    "delete-device"
}
```


## 3. Actions on a Device

Each Device supports a number of actions based on the device type, the
same actions are also supported per Project on all devices. Please be
careful when interacting on unique devices as these may desynchronize
your whole project.


### 3.1. Ping a Device

See [Ping Devices of Project X](../entities/projects.md)


### 3.2. Status of a Device

See [Status of Devices of Project X](../entities/projects.md)


### 3.3. Update Firmeware or OS of a Device

[Update Devices of Project X](../entities/projects.md)


### 3.4. Reboot a Device

See [Reboot Devices of Project X](../entities/projects.md)


### 3.5. Shutdown a Device

See [Shutdown Devices of Project X](../entities/projects.md)


### 3.6. Deploy an Application on a Device

See [Deploy an Application on Devices of Project X](../entities/projects.md)


### 3.7. Start an Application on a Device

See [Start Application on Devices of Project X](../entities/projects.md)


### 3.8. Stop an Application that is running on a Device

See [Stop Application running on Devices of Project X](../entities/projects.md)

### 3.9. Delete an Application that is deployed on a Device

See [Delete Application from Devices of Project X](../entitiers/projects.md)


## 4. Filter and Tag Devices

To Filter Devices you can apply tags on them, please see [Tag Devices of
Project X](../entities/projects.md)
