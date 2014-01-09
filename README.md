bCDMI
=====
Simple Bash client for basic CDMI storage operations.

The script support different authentication methods:
 * basic             HTTP basic authentication  (username/password)
 * token             HTTP token authentication
 * keystone-basic    Keystone auth token (with username/password authentication)
 * keystone-voms     Keystone auth toke (with VOMS-enabled certificates)

and the following CDMI operations:
 * auth        Display auth information (for integration with other services)
 * list        List contents of the container [default action]
 * stat        Get info for the file (as CDMI metadata)
 * get         Download file
 * put         Upload a file (needs -T switch in the arguments)
 * post        Update metadata (ex. file ACL, see post command options for the full metadata list)
 * delete      Delete a file (or container)
 * mkdir       Create folder

Requirements
=====
This script requires:
 * cURL
 * fetch-crl and voms-clients (For keystone-voms support)

To install the script, just copy it and the sample bcdmi.auth file into your home/bin folder.

Configuration
=====
Prior using the software, you need to configure the authorization file (default bcdmi.auth). See the comments in the sample configuration bcdmi.auth to check how to fill the file.

Usage
=====
 ./bcdmi -e <endpoint> <action> [options]

<endpoint> is the endpoint of the CDMI service.

<action> is the action to be performed on the storage. Possible actions are:
  auth        Display auth information (for integration with other services)
  list        List contents of the container [default action]
  stat        Get info for the file (as CDMI metadata)
  get         Download file
  put         Upload a file (needs -T switch in the arguments)
  post        Update metadata (see post command options for the metadata list)
  delete      Delete a file (or container)
  mkdir       Create folder

Generic options:
  -o | --output <file>      Redirect output to file <file>
  --auth-file <file>        Local authorization file. Default authorization file is ./bcdmi.auth .
                            This file cointains the service authorization data. See sample authorization file for more info
  -a | --auth               Override authorization data (format shall be understandable by cURL command line).
  --cdmi-version <version>  Version of the CDMI standard to use (default 1.0.1)
  --crl-update              Update CRL before creating a new proxy. Recommended if fetch-crl is not enabled in the cron (ex. on Windows machines)

put command:
 -T | --upload-file <file>  File to upload [mandatory]

delete command:
  -r                        Enable recursive directory deletion

post command:
  -m <metadata>             Add metadata features. Metadata format is pipe separated <name>=<value> . Allowed metadata is
    readacl                   Read permission for containers. Allowed values are '.r:*' or '.'
    weblist                   Listing of container contents in web format. Allowed values are 'true' or 'false'

