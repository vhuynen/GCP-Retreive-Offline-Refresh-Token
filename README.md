# Google Cloud Platform - How to retrieve Refresh-Token
How to retrieve on offline Refresh Token for your application ?
In this article we authorize the application to send an email on behalf of the user. For other scopes it's the same procedure.

### Google Cloud Platform (GCP)
First login you on the [Google Cloud Platform Console] [GCP] with you Google account


### Enable Gmail RESTfull API
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

- Step 2 `SCOPES` 
  - Click on `ADD OR REMOVE SCOPES`
  - Fill gmail term in the filter and choose the scope `.../auth/gmail.send`
  - Click on the `UPDATE` button
  - Finally, click on the button `SAVE ANS CONTINUE`
<p align="center">
<img src="https://github.com/vhuynen/GCP-Retreive-Offline-Refresh-Token/blob/master/screenshot/Scope%20Gmail%20Send.JPG" width="50%">
</p>

- Step 3 `Optional info` click on the button `SAVE ANS CONTINUE`
- Step 4 `Summary` click on the button `BACK TO DASHBOARD`

At this step you are activated Gmail API on your Google Cloud Platform and setting a **consent screen** for that clients authorize your application to use their credentials on behalf of themselves.
Now that your consent screen has been configured for your application, you can resume you settings by going to menu : `APIs & Services` >> `Credentials`

Then click on the button : `+ CREATE CREDENTIALS` and go to sub-menu `OAuth client ID`

[GCP] : <https://console.cloud.google.com/>
