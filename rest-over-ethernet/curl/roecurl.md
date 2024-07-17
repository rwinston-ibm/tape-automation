


<!-- Name of the example script -->
# Guide for using CURL for REST over Ethernet

<!-- Description of what the example script does -->
## Description

A user can construct REST over Ethernet requests to the TS4500 or Diamondback Tape Library using curl commands.
The first step is to log into the library to create an active session. 
Subsequent REST over Ethernet requests to the library can then use the active session.
Once the user is done using the REST over Ethernet API, a logout request can be sent to the library to close the session.
If the user does not logout of the session, it will automatically be closed by the library once the session becomes inactive.

<!-- Description of how to use the script -->
## Usage
```
curl GET|-X POST https://<ip>/web/api/<endpoint> [-k][-v][-c filename][-b filename][-H header][-d data]
```
Arguments:

  * **GET**                             GET request type 
  * **-X POST**                         POST request type
  * **-X PUT**                          PUT request type
  * **<ip>**                            IP address or hostname of library 
  * **<endpoint>**                      REST API endpoint
  * **-k**                              Skip certificate validation. This is used for libraries with self-signed certificates.
  * **-v** 	                            Verbose
  * **-c**  	                        Store session ID in filename (used only for Login request)
  * **-b** 	                            Use session ID in filename. 
  * **-H** 	                            Adds header string to request header (used in POST|PUT)
  * **-d**	                            Sends data in POST, PATCH, DELETE request
  
<!-- Show product support information here -->
## Product Support

The curl examples were designed for the TS4500 and Diamondback tape libraries, and tested on code levels starting with 1.10.x.x and 2.10.x.x respectively.

<!-- Change history includes data and one line saying what changed -->
## Change History

  * July 2, 2024 - **Roberta Winston** - Initial release.

<hr>

## CURL Examples

### Login

```
curl -k -H "Content-Type: application/json" -X POST https://192.0.2.0/web/api/v1/login -c cookies.txt -d "{\"user\":\"myusername\",\"password\":\"mypassword\"}" -v
```

### Logout

```
curl -k -H "Content-Type: application/json" -X POST https://192.0.2.0/web/api/v1/logout -b cookies.txt
```
### Cleaning Cartridges

#### Get All Cleaning Cartridges
##### GET/v1/cleaningCartridges

```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/cleaningCartridges
```

#### Get Cleaning Cartridge by Volser
##### GET /v1/cleaningCartridges/`<volser>`

```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/cleaningCartridges/<volser>
```
where `<volser>` is taken from one of the cartridges returned by GET/v1/cleaningCartridges


#### Get Cleaning Cartridge by Internal Address
##### GET /v1/cleaningCartridges/`<internalAddress>`

```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/cleaningCartridges/<internalAddress>
```
where `<internalAddress>` is taken from one of the cartridges returned by GET/v1/cleaningCartridges

### Data cartridges

#### GET /v1/dataCartridges

```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/dataCartridges
```

#### GET /v1/dataCartridges/`<internalAddress>`

```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/dataCartridges/<internalAddress>
```
where `<internalAddress>` is taken from one of the cartridges returned by GET/v1/dataCartridges

#### GET /v1/dataCartridges/`<volser>`

```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/dataCartridges/<volser>
```
where `<volser>` is taken from one of the cartridges returned by GET/v1/dataCartridges

### Diagnostic cartridges

#### GET /v1/diagnosticCartridges

```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/diagnosticCartridges
```

#### GET /v1/diagnosticCartridges/`<volser>`

```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/diagnosticCartridges/<volser>
```
where `<volser>` is taken from one of the cartridges returned by GET/v1/diagnosticCartridges

#### GET /v1/diagnosticCartridges/`<internalAddress>`

```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/diagnosticCartridges/<internalAddress>
```
where `<internalAddress>` is taken from one of the cartridges returned by GET/v1/diagnosticCartridges
 
