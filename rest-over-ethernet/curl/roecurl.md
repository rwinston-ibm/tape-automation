


<!-- Name of the example script -->
# Guide for using CURL for REST over Ethernet

<!-- Description of what the example script does -->
## Description

Curl can be used to send REST over Ethernet (RoE) requests to the TS4500 or Diamondback Tape Library. 
Once a user/script successfully logs into the library, the active session may be used to send further RoE requests to the library.
To close the session a logout request can be sent to the library.
Sessions left open will be closed, automatically, by the library once the session becomes inactive.

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

  * July 19, 2024 - **Roberta Winston** - Initial release.

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


### Accessors (TS4500 only)

##### GET /v1/accessors
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/accessors
```

##### GET /v1/accessors/`<location>`
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/accessors/accessor_Aa
```
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/accessors/accessor_Ab
```
##### PUT /v1/accessors/`<location>` {"velocityScalingXY": <value>, "velocityScalingPivot": <value>}
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/accessors/accessor_Aa -d "{\"velocityScalingXY\": 60, \"velocityScalingPivot\": 80}
```

### Cleaning Cartridges

#### GET/v1/cleaningCartridges
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/cleaningCartridges
```
#### GET /v1/cleaningCartridges/`<volser>`


```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/cleaningCartridges/CLNU87L9
```

#### GET /v1/cleaningCartridges/`<internalAddress>`

```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/cleaningCartridges/FF0400
```

### Data cartridges

###### GET /v1/dataCartridges

```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/dataCartridges
```

###### GET /v1/dataCartridges/`<internalAddress>`


```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/dataCartridges/FF0412
```

##### GET /v1/dataCartridges/`<volser>`

```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/dataCartridges/IBM011LT
```

### Diagnostic cartridges

##### GET /v1/diagnosticCartridges

```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/diagnosticCartridges
```

##### GET /v1/diagnosticCartridges/`<volser>`

```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/diagnosticCartridges/IBM011LT
```

##### GET /v1/diagnosticCartridges/`<internalAddress>`
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/diagnosticCartridges/FF0412
```
 
### Drives

##### GET /v1/drives
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/drives
```

##### GET /v1/drives/`<location>`
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/drives/drive_F1C3R2
```

##### GET /v1/drives/`<sn>`
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/drives/607BBFFFF8
```

##### POST /v1/drives/`<location>`/clean
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/drives/drive_F1C3R2
```

##### POST /v1/drives/`<sn>`/clean
```
curl -k -H "Content-Type: application/json" -X POST https://192.0.2.0/web/api/v1/drives/607BBFFFF8/clean -b cookies.txt
```

##### PUT /v1/drives/`<location>` {"use": <"access" | "controlPath" | "verification">}
```
curl -k -H "Content-Type: application/json" -X PUT https://192.0.2.0/web/api/v1/drives/drive_F1C2R4 -b cookies.txt -d "{\"use\":\"access\"}"
```
```
curl -k -H "Content-Type: application/json" -X PUT https://192.0.2.0/web/api/v1/drives/drive_F1C2R4 -b cookies.txt -d "{\"use\":\"controlPath\"}"
```
```
curl -k -H "Content-Type: application/json" -X PUT https://192.0.2.0/web/api/v1/drives/drive_F1C2R4 -b cookies.txt -d "{\"use\":\"verification\"}"
```

##### PUT /v1/drives/`<sn>` {"use": <"access" | "controlPath" | "verification">}
```
curl -k -H "Content-Type: application/json" -X PUT  https://192.0.2.0/web/api/v1/drives/drive_F1C2R4 -b cookies.txt -d "{"use":\"access"\"}"
```
```
curl -k -H "Content-Type: application/json" -X PUT  https://192.0.2.0/web/api/v1/drives/drive_F1C2R4-b cookies.txt -d "{"use":\"controlPath\"}"
```
```
curl -k -H "Content-Type: application/json" -X PUT  https://192.0.2.0/web/api/v1/drives/drive_F1C2R4 -b cookies.txt -d "{"use":\"verification\"}"
```

