# Architectural Design Principles
`DESIGNER : Zhuo Li` <br/>
`EXECUTED BY : Zhuo Li` <br/>
`UPDATED ON : 31OCT17` <br/>
`EXECUTED ON : 31OCT17` <br/>

### ADP01
Least Privilege : A subject (user/other system) should be given only those privileges it needs to complete its task.

Test Step:
Step 1: Login as System admin(sysadmin).
Step 2: Then enter Appointment Scheduling and click Manage Service Types.
Step 3: Click New Service Type then copy the url.http://localhost:8082/openmrs-standalone/appointmentschedulingui/appointmentType.page
Step 4: Log out and Login as an clerk.
Step 5: Paste the url and then you will find you can manage the service type as a clerk.

Result: Failed. As we can see, the privilege of a clerk only include manage appointments, daily appointments and appointments required. Service type is not a function that the clerk can manage.

Solution: The system should manage the access control using something like Role Based Access Control instead of url access. The system should check the role on both client and server side.

![alt text](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/SecReq01.PNG)

### ADP02
Securing the Weakest Link : Attackers are more likely to attack a weak spot in a software system than to penetrate a heavily fortified component.

Test Step:
Step 1: Login as admin(admin).
Step 2: Then click register a patient.

Result: Failed. Web application show session id, Fail the test. Hacker can hijack this session and get
full access of the system.

Solution : Apply the filter function to the whole system, not only the search part.
![alt text](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/SecReq02.PNG)

### ADP03
Quiet Your Error Messages : Attackers can cause system errors intentionally to gather information about the system. Error messages should be minimalistic, without giving details on the failure.

Test Step:
Step 1: Login as admin(admin).
Step 2: Click register a patient.
Step 3: Delete the appId part of the url. http://localhost:8082/openmrs-standalone/registrationapp/registerPatient.page
Step 4: See if there are some detailed error message.

Result: Failed. There are detailed error message about the source code. The hacker can try multiple error to get the logic and detail about the source code.

Solution: The system should only return a simple error message without showing any detail about the code. E.g. 404 Error.

![alt text](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/SecReq03.PNG)


