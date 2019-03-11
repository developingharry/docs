---
title: OAuth Authentication
sidebar: cyclr_sidebar
permalink: oauth-authentication.html
tags: [installing]
---

# OAuth Authentication #

**_For connectors that require your user to be taken through an OAuth flow._**

Connectors using OAuth require that the user goes through a webflow where they are sent to the third party application to sign in and grant access to Cyclr.

This process is simpler than it sounds.

First of all an Account Sign-In Token needs to be generated for the User see below.

    POST /v1.0/accounts/tokens
    Authorization Bearer 0000000000000000000000000000000000000000000000000000000000000000

Response:

    {
        "Token": "+7fCuHJ1LUq1bGasmHGVvnVw/UfsVe1DlYHXDrFuaBo=",
        "ExpiresAtUtc": "2017-12-08T11:02:48.7436471Z"
    }

The user should then be sent, in there browser to _/web/connector/updateaccountconnectoroauth?id={Account Connector ID}&token{Account Sign-In Token}_

The following query string parameters can also be included:

<table>
    <tr>
        <th>token</th>
        <td>The account sign-in token generated above. <br/>Example: 2890edffcb964e8aab038cf4efc340ab62a4f604bd5a41369654086f5bd25519</td>
    </tr>
    <tr>
        <th>targetOrigin</th>
        <td>Either the origin of the other window for the javascript callback event to be dispatched or a URL to redirect the user to after the OAuth authentication is completed.<br/>Example: https://partner.cyclr.com/connectors</td>
    </tr>
    <tr>
        <th>callbackMessage</th>
        <td>Callback message to be sent by JavaScript postMessage to the parent window, don’t include if using redirect.<br/>Example: done</td>
    </tr>
</table>

Remember to URL encode all parameter values.

Cyclr redirects the user to the appropriate sign in page in the target application, captures the OAuth tokens generated by that app, and stores it internally. Token refresh is handled automatically.

On completion they will be either redirected to targetOrigin or the JavaScript message specified by the callbackMessage will be posted to the parent window to notify the host app that the authentication flow has completed.

[Step Setup](./step-set-up)  
[API Key Authentication](./api-key-authentication)  
[HTTP Basic Authentication](./basic-authentication)