---
layout: post
title: Business Logic
subtitle: Web Development
date: 2019-07-07
author: Jalever
header-img: img/home_bg_tree.png
catalog: true
tags:
  - Node.js
---
- [Overview](#overview)
- [Details and Example](#details-and-example)
    - [Detailed Example](#detailed-example)

## Overview
In Computer Software, <strong>Business Logic</strong> or <strong>Domain Logic</strong> is the part of the program that encodes the real-world <strong>Business Rules</strong> that determine how data can be created, stored, and changed. It is contrasted with the remainder of the software that might be concerned with lower-level details of managing a database or displaying the user interface, system infrastructure, or generally connecting various parts of the program.

## Details and Example
<strong>Business Logic</strong> should be distinguished from <strong>Business Rules</strong>.

<strong>Business Logic</strong> is the portion of an enterprise system which determines how data is transformed or calculated, and how it is routed to people or software (workflow).

<strong>Business Rules</strong> are formal expressions of <strong>Business Policy</strong>.

Anything that is a process or procedure is <strong>Business Logic</strong>, and anything that is neither a process nor a procedure is a <strong>Business Rule</strong>.

Welcoming a new visitor is a process (workflow) consisting of steps to be taken, whereas saying every new visitor must be welcomed is a <strong>Business Rule</strong>. Further, <strong>Business Logic</strong> is procedural whereas <strong>Business Rules</strong> are declarative.

#### Detailed Example
For example, an e-commerce website might allow visitors to <ins>add items to a shopping cart</ins>, <ins>specify a shipping address</ins>, and <ins>supply payment information</ins>. The <strong>Business Logic</strong> of the website might include a workflow such as:
- The sequence of events that happens during checkout, for example a Multi-page Form which first <ins>asks for the shipping address</ins>, then for the <ins>billing address</ins>, next page will <ins>contain the payment method</ins>, and last page will <ins>show congratulations</ins>.

There will be also <strong>Business Rules</strong> of the website:
- Adding an item more than once from the item Description Page increments the quantity for that item.
- Specific formats that the visitor's address, email address, and credit card information must follow.
- A specific communication protocol for talking to the credit card network

The web site software also contains other code which is not considered part of <strong>Business Logic</strong> nor business rules:
- Peripheral content not related to the core business data, such as the HTML that defines the colors, appearance, background image, and navigational structure of the site
- Generic error-handling code (e.g. which displays the HTTP Error Code 500 page)
- Initialization code that runs when the web server starts up the site, which sets up the system
- Monitoring infrastructure to make sure all the parts of the site are working properly (e.g. the billing system is available)
- Generic code for making network connections, transmitting objects to the database, parsing user input via HTTP POST events, etc.
