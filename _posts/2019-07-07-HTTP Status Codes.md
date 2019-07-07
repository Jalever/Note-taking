---
layout: post
title: HTTP Response Status Codes
subtitle: HTTP Learning Keynotes
date: 2019-07-07
author: Jalever
header-img: img/computer_network_bg_simple.png
catalog: true
tags:
  - Computer Network
---

- [Introduction](#introduction)
- [Overview](#overview)
- [Meaning](#meaning)
    - [1×× Informational](#1××-informational)
        - [100 Continue](#100-continue)
        - [101 Switching Protocols](#101-switching-protocols)
        - [102 Processing](#102-processing)
    - [2×× Success](#2××-success)
        - [200 OK](#200-ok)
        - [201 Created](#201-created)
        - [202 Accepted](#202-accepted)
        - [203 Non-Authoritative Information](#203-non-authoritative-information)
        - [204 No Content](#204-no-content)
        - [205 Reset Content](#205-reset-content)
        - [206 Partial Content](#206-partial-content)
        - [207 Multi-Status](#207-multi-status)
        - [208 Already Reported](#208-already-reported)
    - [3×× Redirection](#3××-redirection)
        - [300 Multiple Choices](#300-multiple-choices)
        - [301 Moved Permanently](#301-moved-permanently)
        - [302 Found](#302-found)
        - [303 See Other](#303-see-other)
        - [304 Not Modified](#304-not-modified)
        - [305 Use Proxy](#305-use-proxy)
        - [307 Temporary Redirect](#307-temporary-redirect)
        - [308 Permanent Redirect](#308-permanent-redirect)
    - [4×× Client Error](#4××-client-error)
        - [402 Payment Required](#402-payment-required)
    - [5×× Server Error](#5××-server-error)

## Introduction
HTTP Response Status Codes indicate whether a specific HTTP request has been successfully completed.

Responses are grouped in five classes:
- informational responses
- successful responses
- redirects
- client errors
- servers errors

## Overview
<table>
    <thead>
        <tr>
            <td>Status Code</td>
            <td>Definition</td>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td colspan="2">1×× Informational</td>
        </tr>
        <tr>
            <td>100</td>
            <td>Continue</td>
        </tr>
        <tr>
            <td>101</td>
            <td>Switching Protocols</td>
        </tr>
        <tr>
            <td>102</td>
            <td>Processing</td>
        </tr>
        <tr>
            <td colspan="2">2×× Success</td>
        </tr>
        <tr>
            <td>200</td>
            <td>OK</td>
        </tr>
        <tr>
            <td>201</td>
            <td>Created</td>
        </tr>
        <tr>
            <td>202</td>
            <td>Accepted</td>
        </tr>
        <tr>
            <td>203</td>
            <td>Non-authoritative Information</td>
        </tr>
        <tr>
            <td>204</td>
            <td>No Content</td>
        </tr>
        <tr>
            <td>205</td>
            <td>Reset Content</td>
        </tr>
        <tr>
            <td>206</td>
            <td>Partial Content</td>
        </tr>
        <tr>
            <td>207</td>
            <td>Multi-Status</td>
        </tr>
        <tr>
            <td>208</td>
            <td>Already Reported</td>
        </tr>
        <tr>
            <td>226</td>
            <td>IM Used</td>
        </tr>
        <tr>
            <td colspan="2">3×× Redirection</td>
        </tr>
        <tr>
            <td>300</td>
            <td>Multiple Choices</td>
        </tr>
        <tr>
            <td>301</td>
            <td>Moved Permanently</td>
        </tr>
        <tr>
            <td>302</td>
            <td>Found</td>
        </tr>
        <tr>
            <td>303</td>
            <td>See Other</td>
        </tr>
        <tr>
            <td>304</td>
            <td>Not Modified</td>
        </tr>
        <tr>
            <td>305</td>
            <td>Use Proxy</td>
        </tr>
        <tr>
            <td>307</td>
            <td>Temporary Redirect</td>
        </tr>
        <tr>
            <td>308</td>
            <td>Permanent Redirect</td>
        </tr>
        <tr>
            <td colspan="2">4×× Client Error</td>
        </tr>
        <tr>
            <td>400</td>
            <td>Bad Request</td>
        </tr>
        <tr>
            <td>401</td>
            <td>Unauthorized</td>
        </tr>
        <tr>
            <td>402</td>
            <td>Payment Required</td>
        </tr>
        <tr>
            <td>403</td>
            <td>Forbidden</td>
        </tr>
        <tr>
            <td>404</td>
            <td>Not Found</td>
        </tr>
        <tr>
            <td>405</td>
            <td>Method Not Allowed</td>
        </tr>
        <tr>
            <td>406</td>
            <td>Not Acceptable</td>
        </tr>
        <tr>
            <td colspan="2">5×× Server Error</td>
        </tr>
        <tr>
            <td>500</td>
            <td>Internal Server Error</td>
        </tr>
    </tbody>
</table>

## Meaning
#### 1×× Informational
###### 100 Continue
The initial part of a request has been received and has not yet been rejected by the server. The server intends to send a final response after the request has been fully received and acted upon.

###### 101 Switching Protocols
The server understands and is willing to comply with the client's request, via the Upgrade header field, for a change in the application protocol being used on this connection.

###### 102 Processing
An interim response used to inform the client that the server has accepted the complete request, but has not yet completed it.

#### 2×× Success
###### 200 OK
The request has succeeded

###### 201 Created
The request has been fulfilled and has resulted in one or more new resources being created

###### 202 Accepted
The request has been accepted for processing, but the processing has not been completed. The request might or might not eventually be acted upon, as it might be disallowed when processing actually takes place

###### 203 Non-Authoritative Information
The request was successful but the enclosed payload has been modified from that of the origin server's 200 OK response by a transforming proxy

###### 204 No Content
The server has successfully fulfilled the request and that there is no additional content to send in the response payload body

###### 205 Reset Content
The server has fulfilled the request and desires that the user agent reset the "document view", which caused the request to be sent, to its original state as received from the origin server

###### 206 Partial Content
The server has fulfilled the request and desires that the user agent reset the "document view", which caused the request to be sent, to its original state as received from the origin server

###### 207 Multi-Status
A Multi-Status response conveys information about multiple resources in situations where multiple status codes might be appropriate

###### 208 Already Reported
Used inside a DAV: propstat response element to avoid enumerating the internal members of multiple bindings to the same collection repeatedly

#### 3×× Redirection
###### 300 Multiple Choices
The target resource has more than one representation, each with its own more specific identifier, and information about the alternatives is being provided so that the user (or user agent) can select a preferred representation by redirecting its request to one or more of those identifiers

###### 301 Moved Permanently
Used inside a DAV: propstat response element to avoid enumerating the internal members of multiple bindings to the same collection repeatedly

###### 302 Found
The target resource resides temporarily under a different URI. Since the redirection might be altered on occasion, the client ought to continue to use the effective request URI for future requests

###### 303 See Other
The server is redirecting the user agent to a different resource, as indicated by a URI in the Location header field, which is intended to provide an indirect response to the original request

###### 304 Not Modified
A conditional GET or HEAD request has been received and would have resulted in a 200 OK response if it were not for the fact that the condition evaluated to false.

###### 305 Use Proxy
Defined in a previous version of this specification and is now deprecated, due to security concerns regarding in-band configuration of a proxy

###### 307 Temporary Redirect
The target resource resides temporarily under a different URI and the user agent MUST NOT change the request method if it performs an automatic redirection to that URI

###### 308 Permanent Redirect
The target resource has been assigned a new permanent URI and any future references to this resource ought to use one of the enclosed URIs

#### 4×× Client Error
###### 402 Payment Required
Reserved for future use.

#### 5×× Server Error
###### 500 Internal Server Error
The server encountered an unexpected condition that prevented it from fulfilling the request.
