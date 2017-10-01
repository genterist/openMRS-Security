Welcome to the openMRS-Security wiki!
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
      * Jquerry
            jquery-ui-1.9.2.custon.min.js
            jquery-1.12.4.min.js
            jquery.toastmessage.js
            jquery.simplemodal.1.4.4.min.js
      * UIcommons
            handlebars.min.js
            underscore-min.js
            knockout-2.2.1.js
            emr.js
            validator.js
            navigator.js
            navigatorHandlers.js
            navigatorModels.js
            navigatorTemplates.js
            exitHandlers.js
            typeahead.js
            personService.js
            personRelationship.js
      * AppUI

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
https://github.com/openmrs/openmrs-module-registrationapp/blob/master/omod/src/main/webapp/pages/registerPatient.gsp
https://github.com/openmrs/openmrs-module-registrationapp/blob/master/omod/src/main/webapp/pages/findPatient.gsp



## NETWORK BASED
Network based attack surface

### * Precondition
Pre-cond

### * Dependencies
Determine any dependencies on test requirements or other test cases

### * Attack surface



## LOCAL-HOST BASED

### * Precondition
Pre-cond

### * Dependencies
Determine any dependencies on test requirements or other test cases

### * Attack surface
1. OS
2. Browser
3. Javascript
4. SQL server
5. OpenMRS server



## HUMAN BASED
Human based attack surface

### * Precondition
Pre-cond

### * Dependencies
Determine any dependencies on test requirements or other test cases

### * Attack surface
