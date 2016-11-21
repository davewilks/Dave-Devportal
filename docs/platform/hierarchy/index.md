---
heading: Hierarchy
seo: Hierarchy Overview | Organization Structure | Account Structure
title: Hierarchy
description: Understand Cloud Elements Account Structure
layout: docs
platform: hierarchy
breadcrumbs: /docs/platform/platform-docs.html
parent: Back to Platform Docs
order: 1
sitemap: false
---

## Signing Up

When you sign up for an account with Cloud Elements you are automatically given an Organization and an Account within that organization. Your user account will be the Admin and owner of that Organization.  

Below an Organization, there are Accounts and Users under Accounts.  

![Hierarchy](/assets/img/hierarchy-2.png)

### Inheritance

Every user of Cloud Elements will be owned by an Account, and each Account by an Organization.  
The different Objects of Cloud Elements like: Transformations, Object Definitions, Elements and Formulas can be shared throughout an organization using this hierarchy.  

### Starting Structure  

When you sign up, we will create an Organization, Account, and User for you.
![Default Account](https://cl.ly/1A0T3t011D0n/Image%202016-11-17%20at%2011.28.38%20AM.png)

This default account will be the parent Organization account, and your admin user will live in this account. With this admin user. You will be able to create new accounts and new users within those accounts inside your organization.  

## How to use

As a SAAS provider, you will have a variety of customers. Lets say you have a customer "Best Buy." Best Buy has hundreds of users that will use your integrations. You can create a new Account in Cloud Elements that will represent "Best Buy." Then create a user/s in that Sub Account. Then create instances for those sub users.  

Because you have all Best Buy instances in a Sub Account, you can create Elements, Transformations, and Formulas that will only be inherited by your Best Buy customer.

> **PROTIP:** This is an optional feature. You can just as well create all of your customers instances in a single account. It is recommended to use this only if you have a reason to leverage the inheritance of different Cloud Elements objects.
