---
title: Create Account
sidebar: cyclr_sidebar
permalink: create-account
tags: [installing]
---

_**A Cyclr account contains Account Connectors and Integrations and will typically have a one to one relationship with an account in your application.**_

If an Account does not already exist, one should be created.

    POST /v1.0/accounts
    Authorization: Bearer 0000000000000000000000000000000000000000000000000000000000000000

    {
        "Name": "Test Account 001",
        "Description": "An account we will use for testing",
        "Timezone": "Europe/London"
    }

<table>
    <tr>
        <th>Name</th>
        <td>The name for the new account</td>
    </tr>
    <tr>
        <th>Description</th>
        <td>Optional, a description for the account</td>
    </tr>
    <tr>
        <th>Timezone</th>
        <td>Timezone of the account as found in the "TZ database name" column of this  <a href='https://en.wikipedia.org/wiki/List_of_tz_database_time_zones'>IANA Timezone list</a></td>
    </tr>
</table>

Response:

    200 OK
    {
        "Id": "00000000-0000-0000-0000-000000000000",
        "Name": "Test account 001",
        "Description": "An account we will use for testing",
        "AuditInfo": null,
        "Timezone": "Europe/London",
        "CreatedDate": "2017-12-06T15:54:06.6440352Z"
    }

[How to Create a User](./create-account-user)
