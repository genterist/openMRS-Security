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
|5.Go back to Advance Administration and click Server Log|||

#### Expect Result: ####
OpenMrs should have a function to allow the user to easily review any active authority relationships that would affect security-relevant decisions.


#### Result: ####
Fail

#### Solution: ####
OpenMrs should implement a function to only show the active authority relationships that would affect security-relevant decisions.
