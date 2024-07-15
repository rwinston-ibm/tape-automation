


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

### LOGIN
```
curl -k -H "Content-Type: application/json" -X POST https://192.0.2.0/web/api/v1/login -c cookies.txt -d "{\"user\":\"myusername\",\"password\":\"mypassword\"}" -v
```

### LOGOUT
```
curl -k -H "Content-Type: application/json" -X POST https://192.0.2.0/web/api/v1/logout -b cookies.txt
```

### Cleaning cartridges

#### GET/v1/cleaningCartridges
```
curl -k -b cookies.txt  -X GET https://192.0.2.0/web/api/v1/cleaningCartridges
```

#### GET /v1/cleaningCartridges/`<`volser`>`
Retrieves information about the cleaning cartridge with the specified VOLSER number.

```
curl -k -b cookies.txt  -X GET https://192.0.2.0/web/api/v1/cleaningCartridges/<volser>
```
where `<volser>` is taken from one of the cartridges returned by GET/v1/cleaningCartridges


#### GET /v1/cleaningCartridges/<internalAddress>
Retrieves information about the cleaning cartridge with the specified internalAddress.
curl -k -b cookies.txt  -X GET https://192.0.2.0/web/api/v1/cleaningCartridges/<internalAddress>
where <internalAddress> is taken from one of the cartridges returned by GET/v1/cleaningCartridges

Data cartridges
Data tape cartridges hold information that is written by a host securely and reliably. This information is read from and written to the cartridge by a tape drive.

GET /v1/dataCartridges
Retrieves information about all host-accessible or unassigned data cartridges in the tape library. If a data cartridge is removed from the library or missing during an inventory scan, it does not appear in this list.
curl -k -b cookies.txt  -X GET https://192.0.2.0/web/api/v1/dataCartridges

GET /v1/dataCartridges/<internalAddress>
Retrieves information about the data cartridge with the specified internalAddress.
curl -k -b cookies.txt  -X GET https://192.0.2.0/web/api/v1/dataCartridges/<internalAddress>
where <internalAddress> is taken from one of the cartridges returned by GET/v1/dataCartridges

GET /v1/dataCartridges/<volser>
Retrieves information about the data cartridge with the specified VOLSER number.
curl -k -b cookies.txt  -X GET https://192.0.2.0/web/api/v1/dataCartridges/<volser>
where <volser> is taken from one of the cartridges returned by GET/v1/dataCartridges

Diagnostic cartridges
Diagnostic cartridges are used periodically to test drive performance and troubleshoot problems.

GET /v1/diagnosticCartridges
Retrieves information about all diagnostic cartridges in the tape library.
curl -k -b cookies.txt  -X GET https://192.0.2.0/web/api/v1/diagnosticCartridges

GET /v1/diagnosticCartridges/<volser>
Retrieves information about the diagnostic cartridge with the specified VOLSER number.
curl -k -b cookies.txt  -X GET https://192.0.2.0/web/api/v1/diagnosticCartridges/<volser>
where <volser> is taken from one of the cartridges returned by GET/v1/diagnosticCartridges

GET /v1/diagnosticCartridges/<internalAddress>
Retrieves information about the diagnostic cartridge with the specified internalAddress.
curl -k -b cookies.txt  -X GET https://192.0.2.0/web/api/v1/diagnosticCartridges/<internalAddress>
where <internalAddress> is taken from one of the cartridges returned by GET/v1/diagnosticCartridges
 
Ethernet ports
Ethernet ports allow network access to the tape library.

GET /v1/ethernetPorts
Retrieves information about all Ethernet ports in the tape library.
curl -k -b cookies.txt  -X GET https://192.0.2.0/web/api/v1/ethernetPorts

Events
Library events are used to track all resource state changes within the library. The events are also listed in the GUI under the Monitoring > Events page. The cartridge movement is not a part of the events.

GET /v1/events
Retrieves a list of all events. Events can be filtered by date or time range and by a specific library component.
curl -k -b cookies.txt  -X GET https://192.0.2.0/web/api/v1/events

GET /v1/events/<ID>
Retrieves information about the events with the specified ID number.
curl -k -b cookies.txt  -X GET https://192.0.2.0/web/api/v1/events/<ID>
where <ID> is taken from one of the events returned by GET/v1/events