### Ethernet ports

#### GET /v1/ethernetPorts
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/ethernetPorts
```

### Events

#### GET /v1/events
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/events
```

#### GET /v1/events/`<ID>`
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/events/<ID>
```
where `<ID>` is taken from one of the events returned by GET/v1/events

#### GET /v1/events/<ID>/fixProcedure
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/events/<ID>/fixProcedure
```
where `<ID>` is taken from one of the events returned by GET/v1/events

### Fibre Channel ports

#### GET /v1/fcPorts
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/fcPorts
```

#### GET /v1/fcports/`<location>`
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/fcports/<location>
```
where `<location>` is taken from one of the fcports returned by GET/v1/fcports

 
### Frames

#### GET /v1/frames
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/frames
```

#### GET /v1/frames/`<location>`
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/frames/<location>
```
where `<location>` is taken from one of the fcports returned by GET/v1/frames
 
### I/O stations

#### GET /v1/ioStations
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/ioStations
```

#### GET /v1/iostations/`<location>`
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/iostations/<location>
```
where `<location>` is taken from one of the fcports returned by GET/v1/iostations

 
### Library

#### GET /v1/library
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/library
```

#### POST /v1/library/reset
```
curl -k -H "Content-Type: application/json" -X POST https://192.0.2.0/web/api/v1/library/reset -b cookies.txt
```

#### GET /v1/library/saveConfig
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/library/saveConfig
```

### Logs

#### GET /v1/logs
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/logs
```

#### GET /v1/logs/`<filename>`
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/logs/<filename>
```
where `<filename>` is the name of one of the files returned by GET /v1/logs

#### GET /v1/logs/`<filename>`/export
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/logs/<filename>/export
```
where `<filename>` is the name of one of the files returned by GET /v1/logs

### Node cards

#### GET /v1/nodeCards
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/nodeCards
```

#### GET /v1/nodeCards/`<ID>`
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/nodeCards/<ID>
```
where `<ID>` is the name of one of the files returned by GET /v1/nodeCards

#### POST /v1/nodeCards/`<ID>`/reset
```
curl -k -H "Content-Type: application/json" -X POST https://192.0.2.0/web/api/v1/nodeCards/<ID>/reset -b cookies.txt
```
where `<ID>` is the name of one of the files returned by GET /v1/nodeCards

### Power supplies

#### GET /v1/powerSupplies
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/powerSupplies
```

#### GET /v1/powerSupplies/`<location>`
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/powerSupplies/<location>
```
where `<location>` is taken from one of the power supplies returned by GET /v1/powerSupplies

 
### Logical libraries

#### GET /v1/logicalLibraries
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/logicalLibraries
```

#### GET /v1/logicalLibraries/`<name>`
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/logicalLibraries/<name>
```
where `<name>` is taken from one of the logical libraries returned from GET /v1/logicalLibraries

#### GET /v1/logicalLibraries/`<name>`/voslerRanges
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/logicalLibraries/<name>/voslerRanges
```
where `<name>` is taken from one of the logical libraries returned from GET /v1/logicalLibraries


### Reports

#### Get Reports

##### GET /v1/reports/library
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/reports/library
```

##### GET /v1/reports/drives
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/reports/drives
```

##### GET /v1/reports/accessors
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/reports/accessors
```

#### Save Configuration
##### GET /v1/library/saveConfig 
```
curl -k -b cookie.txt -X GET https://192.0.2.0/web/api/v1/library/saveConfig --output dbfile.dbz
```

#### Restore Configuration
##### POST /v1/library/restoreConfig  
```
curl -k -v -b cookie.txt -H "Content-Type: multipart/form-data" POST https://192.0.2.0/web/api/v1/library/restoreConfig -F 'filename=@dbfile.dbz; type=application/octet-stream'
```

### Robotic accessors

#### GET /v1/accessors
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/accessors
```
 
