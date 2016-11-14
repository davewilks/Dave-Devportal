---
heading: OAuth2
title: OAuth2
seo: OAuth2 | Cloud Elements API Docs
description: How OAuth2 Works with Cloud Elements
layout: docs
order: 3
categories: [gettingstarted]
---

## OAUTH2 WITH CLOUD ELEMENTS

Cloud Elements has standardized the OAuth2 flow for each OAuth2 element. Salesforce, Hubspot, all Documents Hub Elements are
just some of the OAuth2 elements that we expose.  
{% include padding-all.html %}
### The Connected App
OAuth2 is completely dependent on a connected app that you create at the Endpoint. This is where you get an API Key and Secret
used for provisioning.  

The API key and secret will represent your Application within the Endpoint. When you get your own API key and secret it will show the following
in the OAuth2 flow.
![Eloqua App](/assets/img/eloqua-app.png)  

It says grant access to "Cloud Elements Staging Connector" because you are using the Cloud Elements API Key and Secret.  

### Generic OAuth2 Steps

#### 1. Call ```GET /{elementKey}/oauth/url ```
In your application, if you have a button that says, "Connect to your Salesforce." When the user clicks that button you would call this API.
That will return an URL that you will then redirect your user to:  

```json
{
    "oauthUrl": "https://login.salesforce.com/services/oauth2/authorize?response_type=code&client_id=MVG9A2kN3Bn17huqpbZ.99EPdhIK6o1gB7E3Y42_swsBVklSkNNChnvIGTxb0GAzTUrZKrnMLbbazmLkeZrt&client_secret=996596135756415222&scope=full%20refresh_token&redirect_uri=https://console.cloud-elements.com/elements/jsp/home.jsp&state=sfdc",
    "element": "sfdc"
}
```
This will take the customer to the endpoint, where they will login and grand your application access the their account.  
When they are done, it will callback to the callback URL. When authentication is integrated it will callback to your application.  

#### 2. Handle Callback
When you configure a connected app at the endpoint you will set a Callback URL. This will be a URL on your web application that the OAuth2 flow will
return to. When it this callback happens it will redirect with an "Authorization Code" as a query parameter.  

```bash
https://console.cloud-elements.com/elements/jsp/home.jsp?code=aPrxMZkm7lCkgfRp6r.wjav5No7dhomWdZo.nU.MY1YNwQ9NatZ.zx9iGCp6TmYZA4b0v4igeQ%3D%3D&state=sfdc
```
You will need to take this Code and use it to create an instance on Cloud Elements  

#### 3. Call ```POST /instances```
Once you have the code all you have to do is send it to Cloud Element with the Same API key and Secret. With the following payload as an example.  

```json
{
  "element": {
    "key": "sfdc"
  },
  "providerData": {
    "code": "aPrxMZkm7lCkgfRp6r.wjav5NtEiWEdm0Ol4UxpgX.3WGDkFjtt1.AuAx_nqCQ05p94a50Anrw%3D%3D"
  },
  "configuration": {
    "oauth.callback.url": "https://console.cloud-elements.com/elements/jsp/home.jsp",
    "oauth.api.key": "3MVG9A2kN3Bn17huqpbZ.99EPdhIK6o1gB7E3Y42_swsBVklSkNNChnvIGTxb0GAzTUrZKrnMLbbazmLkeZrt",
    "oauth.api.secret": "5996596135756415222"
  },
  "tags": [
    "api tag"
  ],
  "name": "sfdc api"
}
```

Keep in mind this is a generic example. These steps will be the same for each OAuth2 Element, but different elements will require different information
to create instances.  

*  NOTE
The API Key, Secret and Callback URL needs to be exactly the same in all three places in order to create an instance.  
  1. In the connected app setting in the endpoint.
  2. In your call to ```GET {elementKey}/oauth/url```
  3. In your call to ```POST /instances```

If these are not exactly the same in all three places it the authentication will not work.

### Thats It
When you create an instance we will return you an Element Token for that instance. You will need to save the Element Token along with the Instance ID in your app.   
If you are familiar with OAuth, the access token that is used for authentication needs to be refreshed on a specific interval.
Cloud Elements will take care of that for you. So all you need to worry about is saving the Element Token.
