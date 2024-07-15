


<!-- Name of the example script -->
# GUide for using CURL for REST over Ethernet

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
curl -k -H "Content-Type: application/json" -X POST https://9.11.45.116/web/api/v1/login -c cookies.txt -d "{\"user\":\"penTestAdmin\",\"password\":\"Pen12345\"}" -v
```

### LOGOUT
```
curl -k -H "Content-Type: application/json" -X POST https://9.11.45.116/web/api/v1/logout -b cookies.txt
```

### Cleaning cartridges

#### GET/v1/cleaningCartridges
```
curl -k -b cookies.txt  -X GET https://9.11.45.116/web/api/v1/cleaningCartridges
```

#### GET /v1/cleaningCartridges/<volser>
Retrieves information about the cleaning cartridge with the specified VOLSER number.

```
curl -k -b cookies.txt  -X GET https://9.11.45.116/web/api/v1/cleaningCartridges/<volser>
```
where '<volser>' is taken from one of the cartridges returned by GET/v1/cleaningCartridges

