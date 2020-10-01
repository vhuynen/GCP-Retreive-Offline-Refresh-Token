# How to retrieve a Refresh Token via Google Cloud Platform ?
How to retrieve on offline Refresh Token for your application ?
In this article we authorize an application to send an email on behalf of the user.
For other Google API or scopes it's the same procedure.

If you want to understand a few words about what we are doing below, I advice you to read this link about how to access Google APIs through [OAuth 2.0][oauth].

### Google Cloud Platform (GCP)

First log-in on the [Google Cloud Platform Console][df1] through you Google account.

### Create a New Project
Create a project for your application as below :
<p align="center">
  <img src="https://github.com/vhuynen/GCP-Retreive-Offline-Refresh-Token/blob/master/screenshots/Create%20Project.JPG" width="50%">
</p>

### Enable Gmail RESTfull API for your application
Go to menu : `APIs & Services` >> `Library` search Gmail and enable Gmail API
<p align="center">
  <img src="https://github.com/vhuynen/GCP-Retreive-Offline-Refresh-Token/blob/master/screenshots/Enable%20Gmail%20RestFull%20API.JPG" width="50%">
</p>

### Create credentials to access your enabled APIs
Go to menu : `APIs & Services` >> `Credentials`

Then click on the button : `+ CREATE CREDENTIALS` then go to sub-menu `OAuth client ID` 

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
<img src="https://github.com/vhuynen/GCP-Retreive-Offline-Refresh-Token/blob/master/screenshots/Scope%20Gmail%20Send.JPG" width="50%">
</p>

- Step 3 `Optional info` click on the button `SAVE ANS CONTINUE`
- Step 4 `Summary` click on the button `BACK TO DASHBOARD`

From here, you have activated Gmail API on your Google Cloud Platform, created an application and defined a **consent screen** so that the users authorize your application to use their credentials on behalf of themselves.

Now that your consent screen has been configured for your application, you can resume your settings by clicking on "menu" : `APIs & Services` >> `Credentials`

Then click on the button : `+ CREATE CREDENTIALS` and go to sub-menu `OAuth client ID`

On the screen `Create OAuth client ID` fill the `Name` and fill the choose list `Application type` with the value `Web application`

At the section `Authorized redirect URIs` click on `+ ADD URI` button and add the value `https://developers.google.com/oauthplayground`.
Indeed, we will use the OAuth Playground of Google to retrieve our famous Refresh Token that's the reason why we authorize the consent screen to redirect through Playground.

Finally, `SAVE` the configuration.

### Retrieve your OAuth Client ID and OAuth Client Secret of your application

On the `OAuth 2.0 Client IDs`, click on the download button in order to save your OAuth Client ID en OAuth Client Secret of your application.
Keep this warm, you will need this on the next section.
<p align="center">
<img src="https://github.com/vhuynen/GCP-Retreive-Offline-Refresh-Token/blob/master/screenshots/OAuth%20Client%20ID%20Client%20Secret.JPG" width="50%">
</p>

Now that you are done setting your application on GCP, let's go to retrieve Access Token from Refresh Token...

### Retrieve a Refresh Token for offline call API
Now, we are going to [OAuth Playground][playground] from Google to retrieve a Refresh Token.
- Step 1 : Select & authorize APIs
  - Select the scope : https://www.googleapis.com/auth/gmail.send
- Click on the `OAuth 2.0 configuration` button at the top right-hand corner of the screen and fill both fields `OAuth Client ID` and `OAuth Client secret` with the Client ID and the Client Secret of your application defined on GCP.

<p align="center">
<img src="https://github.com/vhuynen/GCP-Retreive-Offline-Refresh-Token/blob/master/screenshots/OAuth%20Playground.JPG" width="50%">
</p>

- Press the `Authorize APIs` button of the Step 1
- You are going to be redirected to the login screen of Google
- Select the Google account you want to use for this application
- The Identity Provider Google redirects the user to the consent screen that you previously defined on GCP
- You will have to accept to delegate the application to use your credentials to send an email on behalf of yourself
<p align="center">
<img src="https://github.com/vhuynen/GCP-Retreive-Offline-Refresh-Token/blob/master/screenshots/Consent%20Screen.JPG" width="35%">
</p>