GET /v1/events/<ID>/fixProcedure
Retrieves fix procedure for the given error or warning event.
curl -k -b cookies.txt  -X GET https://192.0.2.0/web/api/v1/events/<ID>/fixProcedure
where <ID> is taken from one of the events returned by GET/v1/events

Fibre Channel ports
Fibre Channel ports that are installed on the drives allow reading, writing, and library control operations to be passed to the drive and library over the storage area network (SAN). They are identified by their location within the library.

GET /v1/fcPorts
Retrieves information about all Fibre Channel ports in the tape library.
curl -k -b cookies.txt  -X GET https://192.0.2.0/web/api/v1/fcPorts

GET /v1/fcports/<location>
Retrieves information about the Fibre Channel ports in the specified location.
curl -k -b cookies.txt  -X GET https://192.0.2.0/web/api/v1/fcports/<location>
where <location> is taken from one of the fcports returned by GET/v1/fcports

Get Fibre Channel ports
 
Frames
The frame in a library is the rack that houses all the components of the library and includes the front door, rear door, and side doors (if any).

GET /v1/frames
Retrieves information about all frames in the tape library.
curl -k -b cookies.txt  -X GET https://192.0.2.0/web/api/v1/frames

GET /v1/frames/<location>
Retrieves information about the frame in the specified location.
curl -k -b cookies.txt  -X GET https://192.0.2.0/web/api/v1/frames/<location>
where <location> is taken from one of the fcports returned by GET/v1/frames
 
I/O stations
I/O stations and magazines are used to insert or remove cartridges from the library without interrupting the operation of the library.

GET /v1/ioStations
Retrieves information about all I/O Stations in the tape library.
curl -k -b cookies.txt  -X GET https://192.0.2.0/web/api/v1/ioStations

GET /v1/iostations/<location>
Retrieves information about the I/O station in the specified location.
curl -k -b cookies.txt  -X GET https://192.0.2.0/web/api/v1/iostations/<location>
where <location> is taken from one of the fcports returned by GET/v1/iostations

 
Library
The library represents the physical tape library and its current library level settings.

GET /v1/library
Retrieves information about the library and its settings.
curl -k -b cookies.txt  -X GET https://192.0.2.0/web/api/v1/library

POST /v1/library/reset
Restarts the library.
curl -k -H "Content-Type: application/json" -X POST https://192.0.2.0/web/api/v1/library/reset -b cookies.txt

GET /v1/library/saveConfig
Saves the library configuration to a file external to the library. This file can be used with the restoreConfiguration CLI command to restore the library configuration back to what it was before.
curl -k -b cookies.txt  -X GET https://192.0.2.0/web/api/v1/library/saveConfig

Logs
Logs contain debug information that is used by the IBM Support to ensure they have all the information that they need to troubleshoot and repair tape library components quickly and reliably. These log files are not designed to be directly consumed by users.

GET /v1/logs
Retrieves a list of existing log files.
curl -k -b cookies.txt  -X GET https://192.0.2.0/web/api/v1/logs

GET /v1/logs/<filename>
Retrieves information about the log file with the specified file name.
curl -k -b cookies.txt  -X GET https://192.0.2.0/web/api/v1/logs/<filename>
where <filename> is the name of one of the files returned by GET /v1/logs

GET /v1/logs/<filename>/export
Exports the log file with the specified name.
curl -k -b cookies.txt  -X GET https://192.0.2.0/web/api/v1/logs/<filename>/export
where <filename> is the name of one of the files returned by GET /v1/logs

Node cards
Physical node cards within the library control all aspects of the library's operation.

GET /v1/nodeCards
Retrieves information about all node cards in the tape library.
curl -k -b cookies.txt  -X GET https://192.0.2.0/web/api/v1/nodeCards

GET /v1/nodeCards/<ID>
Retrieves information about the specified node card.
curl -k -b cookies.txt  -X GET https://192.0.2.0/web/api/v1/nodeCards/<ID>
where <ID> is the name of one of the files returned by GET /v1/nodeCards

POST /v1/nodeCards/<ID>/reset
Resets the specified node card.
curl -k -H "Content-Type: application/json" -X POST https://192.0.2.0/web/api/v1/nodeCards/<ID>/reset -b cookies.txt
where <ID> is the name of one of the files returned by GET /v1/nodeCards

Power supplies
Power supplies convert standard AC current to the lower voltage DC current used by the library.

GET /v1/powerSupplies
Retrieves information about all power supplies in the tape library.
curl -k -b cookies.txt  -X GET https://192.0.2.0/web/api/v1/powerSupplies

