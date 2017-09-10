# ZAP Scanning Report 1




## Summary of alerts

| Risk Level | Number of Alerts |
| --- | --- |
| High | 3 |
| Medium | 3 |
| Low | 4 |
| Informational | 0 |


## Alert details  

### SQL Injection
##### High (Medium)
  
  
  
  
#### Description
<p>SQL injection may be possible.</p>
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/referenceapplication/login.page;jsessionid=5038D26982756CDE5D33312187C191EB?query=query+AND+1%3D1+--+](http://localhost:8081/openmrs-standalone/referenceapplication/login.page;jsessionid=5038D26982756CDE5D33312187C191EB?query=query+AND+1%3D1+--+)
  
  
  * Method: `GET`
  
  
  * Parameter: `query`
  
  
  * Attack: `query AND 1=1 -- `
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/referenceapplication/login.page?query=query%27+AND+%271%27%3D%271](http://localhost:8081/openmrs-standalone/referenceapplication/login.page?query=query%27+AND+%271%27%3D%271)
  
  
  * Method: `GET`
  
  
  * Parameter: `query`
  
  
  * Attack: `query' AND '1'='1`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/login.htm?query=query+AND+1%3D1](http://localhost:8081/openmrs-standalone/login.htm?query=query+AND+1%3D1)
  
  
  * Method: `GET`
  
  
  * Parameter: `query`
  
  
  * Attack: `query AND 1=1`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/referenceapplication/login.page;jsessionid=5038D26982756CDE5D33312187C191EB?query=query%27+AND+%271%27%3D%271%27+--+](http://localhost:8081/openmrs-standalone/referenceapplication/login.page;jsessionid=5038D26982756CDE5D33312187C191EB?query=query%27+AND+%271%27%3D%271%27+--+)
  
  
  * Method: `GET`
  
  
  * Parameter: `query`
  
  
  * Attack: `query' AND '1'='1' -- `
  
  
  
  
Instances: 4
  
### Solution
<p>Do not trust client side input, even if there is client side validation in place.  </p><p>In general, type check all data on the server side.</p><p>If the application uses JDBC, use PreparedStatement or CallableStatement, with parameters passed by '?'</p><p>If the application uses ASP, use ADO Command Objects with strong type checking and parameterized queries.</p><p>If database Stored Procedures can be used, use them.</p><p>Do *not* concatenate strings into queries in the stored procedure, or use 'exec', 'exec immediate', or equivalent functionality!</p><p>Do not create dynamic SQL queries using simple string concatenation.</p><p>Escape all data received from the client.</p><p>Apply a 'whitelist' of allowed characters, or a 'blacklist' of disallowed characters in user input.</p><p>Apply the principle of least privilege by using the least privileged database user possible.</p><p>In particular, avoid using the 'sa' or 'db-owner' database users. This does not eliminate SQL injection, but minimizes its impact.</p><p>Grant the minimum database access that is necessary for the application.</p>
  
### Other information
<p>The page results were successfully manipulated using the boolean conditions [query AND 1=1 -- ] and [query AND 1=2 -- ]</p><p>The parameter value being modified was NOT stripped from the HTML output for the purposes of the comparison</p><p>Data was returned for the original parameter.</p><p>The vulnerability was detected by successfully restricting the data originally returned, by manipulating the parameter</p>
  
### Reference
* https://www.owasp.org/index.php/Top_10_2010-A1
* https://www.owasp.org/index.php/SQL_Injection_Prevention_Cheat_Sheet

  
#### CWE Id : 89
  
#### WASC Id : 19
  
#### Source ID : 1

  
  
  
### Cross Site Scripting (Reflected)
##### High (Medium)
  
  
  
  
#### Description
<p>Cross-site Scripting (XSS) is an attack technique that involves echoing attacker-supplied code into a user's browser instance. A browser instance can be a standard web browser client, or a browser object embedded in a software product such as the browser within WinAmp, an RSS reader, or an email client. The code itself is usually written in HTML/JavaScript, but may also extend to VBScript, ActiveX, Java, Flash, or any other browser-supported technology.</p><p>When an attacker gets a user's browser to execute his/her code, the code will run within the security context (or zone) of the hosting web site. With this level of privilege, the code has the ability to read, modify and transmit any sensitive data accessible by the browser. A Cross-site Scripted user could have his/her account hijacked (cookie theft), their browser redirected to another location, or possibly shown fraudulent content delivered by the web site they are visiting. Cross-site Scripting attacks essentially compromise the trust relationship between a user and the web site. Applications utilizing browser object instances which load content from the file system may execute code under the local machine zone allowing for system compromise.</p><p></p><p>There are three types of Cross-site Scripting attacks: non-persistent, persistent and DOM-based.</p><p>Non-persistent attacks and DOM-based attacks require a user to either visit a specially crafted link laced with malicious code, or visit a malicious web page containing a web form, which when posted to the vulnerable site, will mount the attack. Using a malicious form will oftentimes take place when the vulnerable resource only accepts HTTP POST requests. In such a case, the form can be submitted automatically, without the victim's knowledge (e.g. by using JavaScript). Upon clicking on the malicious link or submitting the malicious form, the XSS payload will get echoed back and will get interpreted by the user's browser and execute. Another technique to send almost arbitrary requests (GET and POST) is by using an embedded client, such as Adobe Flash.</p><p>Persistent attacks occur when the malicious code is submitted to a web site where it's stored for a period of time. Examples of an attacker's favorite targets often include message board posts, web mail messages, and web chat software. The unsuspecting user is not required to interact with any additional site/link (e.g. an attacker site or a malicious link sent via email), just simply view the web page containing the code.</p>
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/help.htm?lang=%27%3Balert%281%29%3B%27](http://localhost:8081/openmrs-standalone/help.htm?lang=%27%3Balert%281%29%3B%27)
  
  
  * Method: `GET`
  
  
  * Parameter: `lang`
  
  
  * Attack: `';alert(1);'`
  
  
  * Evidence: `';alert(1);'`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/login.htm](http://localhost:8081/openmrs-standalone/login.htm)
  
  
  * Method: `POST`
  
  
  * Parameter: `sessionLocation`
  
  
  * Attack: `</pre><script>alert(1);</script><pre>`
  
  
  * Evidence: `</pre><script>alert(1);</script><pre>`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/referenceapplication/login.page;jsessionid=5038D26982756CDE5D33312187C191EB](http://localhost:8081/openmrs-standalone/referenceapplication/login.page;jsessionid=5038D26982756CDE5D33312187C191EB)
  
  
  * Method: `POST`
  
  
  * Parameter: `sessionLocation`
  
  
  * Attack: `</pre><script>alert(1);</script><pre>`
  
  
  * Evidence: `</pre><script>alert(1);</script><pre>`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=%27%3Balert%281%29%3B%27](http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=%27%3Balert%281%29%3B%27)
  
  
  * Method: `GET`
  
  
  * Parameter: `lang`
  
  
  * Attack: `';alert(1);'`
  
  
  * Evidence: `';alert(1);'`
  
  
  
  
