# ATTACK SURFACE ANALYSIS OF "FIND/CREATE PATIENT" MODULE

`AUTHOR : TAM N. NGUYEN` <br/>
`UPDATED ON : 01OCT2017` <br/>


### * Description
#### This report analysis focuses on the attack surface of the OpenMRS' "Register a paatient" (/openmrs/registrationapp/registerPatient.page?appId=referenceapplication.registrationapp.registerPatient) and "Find Patient Record" (/openmrs/coreapps/findpatient/findPatient.page?app=coreapps.findPatient). The purpose of this documentation is to support the design of misuse/abuse cases and other threat modeling tasks. By no mean this report is comprehensive since attack surface changes frequently, by many factors.
This report is based on OpenMRS docummentations and its live demo at https://demo.openmrs.org/openmrs/

## SOFTWARE BASED
Software based attack surface. By "Software", we mean all codes associated with the mentioned module, including API. We assume the software was installed locally, using proper default settings.

1. UIFramework
   1. Angular
      * angular.js
      * angular-common.js
      * angular-resource.min.js
      * ui-bootstrap-tpls-0.6.0.min.js
   2. Jquerry
      * jquery-ui-1.9.2.custon.min.js
      * jquery-1.12.4.min.js
      * jquery.toastmessage.js
      * jquery.simplemodal.1.4.4.min.js
   3. UIcommons
      * handlebars.min.js
      * underscore-min.js
      * knockout-2.2.1.js
      * emr.js
      * validator.js
      * navigator.js
      * navigatorHandlers.js
      * navigatorModels.js
      * navigatorTemplates.js
      * exitHandlers.js
      * typeahead.js
      * personService.js
      * personRelationship.js
   4. AppUI
   5. Maven

2. Registration App
Source code :
https://github.com/openmrs/openmrs-module-registrationapp
Directly affected page:
/openmrs/registrationapp/registerPatient.page
/openmrs/registrationapp/personName/getSimilarNames.action
      * API (https://github.com/openmrs/openmrs-module-registrationapp/tree/master/api/src/main/java/org/openmrs/module/registrationapp)
      * OMOD (https://github.com/openmrs/openmrs-module-registrationapp/tree/master/omod/src/main/webapp/pages)
      * Web-1.9 (https://github.com/openmrs/openmrs-module-registrationapp/tree/master/omod/src/main/webapp/pages)
      * Web-2.0 (https://github.com/openmrs/openmrs-module-registrationapp/tree/master/web-2.0/src/main/java/org/openmrs/module/registrationapp)

3. Page source codes
      * https://github.com/openmrs/openmrs-module-registrationapp/blob/master/omod/src/main/webapp/pages/registerPatient.gsp
      * https://github.com/openmrs/openmrs-module-registrationapp/blob/master/omod/src/main/webapp/pages/findPatient.gsp



## NETWORK BASED
Network based attack surface

### * Assumptions
While this is analysis is focused on the localized version of OpenMRS, we assume networking interfaces and default ports are opened. It is a reasonable assumption because the computer might be used for purposes other than hosting OpenMRS and those purposes may require internet connections. Even when there is absolutely no networked environment, it is still safe to assume network interfaces (ethernet and/or wifi) together with associated default ports (DNS, http,...) are open.

### * Attack surface
1. Ethernet ports
2. Wifi
3. Bluetooth
4. Common ports
      * TCP 20 and 21 (File Transfer Protocol, FTP)
      * TCP 22 (Secure Shell, SSH)
      * TCP 23 (Telnet)
      * TCP 25 (Simple Mail Transfer Protocol, SMTP)
      * TCP and UDP 53 (Domain Name System, DNS)
      * UDP 69 (Trivial File Transfer Protocol, tftp)
      * TCP 79 (finger)
      * TCP 80 (Hypertext Transfer Protocol, HTTP)
      * TCP 110 (Post Office Protocol v3, POP3)
      * TCP 119 (Network News Protocol, NNTP)
      * UDP 161 and 162 (Simple Network Management Protocol, SNMP)
      * UDP 443 (Secure Sockets Layer over HTTP, https)
5. OpenMRS ports
      * 8081
      * 8080
6. System service ports
      * Apache port
      * MySQL port
      * Java server port

## LOCAL-HOST BASED

### * Assumption
We assume the host OS is one of the most common OS'es such as Windows, Ubuntu, OS X, ... We also assume that most logged on sessions are regular user sessions and administrators sometimes log on to do system maintenance.

### * Attack surface
1. OS
      * Secret and security certificate stores
      * Settings
      * User stores
      * Regular file system
      * Memory, stacks, execution flows
      * Update mechanism
      * Policy stores
2. Browser
      * Cookies, saved passwords, cached files
      * Plugins
      * Script engines (Java, Javascript, ActiveX, VBScript, native client )
      * Browser access to devices (camera, microphone, printers, ...)
3. MySQL server
      * Server files
      * Command line interface
      * Admin tools (if installed)
      * Data values and structures
4. OpenMRS server
      * Serfer files
      * Github repo
      * Plugins
      * In-memory codes
5. Java
6. Machine
      * I/O devices
      * memory


## HUMAN BASED
Human based attack surface

### * Precondition
Pre-cond

### * Dependencies
Determine any dependencies on test requirements or other test cases

### * Attack surface