GET /v1/powerSupplies/<location>
Retrieves information about the power supplies in the specified location.
curl -k -b cookies.txt  -X GET https://192.0.2.0/web/api/v1/powerSupplies/<location>
where <location> is taken from one of the power supplies returned by GET /v1/powerSupplies

 
Logical libraries
A logical library is a set of tape drives and tape cartridges that are defined as a virtualized library by a user. The ability to partition logical libraries makes it possible for similar and dissimilar hosts (servers) to share a single physical library. As a result, hosts can simultaneously run separate software applications in separate logical libraries.

GET /v1/logicalLibraries
Retrieves information about the logical libraries that are partitioned in the library.
curl -k -b cookies.txt  -X GET https://192.0.2.0/web/api/v1/logicalLibraries

GET /v1/logicalLibraries/<name>
Retrieves information about the logical library with the specified name.
curl -k -b cookies.txt  -X GET https://192.0.2.0/web/api/v1/logicalLibraries/<name>
where <name> is taken from one of the logical libraries returned from GET /v1/logicalLibraries

GET /v1/logicalLibraries/<name>/voslerRanges
Retrieves the VOLSER ranges assigned to a given logical library that is partitioned in the library.
curl -k -b cookies.txt  -X GET https://192.0.2.0/web/api/v1/logicalLibraries/<name>/voslerRanges
where <name> is taken from one of the logical libraries returned from GET /v1/logicalLibraries


Reports
The reports contain usage history and other data for resources in the library. The data in the report is presented in a consistent, time centered way and are used to populate graphs or charts.

GET /v1/reports/library
Retrieves all reports for the last week.
curl -k -b cookies.txt  -X GET https://192.0.2.0/web/api/v1/reports/library

GET /v1/reports/drives
Retrieves all reports for the last week.
curl -k -b cookies.txt  -X GET https://192.0.2.0/web/api/v1/reports/drives

GET /v1/reports/accessors
Retrieves all reports for the last week.
curl -k -b cookies.txt  -X GET https://192.0.2.0/web/api/v1/reports/accessors

Robotic accessors
Robotic accessors move cartridges within the library in response to SCSI commands or manual move requests from the library’s interfaces. The accessor resource includes attributes that describe its two grippers and one bar code reader.

GET /v1/accessors
Retrieves information about all robotic accessors in the tape library.
curl -k -b cookies.txt  -X GET https://192.0.2.0/web/api/v1/accessors

 
Slots and Tiers
Cartridge storage slots in the tape library hold one or more tape cartridges. The TS4500 and Diamondback library offers high-density (HD) slots that are designed to greatly increase storage capacity without increasing frame size or required floor space. Each cartridge within a high-density slot stored is said to occupy a tier within in the slot.

GET /v1/slots
Retrieves information about all storage slots in the tape library.
curl -k -b cookies.txt  -X GET https://192.0.2.0/web/api/v1/slots

GET /v1/slots/<location>
Retrieves information about the storage slot in the specified location.
curl -k -b cookies.txt  -X GET https://192.0.2.0/web/api/v1/slots/<location>
where <location> is taken from one of the slots returned by GET /v1/slots
 
Tape drive
A tape drive reads data from and writes data to a cartridge mounted in the drive. It communicates over the SCSI interface to the host system. Control path drives handle library actions from the host system. All drives communicate with the library over an internal network.

GET /v1/drives
Retrieves information about all drives in the tape library.
curl -k -b cookies.txt  -X GET https://192.0.2.0/web/api/v1/drives

GET /v1/drives/<location>
Retrieves information about the drive in the specified location.
curl -k -b cookies.txt  -X GET https://192.0.2.0/web/api/v1/drives/<location>
where <location> is taken from one of the drives returned by GET /v1/drives

GET /v1/drives/<sn>
Retrieves information about the drive with the specified serial number.
curl -k -b cookies.txt  -X GET https://192.0.2.0/web/api/v1/drives/<sn>
where <sn> is taken from one of the drives returned by GET /v1/drives

POST /v1/drives/<location>/clean
Initiates a cleaning operation for the drive in the specified location.
curl -k -b cookies.txt  -X GET https://192.0.2.0/web/api/v1/drives/<location>
where <location> is taken from one of the drives returned by GET /v1/drives