Instances: 4
  
### Solution
<p>Phase: Architecture and Design</p><p>Use a vetted library or framework that does not allow this weakness to occur or provides constructs that make this weakness easier to avoid.</p><p>Examples of libraries and frameworks that make it easier to generate properly encoded output include Microsoft's Anti-XSS library, the OWASP ESAPI Encoding module, and Apache Wicket.</p><p></p><p>Phases: Implementation; Architecture and Design</p><p>Understand the context in which your data will be used and the encoding that will be expected. This is especially important when transmitting data between different components, or when generating outputs that can contain multiple encodings at the same time, such as web pages or multi-part mail messages. Study all expected communication protocols and data representations to determine the required encoding strategies.</p><p>For any data that will be output to another web page, especially any data that was received from external inputs, use the appropriate encoding on all non-alphanumeric characters.</p><p>Consult the XSS Prevention Cheat Sheet for more details on the types of encoding and escaping that are needed.</p><p></p><p>Phase: Architecture and Design</p><p>For any security checks that are performed on the client side, ensure that these checks are duplicated on the server side, in order to avoid CWE-602. Attackers can bypass the client-side checks by modifying values after the checks have been performed, or by changing the client to remove the client-side checks entirely. Then, these modified values would be submitted to the server.</p><p></p><p>If available, use structured mechanisms that automatically enforce the separation between data and code. These mechanisms may be able to provide the relevant quoting, encoding, and validation automatically, instead of relying on the developer to provide this capability at every point where output is generated.</p><p></p><p>Phase: Implementation</p><p>For every web page that is generated, use and specify a character encoding such as ISO-8859-1 or UTF-8. When an encoding is not specified, the web browser may choose a different encoding by guessing which encoding is actually being used by the web page. This can cause the web browser to treat certain sequences as special, opening up the client to subtle XSS attacks. See CWE-116 for more mitigations related to encoding/escaping.</p><p></p><p>To help mitigate XSS attacks against the user's session cookie, set the session cookie to be HttpOnly. In browsers that support the HttpOnly feature (such as more recent versions of Internet Explorer and Firefox), this attribute can prevent the user's session cookie from being accessible to malicious client-side scripts that use document.cookie. This is not a complete solution, since HttpOnly is not supported by all browsers. More importantly, XMLHTTPRequest and other powerful browser technologies provide read access to HTTP headers, including the Set-Cookie header in which the HttpOnly flag is set.</p><p></p><p>Assume all input is malicious. Use an "accept known good" input validation strategy, i.e., use a whitelist of acceptable inputs that strictly conform to specifications. Reject any input that does not strictly conform to specifications, or transform it into something that does. Do not rely exclusively on looking for malicious or malformed inputs (i.e., do not rely on a blacklist). However, blacklists can be useful for detecting potential attacks or determining which inputs are so malformed that they should be rejected outright.</p><p></p><p>When performing input validation, consider all potentially relevant properties, including length, type of input, the full range of acceptable values, missing or extra inputs, syntax, consistency across related fields, and conformance to business rules. As an example of business rule logic, "boat" may be syntactically valid because it only contains alphanumeric characters, but it is not valid if you are expecting colors such as "red" or "blue."</p><p></p><p>Ensure that you perform input validation at well-defined interfaces within the application. This will help protect the application even if a component is reused or moved elsewhere.</p>
  
