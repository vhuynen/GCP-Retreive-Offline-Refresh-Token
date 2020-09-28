# Google Cloud Platform - How to retrieve Refresh-Token
How to retrieve offline Refresh Token for your application


### Enable Gmail RESTFull API
Go to menu : `APIs & Services` >> `Library` search Gmail and enable Gmail API
<p align="center">
  <img src="https://github.com/vhuynen/GCP-Retreive-Offline-Refresh-Token/blob/master/screenshot/Enable%20Gmail%20RestFull%20API.JPG" width="50%">
</p>

### Create credentials to access your enabled APIs
Go to menu : `APIs & Services` >> `Credentials`

Then click on the button : `+ CREATE CREDENTIALS` and go to sub-menu `OAuth client ID` 

Click on `CONFIGURE CONSENT SCREEN` button

Choose radio button `External` and then click `CREATE` button

At this step fill all required fields from App Information form :

In step 2 `SCOPES` click on the button `SAVE ANS CONTINUE`

In step 3 `Optional info` click on the button `SAVE ANS CONTINUE`

In step 4 `Summary` click on the button `BACK TO DASHBOARD`

At this step you are activated Gmail API on your Google Cloud Platform and setting a consent screen for that clients authorize your application to use their credentials on behalf of themselves.