POST /v1/drives/<sn>/clean
Initiates a cleaning operation for the drive with the specified serial number.
curl -k -H "Content-Type: application/json" -X POST https://192.0.2.0/web/api/v1/drives/<sn>/clean -b cookies.txt
where <sn> is taken from one of the drives returned by GET /v1/drives

PUT /v1/drives/<location> {"use": <"access" | "controlPath" | "verification">}
Modifies the use of the drive in the specified location (data access, control path, or verification).
curl -k -H "Content-Type: application/json" -X PUT https://192.0.2.0/web/api/v1/drives/<location> -b cookies.txt -d "{\"use\":\"access\"}"
curl -k -H "Content-Type: application/json" -X PUT https://192.0.2.0/web/api/v1/drives/<location> -b cookies.txt -d "{\"use\":\"controlPath\"}"
curl -k -H "Content-Type: application/json" -X PUT https://192.0.2.0/web/api/v1/drives/<location> -b cookies.txt -d "{\"use\":\"verification\"}"
where <location> is taken from one of the drives returned by GET /v1/drives

PUT /v1/drives/<sn> {"use": <"access" | "controlPath" | "verification">}
Modifies the use of the drive with the specified serial number (data access, control path, or verification).
curl -k -H "Content-Type: application/json" -X PUT  https://192.0.2.0/web/api/v1/drives/<sn> -b cookies.txt -d "{"use":\"access"\"}"
curl -k -H "Content-Type: application/json" -X PUT  https://192.0.2.0/web/api/v1/drives/<sn> -b cookies.txt -d "{"use":\"controlPath\"}"
curl -k -H "Content-Type: application/json" -X PUT  https://192.0.2.0/web/api/v1/drives/<sn> -b cookies.txt -d "{"use":\"verification\"}"
where <sn> is taken from one of the drives returned by GET /v1/drives

POST /v1/drives/<location>/reset {"mode": <"normal" | "hard">}
Restarts the drive in the specified location.
curl -k -H "Content-Type: application/json" -X POST https://192.0.2.0/web/api/v1/drives/<location>/reset -b cookies.txt -d "{\"mode\":\"hard\"}"
curl -k -H "Content-Type: application/json" -X POST https://192.0.2.0/web/api/v1/drives/<location>/reset -b cookies.txt -d "{\"mode\":\"normal\"}"
where <location> is taken from one of the drives returned by GET /v1/drives

POST /v1/drives/<sn>/reset {"mode": <"normal" | "hard">}
Restarts the drive with the specified serial number.
curl -k -H "Content-Type: application/json" -X POST https://192.0.2.0/web/api/v1/drives/<sn>/reset -b cookies.txt -d "{\"mode\":\"hard\"}"
curl -k -H "Content-Type: application/json" -X POST https://192.0.2.0/web/api/v1/drives/<sn>/reset -b cookies.txt -d "{\"mode\":\"normal\"}"
where <sn> is taken from one of the drives returned by GET /v1/drives

PUT /v1/drives/<sn> {"beacon": <"enabled" | "disabled">}
Turns beacon on or off for the drive with the specified serial number for the drive at the specified location.
curl -k -H "Content-Type: application/json" -X POST https://192.0.2.0/web/api/v1/drives/<sn> -b cookies.txt -d "{\"beacon\":\"disabled\"}"
curl -k -H "Content-Type: application/json" -X POST https://192.0.2.0/web/api/v1/drives/<sn> -b cookies.txt -d "{\"beacon\":\"enabled\"}"
where <sn> is taken from one of the drives returned by GET /v1/drives
 
Tasks
Tasks are used to submit and monitor asynchronous actions to the library. Each task describes its type (describes the action being taken), current state (in progress, completed, failed), and start time. After a task completes successfully, it is removed from the library and is no longer reported in the task list. To see the status of completed tasks, use the library event list.

GET /v1/tasks
Retrieves information about all currently running tasks.
curl -k -b cookies.txt  -X GET https://192.0.2.0/web/api/v1/tasks

GET /v1/tasks/<ID>
Retrieves information about the task with the specified ID number.
curl -k -b cookies.txt  -X GET https://192.0.2.0/web/api/v1/tasks/<ID>
where <ID> is the name of one of the tasks returned by GET /v1/tasks

POST /v1/tasks {"type": "inventoryTier0and1", "location": <"library" | "frame_F<f>">}
Runs an inventory scan on tiers 0 and 1 of the library or the specified frame. This starts a long-running task in the library that is visible from the GUI.
curl -k -H "Content-Type: application/json" -X POST https://192.0.2.0/web/api/v1/tasks -b cookies.txt -d "{\"type\":\"inventoryTier0and1\", \"location\":\"library\"}"