### Slots and Tiers

#### GET /v1/slots
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/slots
```

#### GET /v1/slots/`<location>`
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/slots/<location>
```
where `<location>` is taken from one of the slots returned by GET /v1/slots
 
### Tape drive

#### GET /v1/drives
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/drives
```

#### GET /v1/drives/`<location>`
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/drives/<location>
```
where `<location>` is taken from one of the drives returned by GET /v1/drives

#### GET /v1/drives/`<sn>`
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/drives/<sn>
```
where `<sn>` is taken from one of the drives returned by GET /v1/drives

#### POST /v1/drives/`<location>`/clean
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/drives/<location>
```
where `<location>` is taken from one of the drives returned by GET /v1/drives

#### POST /v1/drives/`<sn>`/clean
```
curl -k -H "Content-Type: application/json" -X POST https://192.0.2.0/web/api/v1/drives/<sn>/clean -b cookies.txt
```
where `<sn>` is taken from one of the drives returned by GET /v1/drives

#### PUT /v1/drives/`<location>` {"use": <"access" | "controlPath" | "verification">}
```
curl -k -H "Content-Type: application/json" -X PUT https://192.0.2.0/web/api/v1/drives/<location> -b cookies.txt -d "{\"use\":\"access\"}"
```
```
curl -k -H "Content-Type: application/json" -X PUT https://192.0.2.0/web/api/v1/drives/<location> -b cookies.txt -d "{\"use\":\"controlPath\"}"
```
```
curl -k -H "Content-Type: application/json" -X PUT https://192.0.2.0/web/api/v1/drives/<location> -b cookies.txt -d "{\"use\":\"verification\"}"
```
where `<location>` is taken from one of the drives returned by GET /v1/drives

#### PUT /v1/drives/`<sn>` {"use": <"access" | "controlPath" | "verification">}
```
curl -k -H "Content-Type: application/json" -X PUT  https://192.0.2.0/web/api/v1/drives/<sn> -b cookies.txt -d "{"use":\"access"\"}"
```
```
curl -k -H "Content-Type: application/json" -X PUT  https://192.0.2.0/web/api/v1/drives/<sn> -b cookies.txt -d "{"use":\"controlPath\"}"
```
```
curl -k -H "Content-Type: application/json" -X PUT  https://192.0.2.0/web/api/v1/drives/<sn> -b cookies.txt -d "{"use":\"verification\"}"
```
where `<sn>` is taken from one of the drives returned by GET /v1/drives

#### POST /v1/drives/<location>/reset {"mode": <"normal" | "hard">} 
```
curl -k -H "Content-Type: application/json" -X POST https://192.0.2.0/web/api/v1/drives/<location>/reset -b cookies.txt -d "{\"mode\":\"hard\"}"
```
```
curl -k -H "Content-Type: application/json" -X POST https://192.0.2.0/web/api/v1/drives/<location>/reset -b cookies.txt -d "{\"mode\":\"normal\"}"
```
where `<location>` is taken from one of the drives returned by GET /v1/drives

#### POST /v1/drives/<sn>/reset {"mode": <"normal" | "hard">}
```
curl -k -H "Content-Type: application/json" -X POST https://192.0.2.0/web/api/v1/drives/<sn>/reset -b cookies.txt -d "{\"mode\":\"hard\"}"
```
```
curl -k -H "Content-Type: application/json" -X POST https://192.0.2.0/web/api/v1/drives/<sn>/reset -b cookies.txt -d "{\"mode\":\"normal\"}"
```
where `<sn>` is taken from one of the drives returned by GET /v1/drives

#### PUT /v1/drives/<sn> {"beacon": <"enabled" | "disabled">}
```
curl -k -H "Content-Type: application/json" -X POST https://192.0.2.0/web/api/v1/drives/<sn> -b cookies.txt -d "{\"beacon\":\"disabled\"}"
```
```
curl -k -H "Content-Type: application/json" -X POST https://192.0.2.0/web/api/v1/drives/<sn> -b cookies.txt -d "{\"beacon\":\"enabled\"}"
```
where `<sn>` is taken from one of the drives returned by GET /v1/drives
 
