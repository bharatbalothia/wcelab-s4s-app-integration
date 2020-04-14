Deployment process

1.Developer is ready to push to prod

2.Developer exports the yaml to local machine

3.Developoer uploads the yaml to github and tag for release to prod.

4.Release team downloads from github by release tag 

5.Release team logs in to production app connect.

6.import the Yaml in to production environment

7.Open the flow

8.Click on Edit flow

9.Select any Http connecter.

10.Create account configuration by clicking on Add a new account
	
	Leave all fileds blank Click on ‘Connect’
	Ensure All fields are seen and populated with values.
	
11) Modify the S4S service url and Authorization values (Client ID and Client secret ) 
	Click on  Http Connector 1
	Modify URL 
	Modify Client ID & Client Secret in 'Authroization' Field
	Do the same steps for the ‘Http connector 3 

12) Click on 'Done' button at right corner		

13) Start the API

14) Click on Manage

15) 'Require applicaton authentication by api key' can be disabled no authentication method is needed.By default this will be enabled.. If it is enabled, then the calling application has to pass IBM Client ID as part of http headers for authentication purpose.

	If you disable ‘Click on Save’ button on the same page in below.

16)Create endpoint by clicking on ‘Create API key and documentation link’
	Provide some name and click on Create button. It will display the link.
17)Copy the link and paste in browser and look for endpoint url and sample curl statement.
18) Use the same end point in calling application.