### Reference
* http://projects.webappsec.org/Cross-Site-Scripting
* http://cwe.mitre.org/data/definitions/79.html

  
#### CWE Id : 79
  
#### WASC Id : 8
  
#### Source ID : 1

  
  
  
### SQL Injection - Authentication Bypass
##### High (Medium)
  
  
  
  
#### Description
<p>SQL injection may be possible on a login page, potentially allowing the application's authentication mechanism to be bypassed </p>
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/login.htm](http://localhost:8081/openmrs-standalone/login.htm)
  
  
  * Method: `GET`
  
  
  * Parameter: `query`
  
  
  * Attack: `query AND 1=1`
  
  
  
  
Instances: 1
  
### Solution
<p>Do not trust client side input, even if there is client side validation in place.  </p><p>In general, type check all data on the server side.</p><p>If the application uses JDBC, use PreparedStatement or CallableStatement, with parameters passed by '?'</p><p>If the application uses ASP, use ADO Command Objects with strong type checking and parameterized queries.</p><p>If database Stored Procedures can be used, use them.</p><p>Do *not* concatenate strings into queries in the stored procedure, or use 'exec', 'exec immediate', or equivalent functionality!</p><p>Do not create dynamic SQL queries using simple string concatenation.</p><p>Escape all data received from the client.</p><p>Apply a 'whitelist' of allowed characters, or a 'blacklist' of disallowed characters in user input.</p><p>Apply the principle of least privilege by using the least privileged database user possible.</p><p>In particular, avoid using the 'sa' or 'db-owner' database users. This does not eliminate SQL injection, but minimizes its impact.</p><p>Grant the minimum database access that is necessary for the application.</p>
  
### Reference
* https://www.owasp.org/index.php/Top_10_2010-A1
* https://www.owasp.org/index.php/SQL_Injection_Prevention_Cheat_Sheet

  
#### CWE Id : 89
  
#### WASC Id : 19
  
#### Source ID : 1

  
  
  
### X-Frame-Options Header Not Set
##### Medium (Medium)
  
  
  
  
#### Description
<p>X-Frame-Options header is not included in the HTTP response to protect against 'ClickJacking' attacks.</p>
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=fr](http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=fr)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Frame-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/help.htm?lang=fr](http://localhost:8081/openmrs-standalone/help.htm?lang=fr)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Frame-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/help.htm](http://localhost:8081/openmrs-standalone/help.htm)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Frame-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/help.htm?lang=en_US](http://localhost:8081/openmrs-standalone/help.htm?lang=en_US)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Frame-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/help.htm?lang=pt](http://localhost:8081/openmrs-standalone/help.htm?lang=pt)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Frame-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/scripts/openmrsmessages.js?locale=pt&v=2.0.5](http://localhost:8081/openmrs-standalone/scripts/openmrsmessages.js?locale=pt&v=2.0.5)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Frame-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=es](http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=es)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Frame-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=en_US](http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=en_US)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Frame-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/](http://localhost:8081/openmrs-standalone/)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Frame-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=it](http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=it)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Frame-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/scripts/openmrsmessages.js?locale=es&v=2.0.5](http://localhost:8081/openmrs-standalone/scripts/openmrsmessages.js?locale=es&v=2.0.5)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Frame-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/scripts/openmrsmessages.js?locale=fr&v=2.0.5](http://localhost:8081/openmrs-standalone/scripts/openmrsmessages.js?locale=fr&v=2.0.5)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Frame-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/help.htm?lang=it](http://localhost:8081/openmrs-standalone/help.htm?lang=it)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Frame-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/referenceapplication/login.page;jsessionid=5038D26982756CDE5D33312187C191EB](http://localhost:8081/openmrs-standalone/referenceapplication/login.page;jsessionid=5038D26982756CDE5D33312187C191EB)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Frame-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/help.htm?lang=es](http://localhost:8081/openmrs-standalone/help.htm?lang=es)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Frame-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page](http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Frame-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/scripts/openmrsmessages.js?locale=en_US&v=2.0.5](http://localhost:8081/openmrs-standalone/scripts/openmrsmessages.js?locale=en_US&v=2.0.5)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Frame-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/scripts/openmrsmessages.js?locale=en_GB&v=2.0.5](http://localhost:8081/openmrs-standalone/scripts/openmrsmessages.js?locale=en_GB&v=2.0.5)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Frame-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/login.htm](http://localhost:8081/openmrs-standalone/login.htm)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Frame-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=pt](http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=pt)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Frame-Options`
  
  
  
  
Instances: 25
  
### Solution
<p>Most modern Web browsers support the X-Frame-Options HTTP header. Ensure it's set on all web pages returned by your site (if you expect the page to be framed only by pages on your server (e.g. it's part of a FRAMESET) then you'll want to use SAMEORIGIN, otherwise if you never expect the page to be framed, you should use DENY. ALLOW-FROM allows specific websites to frame the web page in supported web browsers).</p>
  
