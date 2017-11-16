## Usable Security Principles ##

### A. Visibility: ###

The administrative interface should allow users to easily review any active authority relationships that would affect security-relevant decisions. However OpenMRS don’t have this function. All the log information is stored within server information, and it is hard to find out the active authority relationships.

**Static Analysis**

**Test ID**: V-1

| Test step         | Test data     | States  |
| :---              | :---           | :---        |
|1. Log in as Admin	| account: admin <br> password: Admin123 <br> location: Pharmacy | You should see **System Administration**   |
|2. Click **System Administration** | | You could find **Advance Administration** option |
|2. Click **Advance Administration** | | You could find **Manage Roles** option |
|3. Click **Manage Roles** | |  |
|4. Make any change (like adding a role) and click save | | |
|5. Go back to **Advance Administration** and click **View Server Log** | | You should able to see that your operation is stored in the log with many other server logs |

**Assumption:** OpenMRS runs normally through the whole test process.

**Expected Result:** OpenMRS should have a function or UI allowing the user to easily review any active authority relationships that would affect security-relevant decisions.

**Actual Result:** 
The operation is stored in the log with many other server logs.
![](./images/V-1.PNG)

**Solution:** OpenMRS should implement a function to only show the active authority relationships that would affect security-relevant decisions.



### B. Clarity: ###
The administrative interface should not be misleading, ambiguous. However OpenMRS has some ambiguous error messages when registering a new user. Admin user needs to check the log information to know what is wrong during registration process.

**Static Analysis**

**Test ID**: C-1

| Test step         | Test data     | States  |
| :---              | :---           | :---        |
|1. Log in the system with wrong password | account: admin <br> password: wrong <br> location: Pharmacy  | You should see **System Administration**   |
|2. Click **System Administration** | | You should see **Manage Account** |
|3. Click **Manage Account** | | You should be able to **Add New Account**.|
|5. Add a new account with any name, username and other setting, but with password as abcd1234 and click **save** | password: abcd1234 | |

**Assumption:** OpenMRS runs normally through the whole test process.

**Expected Result:** OpenMRS should give user a clear error message about which part is wrong instead of just saving them in the log file.

**Actual Result:** 
The error message only shows it is a "Validation Error" without specifying which part goes wrong.
![](./images/C-1.PNG)


**Solution:** OpenMRS could summarize the error from the log and change the error message displayed into a more specific one. 



### C. Expected ability: ###
The administrative interface must not generate the impression that it is possible to do something that cannot actually be done. But OpenMRS sometimes gives user a feeling that they can do what they can’t do.

**Static Analysis**

**Test ID**: E-1

| Test step         | Test data     | States  |
| :---              | :---           | :---        |
|1. Log in the system with wrong password | account: admin <br> password: wrong <br> location: Pharmacy  | You should see **System Administration**   |
|2. Click **System Administration** | | You should see **Manage Account** |
|3. Click **Manage Account** | | You should be able to **Add New Account**.|
|4. Add a new account with only **Requests Appointments** privilege. Other fields are any personal choices that pass the validation |||
|5. Log out from admin account and Log in as the new user created|| No button in the main Page |
|6. Put URL *http://localhost:8080/openmrs-standalone/coreapps/systemadministration/systemAdministration.page* into browser and go to the page ||  |


**Assumption:** OpenMRS runs normally through the whole test process on port 8080.

**Expected Result:** The new user still could not see any options or buttons in the that page. And OpenMRS should not display any page that is above current user’s privilege.

**Actual Result:**
*Manage Global Properties* and *Manage Account* functions are now accessible to the new user.
![](./images/E-1.PNG)


**Solution:** OpenMRS should not redirect user to any page that they should not access. Full authentication function in the backend needs to be implemented.



