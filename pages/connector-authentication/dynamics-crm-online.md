---
title: Microsoft Dynamics Authentication
sidebar: cyclr_sidebar
permalink: dynamics-connector
tags: [connector]
---

# Dynamics CRM #

Partner Setup
-------------

Dynamics CRM Online uses OAuth 2. Please sign up for an application on Microsoft first and get an OAuth client ID and client secret.

See here for the [official documentation for creating an Azure Active Directory application](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-integrating-applications).

We will summarise it in a few points:

1. Register a free Azure account or Dynamics Online trial account; log into your Azure or Dynamics Online account if you already have one.
2. Go to Microsoft Azure portal -> Azure Active Directory -> App Registrations -> New application registration.

   Below are the details you should provide:

   **Name**: Your Application Name

   **Application type**: Web app / API

   **Sign-on URL**: Your Cyclr service domain, e.g. https://app-h.cyclr.com/. This can be found in your Cyclr Console under Settings > Integration Settings > Service Domain.

   **Reply URLs**: you must add 2 callback URLs to allow Dynamics CRM to be used in your Cyclr Console templates as well as your Cyclr accounts.

   These URLs are:

   * {% raw %}https://{{Your Cyclr console domain e.g. my.cyclr.com or my.cyclr.uk}}/connector/callback{% endraw %}
   * {% raw %}https://{{Your Cyclr service domain e.g. app-h.cyclr.com}}/connector/callback{% endraw %}

   **Multi-tenanted**: Yes

   **Required Permissions**: Dynamics CRM Online and Windows Azure Active Directory

3. Go to Cyclr Console (https://yourCyclrInstance/console) > Connectors > Connector Library > Dynamics CRM Online > Setup

   **Client ID**: This is the Application ID displayed in the portal

   **Client Secret**: Create a Password under Microsoft Azure portal > Azure Active Directory > App Registrations > Your Application > API Access > Keys. Copy and paste the password as the client secret

Dynamics CRM Online connector is now set up! You can test it by installing it in one of your customer accounts.

API Integration Guide
---------------------

Dynamics CRM Online uses OAuth 2 Authorisation Code. The only thing to set up before getting an authentication token is to provide the domain of your Dynamics CRM Online instance.

To do this, create an account connector property named **Resource**:

```
curl -X POST 
     -H 'Content-Type: application/json' 
     -H 'Accept: application/json' 
     -d '{
            "Name": "Resource",
            "Value": "https://example.crm.dynamics.com"
         }'
'https://yourCyclrInstance/v1.0/account/connectors/DYNAMICS_ACCOUNT_CONNECTOR_ID/properties'
```

After successfully creating the account connector property, you can get a one-time sign-in token and call _/UpdateAccountConnectorOAuth_ to complete the user challenge.

FAQ
---

### Error: AADSTS65001

Follow the below step if you are getting the error AADSTS65001: The user or administrator has not consented to use the application with ID ” named ”. Send an interactive authorization request for this user and resource.

1.  Go to Microsoft Azure portal -> Azure Active Directory -> App Registrations -> Your Application name -> Required Permissions
2.  Click the Grant permissions button to allow the app to be installed in your own directory.