##### POST /v1/drives/<location>/reset {"mode": <"normal" | "hard">} 
```
curl -k -H "Content-Type: application/json" -X POST https://192.0.2.0/web/api/v1/drives/drive_F1C2R2/reset -b cookies.txt -d "{\"mode\":\"hard\"}"
```
```
curl -k -H "Content-Type: application/json" -X POST https://192.0.2.0/web/api/v1/drives/drive_F1C2R2/reset -b cookies.txt -d "{\"mode\":\"normal\"}"
```

##### POST /v1/drives/<sn>/reset {"mode": <"normal" | "hard">}
```
curl -k -H "Content-Type: application/json" -X POST https://192.0.2.0/web/api/v1/drives/drive_F1C2R2/reset -b cookies.txt -d "{\"mode\":\"hard\"}"
```
```
curl -k -H "Content-Type: application/json" -X POST https://192.0.2.0/web/api/v1/drives/drive_F1C2R2/reset -b cookies.txt -d "{\"mode\":\"normal\"}"
```

##### PUT /v1/drives/<sn> {"beacon": <"enabled" | "disabled">}
```
curl -k -H "Content-Type: application/json" -X POST https://192.0.2.0/web/api/v1/drives/drive_F1C2R2 -b cookies.txt -d "{\"beacon\":\"disabled\"}"
```
```
curl -k -H "Content-Type: application/json" -X POST https://192.0.2.0/web/api/v1/drives/drive_F1C2R2 -b cookies.txt -d "{\"beacon\":\"enabled\"}"
```

### Ethernet ports

##### GET /v1/ethernetPorts
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/ethernetPorts
```

##### GET /v1/ethernetPorts/`<location>`
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/ethernetPorts/ethernetPort_F1Pa
```

### Events

##### GET /v1/events
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/events
```

##### GET /v1/events/`<ID>`
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/events/876
```

##### GET /v1/events/`<ID>`/fixProcedure
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/events/1038/fixProcedure
```

### Fibre Channel ports

##### GET /v1/fcPorts
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/fcPorts
```

##### GET /v1/fcports/`<location>`
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/fcports/fcPort_F1C1R4P0
```

 
### Frames

##### GET /v1/frames
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/frames
```

##### GET /v1/frames/`<location>`
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/frames/frame_F1
```
 
### I/O stations

##### GET /v1/ioStations
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/ioStations
```

##### GET /v1/iostations/`<location>`
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/iostations/ioStation__C3
```

 
### Library

##### GET /v1/library
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/library
```

##### POST /v1/library/reset
```
curl -k -H "Content-Type: application/json" -X POST https://192.0.2.0/web/api/v1/library/reset -b cookies.txt
```

##### PUT /v1/library
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/library -d "{\"time\":\"2024-10-20T22:46:00\"}"
```

###### PUT /v1/library/saveConfig 
```
curl -k -b cookie.txt -X GET https://192.0.2.0/web/api/v1/library/saveConfig --output dbfile.dbz
```

###### POST /v1/library/restoreConfig  
```
curl -k -v -b cookie.txt -H "Content-Type: multipart/form-data" POST https://192.0.2.0/web/api/v1/library/restoreConfig -F 'filename=@dbfile.dbz; type=application/octet-stream'
```

### Logs

##### GET /v1/logs
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/logs
```

##### GET /v1/logs/`<filename>`
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/logs/TS4500_LOG_FA004_20240507102856.zip
```

##### GET /v1/logs/`<filename>`/export
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/logs/TS4500_LOG_FA004_20240507102856.zip/export
```

### Node cards

##### GET /v1/nodeCards
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/nodeCards
```

##### GET /v1/nodeCards/`<ID>`
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/nodeCards/65
```

##### POST /v1/nodeCards/`<ID>`/reset
```
curl -k -H "Content-Type: application/json" -X POST https://192.0.2.0/web/api/v1/nodeCards/65/reset -b cookies.txt
```

