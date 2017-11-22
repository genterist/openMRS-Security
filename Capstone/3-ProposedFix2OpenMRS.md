## PROPOSED PULL REQUEST FOR 1-2 LOGIN PAGE REDIRECT TO LOGOUT 

### Affected module : OpenMRS login
+ Page location : http://localhost:8081/openmrs-standalone/login.htm
+ Attack type : unauthorized redirect after login
+ Attack value : %2Fopenmrs-standalone%2Fappui%2Fheader%2Flogout.action%3FsuccessUrl%3Dopenmrs-standalone

We propose the following bug fixe - replacing any "logout" string with a "home" string so that even when attackers found a way to force the logout page (to accomplish denial of service), the server codes will change that and redirect user back to home.

#### Original code
![alt text](https://github.com/genterist/openMRS-Security/blob/master/4-SecurityPrinciples/images/t-fix3.png)
<br/>

#### Modified code
![alt text](https://github.com/genterist/openMRS-Security/blob/master/4-SecurityPrinciples/images/t-fix4.png)
<br/>

#### Code locations

Searching 3348 files for "redirectUrl"

\openmrs-module-referenceapplication\omod\src\main\java\org\openmrs\module\referenceapplication\page\controller\LoginPageController.java:
   72  	 * @should redirect the user to the home page if they are already authenticated
   73  	 * @should show the user the login page if they are not authenticated
   74: 	 * @should set redirectUrl in the page model if any was specified in the request
   75: 	 * @should set the referer as the redirectUrl in the page model if no redirect param exists
   76: 	 * @should set redirectUrl in the page model if any was specified in the session
   77: 	 * @should not set the referer as the redirectUrl in the page model if referer URL is outside context path
   78: 	 * @should set the referer as the redirectUrl in the page model if referer URL is within context path
   79  	 */
   80  	public String get(PageModel model,
   ..
   85  	                  @SpringBean("appFrameworkService") AppFrameworkService appFrameworkService) {
   86  
>> 87: 		String redirectUrl = getRedirectUrl(pageRequest);
   88  
   89  		if (Context.isAuthenticated()) {
   90: 			if(StringUtils.isNotBlank(redirectUrl)){
   91: 				return "redirect:" + getRelativeUrl(redirectUrl, pageRequest);
   92  			}
   93  			return "redirect:" + ui.pageLink(ReferenceApplicationConstants.MODULE_ID, "home");
   94  		}
   95  
   96: 		model.addAttribute(REQUEST_PARAMETER_NAME_REDIRECT_URL, getRelativeUrl(redirectUrl, pageRequest));
   97  
   98  		Location lastSessionLocation = null;
   ..
  116  	}
  117  
  118: 	private boolean isUrlWithinOpenmrs(PageRequest pageRequest, String redirectUrl){
  119: 		if (StringUtils.isNotBlank(redirectUrl)) {
  120: 			if (redirectUrl.startsWith("http://") || redirectUrl.startsWith("https://")) {
  121  				try {
  122:                     URL url = new URL(redirectUrl);
  123                      String urlPath = url.getFile();
  124                      String urlContextPath = urlPath.substring(0, urlPath.indexOf('/', 1));
  ...
  129                      log.error(e.getMessage());
  130                  }
  131: 			} else if(redirectUrl.startsWith(pageRequest.getRequest().getContextPath())){
  132  				return true;
  133  			}
  ...
  136  	}
  137  
>>138: 	private String getRedirectUrlFromReferer(PageRequest pageRequest) {
  139  		String manualLogout = pageRequest.getSession().getAttribute(AppUiConstants.SESSION_ATTRIBUTE_MANUAL_LOGOUT, String.class);
  140: 		String redirectUrl = "";
  141  		if(!Boolean.valueOf(manualLogout)){
  142: 			redirectUrl = pageRequest.getRequest().getHeader("Referer");
  143  		} else {
  144  			Cookie cookie = new Cookie(ReferenceApplicationWebConstants.COOKIE_NAME_LAST_USER, null);
  ...
  148  		}
  149  		pageRequest.getSession().setAttribute(AppUiConstants.SESSION_ATTRIBUTE_MANUAL_LOGOUT, null);
  150: 		return redirectUrl;
  151  	}
  152  
  153: 	private String getRedirectUrlFromRequest(PageRequest pageRequest){
  154  		return pageRequest.getRequest().getParameter(REQUEST_PARAMETER_NAME_REDIRECT_URL);
  155  	}
  156  
  157: 	private String getRedirectUrl(PageRequest pageRequest) {
  158: 		String redirectUrl = getRedirectUrlFromRequest(pageRequest);
  159: 		if (StringUtils.isBlank(redirectUrl)) {
  160: 			redirectUrl = getStringSessionAttribute(SESSION_ATTRIBUTE_REDIRECT_URL, pageRequest.getRequest());
  161  		}
  162: 		if (StringUtils.isBlank(redirectUrl)) {
  163: 			redirectUrl = getRedirectUrlFromReferer(pageRequest);
  164  		}
  165: 		if (StringUtils.isNotBlank(redirectUrl) && isUrlWithinOpenmrs(pageRequest, redirectUrl)) {
  166: 			return redirectUrl;
  167  		}
  168  		return "";
  ...
  180  	 * @param sessionContext
  181  	 * @return
  182: 	 * @should redirect the user back to the redirectUrl if any
  183: 	 * @should redirect the user to the home page if the redirectUrl is the login page
  184  	 * @should send the user back to the login page if an invalid location is selected
  185  	 * @should send the user back to the login page when authentication fails
  ...
  191  	                   UiSessionContext sessionContext) {
  192  
  193: 		String redirectUrl = pageRequest.getRequest().getParameter(REQUEST_PARAMETER_NAME_REDIRECT_URL);
  194: 		redirectUrl = getRelativeUrl(redirectUrl, pageRequest);
  195  		Location sessionLocation = null;
  196  		if (sessionLocationId != null) {
  ...
  238  					}
  239  
  240: 					if (StringUtils.isNotBlank(redirectUrl)) {
  241  						//don't redirect back to the login page on success nor an external url
  242: 						if (isUrlWithinOpenmrs(pageRequest, redirectUrl)) {
  243: 							if (!redirectUrl.contains("login.") && isSameUser(pageRequest, username)) {
  244                                  if (log.isDebugEnabled())
  245:                                     log.debug("Redirecting user to " + redirectUrl);
  246:                                 return "redirect:" + redirectUrl;
  247                              } else {
  248                                  if (log.isDebugEnabled())
  ...
  277  		//TODO limit login attempts by IP Address
  278  
  279: 		pageRequest.getSession().setAttribute(SESSION_ATTRIBUTE_REDIRECT_URL, redirectUrl);
  280  
  281  		return "redirect:" + ui.pageLink(ReferenceApplicationConstants.MODULE_ID, "login");


\openmrs-module-referenceapplication\omod\src\main\java\org\openmrs\module\referenceapplication\ReferenceApplicationWebConstants.java:
   22  	public static final String SESSION_ATTRIBUTE_REDIRECT_URL = "_REFERENCE_APPLICATION_REDIRECT_URL_";
   23  	
   24: 	public static final String REQUEST_PARAMETER_NAME_REDIRECT_URL = "redirectUrl";
   25  
   26      public static final String COOKIE_NAME_LAST_SESSION_LOCATION = "referenceapplication.lastSessionLocation";


\openmrs-module-referenceapplication\omod\src\main\webapp\pages\login.gsp:
  158              </fieldset>
  159  
  160:     		<input type="hidden" name="redirectUrl" value="${redirectUrl}" />
  161  
  162          </form>


\openmrs-module-referenceapplication\omod\src\test\java\org\openmrs\module\referenceapplication\page\controller\LoginPageControllerTest.java:
  162  	 */
  163  	@Test
  164: 	@Verifies(value = "should set redirectUrl in the page model if openmrs related url was specified in the request", method = "get(PageModel,UiUtils,PageRequest)")
  165: 	public void get_shouldSetRedirectUrlInThePageModelIfOpenmrsRelatedUrlWasSpecifiedInTheRequest() throws Exception {
  166  		when(Context.isAuthenticated()).thenReturn(false);
  167  
  168: 		String redirectUrl = TEST_CONTEXT_PATH + "/referenceapplication/patient.page";
  169  		MockHttpServletRequest request = new MockHttpServletRequest();
  170  		request.setContextPath(TEST_CONTEXT_PATH);
  171: 		request.addParameter(REQUEST_PARAMETER_NAME_REDIRECT_URL, redirectUrl);
  172  		PageModel pageModel = new PageModel();
  173  
  174  		new LoginPageController().get(pageModel, uiUtils, createPageRequest(request, null), null, null, appFrameworkService);
  175  
  176: 		assertEquals(redirectUrl, pageModel.get(REQUEST_PARAMETER_NAME_REDIRECT_URL));
  177  	}
  178  
  ...
  184  	 */
  185  	@Test
  186: 	@Verifies(value = "should set the referer as the redirectUrl in the page model if no redirect param exists", method = "get(PageModel,UiUtils,PageRequest)")
  187: 	public void get_shouldSetTheRefererAsTheRedirectUrlInThePageModelIfNoRedirectParamExists() throws Exception {
  188  		when(Context.isAuthenticated()).thenReturn(false);
  189  
  ...
  206  	 */
  207  	@Test
  208: 	@Verifies(value = "should set redirectUrl in the page model if any was specified in the session", method = "get(PageModel,UiUtils,PageRequest)")
  209: 	public void get_shouldSetRedirectUrlInThePageModelIfAnyWasSpecifiedInTheSession() throws Exception {
  210  		when(Context.isAuthenticated()).thenReturn(false);
  211  
  212: 		String redirectUrl = TEST_CONTEXT_PATH + "/referenceapplication/patient.page";
  213  		MockHttpServletRequest request = new MockHttpServletRequest();
  214  		request.setContextPath(TEST_CONTEXT_PATH);
  215  		PageRequest pageRequest = createPageRequest(request, null);
  216  		HttpSession httpSession = new MockHttpSession();
  217: 		httpSession.setAttribute(SESSION_ATTRIBUTE_REDIRECT_URL, redirectUrl);
  218  		request.setSession(httpSession);
  219  
  ...
  221  		new LoginPageController().get(pageModel, uiUtils, pageRequest, null, null, appFrameworkService);
  222  
  223: 		assertEquals(redirectUrl, pageModel.get(REQUEST_PARAMETER_NAME_REDIRECT_URL));
  224  	}
  225  
  ...
  231  	 */
  232  	@Test
  233: 	@Verifies(value = "should redirect user to requested url specified in ?redirectUrl if it is openmrs related and user is authenticated", method = "get(PageModel,UiUtils,PageRequest)")
  234  	public void get_shouldRedirectUserToRequestedUrlIfAuthenticated() throws Exception{
  235  		when(Context.isAuthenticated()).thenReturn(true);
  236  
  237: 		String redirectUrl = TEST_CONTEXT_PATH + "/referenceapplication/patient.page";
  238  		MockHttpServletRequest request = new MockHttpServletRequest();
  239  		request.setContextPath(TEST_CONTEXT_PATH);
  240: 		request.setParameter(REQUEST_PARAMETER_NAME_REDIRECT_URL, redirectUrl);
  241  		PageRequest pageRequest = createPageRequest(request, null);
  242  		HttpSession httpSession = new MockHttpSession();
  ...
  245  		PageModel pageModel = new PageModel();
  246  
  247: 		assertEquals("redirect:" + redirectUrl, new LoginPageController().get(pageModel, uiUtils, pageRequest, null, null, appFrameworkService));
  248  	}
  249  
  ...
  255  	 */
  256  	@Test
  257: 	@Verifies(value = "should redirect user to home if ?redirectUrl is not openmrs related and user is authenticated", method = "get(PageModel,UiUtils,PageRequest)")
  258  	public void get_shouldRedirectUserToHomeIfAuthenticated() throws Exception{
  259  		when(Context.isAuthenticated()).thenReturn(true);
  260  
  261: 		String redirectUrl = "/somePage/notOpenmrs.page";
  262  		MockHttpServletRequest request = new MockHttpServletRequest();
  263  		request.setContextPath(TEST_CONTEXT_PATH);
  264: 		request.setParameter(REQUEST_PARAMETER_NAME_REDIRECT_URL, redirectUrl);
  265  		PageRequest pageRequest = createPageRequest(request, null);
  266  		HttpSession httpSession = new MockHttpSession();
  ...
  269  		PageModel pageModel = new PageModel();
  270  
  271: 		assertNotEquals("redirect:" + redirectUrl, new LoginPageController().get(pageModel, uiUtils, pageRequest, null, null, appFrameworkService));
  272  	}
  273  
  ...
  279  	@Test
  280  	@Verifies(value = "should redirect user to home after manual logout and login", method = "get(String,String,UiUtils,PageRequest)")
  281: 	public void get_shouldNotSetRedirectUrlParamAfterManualLogout() throws Exception {
  282  		when(Context.isAuthenticated()).thenReturn(false);
  283  
  ...
  310  
  311  		final String homeRedirect = "redirect:" + uiUtils.pageLink(ReferenceApplicationConstants.MODULE_ID, "home");
  312: 		String redirectUrl = TEST_CONTEXT_PATH + "/referenceapplication/patient.page";
  313  
  314  		MockHttpServletRequest request = new MockHttpServletRequest();
  315: 		request.setParameter(REQUEST_PARAMETER_NAME_REDIRECT_URL, redirectUrl);
  316  		request.setCookies(new Cookie(ReferenceApplicationWebConstants.COOKIE_NAME_LAST_USER, String.valueOf("oldUser".hashCode())));
  317  
  ...
  330  	 */
  331  	@Test
  332: 	@Verifies(value = "should redirect old user to page requested in redirectUrl param", method = "post(String,String,UiUtils,PageRequest)")
  333: 	public void post_shouldRedirectOldUserToRedirectUrl() throws Exception {
  334  		setupMocksForSuccessfulAuthentication(true);
  335  
  336: 		String redirectUrl = TEST_CONTEXT_PATH + "/referenceapplication/patient.page";
  337  
  338  		MockHttpServletRequest request = new MockHttpServletRequest();
  339: 		request.setParameter(REQUEST_PARAMETER_NAME_REDIRECT_URL, redirectUrl);
  340  		request.setCookies(new Cookie(ReferenceApplicationWebConstants.COOKIE_NAME_LAST_USER, String.valueOf(USERNAME.hashCode())));
  341  		PageRequest pageRequest = createPageRequest(request, null);
  ...
  343  		mockAuthenticatedUser();
  344  		
  345: 		assertEquals("redirect:" + redirectUrl, new LoginPageController().post(USERNAME, PASSWORD, SESSION_LOCATION_ID,
  346  				locationService, uiUtils, pageRequest, sessionContext));
  347  	}
  ...
  353  	 */
  354  	@Test
  355: 	@Verifies(value = "should redirect the user to the home page if the redirectUrl is the login page", method = "post(String,String,UiUtils,PageRequest)")
  356: 	public void post_shouldRedirectTheUserToTheHomePageIfTheRedirectUrlIsTheLoginPage() throws Exception {
  357  		setupMocksForSuccessfulAuthentication(true);
  358  
  359: 		final String redirectUrl = uiUtils.pageLink(ReferenceApplicationConstants.MODULE_ID, "login");
  360  		final String homeRedirect = "redirect:" + uiUtils.pageLink(ReferenceApplicationConstants.MODULE_ID, "home");
  361  		MockHttpServletRequest request = new MockHttpServletRequest();
  362  		request.setContextPath("/openmrs");
  363: 		request.setParameter(REQUEST_PARAMETER_NAME_REDIRECT_URL, redirectUrl);
  364  		PageRequest pageRequest = createPageRequest(request, null);
  365  
  ...
  409  	/**
  410       * @see LoginPageController#get(PageModel,UiUtils,PageRequest,String,LocationService,AppFrameworkService)
  411:      * @verifies not set the referer as the redirectUrl in the page model if referer URL is outside context path
  412       */
  413      @Test
  414:     public void get_shouldNotSetTheRefererAsTheRedirectUrlInThePageModelIfRefererUrlIsOutsideContextPath() throws Exception {
  415      	when(Context.isAuthenticated()).thenReturn(false);
  416      	
  ...
  427  	/**
  428       * @see LoginPageController#get(PageModel,UiUtils,PageRequest,String,LocationService,AppFrameworkService)
  429:      * @verifies set the referer as the redirectUrl in the page model if referer URL is within context path
  430       */
  431      @Test
  432:     public void get_shouldSetTheRefererAsTheRedirectUrlInThePageModelIfRefererUrlIsWithinContextPath() throws Exception {
  433      	when(Context.isAuthenticated()).thenReturn(false);
  434      	
  435:     	String redirectUrl = TEST_CONTEXT_PATH +"/demo/";
  436: 		String refererUrl = "http://openmrs.org" + redirectUrl;    	
  437  		MockHttpServletRequest request = new MockHttpServletRequest();
  438  		request.setContextPath(TEST_CONTEXT_PATH);
  ...
  441  		new LoginPageController().get(pageModel, uiUtils, createPageRequest(request, null), null, null, appFrameworkService);
  442  		
  443: 		assertEquals(redirectUrl, pageModel.get(REQUEST_PARAMETER_NAME_REDIRECT_URL));
  444      }
  445  
  ...
  451  	 */
  452  	@Test
  453: 	@Verifies(value = "should set redirectUrl as redirectUrl param when referer specified", method = "get(PageModel,UiUtils,PageRequest)")
  454: 	public void get_shouldChooseRedirectUrlOverReferer() throws Exception{
  455  		when(Context.isAuthenticated()).thenReturn(true);
  456  
  457: 		String redirectUrl = "/openmrs/redirect.page";
  458  		String refererUrl = "/openmrs/referer.page";
  459  		MockHttpServletRequest request = new MockHttpServletRequest();
  460  		request.setContextPath(TEST_CONTEXT_PATH);
  461: 		request.setParameter(REQUEST_PARAMETER_NAME_REDIRECT_URL, redirectUrl);
  462  		request.addHeader("Referer", refererUrl);
  463  		PageRequest pageRequest = createPageRequest(request, null);
  ...
  467  		PageModel pageModel = new PageModel();
  468  
  469: 		assertEquals("redirect:" + redirectUrl, new LoginPageController().get(pageModel, uiUtils, pageRequest, null, null, appFrameworkService));
  470  	}
  471  }


\openmrs-module-registrationapp\omod\src\main\java\org\openmrs\module\registrationapp\fragment\controller\RegisterPatientFragmentController.java:
  266          InfoErrorMessageUtil.flashInfoMessage(request.getSession(), ui.message("registrationapp.createdPatientMessage", ui.encodeHtml(ui.format(patient))));
  267  
  268:         String redirectUrl = app.getConfig().get("afterCreatedUrl").getTextValue();
  269:         redirectUrl = redirectUrl.replaceAll("\\{\\{patientId\\}\\}", patient.getUuid().toString());
  270          if (registrationEncounter != null) {
  271:             redirectUrl = redirectUrl.replaceAll("\\{\\{encounterId\\}\\}", registrationEncounter.getId().toString());
  272          }
  273  
  274:         return new SuccessResult(redirectUrl);
  275      }
  276  


\openmrs-module-uiframework\omod\src\main\java\org\openmrs\module\uiframework\PageController.java:
  126              }
  127              
  128:             setRedirectUrl(request);
  129              
  130              return "redirect:" + ret;
  ...
  145              APIAuthenticationException authEx = ExceptionUtil.findExceptionInChain(ex, APIAuthenticationException.class);
  146              if (authEx != null) {
  147:             	setRedirectUrl(request);
  148                  throw authEx;
  149              }
  ...
  170      }
  171      
  172:     private void setRedirectUrl(HttpServletRequest request) {
  173      	StringBuffer url = request.getRequestURL();
  174      	String queryStr = request.getQueryString();


\openmrs-module-webservices.rest\omod\src\main\webapp\resources\js\swagger-ui-3.0.10\swagger-ui-bundle.js:
    <binary>


\openmrs-module-webservices.rest\omod\src\main\webapp\resources\js\swagger-ui-3.0.10\swagger-ui-standalone-preset.js:
    <binary>