POST /v1/tasks [{"type": "inventoryAllTiers", "location": <"library" | "frame_F<f>">}]
Runs an inventory scan on all tiers of the library or the specified frame. This starts a long-running task in the library that is visible from the GUI.
curl -k -H "Content-Type: application/json" -X POST https://192.0.2.0/web/api/v1/tasks -b cookies.txt -d "{\"type\":\"inventoryAllTiers\", \"location\":\"library\"}"

POST /v1/tasks {"type": "startDriveService", "location": "drive_F<f>C<c>R<r>"}
Initiates a service action on the specified drive. This puts the drive in the inServiceMode state and starts a long-running task in the library that is visible from the GUI.
curl -k -H "Content-Type: application/json" -X POST https://192.0.2.0/web/api/v1/tasks -b cookies.txt -d "{\"type\":\"startDriveService\", \"location\":\"drive_F1C3R5\"}"

POST /v1/tasks {"type": "completeDriveService", "location": "drive_F<f>C<c>R<r>"}
Completes a service action on the specified drive. This takes the drive out of the inServiceMode state and starts a long-running task in the library that is visible from the GUI.
curl -k -H "Content-Type: application/json" -X POST https://192.0.2.0/web/api/v1/tasks -b cookies.txt -d "{\"type\":\"completetDriveService\", \"location\":\"drive_F1C3R5\"}"

POST /v1/tasks {"type": "calibrateLibrary", "accessor": "accessor_A<a|b>"}
Runs the calibration task on the library. This starts a long-running task in the library that is visible from the GUI.
curl -k -H "Content-Type: application/json" -X POST https://192.0.2.0/web/api/v1/tasks -b cookies.txt -d "{\"type\":\"calibrateLibrary\", \"accessor\":\"accessor_Aa\"}"

POST /v1/tasks {"type": "calibrateFrame", “location": "frame_F<f>", "accessor": “accessor_A<a|b>"}
Runs the calibration task on the given frame. This starts a long-running task in the library that is visible from the GUI.
curl -k -H "Content-Type: application/json" -X POST https://192.0.2.0/web/api/v1/tasks -b cookies.txt -d "{\"type\":\"calibrateFrame\", \"location\":\"frame_F1\", \"accessor\": \"accessor_Aa\"}"

POST /v1/tasks {"type": "calibrateAccessor", "accessor": "accessor_A<a|b>"}
Runs the calibration task on the given accessor. This starts a long-running task in the library that is visible from the GUI.
curl -k -H "Content-Type: application/json" -X POST https://192.0.2.0/web/api/v1/tasks -b cookies.txt -d "{\"type\":\"calibrateAccessor\", \"accessor\":\"accessor_Aa\"}"

POST /v1/tasks {"type": "testDrive", "location": "drive_F<f>C<c>R<r>"}
Starts a test drive operation by using a diagnostic cartridge. This starts a long-running task in the library that is visible from the GUI.
curl -k -H "Content-Type: application/json" -X POST https://192.0.2.0/web/api/v1/tasks -b cookies.txt -d "{\"type\":\"testDrive\", \"location\": \"drive_F1C5R3\"}"


Authentication
This shows an overview of the authentication settings in the library.

GET /v1/authentication/passwordPolicy
Retrieves information about password policy for local user accounts that are configured on the library.
curl -k -b cookies.txt  -X GET https://192.0.2.0/web/api/v1/authentication/passwordPolicy

GET /v1/authentication/sessions
Retrieves list sessions for user accounts that are authenticated and logged in to with the library.
curl -k -b cookies.txt  -X GET https://192.0.2.0/web/api/v1/authentication/sessions

GET /v1/authentication/sessions/<name>
Retrieves list of sessions for specified user account that is logged in to the library.
curl -k -b cookies.txt  -X GET https://192.0.2.0/web/api/v1/authentication/sessions/<name>
where <name> is taken from one of the names returned from GET /v1/sessions


POST /v1/authentication/sessions/<name>/disconnect {"reason": <reason>}
Disconnects all sessions for the given user account.
curl -k -H "Content-Type: application/json" -X POST https://192.0.2.0/web/api/v1/authentication/sessions/<name>/disconnect  -b cookies.txt -d "{\"reason\":\"<reason>\"}"
where <name> is taken from one of the names returned from GET /v1/sessions and <reason> is text explaining why the user is being disconnected.

 
Local user accounts
The local user accounts allowed to access the GUI, CLI, or REST API when local authentication is enabled.