### Power supplies

##### GET /v1/powerSupplies
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/powerSupplies
```

##### GET /v1/powerSupplies/`<location>`
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/powerSupplies/powerSupply_F1PSa
```

 
### Logical libraries

##### GET /v1/logicalLibraries
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/logicalLibraries
```

##### GET /v1/logicalLibraries/`<name>`
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/logicalLibraries/BackupLib
```

##### GET /v1/logicalLibraries/`<name>`/voslerRanges
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/logicalLibraries/LogicalLibrary1/voslerRanges
```


### Reports

###### GET /v1/reports/accessors
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/reports/accessors
```

###### GET /v1/reports/accessors?after=<YYYY-MM-DDThh:mm:ss>&before=<YYYY-MM-DDThh:mm:ss
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/reports/accessors
```

###### GET /v1/reports/drives
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/reports/drives
```

###### GET /v1/reports/drives?after=<YYYY-MM-DDThh:mm:ss>&before=<YYYY-MM-DDThh:mm:ss>
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/reports/drives
```

###### GET /v1/reports/library
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/reports/library
```

###### GET /v1/reports/library?after=<YYYY-MM-DDThh:mm:ss>&before=<YYYY-MM-DDThh:mm:ss>
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/reports/library
```

 
### Slots and Tiers

##### GET /v1/slots
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/slots
```

##### GET /v1/slots/`<location>`
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/slots/slot_F1C4R8
```
 

 
### Tasks

##### GET /v1/tasks
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/tasks
```

##### GET /v1/tasks/`<ID>`
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/tasks/82
```

##### POST /v1/tasks {"type": "inventoryTier0and1", "location": <"library" | "frame_F`<f>`">}
```
curl -k -H "Content-Type: application/json" -X POST https://192.0.2.0/web/api/v1/tasks -b cookies.txt -d "{\"type\":\"inventoryTier0and1\", \"location\":\"library\"}"
```

##### POST /v1/tasks [{"type": "inventoryAllTiers", "location": <"library" | "frame_F`<f>`">}]
```
curl -k -H "Content-Type: application/json" -X POST https://192.0.2.0/web/api/v1/tasks -b cookies.txt -d "{\"type\":\"inventoryAllTiers\", \"location\":\"library\"}"
```

##### POST /v1/tasks {"type": "startDriveService", "location": "drive_F`<f>`C`<c>`R`<r>`"}
```
curl -k -H "Content-Type: application/json" -X POST https://192.0.2.0/web/api/v1/tasks -b cookies.txt -d "{\"type\":\"startDriveService\", \"location\":\"drive_F1C3R5\"}"
```

##### POST /v1/tasks {"type": "completeDriveService", "location": "drive_F`<f>`C`<c>`R`<r>`"}
```
curl -k -H "Content-Type: application/json" -X POST https://192.0.2.0/web/api/v1/tasks -b cookies.txt -d "{\"type\":\"completetDriveService\", \"location\":\"drive_F1C3R5\"}"
```

##### POST /v1/tasks {"type": "calibrateLibrary", "accessor": "accessor_A`<a|b>`"}
```
curl -k -H "Content-Type: application/json" -X POST https://192.0.2.0/web/api/v1/tasks -b cookies.txt -d "{\"type\":\"calibrateLibrary\", \"accessor\":\"accessor_Aa\"}"
```

##### POST /v1/tasks {"type": "calibrateFrame", “location": "frame_F`<f>`", "accessor": "accessor_A`<a|b>`"}
```
curl -k -H "Content-Type: application/json" -X POST https://192.0.2.0/web/api/v1/tasks -b cookies.txt -d "{\"type\":\"calibrateFrame\", \"location\":\"frame_F1\", \"accessor\": \"accessor_Aa\"}"
```

##### POST /v1/tasks {"type": "calibrateAccessor", "accessor": "accessor_A`<a|b>`"}
```
curl -k -H "Content-Type: application/json" -X POST https://192.0.2.0/web/api/v1/tasks -b cookies.txt -d "{\"type\":\"calibrateAccessor\", \"accessor\":\"accessor_Aa\"}"
```

##### POST /v1/tasks testDrive {"type": "testDrive", "location": "drive_F`<f>`C`<c>`R`<r>`"}
```
curl -k -H "Content-Type: application/json" -X POST https://192.0.2.0/web/api/v1/tasks -b cookies.txt -d "{\"type\":\"testDrive\", \"location\": \"drive_F1C5R3\"}"
```

##### POST /v1/tasks testDrive {"type": "updateLibraryFirmware"}
```
curl -k -H "Content-Type: multipart/form-data" POST https://192.0.2.0/web/api/v1/tasks -b cookie.txt -F 'filename=@TS4500_11100-05G.afwz; type=application/octet-stream' -F '{"type": "updateLibraryFirmware"};type= application/json'
```

##### POST /v1/tasks testDrive {"type": "updateDriveFirmware", "drive_F`<f>`C`<c>`R`<r>`"}
```
curl -k -H "Content-Type: multipart/form-data" POST https://192.0.2.0/web/api/v1/tasks -b cookie.txt -F 'filename=@D3I4_A0B.fcp_fj_D.fmrz; type=application/octet-stream' -F '{"type": "updateDriveFirmware", "location":"drive_F1C4R4"};type= application/json'
```

### Authentication

##### GET /v1/authentication/passwordPolicy
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/authentication/passwordPolicy
```

