This open-source systems provides electronic health care functionality for “resource-constrained environments”.   While the system has not been designed for deployment within the United States, security and privacy concerns are still a paramount security concern for any patient.

For the first phase of the project, we will perform a security review based upon the OWASP Top 10 (use the 2017 RC1 version).  Our team will be responsible for documenting the findings and providing remediation suggestions to correct and adverse findings. 

## Software:
OpenMRS 2.6:  The standalone version is sufficient: (http://openmrs.org/download/)
For A10, we will use the OpenMRS REST Module: https://wiki.openmrs.org/display/docs/REST+Module

## Deliverables:<br/>
### 1. OWASP Top Ten (Ethical Hack Test Plan and Execution)<br/>
Repeatable black box test plan for the OWASP Top 10 Vulnerabilities.  For each of the Top 10 vulnerability, we create two repeatable test cases.  For each test case, we provide:
* A unique test case id
* Repeatable instructions for how to execute the test case
* Expected results when running the test case
For A9 (“Using Components with Known Vulnerabilities”), we will list the third-party software libraries the application uses as well as the database management system (DBMS) software.  Additionally, we will search at least 2 of the libraries and the DBMS name/version to see if any known vulnerabilities exist and document whether such vulnerabilities exist.  If vulnerabilities do exist, we will provide a brief sentence describing at least one with a link to the originating source material.

### 2. Run the test cases on OpenMRS (Version 2.6).<br/>
For each test case, we will report the actual results of running compared with the expected results and whether the test cases passes (indicating the system is secure) or fails (indicating the system is insecure).  We will describe the vulnerability and what it would take to stress the system to see if the vulnerability exists.  

### 3. For each of the Top 10, we will summarize our test results<br/>
If we do not find any vulnerabilities, document how we tested for each vulnerability and how the OpenMRS development team mitigated against such attacks.  
If we find a vulnerability, document repeatable instructions for replicating the vulnerability that should be submitted to OpenMRS.