GET /v1/authentication/userAccounts
Retrieves the local user accounts that are configured on this library.
curl -k -b cookies.txt  -X GET https://192.0.2.0/web/api/v1/authentication/userAccounts

GET /v1/authentication/userAccounts/<name>
Retrieves the user account of specified name.
curl -k -b cookies.txt  -X GET https://192.0.2.0/web/api/v1/authenticatiion/userAccounts/<name>
where <name> is taken from one of the names returned from GET /v1/userAccounts

POST /v1/authentication/userAccounts{"name": <name>, "role": <role>, "email": <email>, "password": <password>, "expirePassword": <"yes"|"no">}
Creates a local user account for the library.
curl -k -H "Content-Type: application/json" -X POST https://192.0.2.0/web/api/v1/authentication/userAccounts -b cookies.txt -d "{\"name\":\"<name>\", \"role\":\"<role>\", \"email\":\"<email>\", \"password\":\"<password>\", \"expirePassword\": <"yes"|"no">}"

where <name> is taken from one of the names returned from GET /v1/userAccounts and either "yes" or "no" must be specified for expirePassword parameter.

PUT /v1/authentication/userAccounts/<name> {"role": <role>, "email": <email>}
Modifies the email address or role of the user account.
curl -k -H "Content-Type: application/json" -X POST https://192.0.2.0/web/ap/v1/authentication/userAccounts/<name> i -b cookies.txt -d "{\"role\":\"<role>\", \"email\":\"<email>\"}"
where <name> is taken from one of the names returned from GET /v1/userAccounts

POST /v1/authentication/userAccounts/<name>/unlock
Unlocks a user account.
curl -k -H "Content-Type: application/json" -X POST https://192.0.2.0/web/api/v1/authentication/userAccounts/<name>/unlock -b cookies.txt -d
where <name> is taken from one of the names returned from GET /v1/userAccounts

POST /v1/authentication/userAccounts/<name>/setPassword{"password": <new password or temporary password>, "expirePassword": <"yes"|"no">}
Change a password for the user account.
curl -k -H "Content-Type: application/json" -X POST https://192.0.2.0/web/api/v1/authentication/userAccounts/<name>/setPassword -b cookies.txt -d "{\"password\":\"<new password or temporary password>\", \"expirePassword\": <"yes"|"no">}"
where <name> is taken from one of the names returned from GET /v1/userAccounts and either "yes" or "no" must be specified for expirePassword parameter.

Roles
User roles control how authenticated user accounts are authorized for command execution. The set of actions a user can perform depends on their role.

GET /v1/authentication/roles
Gets information about all the roles that are defined in the library.
curl -k -b cookies.txt  -X GET https://192.0.2.0/web/api/v1/authentication/roles

GET /v1/authentication/roles/<name>
Gets information about specified name of the role that is defined in the library.
curl -k -b cookies.txt  -X GET https://192.0.2.0/web/api/v1/authentication/roles/<name>
where <name> is taken from one of the names returned from GET /v1/roles
 
Syslog notifications
If the library is configured to send syslog (system log) notifications, it sends a notification of each event to the syslog server. The syslog server keeps its own log of events and can be set to filter them, distribute more notifications, or record them in any was as needed. Events sent to Syslog servers can be filtered at the library level by severity level (error, warning, and/or information).

GET /v1/notification/syslog/servers
Returns the list of Syslog servers that are registered with the library to receive Syslog notifications and their current settings.
curl -k -b cookies.txt  -X GET https://192.0.2.0/web/api/v1/notification/syslog/servers

GET /v1/notification/syslog/servers/<ipAddress>
Returns the list of Syslog servers for a specified IP address or host name.
curl -k -b cookies.txt  -X GET https://192.0.2.0/web/api/v1/notification/syslog/servers/<ipAddress>
where <ipAddress> is taken from one of the servers returned by GET /v1/notification/syslog/servers

 
GUI settings
GUI settings controls the behavior and view of the graphical user interface (GUI) that is used to manage the tape library.

GET /v1/guiSettings
Retrieves information about the password and session policy for the library.
curl -k -b cookies.txt  -X GET https://192.0.2.0/web/api/v1/guiSettings