### Tasks

#### GET /v1/tasks
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/tasks
```

#### GET /v1/tasks/`<ID>`
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/tasks/<ID>
```
where `<ID>` is the name of one of the tasks returned by GET /v1/tasks

#### POST /v1/tasks {"type": "inventoryTier0and1", "location": <"library" | "frame_F`<f>`">}
```
curl -k -H "Content-Type: application/json" -X POST https://192.0.2.0/web/api/v1/tasks -b cookies.txt -d "{\"type\":\"inventoryTier0and1\", \"location\":\"library\"}"
```

#### POST /v1/tasks [{"type": "inventoryAllTiers", "location": <"library" | "frame_F`<f>`">}]
```
curl -k -H "Content-Type: application/json" -X POST https://192.0.2.0/web/api/v1/tasks -b cookies.txt -d "{\"type\":\"inventoryAllTiers\", \"location\":\"library\"}"
```

#### POST /v1/tasks {"type": "startDriveService", "location": "drive_F`<f>`C`<c>`R`<r>`"}
```
curl -k -H "Content-Type: application/json" -X POST https://192.0.2.0/web/api/v1/tasks -b cookies.txt -d "{\"type\":\"startDriveService\", \"location\":\"drive_F1C3R5\"}"
```

####  POST /v1/tasks {"type": "completeDriveService", "location": "drive_F`<f>`C`<c>`R`<r>`"}
```
curl -k -H "Content-Type: application/json" -X POST https://192.0.2.0/web/api/v1/tasks -b cookies.txt -d "{\"type\":\"completetDriveService\", \"location\":\"drive_F1C3R5\"}"
```

#### POST /v1/tasks {"type": "calibrateLibrary", "accessor": "accessor_A`<a|b>`"}
```
curl -k -H "Content-Type: application/json" -X POST https://192.0.2.0/web/api/v1/tasks -b cookies.txt -d "{\"type\":\"calibrateLibrary\", \"accessor\":\"accessor_Aa\"}"
```

#### POST /v1/tasks {"type": "calibrateFrame", “location": "frame_F`<f>`", "accessor": "accessor_A`<a|b>`"}
```
curl -k -H "Content-Type: application/json" -X POST https://192.0.2.0/web/api/v1/tasks -b cookies.txt -d "{\"type\":\"calibrateFrame\", \"location\":\"frame_F1\", \"accessor\": \"accessor_Aa\"}"
```

#### POST /v1/tasks {"type": "calibrateAccessor", "accessor": "accessor_A`<a|b>`"}
```
curl -k -H "Content-Type: application/json" -X POST https://192.0.2.0/web/api/v1/tasks -b cookies.txt -d "{\"type\":\"calibrateAccessor\", \"accessor\":\"accessor_Aa\"}"
```

#### POST /v1/tasks testDrive {"type": "testDrive", "location": "drive_F`<f>`C`<c>`R`<r>`"}
```
curl -k -H "Content-Type: application/json" -X POST https://192.0.2.0/web/api/v1/tasks -b cookies.txt -d "{\"type\":\"testDrive\", \"location\": \"drive_F1C5R3\"}"
```

#### POST /v1/tasks testDrive {"type": "updateLibraryFirmware"}
Content type must be multipart form-data to send both the json data and file contents in a single http request. 
```
curl -k -H "Content-Type: multipart/form-data" POST https://192.0.2.0/web/api/v1/tasks -b cookie.txt -F 'filename=@TS4500_11100-05G.afwz; type=application/octet-stream' -F '{"type": "updateLibraryFirmware"};type= application/json'
```

