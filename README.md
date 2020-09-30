# Google Cloud Platform - How to retrieve Refresh-Token
How to retrieve on offline Refresh Token for your application ?
In this article we authorize the application to send an email on behalf of the user.
For other Google API or scopes it's the same procedure.

### Google Cloud Platform (GCP)
First login you on the [Google Cloud Platform Console][df1] with you Google account.

### Create a New Project
Create a project for your application as it :
<p align="center">
  <img src="https://github.com/vhuynen/GCP-Retreive-Offline-Refresh-Token/blob/master/screenshot/Create%20Project.JPG" width="50%">
</p>

### Enable Gmail RESTfull API for your application
Go to menu : `APIs & Services` >> `Library` search Gmail and enable Gmail API
<p align="center">
  <img src="https://github.com/vhuynen/GCP-Retreive-Offline-Refresh-Token/blob/master/screenshot/Enable%20Gmail%20RestFull%20API.JPG" width="50%">
</p>

### Create credentials to access your enabled APIs
Go to menu : `APIs & Services` >> `Credentials`

Then click on the button : `+ CREATE CREDENTIALS` and go to sub-menu `OAuth client ID` 

Click on `CONFIGURE CONSENT SCREEN` button

Choose radio button `External` and then click `CREATE` button

- Step 1, fill all required fields from App Information form :

- Step 2 `SCOPES` 
  - Click on `ADD OR REMOVE SCOPES`
  - Fill gmail term in the filter and choose the scope `.../auth/gmail.send`
  > Keep in mind that we want to send an email on behalf of user.
  > The scope we need to access is : https://www.googleapis.com/auth/gmail.send
  > All scopes for Gmail API are here [Gmail scopes][scopes]
  - Click on the `UPDATE` button
  - Finally, click on the button `SAVE ANS CONTINUE`
<p align="center">
<img src="https://github.com/vhuynen/GCP-Retreive-Offline-Refresh-Token/blob/master/screenshot/Scope%20Gmail%20Send.JPG" width="50%">
</p>

- Step 3 `Optional info` click on the button `SAVE ANS CONTINUE`
- Step 4 `Summary` click on the button `BACK TO DASHBOARD`

At this step, you have activated Gmail API on your Google Cloud Platform, created an application and defined a **consent screen** for that clients authorize your application to use their credentials on behalf of themselves.

Now that your consent screen has been configured for your application, you can resume you settings by going to menu : `APIs & Services` >> `Credentials`

Then click on the button : `+ CREATE CREDENTIALS` and go to sub-menu `OAuth client ID`

On the screen `Create OAuth client ID` fill the `Name` and fill the choose list `Application type` with the value `Web application`

Click on button `+ ADD URI` and at the section `Authorized redirect URIs` and add the value `https://developers.google.com/oauthplayground`
Indeed, we will use the OAuth Playground of Google to retrieve our famous Refresh Token it's the reason we authorize the consent screen to redirect through Playground.

Finally, `SAVE` the configuration.

### Retrieve your OAuth Client ID and OAuth Client Secret of your application

On the `OAuth 2.0 Client IDs`, click on the download button in order to save your OAuth Client ID en OAuth Client Secret of your application.
Keep this warm, you will need this on the next section.
<p align="center">
<img src="https://github.com/vhuynen/GCP-Retreive-Offline-Refresh-Token/blob/master/screenshot/OAuth%20Client%20ID%20Client%20Secret.JPG" width="50%">
</p>

Right now, we have finished to set your application on GCP. Let's go to retrieve Access Token from Refresh Token...

### Retrieve a Refresh Token for offline call API
Now, we are going to [OAuth Playground][playground] of Google to retrieve a Refresh Token.
- Step 1 : Select & authorize APIs
  - Select the scope : https://www.googleapis.com/auth/gmail.send
- Click on the `OAuth 2.0 configuration` button on the right of the screen and fill both fields `OAuth Client ID` and `OAuth Client secret` with the Client ID and the Client Secret of your application defined on GCP.

<p align="center">
<img src="https://github.com/vhuynen/GCP-Retreive-Offline-Refresh-Token/blob/master/screenshot/OAuth%20Playground.JPG" width="50%">
</p>

- Press on the `Authorize APIs` button of the Step 1
- You are redirected on the login screen of Google
- Choose the Google account you want to use for this application
- The IdP Google redirect the user on the consent screen you are defined on GCP
- The user accept to delegate the application to use his credentials to send on email on behalf of him
<p align="center">
<img src="https://github.com/vhuynen/GCP-Retreive-Offline-Refresh-Token/blob/master/screenshot/Consent%20Screen.JPG" width="50%">
</p>

- Step 2, press on the button `Exchange authorization code for tokens`
- Then, you retrieve an Access Token and the Refresh Token !

```
HTTP/1.1 200 OK
Content-length: 425
X-xss-protection: 0
X-content-type-options: nosniff
Transfer-encoding: chunked
Vary: Origin, X-Origin, Referer
Server: scaffolding on HTTPServer2
-content-encoding: gzip
Cache-control: private
Date: Tue, 29 Sep 2020 16:45:38 GMT
X-frame-options: SAMEORIGIN
Alt-svc: h3-Q050=":443"; ma=2592000,h3-29=":443"; ma=2592000,h3-27=":443"; ma=2592000,h3-T051=":443"; ma=2592000,h3-T050=":443"; ma=2592000,h3-Q046=":443"; ma=2592000,h3-Q043=":443"; ma=2592000,quic=":443"; ma=2592000; v="46,43"
Content-type: application/json; charset=utf-8
{
  "access_token": "ya29.a0AfH6SMBkylMobb2awutHFaxdcZesmvNvU4zGRdVfTABDwVMbzX7ldMvD53CUZHTY-ii9-LdBzx-3-zy0Qj9TQGtStJuhGzqifUb_iaEHh655cAjM0R4cMo6rr_MWbI1zUnlmiw5PrA76u3uxTZjN78DeWLU6sj1Fuyo", 
  "scope": "https://www.googleapis.com/auth/gmail.send", 
  "token_type": "Bearer", 
  "expires_in": 3599, 
  "refresh_token": "1//04AQ61pvoFSOBCgYIARAAGAQSNwF-L9Ir8jMd6pSAXnE0s2x7Hu4wVElgo_hB_s7W_nO61zEiDuZGtSQuADJamaZOO4robDvjsIo"
}
``` 
### How to use your Refresh Token to retreive on Access Token
In this section, we will use [Postman][postman] to first retrieve an Access Token from the Refresh Token and second use the Access Token in order to send an email thanks to the Gmail API.



 
 
 
 [df1]: <https://console.cloud.google.com/>
 [scopes]: <https://developers.google.com/gmail/api/auth/scopes>
 [playground]: <https://developers.google.com/oauthplayground>
 [postman]: <https://www.postman.com>