- Step 2, press the button `Exchange authorization code for tokens`
- Then, you will fetch an Access Token and the offline Refresh Token for your application

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
### How to use your Refresh Token to retreive an Access Token
In this section, [Postman][postman] will be used to first retrieve an Access Token from the Refresh Token. Next, this exact same Access Token will be used to send an email through Gmail API.


### Retreive an Access Token with Postman
Click on this link if you are looking for more details : [refreshing an access token (offline access)][offline]

The request's format to retrieve the Access Token should look like that :
```
POST /token HTTP/1.1
Host: oauth2.googleapis.com
Content-Type: application/x-www-form-urlencoded

client_id=889667048706-ifka3cves5utl4k1f60a8k76l7r7gq3s.apps.googleusercontent.com&client_secret=lryqPIM6pZJyY6a9NF-g0PD1&refresh_token=1//04AQ61pvoFSOBCgYIARAAGAQSNwF-L9Ir8jMd6pSAXnE0s2x7Hu4wVElgo_hB_s7W_nO61zEiDuZGtSQuADJamaZOO4robDvjsIo&grant_type=refresh_token
```
the token server returns a JSON object that contains a new access token for the scope https://www.googleapis.com/auth/gmail.send
 ```
 {
    "access_token": "ya29.a0AfH6SMBkHYSGMpv4rfN9ICB9mIpvnXqd68r3dkMCTIrhvuUVupnLgVoVzakd_jGiIMjRsVKEoyzEuBlejX3igGmBEVJcTGXI3kbBM55usXmWEJvDqujlI_ri30YwIkhXz_IMBsENK7aVTL4sjzHj-mYO4PDI12KLsXXi",
    "expires_in": 3599,
    "scope": "https://www.googleapis.com/auth/gmail.send",
    "token_type": "Bearer"
}
 ```
### Send an email via Gmail API

For more details about the REST **send** Gmail API : [users.messages.send][gmailsendapi]  

> URI : https://www.googleapis.com/upload/gmail/v1/users/:userId/messages/send?uploadType=media :**userId** is the user's email address.

Body request :
```
POST /upload/gmail/v1/users/vincent.huynen@gmail.com/messages/send?uploadType=media HTTP/1.1
Host: www.googleapis.com
Content-Type: message/rfc822
Authorization: Bearer ya29.a0AfH6SMBkHYSGMpv4rfN9ICB9mIpvnXqd68r3dkMCTIrhvuUVupnLgVoVzakd_jGiIMjRsVKEoyzEuBlejX3igGmBEVJcTGXI3kbBM55usXmWEJvDqujlI_ri30YwIkhXz_IMBsENK7aVTL4sjzHj-mYO4PDI12KLsXXi

from:vincent.huynen@gmail.com
to:vincent.huynen@gmail.com
subject:Have a Nice Day !

My body content
```
Success response from Gmail API: **HTTP/1.1 200 OK**
```
{
    "id": "174de384530491b0",
    "threadId": "174de384530491b0",
    "labelIds": [
        "UNREAD",
        "SENT",
        "INBOX"
    ]
}
```
You've got mail check your Gmail Inbox !
> You can send at most 100 mails for free per day with this API.
> It's usually enough for your personal projects.

<p align="center">
<img src="https://github.com/vhuynen/GCP-Retreive-Offline-Refresh-Token/blob/master/screenshots/Gmail%20test.JPG" width="75%">
</p>

I hope that this tutorial helped you to demystify OAuth 2.0 as well as the use of Refresh Token in your upcoming IoT project.

 [oauth]: <https://developers.google.com/identity/protocols/oauth2>
 [df1]: <https://console.cloud.google.com/>
 [scopes]: <https://developers.google.com/gmail/api/auth/scopes>
 [playground]: <https://developers.google.com/oauthplayground>
 [postman]: <https://www.postman.com>
 [offline]: <https://developers.google.com/identity/protocols/oauth2/web-server#offline>
 [gmailsendapi]: <https://developers.google.com/gmail/api/reference/rest/v1/users.messages/send>
