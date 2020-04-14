Deployment process

1. Developer is ready to push to prod
1. Developer exports the yaml to local machine
1. Developoer uploads the yaml to github and tag for release to prod.
1. Release team downloads from github by release tag 
1. Release team logs in to production app connect.
1. import the Yaml in to production environment
1. Open the flow
1. Click on Edit flow
1. Select any Http connecter.
1. Create account configuration by clicking on Add a new account
   1. Leave all fileds blank Click on ‘Connect’
   1. Ensure All fields are seen and populated with values.
1. Modify the S4S service url and Authorization values (Client ID and Client secret ) 
   1. Click on  Http Connector 1
   1. Modify URL 
   1. Modify Client ID & Client Secret in 'Authroization' Field
   1. Do the same steps for the ‘Http connector 3 
1. Click on 'Done' button at right corner	
1. Start the API
1. Click on Manage
1. 'Require applicaton authentication by api key' can be disabled no authentication method is needed.By default this will be enabled.. If it is enabled, then the calling application has to pass IBM Client ID as part of http headers for authentication purpose.
   - If you disable ‘Click on Save’ button on the same page in below.
1. Create endpoint by clicking on ‘Create API key and documentation link’
   - Provide some name and click on Create button. It will display the link.
1. Copy the link and paste in browser and look for endpoint url and sample curl statement.
1. Use the same end point in calling application.