##### GET /v1/authentication/sessions
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/authentication/sessions
```

##### GET /v1/authentication/sessions/`<name>`
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/authentication/sessions/admin
```


##### POST /v1/authentication/sessions/`<name>`/disconnect
```
curl -k -H "Content-Type: application/json" -X POST https://192.0.2.0/web/api/v1/authentication/sessions/anotherusername/disconnect  -b cookies.txt -d "{\"reason\":\"`Need to use the library.`\"}"
```

 
### Local user accounts

##### GET /v1/authentication/userAccounts
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/authentication/userAccounts
```

##### GET /v1/authentication/userAccounts/`<name>`
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/authenticatiion/userAccounts/myusername
```

##### POST /v1/authentication/userAccounts
```
curl -k -H "Content-Type: application/json" -X POST https://192.0.2.0/web/api/v1/authentication/userAccounts -b cookies.txt -d "{\"name\":\"<name>\", \"role\":\"Administrator\", \"email\":\"username@example.com\", \"password\":\"mypassword\", \"expirePassword\": "no"}"
```

##### PUT /v1/authentication/userAccounts/`<name>` 
```
curl -k -H "Content-Type: application/json" -X POST https://192.0.2.0/web/ap/v1/authentication/userAccounts/myUsername i -b cookies.txt -d "{\"role\":\"Administrator\", \"email\":\"myusername@example.com\"}"
```

##### POST /v1/authentication/userAccounts/`<name>`/unlock
```
curl -k -H "Content-Type: application/json" -X POST https://192.0.2.0/web/api/v1/authentication/userAccounts/myusername/unlock -b cookies.txt -d
```

##### POST /v1/authentication/userAccounts/`<name>`/setPassword
```
curl -k -H "Content-Type: application/json" -X POST https://192.0.2.0/web/api/v1/authentication/userAccounts/admin/setPassword -b cookies.txt -d "{\"password\":\"mypassword\", \"expirePassword\": "yes"}"
```

### Roles

##### GET /v1/authentication/roles
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/authentication/roles
```

##### GET /v1/authentication/roles/`<name>`
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/authentication/roles/Administrator
```
 
### Syslog notifications

##### GET /v1/notification/syslog/servers
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/notification/syslog/servers
```

##### GET /v1/notification/syslog/servers/`<ipAddress>`
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/notification/syslog/servers/192.0.2.11
```

 
### GUI settings

##### GET /v1/guiSettings
```
curl -k -b cookies.txt -X GET https://192.0.2.0/web/api/v1/guiSettings
```