### Reference
* http://blogs.msdn.com/b/ieinternals/archive/2010/03/30/combating-clickjacking-with-x-frame-options.aspx

  
#### CWE Id : 16
  
#### WASC Id : 15
  
#### Source ID : 3

  
  
  
### Application Error Disclosure
##### Medium (Medium)
  
  
  
  
#### Description
<p>This page contains an error/warning message that may disclose sensitive information like the location of the file that produced the unhandled exception. This information can be used to launch further attacks against the web application. The alert could be a false positive if the error message is found inside a documentation page.</p>
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/ms/uiframework/resource/uicommons/scripts](http://localhost:8081/openmrs-standalone/ms/uiframework/resource/uicommons/scripts)
  
  
  * Method: `GET`
  
  
  * Evidence: `HTTP/1.1 500 Internal Server Error`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/ms/uiframework/resource/uicommons/styles/styleguide](http://localhost:8081/openmrs-standalone/ms/uiframework/resource/uicommons/styles/styleguide)
  
  
  * Method: `GET`
  
  
  * Evidence: `HTTP/1.1 500 Internal Server Error`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/ms/uiframework/resource/referenceapplication/fonts](http://localhost:8081/openmrs-standalone/ms/uiframework/resource/referenceapplication/fonts)
  
  
  * Method: `GET`
  
  
  * Evidence: `HTTP/1.1 500 Internal Server Error`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/ms](http://localhost:8081/openmrs-standalone/ms)
  
  
  * Method: `GET`
  
  
  * Evidence: `HTTP/1.1 500 Internal Server Error`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/ms/uiframework/resource/referenceapplication/styles](http://localhost:8081/openmrs-standalone/ms/uiframework/resource/referenceapplication/styles)
  
  
  * Method: `GET`
  
  
  * Evidence: `HTTP/1.1 500 Internal Server Error`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/ms/uiframework/resource/appui/styles](http://localhost:8081/openmrs-standalone/ms/uiframework/resource/appui/styles)
  
  
  * Method: `GET`
  
  
  * Evidence: `HTTP/1.1 500 Internal Server Error`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/ms/uiframework/resource/referenceapplication/images](http://localhost:8081/openmrs-standalone/ms/uiframework/resource/referenceapplication/images)
  
  
  * Method: `GET`
  
  
  * Evidence: `HTTP/1.1 500 Internal Server Error`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/ms/uiframework/resource/uicommons/images](http://localhost:8081/openmrs-standalone/ms/uiframework/resource/uicommons/images)
  
  
  * Method: `GET`
  
  
  * Evidence: `HTTP/1.1 500 Internal Server Error`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/ms/uiframework/resource/uicommons/images/logo](http://localhost:8081/openmrs-standalone/ms/uiframework/resource/uicommons/images/logo)
  
  
  * Method: `GET`
  
  
  * Evidence: `HTTP/1.1 500 Internal Server Error`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/ms/uiframework/resource/uicommons/styles](http://localhost:8081/openmrs-standalone/ms/uiframework/resource/uicommons/styles)
  
  
  * Method: `GET`
  
  
  * Evidence: `HTTP/1.1 500 Internal Server Error`
  
  
  
  
Instances: 10
  
### Solution
<p>Review the source code of this page. Implement custom error pages. Consider implementing a mechanism to provide a unique error reference/identifier to the client (browser) while logging the details on the server side and not exposing them to the user.</p>
  
### Reference
* 

  
#### CWE Id : 200
  
#### WASC Id : 13
  
#### Source ID : 3

  
  
  
### Format String Error
##### Medium (Medium)
  
  
  
  
#### Description
<p>A Format String error occurs when the submitted data of an input string is evaluated as a command by the application. </p>
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/help.htm?lang=ZAP%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%0A](http://localhost:8081/openmrs-standalone/help.htm?lang=ZAP%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%0A)
  
  
  * Method: `GET`
  
  
  * Parameter: `lang`
  
  
  * Attack: `ZAP%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s
`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=ZAP%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%0A](http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=ZAP%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%25n%25s%0A)
  
  
  * Method: `GET`
  
  
  * Parameter: `lang`
  
  
  * Attack: `ZAP%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s
`
  
  
  
  
Instances: 2
  
