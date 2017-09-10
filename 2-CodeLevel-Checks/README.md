The code level checks included in this folder:

1.  Password strength
Describtion of OpenMRS’s password policy (minimum and maximum password length, allowable characters, number of allowable character categories required, password age, password reuse policy, and account lock out.) Links with evidence for each of these policies where possible, or proof from the code directly or from experimentation with creating new passwords for each policy.

2.  Audit/logging implementation
10 test cases that will add/edit/delete/view sensitive medical data, with comments on OpenMRS's transaction log.

3.  Fuzzing with ZAP
We used the jbrofuzz rulesets (introduced in the initial ZAP activity) to perform a fuzzing exercise on OpenMRS with the following vulnerability types: Injection, Buffer Overflow, XSS, and SQL Injection. 
We pick at least one ruleset for each type of vulnerability listed. The ruleset should be appropriate for the target field and backend. We include the chosen fuzzers for each vulnerability type along with the results, and what we believe the team would need to do to fix any vulnerabilities we find. If we don't find any vulnerabilities, we will provide our reasoning as to why that was the case, and describe how we would adjust the fuzzing rules we used.

4.  Client-side bypassing with ZAP 
5 test cases in which we stop user input in OpenMRS with ZAP and change the input string to an attack.  
We include the page URL, the input field, the initial user input, and the malicious input, and describe what "filler" information is used for the rest of the fields on the page (if necessary). 

5.  Static analysis with Fortify
We generate the Fortify security reports.  Based upon these reports, we create a prioritized list of ten changes the systems developers should make to OpenMRS to correct the deficiencies found.  For each change, we document the change required, what weakness the change mitigates, and provide a cross-reference back to the originating report(s) where the issue was documented.

6.  Vulnerability history

We describe, in a broad sense, the vulnerabilities that the product has had in the past by searching the Internet with the URLs where we found the information.