#### POST /v1/tasks testDrive {"type": "updateDriveFirmware", "drive_F`<f>`C`<c>`R`<r>`"}
Content type must be multipart form-data to send both the json data and file contents in a single http request. 
```
curl -k -H "Content-Type: multipart/form-data" POST https://192.0.2.0/web/api/v1/tasks -b cookie.txt -F 'filename=@D3I4_A0B.fcp_fj_D.fmrz; type=application/octet-stream' -F '{"type": "updateDriveFirmware", "location":"drive_F1C4R4"};type= application/json'
```

### Authentication

#### GET /v1/authentication/passwordPolicy
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/authentication/passwordPolicy
```

#### GET /v1/authentication/sessions
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/authentication/sessions
```

#### GET /v1/authentication/sessions/`<name>`
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/authentication/sessions/<name>
```
where `<name>` is taken from one of the names returned from GET /v1/sessions


#### POST /v1/authentication/sessions/`<name>`/disconnect
```
curl -k -H "Content-Type: application/json" -X POST https://192.0.2.0/web/api/v1/authentication/sessions/<name>/disconnect  -b cookies.txt -d "{\"reason\":\"`<reason>`\"}"
```
where `<name>` is taken from one of the names returned from GET /v1/sessions and `<reason>` is text explaining why the user is being disconnected.

 
### Local user accounts

#### GET /v1/authentication/userAccounts
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/authentication/userAccounts
```

#### GET /v1/authentication/userAccounts/`<name>`
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/authenticatiion/userAccounts/<name>
```
where `<name>` is taken from one of the names returned from GET /v1/userAccounts

#### POST /v1/authentication/userAccounts
```
curl -k -H "Content-Type: application/json" -X POST https://192.0.2.0/web/api/v1/authentication/userAccounts -b cookies.txt -d "{\"name\":\"<name>\", \"role\":\"<role>\", \"email\":\"<email>\", \"password\":\"<password>\", \"expirePassword\": <"yes"|"no">}"
```
where `<name>` is taken from one of the names returned from GET /v1/userAccounts and either "yes" or "no" must be specified for expirePassword parameter.

#### PUT /v1/authentication/userAccounts/`<name>` 
```
curl -k -H "Content-Type: application/json" -X POST https://192.0.2.0/web/ap/v1/authentication/userAccounts/<name> i -b cookies.txt -d "{\"role\":\"<role>\", \"email\":\"<email>\"}"
```
where `<name>` is taken from one of the names returned from GET /v1/userAccounts

#### POST /v1/authentication/userAccounts/`<name>`/unlock
```
curl -k -H "Content-Type: application/json" -X POST https://192.0.2.0/web/api/v1/authentication/userAccounts/<name>/unlock -b cookies.txt -d
```
where `<name>` is taken from one of the names returned from GET /v1/userAccounts

#### POST /v1/authentication/userAccounts/`<name>`/setPassword
```
curl -k -H "Content-Type: application/json" -X POST https://192.0.2.0/web/api/v1/authentication/userAccounts/<name>/setPassword -b cookies.txt -d "{\"password\":\"<new password or temporary password>\", \"expirePassword\": <"yes"|"no">}"
```
where `<name>` is taken from one of the names returned from GET /v1/userAccounts and either "yes" or "no" must be specified for expirePassword parameter.

### Roles

#### GET /v1/authentication/roles
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/authentication/roles
```

#### GET /v1/authentication/roles/`<name>`
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/authentication/roles/<name>
```
where `<name>` is taken from one of the names returned from GET /v1/roles
 
### Syslog notifications

#### GET /v1/notification/syslog/servers
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/notification/syslog/servers
```

#### GET /v1/notification/syslog/servers/`<ipAddress>`
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/notification/syslog/servers/<ipAddress>
```
where `<ipAddress>` is taken from one of the servers returned by GET /v1/notification/syslog/servers

 
### GUI settings

#### GET /v1/guiSettings
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/guiSettings
```





