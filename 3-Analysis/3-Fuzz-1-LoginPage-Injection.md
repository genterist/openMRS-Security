# Fuzz -1- LOGIN PAGE INJECTION
### Priority : HIGH
### Test status : FAILED
`DESIGNER : TAM N NGUYEN` <br/>
`EXECUTED BY : TAM N NGUYEN` <br/>
`UPDATED ON : 20OCT17` <br/>
`EXECUTED ON : 20OCT17` <br/>

### * Description
#### Name of module : OpenMRS login
+ Page location : http://localhost:8081/openmrs-standalone/login.htm
+ Fuzz string : username=admin&password=<<fuzz data>>&sessionLocation=2&redirectUrl=
+ Fuzz data : jbrofuzz pre-installed rules in OWASP scanner
Fuzzer will deploy 199 injection attack strings on the variable "password" in form of POST requests. Server HttpResponses will be analyzed and be decided if the attacks were successful or not.


### * Precondition
1. A local computer with administrator privilege
2. Java JRE installed
3. OpenMRS Standalone Version 2.6.0 downloaded and unziped
4. OWASP ZAP Version 2.6.0 downloaded and installed

### * Dependencies
1. OpenMRS with demo database was loaded and runs normally
2. OWASP ZAP runs normally

### * Test Data
jbrofuzz rules came standard with OWASP Zap

### * Test steps
1. Open up OpenMRS V. 2.6.0 Standalone. Make sure Tomcat Port is 8081 and MySQL port is 3316. A web page starting with localhost:8081 will be automatically opened upon successful start.

![alt text](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/portSettings.png)

2. Open OWASP Zap V2.6.0
3. From OWASP Zap, go to Toos > Launch the Zap JxBrowser
4. In the Zap JxBrowser, type "http://localhost:8081/openmrs-standalone/login.htm" (without the double quotes) into the address bar and hit Enter
5. Go to the main Zap window, on the left side bar, in "Sites" tab, under "Sites" sub section, you will now see "http://localhost:8081". Expand that until you see "GET:login.htm". If you don't see it, please go to the JzBrowser and make sure the login page is loaded. If the page is not loaded, you need to double check the OpenMRS to make sure it runs properly

![alt text](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/sitesLoaded.png)

6. Go back to the Zap JxBrowser and type a bogus pair of username/password (we use "admin" for username and "BBBBB" for password), select "Pharmacy" section and click login. When the page got reloaded with "Invalid username/password. Please try again", close JxBrowser window and get back to main Zap window

![alt text](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/adminLoginScreen.png)

7. In zap window, if you see "POST:login.htm(password, redirectURL,sessionLocation,username)" on the left panel (the "Sites" panel) then you got it, if not, please repeat step 3 to 5
8. Select "POST:login.htm(password, redirectURL,sessionLocation,username)" from the left panel and select the "Request" tab on the right panel. The right panel will turn into 2 smaller panels. At the bottom one, you will see "username=admin&password=BBBBB&sessionLocation=2&redirectUrl="
9. Highlight the "BBBBB" part from the string you got in previous step, right click on it and choose "Fuzz". A Fuzzer window will be opened.

![alt text](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/openFuzzMenu.png)

10. In the fuzzer window, click "Payloads..." button. A child window will be opened

![](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/fuzzerWindow.png)

11. In the child "Payloads" window, click "Add". An "Add payload" window will be opened
12. In "Add payload window, in the "Type" box, choose "File Fuzzers". Expand the "jbrofuzz" section. Check the box of "Injection" and click "Add". The child window will be closed.

![](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/injectionSelect.png)

13. In Payloads window, click "OK" and you will be returned to the "Fuzzer" window. In this window, click "Start Fuzzer" button and you will be returned to the main Zap window with the "Fuzzer" tab selected
14. Observe the results in the "Fuzzer" tab, especially the "Code" and "Size Resp. Body". Check the HTTP response by selecting a fuzz entry, and select the "Response" tab in the uper right panel.

