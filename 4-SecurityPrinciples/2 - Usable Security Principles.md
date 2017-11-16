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


**Solution:** OpenMRS should implement a function to only show the active authority relationships that would affect security-relevant decisions.



### B. Clarity: ###
The administrative interface should not be misleading, ambiguous. However OpenMRS have some ambiguous error messages when registering a new user. Admin user need to check the log information to know what is wrong during registration process.

**Static Analysis**

**Test ID**: C-1

| Test step         | Test data     | States  |
| :---              | :---           | :---        |
|1. Log in the system with wrong password | account: admin <br> password: wrong <br> location: Pharmacy  | You should see **System Administration**   |
|2. Click **System Administration** | | You should see **Manage Account** |
|3. Click **Manage Account** | | You should be able to **Add New Account**.|
|5. Add a new account with any name, username and other setting, but with password as abcd1234 and click **save** | password: abcd1234 | You should able to see a message showing " Validation Error" |

**Assumption:** OpenMRS runs normally through the whole test process.

**Expected Result:** OpenMRS should give user a clear error message about which part is wrong instead of just save them in the log file.

**Actual Result:** 


**Solution:** OpenMRS could summarize the error from the log and change the error message displayed into a more detailed one. 



### C. Expected ability: ###
The administrative interface must not generate the impression that it is possible to do something that cannot actually be done. But OpenMRS will give user a feeling that they can do what they can’t do.

**Static Analysis**

**Test ID**: E-1

| Test step         | Test data     | States  |
| :---              | :---           | :---        |
|1. Log in the system with wrong password | account: admin <br> password: wrong <br> location: Pharmacy  | You should see **System Administration**   |
|2. Click **System Administration** | | You should see **Manage User** |
|3. Click **Manage User** | | You should be able to **Add** a new user.|
|4. Before adding a new user, a person should be chosen and click **Next** | person: John Smith | You should be create a user now |
|5. Register a new user with any username and setting, but password with abcd1234 and click save | password: abcd1234 | You should able to see a message showing error |
|1. Log in as Admin | account: admin <br> password: Admin123 <br> location: Pharmacy | You should see **System Administration**   |
|2. Click **System Administration** | | You should see **Manage User** |
|3. Click **Manage User** | | You should be able to **Add** a new user.|
|4. Before adding a new user, a person should be chosen and click **Next** | person: John Smith | You should be create a user now |
|4. Register a new user with only Requests Appointments privilege|||
|5. Log out and Log in with the new user||You should see the Manage Users again|
|6. Edit any account information||You should see your operation is successfully saved|
|7. Log in with admin and check the Log information||You should see your save operation is not successful because lack of the authority|

**Assumption:** OpenMRS runs normally through the whole test process.

**Expected Result:** OpenMRS should not display any page that is above current user’s privilege

**Actual Result:**


**Solution:** OpenMRS should not redirect user to any page that they should not access and implement the full authentication function in the backend.



