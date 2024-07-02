


<!-- Name of the example script -->
# cURL Examples for REST over Ethernet

<!-- Description of what the example script does -->
## Description

A user can construct REST over Ethernet requests using the following cURL examples. 
Requests must be made using an active session, created after successfully logging into the library.  
When the user is done sending requests, a logout request can be sent to close the session.
If no logout is sent, the session is automatically closed when it becomes inactive.

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
  



The **rest.py** script assumes the following:

  1. Where indicated '-ip' address is the IP address of the TS4500 or Diamondback
  2. Where indicated '-u' user is a valid login for the TS4500 or Diamondback
  3. Where indicated '-p' user password for user
  4. A user implementing this in production must edit the script to point the 'ca_file' variable to an actual certificate to utilize SSL


<!-- Show product support information here -->
## Product Support

This script was designed for the TS4500 and Diamondback tape libraries, and tested on code levels starting with 1.10.x.x and 2.10.x.x respectively.

<!-- Change history includes data and one line saying what changed -->
## Change History

  * July 2, 2024 - **Roberta Winston** - Initial release.


