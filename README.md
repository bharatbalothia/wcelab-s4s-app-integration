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



10.create account configuration by clicking on Add a new account
	 
	
	Leave all fileds blank Click on ‘Connect’

	

		Ensure below fields are seen.
	


11) Modify the S4S service url and Authorization values (Client ID and Client secret ) 

	Click on 

		


	Modify URL 

		

	Modify Client ID & Client Secret

		



	Do the same steps for the ‘Http connector 3 

		


12) Click on Done at right corner

		

13) Start the API

	


14) Click on Manage

	



Disable/Enable depends on the authentication model you choose.. by default it’s enabled.. If it is enabled, the calling application has to pass IBM Client ID as part of http headers.



If you disable ‘Click on Save’



Create endpoint by clicking on ‘Create API key and documentation link’







Provide some name and click on Create button




It will create endpoint as shown below



Copy the link and paste in browser and look for below end point




Use the above end point in calling application.
