## Usable Security Principles ##

### A. Visibility: ###

The administrative interface should allow the user to easily review any active authority relationships that would affect security-relevant decisions. However OpenMrs don’t have this function all the log information is stored with server information, It’s hard to find out the active authority relationships.

### Static Analysis ###


| Test step         | test data     | states  |
| :---              | :---           | :---        |
|1.Login as Admin| | You should see System Administration   |
|2. Click System Administration||You should see Advence Administration|
|3. Click Advence Administration||You should able to Manage Roles|
|4. Make any change and click save|||
|5.Go back to Advance Administration and click Server Log||You should able to your operation is stored in many other server errors, which is very hard to find|

#### Expect Result: ####
OpenMrs should have a function to allow the user to easily review any active authority relationships that would affect security-relevant decisions.


#### Result: ####
Fail

#### Solution: ####
OpenMrs should implement a function to only show the active authority relationships that would affect security-relevant decisions.






###  Clarity: ###
The administrative interface should not be misleading, ambiguous. However OpenMrs have some ambiguous when register new user. Admin user need to check the Log information to know what is wrong during register process.

### Static Analysis ###


| Test step         | test data     | states  |
| :---              | :---           | :---        |
|1.Login as Admin| | You should see System Administration   |
|2. Click System Administration||You should see manage account|
|3. Click Manage Account||You should able to Add a new user.|
|4. Regist a new user with any username but password with abcd1234 and click save|abcd1234|You should see a error massage “validation error found”|

#### Expect Result: ####
OpenMrs should give user a specific error message about which part is wrong.

#### Result: ####
True

#### Solution: ####
OpenMrs should specify every error message in the user interface instead of just save in the log file.





###  Expected ability: ###
The administrative The interface must not generate the impression that it is possible to do something that cannot actually be done. But OpenMRS will give user a sense that they can do what they can’t do.

### Static Analysis ###


| Test step         | test data     | states  |
| :---              | :---           | :---        |
|1.Login as Admin| | You should see System Administration   |
|2. Click System Administration||You should see manage account|
|3. Click Manage Account||You should able to Add a new user.|
|4. Regist a new user with only only Requests Appointments privilege|||
|5. Log out and Log in with the new user||You should see the Manage Accounts again|
|6. Edit any account imformation||You should see your operation is successfully saved|
|7.Log in with admin and check the Log information||You should see your save operation is not successful because lack of the authority|





#### Expect Result: ####
 OpenMrs should not display any page that is above current user’s privilege

#### Result: ####
True

#### Solution: ####
OpenMrs should not redirect user to any page that they should not access and implement the full authentication function in the backend