![](https://github.com/genterist/openMRS-Security/blob/master/3-Analysis/images/fuzz-InjectionResults.png)

### * Expected results
+ OpenMRS should redirect invalid logins back to the login page.
+ System has to be able to fail securely.

### * Post-condition
OpenMRS should still be operating normally

### * Actual results
+ 199 fuzz were done on the "password" variable
+ 197 of the entries have 302 code and zero size of Response html body. Confirmed by inspection of html header, noticing that system redirects invalid login to previous page - the login page.
+ 002 of the fuzz entries were able to force system to leak some debugging informations which can be used for further attacks (to be discussed further in the Notes section)
+ We decided that the test is a "FAILED". Even though no exploit directly linked to Injection was successful, the fuzzer was able to leak some important debugging data. 

### * NOTES:

FUZZ STRING USED TO CAUSE THE LEAK
> ' union (select NULL, (select @@version)) --&sessionLocation=2&redirectUrl=

or

> username=admin&password=' union (select NULL, NULL, (select @@version)) --&sessionLocation=2&redirectUrl=

LEAKED SYSTEM INFO

Originally harvested by OWASP fuzzer in HttpResponse and may not be able to reproduce using the regular browser/view source method.
```
<h1>UI Framework Error</h1>

<h2>Root Error</h2>
<pre>com.mysql.jdbc.exceptions.jdbc4.MySQLIntegrityConstraintViolationException: Duplicate entry '1-lockoutTimestamp' for key 'PRIMARY'
	at sun.reflect.NativeConstructorAccessorImpl.newInstance0(Native Method)
	at sun.reflect.NativeConstructorAccessorImpl.newInstance(NativeConstructorAccessorImpl.java:62)
	at sun.reflect.DelegatingConstructorAccessorImpl.newInstance(DelegatingConstructorAccessorImpl.java:45)
	at java.lang.reflect.Constructor.newInstance(Constructor.java:423)
	at com.mysql.jdbc.Util.handleNewInstance(Util.java:411)
	at com.mysql.jdbc.Util.getInstance(Util.java:386)
	at com.mysql.jdbc.SQLError.createSQLException(SQLError.java:1041)
	at com.mysql.jdbc.MysqlIO.checkErrorPacket(MysqlIO.java:4237)
	at com.mysql.jdbc.MysqlIO.checkErrorPacket(MysqlIO.java:4169)
	at com.mysql.jdbc.MysqlIO.sendCommand(MysqlIO.java:2617)
	at com.mysql.jdbc.MysqlIO.sqlQueryDirect(MysqlIO.java:2778)
	at com.mysql.jdbc.ConnectionImpl.execSQL(ConnectionImpl.java:2825)
	at com.mysql.jdbc.PreparedStatement.executeInternal(PreparedStatement.java:2156)
	at com.mysql.jdbc.PreparedStatement.executeUpdate(PreparedStatement.java:2441)
	at com.mysql.jdbc.PreparedStatement.executeBatchSerially(PreparedStatement.java:2007)
	at com.mysql.jdbc.PreparedStatement.executeBatch(PreparedStatement.java:1467)
	at com.mchange.v2.c3p0.impl.NewProxyPreparedStatement.executeBatch(NewProxyPreparedStatement.java:1135)
	at org.hibernate.engine.jdbc.batch.internal.BatchingBatch.performExecution(BatchingBatch.java:127)
	at org.hibernate.engine.jdbc.batch.internal.BatchingBatch.doExecuteBatch(BatchingBatch.java:114)
	at org.hibernate.engine.jdbc.batch.internal.AbstractBatchImpl.execute(AbstractBatchImpl.java:163)
	at org.hibernate.engine.jdbc.internal.JdbcCoordinatorImpl.executeBatch(JdbcCoordinatorImpl.java:226)
	at org.hibernate.engine.spi.ActionQueue.executeActions(ActionQueue.java:484)
	at org.hibernate.engine.spi.ActionQueue.executeActions(ActionQueue.java:351)
	at org.hibernate.event.internal.AbstractFlushingEventListener.performExecutions(AbstractFlushingEventListener.java:350)
	at org.hibernate.event.internal.DefaultFlushEventListener.onFlush(DefaultFlushEventListener.java:56)
	at org.hibernate.internal.SessionImpl.flush(SessionImpl.java:1258)
	at org.hibernate.internal.SessionImpl.managedFlush(SessionImpl.java:425)
	at org.hibernate.engine.transaction.internal.jdbc.JdbcTransaction.beforeTransactionCommit(JdbcTransaction.java:101)
	at org.hibernate.engine.transaction.spi.AbstractTransactionImpl.commit(AbstractTransactionImpl.java:177)
	at org.springframework.orm.hibernate4.HibernateTransactionManager.doCommit(HibernateTransactionManager.java:584)
	at org.springframework.transaction.support.AbstractPlatformTransactionManager.processCommit(AbstractPlatformTransactionManager.java:757)
	at org.springframework.transaction.support.AbstractPlatformTransactionManager.commit(AbstractPlatformTransactionManager.java:726)
	at org.springframework.transaction.interceptor.TransactionAspectSupport.completeTransactionAfterThrowing(TransactionAspectSupport.java:553)
	at org.springframework.transaction.interceptor.TransactionAspectSupport.invokeWithinTransaction(TransactionAspectSupport.java:285)
	at org.springframework.transaction.interceptor.TransactionInterceptor.invoke(TransactionInterceptor.java:96)
	at org.springframework.aop.framework.ReflectiveMethodInvocation.proceed(ReflectiveMethodInvocation.java:179)
	at org.springframework.aop.framework.JdkDynamicAopProxy.invoke(JdkDynamicAopProxy.java:207)
	at com.sun.proxy.$Proxy290.authenticate(Unknown Source)
	at org.openmrs.api.context.UserContext.authenticate(UserContext.java:100)
	at org.openmrs.api.context.Context.authenticate(Context.java:297)
	at org.openmrs.module.referenceapplication.page.controller.LoginPageController.post(LoginPageController.java:217)
	at sun.reflect.GeneratedMethodAccessor542.invoke(Unknown Source)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.lang.reflect.Method.invoke(Method.java:498)
	at org.openmrs.ui.framework.UiFrameworkUtil.invokeMethodWithArguments(UiFrameworkUtil.java:112)
	at org.openmrs.ui.framework.UiFrameworkUtil.executeControllerMethod(UiFrameworkUtil.java:71)
	at org.openmrs.ui.framework.page.PageFactory.handleRequestWithController(PageFactory.java:219)
	at org.openmrs.ui.framework.page.PageFactory.processThisFragment(PageFactory.java:160)
	at org.openmrs.ui.framework.page.PageFactory.process(PageFactory.java:116)
	at org.openmrs.ui.framework.page.PageFactory.handle(PageFactory.java:86)
	at org.openmrs.module.uiframework.PageController.handlePath(PageController.java:116)
	at org.openmrs.module.uiframework.PageController.handleUrlWithDotPage(PageController.java:83)
	at sun.reflect.GeneratedMethodAccessor540.invoke(Unknown Source)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.lang.reflect.Method.invoke(Method.java:498)
	at org.springframework.web.bind.annotation.support.HandlerMethodInvoker.invokeHandlerMethod(HandlerMethodInvoker.java:177)
	at org.springframework.web.servlet.mvc.annotation.AnnotationMethodHandlerAdapter.invokeHandlerMethod(AnnotationMethodHandlerAdapter.java:446)
	at org.springframework.web.servlet.mvc.annotation.AnnotationMethodHandlerAdapter.handle(AnnotationMethodHandlerAdapter.java:434)
	at org.springframework.web.servlet.DispatcherServlet.doDispatch(DispatcherServlet.java:943)
	at org.springframework.web.servlet.DispatcherServlet.doService(DispatcherServlet.java:877)
	at org.springframework.web.servlet.FrameworkServlet.processRequest(FrameworkServlet.java:966)
	at org.springframework.web.servlet.FrameworkServlet.doPost(FrameworkServlet.java:868)
	at javax.servlet.http.HttpServlet.service(HttpServlet.java:647)
	at org.springframework.web.servlet.FrameworkServlet.service(FrameworkServlet.java:842)
	at javax.servlet.http.HttpServlet.service(HttpServlet.java:728)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:305)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:210)
	at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:101)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:243)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:210)
	at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:101)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:243)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:210)
	at org.apache.catalina.core.ApplicationDispatcher.invoke(ApplicationDispatcher.java:749)
	at org.apache.catalina.core.ApplicationDispatcher.processRequest(ApplicationDispatcher.java:487)
	at org.apache.catalina.core.ApplicationDispatcher.doForward(ApplicationDispatcher.java:412)
	at org.apache.catalina.core.ApplicationDispatcher.forward(ApplicationDispatcher.java:339)
	at org.springframework.web.servlet.view.InternalResourceView.renderMergedOutputModel(InternalResourceView.java:168)
	at org.springframework.web.servlet.view.AbstractView.render(AbstractView.java:303)
	at org.springframework.web.servlet.DispatcherServlet.render(DispatcherServlet.java:1228)
	at org.springframework.web.servlet.DispatcherServlet.processDispatchResult(DispatcherServlet.java:1011)
	at org.springframework.web.servlet.DispatcherServlet.doDispatch(DispatcherServlet.java:955)
	at org.springframework.web.servlet.DispatcherServlet.doService(DispatcherServlet.java:877)
	at org.springframework.web.servlet.FrameworkServlet.processRequest(FrameworkServlet.java:966)
	at org.springframework.web.servlet.FrameworkServlet.doPost(FrameworkServlet.java:868)
	at javax.servlet.http.HttpServlet.service(HttpServlet.java:647)
	at org.springframework.web.servlet.FrameworkServlet.service(FrameworkServlet.java:842)
	at javax.servlet.http.HttpServlet.service(HttpServlet.java:728)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:305)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:210)
	at org.openmrs.module.web.filter.ForcePasswordChangeFilter.doFilter(ForcePasswordChangeFilter.java:60)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:243)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:210)
	at org.openmrs.web.filter.GZIPFilter.doFilterInternal(GZIPFilter.java:64)
	at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:107)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:243)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:210)
	at org.openmrs.module.web.filter.ModuleFilterChain.doFilter(ModuleFilterChain.java:72)
	at org.openmrs.module.owa.filter.OwaFilter.doFilter(OwaFilter.java:64)
	at org.openmrs.module.web.filter.ModuleFilterChain.doFilter(ModuleFilterChain.java:70)
	at org.openmrs.module.web.filter.ModuleFilter.doFilter(ModuleFilter.java:54)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:243)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:210)
	at org.openmrs.web.filter.OpenmrsFilter.doFilterInternal(OpenmrsFilter.java:108)
	at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:107)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:243)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:210)
	at org.springframework.orm.hibernate4.support.OpenSessionInViewFilter.doFilterInternal(OpenSessionInViewFilter.java:150)
	at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:107)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:243)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:210)
	at org.openmrs.web.filter.StartupFilter.doFilter(StartupFilter.java:105)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:243)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:210)
	at org.openmrs.web.filter.StartupFilter.doFilter(StartupFilter.java:105)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:243)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:210)
	at org.openmrs.web.filter.StartupFilter.doFilter(StartupFilter.java:105)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:243)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:210)
	at org.springframework.web.filter.CharacterEncodingFilter.doFilterInternal(CharacterEncodingFilter.java:88)
	at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:107)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:243)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:210)
	at org.apache.catalina.core.StandardWrapperValve.invoke(StandardWrapperValve.java:222)
	at org.apache.catalina.core.StandardContextValve.invoke(StandardContextValve.java:123)
	at org.apache.catalina.authenticator.AuthenticatorBase.invoke(AuthenticatorBase.java:502)
	at org.apache.catalina.core.StandardHostValve.invoke(StandardHostValve.java:171)
	at org.apache.catalina.valves.ErrorReportValve.invoke(ErrorReportValve.java:100)
	at org.apache.catalina.core.StandardEngineValve.invoke(StandardEngineValve.java:118)
	at org.apache.catalina.connector.CoyoteAdapter.service(CoyoteAdapter.java:409)
	at org.apache.coyote.http11.AbstractHttp11Processor.process(AbstractHttp11Processor.java:1044)
	at org.apache.coyote.AbstractProtocol$AbstractConnectionHandler.process(AbstractProtocol.java:607)
	at org.apache.tomcat.util.net.JIoEndpoint$SocketProcessor.run(JIoEndpoint.java:315)
	at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1149)
	at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:624)
	at java.lang.Thread.run(Thread.java:748)
</pre>

<h2>Full Error</h2>
<pre>org.springframework.dao.DataIntegrityViolationException: could not execute batch; SQL [insert into user_property (user_id, property, property_value) values (?, ?, ?)]; constraint [null]; nested exception is org.hibernate.exception.ConstraintViolationException: could not execute batch
	at org.springframework.orm.hibernate4.SessionFactoryUtils.convertHibernateAccessException(SessionFactoryUtils.java:163)
	at org.springframework.orm.hibernate4.HibernateTransactionManager.convertHibernateAccessException(HibernateTransactionManager.java:730)
	at org.springframework.orm.hibernate4.HibernateTransactionManager.doCommit(HibernateTransactionManager.java:592)
	at org.springframework.transaction.support.AbstractPlatformTransactionManager.processCommit(AbstractPlatformTransactionManager.java:757)
	at org.springframework.transaction.support.AbstractPlatformTransactionManager.commit(AbstractPlatformTransactionManager.java:726)
	at org.springframework.transaction.interceptor.TransactionAspectSupport.completeTransactionAfterThrowing(TransactionAspectSupport.java:553)
	at org.springframework.transaction.interceptor.TransactionAspectSupport.invokeWithinTransaction(TransactionAspectSupport.java:285)
	at org.springframework.transaction.interceptor.TransactionInterceptor.invoke(TransactionInterceptor.java:96)
	at org.springframework.aop.framework.ReflectiveMethodInvocation.proceed(ReflectiveMethodInvocation.java:179)
	at org.springframework.aop.framework.JdkDynamicAopProxy.invoke(JdkDynamicAopProxy.java:207)
	at com.sun.proxy.$Proxy290.authenticate(Unknown Source)
	at org.openmrs.api.context.UserContext.authenticate(UserContext.java:100)
	at org.openmrs.api.context.Context.authenticate(Context.java:297)
	at org.openmrs.module.referenceapplication.page.controller.LoginPageController.post(LoginPageController.java:217)
	at sun.reflect.GeneratedMethodAccessor542.invoke(Unknown Source)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.lang.reflect.Method.invoke(Method.java:498)
	at org.openmrs.ui.framework.UiFrameworkUtil.invokeMethodWithArguments(UiFrameworkUtil.java:112)
	at org.openmrs.ui.framework.UiFrameworkUtil.executeControllerMethod(UiFrameworkUtil.java:71)
	at org.openmrs.ui.framework.page.PageFactory.handleRequestWithController(PageFactory.java:219)
	at org.openmrs.ui.framework.page.PageFactory.processThisFragment(PageFactory.java:160)
	at org.openmrs.ui.framework.page.PageFactory.process(PageFactory.java:116)
	at org.openmrs.ui.framework.page.PageFactory.handle(PageFactory.java:86)
	at org.openmrs.module.uiframework.PageController.handlePath(PageController.java:116)
	at org.openmrs.module.uiframework.PageController.handleUrlWithDotPage(PageController.java:83)
	at sun.reflect.GeneratedMethodAccessor540.invoke(Unknown Source)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.lang.reflect.Method.invoke(Method.java:498)
	at org.springframework.web.bind.annotation.support.HandlerMethodInvoker.invokeHandlerMethod(HandlerMethodInvoker.java:177)
	at org.springframework.web.servlet.mvc.annotation.AnnotationMethodHandlerAdapter.invokeHandlerMethod(AnnotationMethodHandlerAdapter.java:446)
	at org.springframework.web.servlet.mvc.annotation.AnnotationMethodHandlerAdapter.handle(AnnotationMethodHandlerAdapter.java:434)
	at org.springframework.web.servlet.DispatcherServlet.doDispatch(DispatcherServlet.java:943)
	at org.springframework.web.servlet.DispatcherServlet.doService(DispatcherServlet.java:877)
	at org.springframework.web.servlet.FrameworkServlet.processRequest(FrameworkServlet.java:966)
	at org.springframework.web.servlet.FrameworkServlet.doPost(FrameworkServlet.java:868)
	at javax.servlet.http.HttpServlet.service(HttpServlet.java:647)
	at org.springframework.web.servlet.FrameworkServlet.service(FrameworkServlet.java:842)
	at javax.servlet.http.HttpServlet.service(HttpServlet.java:728)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:305)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:210)
	at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:101)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:243)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:210)
	at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:101)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:243)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:210)
	at org.apache.catalina.core.ApplicationDispatcher.invoke(ApplicationDispatcher.java:749)
	at org.apache.catalina.core.ApplicationDispatcher.processRequest(ApplicationDispatcher.java:487)
	at org.apache.catalina.core.ApplicationDispatcher.doForward(ApplicationDispatcher.java:412)
	at org.apache.catalina.core.ApplicationDispatcher.forward(ApplicationDispatcher.java:339)
	at org.springframework.web.servlet.view.InternalResourceView.renderMergedOutputModel(InternalResourceView.java:168)
	at org.springframework.web.servlet.view.AbstractView.render(AbstractView.java:303)
	at org.springframework.web.servlet.DispatcherServlet.render(DispatcherServlet.java:1228)
	at org.springframework.web.servlet.DispatcherServlet.processDispatchResult(DispatcherServlet.java:1011)
	at org.springframework.web.servlet.DispatcherServlet.doDispatch(DispatcherServlet.java:955)
	at org.springframework.web.servlet.DispatcherServlet.doService(DispatcherServlet.java:877)
	at org.springframework.web.servlet.FrameworkServlet.processRequest(FrameworkServlet.java:966)
	at org.springframework.web.servlet.FrameworkServlet.doPost(FrameworkServlet.java:868)
	at javax.servlet.http.HttpServlet.service(HttpServlet.java:647)
	at org.springframework.web.servlet.FrameworkServlet.service(FrameworkServlet.java:842)
	at javax.servlet.http.HttpServlet.service(HttpServlet.java:728)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:305)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:210)
	at org.openmrs.module.web.filter.ForcePasswordChangeFilter.doFilter(ForcePasswordChangeFilter.java:60)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:243)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:210)
	at org.openmrs.web.filter.GZIPFilter.doFilterInternal(GZIPFilter.java:64)
	at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:107)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:243)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:210)
	at org.openmrs.module.web.filter.ModuleFilterChain.doFilter(ModuleFilterChain.java:72)
	at org.openmrs.module.owa.filter.OwaFilter.doFilter(OwaFilter.java:64)
	at org.openmrs.module.web.filter.ModuleFilterChain.doFilter(ModuleFilterChain.java:70)
	at org.openmrs.module.web.filter.ModuleFilter.doFilter(ModuleFilter.java:54)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:243)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:210)
	at org.openmrs.web.filter.OpenmrsFilter.doFilterInternal(OpenmrsFilter.java:108)
	at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:107)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:243)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:210)
	at org.springframework.orm.hibernate4.support.OpenSessionInViewFilter.doFilterInternal(OpenSessionInViewFilter.java:150)
	at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:107)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:243)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:210)
	at org.openmrs.web.filter.StartupFilter.doFilter(StartupFilter.java:105)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:243)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:210)
	at org.openmrs.web.filter.StartupFilter.doFilter(StartupFilter.java:105)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:243)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:210)
	at org.openmrs.web.filter.StartupFilter.doFilter(StartupFilter.java:105)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:243)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:210)
	at org.springframework.web.filter.CharacterEncodingFilter.doFilterInternal(CharacterEncodingFilter.java:88)
	at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:107)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:243)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:210)
	at org.apache.catalina.core.StandardWrapperValve.invoke(StandardWrapperValve.java:222)
	at org.apache.catalina.core.StandardContextValve.invoke(StandardContextValve.java:123)
	at org.apache.catalina.authenticator.AuthenticatorBase.invoke(AuthenticatorBase.java:502)
	at org.apache.catalina.core.StandardHostValve.invoke(StandardHostValve.java:171)
	at org.apache.catalina.valves.ErrorReportValve.invoke(ErrorReportValve.java:100)
	at org.apache.catalina.core.StandardEngineValve.invoke(StandardEngineValve.java:118)
	at org.apache.catalina.connector.CoyoteAdapter.service(CoyoteAdapter.java:409)
	at org.apache.coyote.http11.AbstractHttp11Processor.process(AbstractHttp11Processor.java:1044)
	at org.apache.coyote.AbstractProtocol$AbstractConnectionHandler.process(AbstractProtocol.java:607)
	at org.apache.tomcat.util.net.JIoEndpoint$SocketProcessor.run(JIoEndpoint.java:315)
	at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1149)
	at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:624)
	at java.lang.Thread.run(Thread.java:748)
Caused by: org.hibernate.exception.ConstraintViolationException: could not execute batch
	at org.hibernate.exception.internal.SQLStateConversionDelegate.convert(SQLStateConversionDelegate.java:129)
	at org.hibernate.exception.internal.StandardSQLExceptionConverter.convert(StandardSQLExceptionConverter.java:49)
	at org.hibernate.engine.jdbc.spi.SqlExceptionHelper.convert(SqlExceptionHelper.java:126)
	at org.hibernate.engine.jdbc.batch.internal.BatchingBatch.performExecution(BatchingBatch.java:136)
	at org.hibernate.engine.jdbc.batch.internal.BatchingBatch.doExecuteBatch(BatchingBatch.java:114)
	at org.hibernate.engine.jdbc.batch.internal.AbstractBatchImpl.execute(AbstractBatchImpl.java:163)
	at org.hibernate.engine.jdbc.internal.JdbcCoordinatorImpl.executeBatch(JdbcCoordinatorImpl.java:226)
	at org.hibernate.engine.spi.ActionQueue.executeActions(ActionQueue.java:484)
	at org.hibernate.engine.spi.ActionQueue.executeActions(ActionQueue.java:351)
	at org.hibernate.event.internal.AbstractFlushingEventListener.performExecutions(AbstractFlushingEventListener.java:350)
	at org.hibernate.event.internal.DefaultFlushEventListener.onFlush(DefaultFlushEventListener.java:56)
	at org.hibernate.internal.SessionImpl.flush(SessionImpl.java:1258)
	at org.hibernate.internal.SessionImpl.managedFlush(SessionImpl.java:425)
	at org.hibernate.engine.transaction.internal.jdbc.JdbcTransaction.beforeTransactionCommit(JdbcTransaction.java:101)
	at org.hibernate.engine.transaction.spi.AbstractTransactionImpl.commit(AbstractTransactionImpl.java:177)
	at org.springframework.orm.hibernate4.HibernateTransactionManager.doCommit(HibernateTransactionManager.java:584)
	... 107 more
Caused by: java.sql.BatchUpdateException: Duplicate entry '1-lockoutTimestamp' for key 'PRIMARY'
	at com.mysql.jdbc.PreparedStatement.executeBatchSerially(PreparedStatement.java:2055)
	at com.mysql.jdbc.PreparedStatement.executeBatch(PreparedStatement.java:1467)
	at com.mchange.v2.c3p0.impl.NewProxyPreparedStatement.executeBatch(NewProxyPreparedStatement.java:1135)
	at org.hibernate.engine.jdbc.batch.internal.BatchingBatch.performExecution(BatchingBatch.java:127)
	... 119 more
Caused by: com.mysql.jdbc.exceptions.jdbc4.MySQLIntegrityConstraintViolationException: Duplicate entry '1-lockoutTimestamp' for key 'PRIMARY'
	at sun.reflect.NativeConstructorAccessorImpl.newInstance0(Native Method)
	at sun.reflect.NativeConstructorAccessorImpl.newInstance(NativeConstructorAccessorImpl.java:62)
	at sun.reflect.DelegatingConstructorAccessorImpl.newInstance(DelegatingConstructorAccessorImpl.java:45)
	at java.lang.reflect.Constructor.newInstance(Constructor.java:423)
	at com.mysql.jdbc.Util.handleNewInstance(Util.java:411)
	at com.mysql.jdbc.Util.getInstance(Util.java:386)
	at com.mysql.jdbc.SQLError.createSQLException(SQLError.java:1041)
	at com.mysql.jdbc.MysqlIO.checkErrorPacket(MysqlIO.java:4237)
	at com.mysql.jdbc.MysqlIO.checkErrorPacket(MysqlIO.java:4169)
	at com.mysql.jdbc.MysqlIO.sendCommand(MysqlIO.java:2617)
	at com.mysql.jdbc.MysqlIO.sqlQueryDirect(MysqlIO.java:2778)
	at com.mysql.jdbc.ConnectionImpl.execSQL(ConnectionImpl.java:2825)
	at com.mysql.jdbc.PreparedStatement.executeInternal(PreparedStatement.java:2156)
	at com.mysql.jdbc.PreparedStatement.executeUpdate(PreparedStatement.java:2441)
	at com.mysql.jdbc.PreparedStatement.executeBatchSerially(PreparedStatement.java:2007)
	... 122 more
</pre>
```