### Solution
<p>Rewrite the background program using proper deletion of bad character strings.  This will require a recompile of the background executable.</p>
  
### Other information
<p>Potential Format String Error.  The script closed the connection on a /%s</p>
  
### Reference
* https://www.owasp.org/index.php/Format_string_attack

  
#### CWE Id : 134
  
#### WASC Id : 6
  
#### Source ID : 1

  
  
  
### Cookie No HttpOnly Flag
##### Low (Medium)
  
  
  
  
#### Description
<p>A cookie has been set without the HttpOnly flag, which means that the cookie can be accessed by JavaScript. If a malicious script can be run on this page then the cookie will be accessible and can be transmitted to another site. If this is a session cookie then session hijacking may be possible.</p>
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/help.htm?lang=en_US](http://localhost:8081/openmrs-standalone/help.htm?lang=en_US)
  
  
  * Method: `GET`
  
  
  * Parameter: `__openmrs_language`
  
  
  * Evidence: `Set-Cookie: __openmrs_language`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=pt](http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=pt)
  
  
  * Method: `GET`
  
  
  * Parameter: `__openmrs_language`
  
  
  * Evidence: `Set-Cookie: __openmrs_language`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=en_US](http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=en_US)
  
  
  * Method: `GET`
  
  
  * Parameter: `__openmrs_language`
  
  
  * Evidence: `Set-Cookie: __openmrs_language`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/help.htm?lang=fr](http://localhost:8081/openmrs-standalone/help.htm?lang=fr)
  
  
  * Method: `GET`
  
  
  * Parameter: `__openmrs_language`
  
  
  * Evidence: `Set-Cookie: __openmrs_language`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=it](http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=it)
  
  
  * Method: `GET`
  
  
  * Parameter: `__openmrs_language`
  
  
  * Evidence: `Set-Cookie: __openmrs_language`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/help.htm?lang=pt](http://localhost:8081/openmrs-standalone/help.htm?lang=pt)
  
  
  * Method: `GET`
  
  
  * Parameter: `__openmrs_language`
  
  
  * Evidence: `Set-Cookie: __openmrs_language`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=es](http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=es)
  
  
  * Method: `GET`
  
  
  * Parameter: `__openmrs_language`
  
  
  * Evidence: `Set-Cookie: __openmrs_language`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/help.htm?lang=es](http://localhost:8081/openmrs-standalone/help.htm?lang=es)
  
  
  * Method: `GET`
  
  
  * Parameter: `__openmrs_language`
  
  
  * Evidence: `Set-Cookie: __openmrs_language`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=en_GB](http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=en_GB)
  
  
  * Method: `GET`
  
  
  * Parameter: `__openmrs_language`
  
  
  * Evidence: `Set-Cookie: __openmrs_language`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/help.htm?lang=it](http://localhost:8081/openmrs-standalone/help.htm?lang=it)
  
  
  * Method: `GET`
  
  
  * Parameter: `__openmrs_language`
  
  
  * Evidence: `Set-Cookie: __openmrs_language`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/help.htm?lang=en_GB](http://localhost:8081/openmrs-standalone/help.htm?lang=en_GB)
  
  
  * Method: `GET`
  
  
  * Parameter: `__openmrs_language`
  
  
  * Evidence: `Set-Cookie: __openmrs_language`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=fr](http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=fr)
  
  
  * Method: `GET`
  
  
  * Parameter: `__openmrs_language`
  
  
  * Evidence: `Set-Cookie: __openmrs_language`
  
  
  
  
Instances: 12
  
### Solution
<p>Ensure that the HttpOnly flag is set for all cookies.</p>
  
### Reference
* http://www.owasp.org/index.php/HttpOnly

  
#### CWE Id : 16
  
#### WASC Id : 13
  
#### Source ID : 3

  
  
  
### Web Browser XSS Protection Not Enabled
##### Low (Medium)
  
  
  
  
#### Description
<p>Web Browser XSS Protection is not enabled, or is disabled by the configuration of the 'X-XSS-Protection' HTTP response header on the web server</p>
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/ms/uiframework/resource/referenceapplication/styles](http://localhost:8081/openmrs-standalone/ms/uiframework/resource/referenceapplication/styles)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-XSS-Protection`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/ms/uiframework/resource/uicommons/styles](http://localhost:8081/openmrs-standalone/ms/uiframework/resource/uicommons/styles)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-XSS-Protection`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/%7B%7B=%20breadcrumb.link%20%7D%7D](http://localhost:8081/openmrs-standalone/%7B%7B=%20breadcrumb.link%20%7D%7D)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-XSS-Protection`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/help.htm?lang=es](http://localhost:8081/openmrs-standalone/help.htm?lang=es)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-XSS-Protection`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/scripts/openmrsmessages.js?locale=en_GB&v=2.0.5](http://localhost:8081/openmrs-standalone/scripts/openmrsmessages.js?locale=en_GB&v=2.0.5)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-XSS-Protection`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=es](http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=es)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-XSS-Protection`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/adminui/myaccount/myAccount.page](http://localhost:8081/openmrs-standalone/adminui/myaccount/myAccount.page)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-XSS-Protection`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/referenceapplication](http://localhost:8081/openmrs-standalone/referenceapplication)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-XSS-Protection`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=en_GB](http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=en_GB)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-XSS-Protection`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/help.htm?lang=it](http://localhost:8081/openmrs-standalone/help.htm?lang=it)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-XSS-Protection`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/scripts/openmrsmessages.js?locale=fr&v=2.0.5](http://localhost:8081/openmrs-standalone/scripts/openmrsmessages.js?locale=fr&v=2.0.5)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-XSS-Protection`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/scripts/openmrsmessages.js?locale=en_US&v=2.0.5](http://localhost:8081/openmrs-standalone/scripts/openmrsmessages.js?locale=en_US&v=2.0.5)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-XSS-Protection`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=it](http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=it)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-XSS-Protection`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/](http://localhost:8081/openmrs-standalone/)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-XSS-Protection`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/ms/uiframework/resource/appui/styles](http://localhost:8081/openmrs-standalone/ms/uiframework/resource/appui/styles)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-XSS-Protection`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=en_US](http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=en_US)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-XSS-Protection`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/adminui/myaccount/%7B%7B=%20breadcrumb.link%20%7D%7D](http://localhost:8081/openmrs-standalone/adminui/myaccount/%7B%7B=%20breadcrumb.link%20%7D%7D)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-XSS-Protection`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page](http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-XSS-Protection`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/help.htm](http://localhost:8081/openmrs-standalone/help.htm)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-XSS-Protection`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/help.htm?lang=pt](http://localhost:8081/openmrs-standalone/help.htm?lang=pt)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-XSS-Protection`
  
  
  
  
Instances: 39
  
### Solution
<p>Ensure that the web browser's XSS filter is enabled, by setting the X-XSS-Protection HTTP response header to '1'.</p>
  
### Other information
<p>The X-XSS-Protection HTTP response header allows the web server to enable or disable the web browser's XSS protection mechanism. The following values would attempt to enable it: </p><p>X-XSS-Protection: 1; mode=block</p><p>X-XSS-Protection: 1; report=http://www.example.com/xss</p><p>The following values would disable it:</p><p>X-XSS-Protection: 0</p><p>The X-XSS-Protection HTTP response header is currently supported on Internet Explorer, Chrome and Safari (WebKit).</p><p>Note that this alert is only raised if the response body could potentially contain an XSS payload (with a text-based content type, with a non-zero length).</p>
  
### Reference
* https://www.owasp.org/index.php/XSS_(Cross_Site_Scripting)_Prevention_Cheat_Sheet
* https://blog.veracode.com/2014/03/guidelines-for-setting-security-headers/

  
#### CWE Id : 933
  
#### WASC Id : 14
  
#### Source ID : 3

  
  
  
### X-Content-Type-Options Header Missing
##### Low (Medium)
  
  
  
  
#### Description
<p>The Anti-MIME-Sniffing header X-Content-Type-Options was not set to 'nosniff'. This allows older versions of Internet Explorer and Chrome to perform MIME-sniffing on the response body, potentially causing the response body to be interpreted and displayed as a content type other than the declared content type. Current (early 2014) and legacy versions of Firefox will use the declared content type (if one is set), rather than performing MIME-sniffing.</p>
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/ms/uiframework/resource/uicommons/scripts/jquery.toastmessage.js?cache=1504310202510](http://localhost:8081/openmrs-standalone/ms/uiframework/resource/uicommons/scripts/jquery.toastmessage.js?cache=1504310202510)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Content-Type-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/ms/uiframework/resource/uicommons/scripts/underscore-min.js?cache=1504310202510](http://localhost:8081/openmrs-standalone/ms/uiframework/resource/uicommons/scripts/underscore-min.js?cache=1504310202510)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Content-Type-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/ms/uiframework/resource/referenceapplication/fonts/fontawesome-webfont.woff?v=3.0.1](http://localhost:8081/openmrs-standalone/ms/uiframework/resource/referenceapplication/fonts/fontawesome-webfont.woff?v=3.0.1)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Content-Type-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/ms/uiframework/resource/referenceapplication/fonts/opensans-regular-webfont.ttf](http://localhost:8081/openmrs-standalone/ms/uiframework/resource/referenceapplication/fonts/opensans-regular-webfont.ttf)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Content-Type-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/moduleResources/legacyui/css/style.css?v=2.0.5](http://localhost:8081/openmrs-standalone/moduleResources/legacyui/css/style.css?v=2.0.5)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Content-Type-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=it](http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=it)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Content-Type-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/scripts/openmrsmessages.js?locale=it&v=2.0.5](http://localhost:8081/openmrs-standalone/scripts/openmrsmessages.js?locale=it&v=2.0.5)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Content-Type-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/ms/uiframework/resource/uicommons/scripts/emr.js?cache=1504310202510](http://localhost:8081/openmrs-standalone/ms/uiframework/resource/uicommons/scripts/emr.js?cache=1504310202510)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Content-Type-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/help.htm?lang=pt](http://localhost:8081/openmrs-standalone/help.htm?lang=pt)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Content-Type-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/referenceapplication/home.page](http://localhost:8081/openmrs-standalone/referenceapplication/home.page)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Content-Type-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/ms/uiframework/resource/referenceapplication/fonts/icomoon.woff](http://localhost:8081/openmrs-standalone/ms/uiframework/resource/referenceapplication/fonts/icomoon.woff)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Content-Type-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/ms/uiframework/resource/appui/styles/header.css?cache=1504310202510](http://localhost:8081/openmrs-standalone/ms/uiframework/resource/appui/styles/header.css?cache=1504310202510)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Content-Type-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=es](http://localhost:8081/openmrs-standalone/adminui/myaccount/changeDefaults.page?lang=es)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Content-Type-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/help.htm?lang=es](http://localhost:8081/openmrs-standalone/help.htm?lang=es)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Content-Type-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/moduleResources/legacyui/css/openmrs.css?v=2.0.5](http://localhost:8081/openmrs-standalone/moduleResources/legacyui/css/openmrs.css?v=2.0.5)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Content-Type-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/ms/uiframework/resource/uicommons/scripts/jquery-1.12.4.min.js?cache=1504310202510](http://localhost:8081/openmrs-standalone/ms/uiframework/resource/uicommons/scripts/jquery-1.12.4.min.js?cache=1504310202510)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Content-Type-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/scripts/openmrsmessages.js?locale=es&v=2.0.5](http://localhost:8081/openmrs-standalone/scripts/openmrsmessages.js?locale=es&v=2.0.5)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Content-Type-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/login.htm](http://localhost:8081/openmrs-standalone/login.htm)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Content-Type-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/help.htm?lang=it](http://localhost:8081/openmrs-standalone/help.htm?lang=it)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Content-Type-Options`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/scripts/openmrsmessages.js?locale=fr&v=2.0.5](http://localhost:8081/openmrs-standalone/scripts/openmrsmessages.js?locale=fr&v=2.0.5)
  
  
  * Method: `GET`
  
  
  * Parameter: `X-Content-Type-Options`
  
  
  
  
Instances: 53
  
### Solution
<p>Ensure that the application/web server sets the Content-Type header appropriately, and that it sets the X-Content-Type-Options header to 'nosniff' for all web pages.</p><p>If possible, ensure that the end user uses a standards-compliant and modern web browser that does not perform MIME-sniffing at all, or that can be directed by the web application/web server to not perform MIME-sniffing.</p>
  
### Other information
<p>This issue still applies to error type pages (401, 403, 500, etc) as those pages are often still affected by injection issues, in which case there is still concern for browsers sniffing pages away from their actual content type.</p><p>At "High" threshold this scanner will not alert on client or server error responses.</p>
  
### Reference
* http://msdn.microsoft.com/en-us/library/ie/gg622941%28v=vs.85%29.aspx
* https://www.owasp.org/index.php/List_of_useful_HTTP_headers

  
#### CWE Id : 16
  
#### WASC Id : 15
  
#### Source ID : 3

  
  
  
### Content-Type Header Missing
##### Low (Medium)
  
  
  
  
#### Description
<p>The Content-Type header was either missing or empty.</p>
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/ms/uiframework/resource/referenceapplication/fonts/opensans-regular-webfont.ttf](http://localhost:8081/openmrs-standalone/ms/uiframework/resource/referenceapplication/fonts/opensans-regular-webfont.ttf)
  
  
  * Method: `GET`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/ms/uiframework/resource/referenceapplication/fonts/icomoon.woff](http://localhost:8081/openmrs-standalone/ms/uiframework/resource/referenceapplication/fonts/icomoon.woff)
  
  
  * Method: `GET`
  
  
  
  
* URL: [http://localhost:8081/openmrs-standalone/ms/uiframework/resource/referenceapplication/fonts/fontawesome-webfont.woff?v=3.0.1](http://localhost:8081/openmrs-standalone/ms/uiframework/resource/referenceapplication/fonts/fontawesome-webfont.woff?v=3.0.1)
  
  
  * Method: `GET`
  
  
  
  
Instances: 3
  
### Solution
<p>Ensure each page is setting the specific and appropriate content-type value for the content being delivered.</p>
  
### Reference
* http://msdn.microsoft.com/en-us/library/ie/gg622941%28v=vs.85%29.aspx

  
#### CWE Id : 345
  
#### WASC Id : 12
  
#### Source ID : 3
