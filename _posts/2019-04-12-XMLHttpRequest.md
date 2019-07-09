---
layout: post
title: XMLHttpRequest
subtitle: AJAX Tutorial
date: 2019-04-12
author: Jalever
header-img: img/post_2019_react_bg_shadow.jpg
catalog: true
tags:
  - AJAX
---

- [Constructor](#constructor)
- [Properties](#properties)
    - [XMLHttpRequest.onreadystatechange](#xmlhttprequestonreadystatechange)
    - [XMLHttpRequest.readyState](#xmlhttprequestreadystate)
    - [XMLHttpRequest.response](#xmlhttprequestresponse)
    - [XMLHttpRequest.responseText](#xmlhttprequestresponsetext)
    - [XMLHttpRequest.responseType](#xmlhttprequestresponsetype)
    - [XMLHttpRequest.responseURL](#xmlhttprequestresponseurl)
    - [XMLHttpRequest.responseXML](#xmlhttprequestresponsexml)
    - [XMLHttpRequest.status](#xmlhttprequeststatus)
    - [XMLHttpRequest.statusText](#xmlhttprequeststatustext)
    - [XMLHttpRequest.timeout](#xmlhttprequesttimeout)
    - [XMLHttpRequestEventTarget.ontimeout](#xmlhttprequesteventtargetontimeout)
    - [XMLHttpRequest.upload](#xmlhttprequestupload)
    - [XMLHttpRequest.withCredentials](#xmlhttprequestwithcredentials)
- [Non-standard Properites](#non-standard-properites)
    - [XMLHttpRequest.channel](#xmlhttprequestchannel)
    - [XMLHttpRequest.mozAnon](#xmlhttprequestmozanon)
    - [XMLHttpRequest.mozSystem](#xmlhttprequestmozsystem)
    - [XMLHttpRequest.mozBackgroundRequest](#xmlhttprequestmozbackgroundrequest)
- [Methods](#methods)
    - [XMLHttpRequest.abort()](#xmlhttprequestabort)
    - [XMLHttpRequest.getAllResponseHeaders()](#xmlhttprequestgetallresponseheaders)
    - [XMLHttpRequest.getResponseHeader()](#xmlhttprequestgetresponseheader)
    - [XMLHttpRequest.open()](#xmlhttprequestopen)
    - [XMLHttpRequest.overrideMimeType()](#xmlhttprequestoverridemimetype)
    - [XMLHttpRequest.send()](#xmlhttprequestsend)
    - [XMLHttpRequest.setRequestHeader()](#xmlhttprequestsetrequestheader)
- [Non-Standard Methods](#non-standard-methods)
    - [XMLHttpRequest.openRequest()](#xmlhttprequestopenrequest)
- [Events](#events)
    - [abort](#abort)
    - [error](#error)
    - [load](#load)
    - [loadend](#loadend)
    - [loadstart](#loadstart)
    - [progress](#progress)
    - [timeout](#timeout)
- [Return XHR](#return-xhr)

## Constructor
The constructor initializes an `XMLHttpRequest`.<br>
It must be called before any other method calls.
## Properties

#### XMLHttpRequest.onreadystatechange

    An `EventHandler` that is called whenever the `readyState` attribute changes.

#### XMLHttpRequest.readyState

    ***Read only***<br>
    Returns an `unsigned short`, the state of the request.<br>

#### XMLHttpRequest.response

    ***Read only***<br>
    Returns an `ArrayBuffer`, `Blob`, `Document`, `JavaScript object`, or a `DOMString`, depending on the value of `XMLHttpRequest.responseType`, that contains the response entity body.<br>

#### XMLHttpRequest.responseText

    ***Read only***<br>
    Returns a `DOMString` that contains the response to the request as text, or null if the request was unsuccessful or has not yet been sent.

#### XMLHttpRequest.responseType

    Is an enumerated value that defines the response type.

#### XMLHttpRequest.responseURL

    ***Read only***<br>
    Returns the serialized `URL` of the response or the empty string if the `URL` is null.

#### XMLHttpRequest.responseXML

    ***Read only***<br>
    Returns a Document containing the response to the request, or null if the request was unsuccessful, has not yet been sent, or cannot be parsed as `XML` or `HTML`. Not available in workers.

#### XMLHttpRequest.status

    ***Read only***<br>
    Returns an unsigned short with the status of the response of the request.

#### XMLHttpRequest.statusText

    ***Read only***<br>
    Returns a `DOMString` containing the response string returned by the `HTTP` server. <br>
    Unlike `XMLHttpRequest.status`, this includes the entire text of the response message ("200 OK", for example).

#### XMLHttpRequest.timeout

    Is an unsigned long representing the number of milliseconds a request can take before automatically being terminated.

#### XMLHttpRequestEventTarget.ontimeout

    Is an `EventHandler` that is called whenever the request times out.

#### XMLHttpRequest.upload

    ***Read only***<br>
    Is an `XMLHttpRequestUpload`, representing the upload process.

#### XMLHttpRequest.withCredentials

    Is a `Boolean` that indicates whether or not cross-site `Access-Control` requests should be made using credentials such as `cookies` or `authorization` headers.

## Non-standard Properites

#### XMLHttpRequest.channel

    ***Read only***<br>
    Is a `nsIChannel`. The channel used by the object when performing the request.<br>

#### XMLHttpRequest.mozAnon

    ***Read only***<br>
    Is a boolean. If true, the request will be sent without cookie and authentication headers.<br>

#### XMLHttpRequest.mozSystem

    ***Read only***<br>
    Is a boolean. If true, the same origin policy will not be enforced on the request.<br>

#### XMLHttpRequest.mozBackgroundRequest

    Is a boolean. It indicates whether or not the object represents a background service request.<br>

## Methods

#### XMLHttpRequest.abort()

    Aborts the request if it has already been sent.

#### XMLHttpRequest.getAllResponseHeaders()

    Returns all the response headers, separated by `CRLF`, as a string, or null if no response has been received.

#### XMLHttpRequest.getResponseHeader()

    Returns the string containing the text of the specified header, or null if either the response has not yet been received or the header doesn't exist in the response.

#### XMLHttpRequest.open()

    Initializes a request. This method is to be used from `JavaScript` code; to initialize a request from native code, use `openRequest()` instead.

#### XMLHttpRequest.overrideMimeType()

    Overrides the `MIME` type returned by the server.

#### XMLHttpRequest.send()

    Sends the request. If the request is asynchronous (which is the default), this method returns as soon as the request is sent.

#### XMLHttpRequest.setRequestHeader()

    Sets the value of an `HTTP` request header. You must call `setRequestHeader()` after `open()`, but before `send()`.

## Non-Standard Methods

#### XMLHttpRequest.openRequest()

    Initializes a request. <br>
    This method is to be used from native code; to initialize a request from `JavaScript` code, use `open()` instead. See the documentation for `open()`.

## Events

#### abort

    Fired when a request has been aborted, for example because the program called `XMLHttpRequest.abort()`.<br>
    Also available via the `onabort` property.

#### error

    Fired when the request encountered an error.<br>
    Also available via the `onerror` property.<br>

#### load

    Fired when an `XMLHttpRequest` transaction completes successfully.<br>
    Also available via the `onload` property.<br>

#### loadend

    Fired when a request has completed, whether successfully (after load) or unsuccessfully (after abort or error).<br>
    Also available via the onloadend property.

#### loadstart

    Fired when a request has started to load data.<br>
    Also available via the onloadstart property.

#### progress

    Fired periodically when a request receives more data.<br>
    Also available via the onprogress property.

#### timeout

    Fired when `Progression` is terminated due to preset time expiring.


## Return XHR
```javascript
onabort: null
onerror: null
onload: null
onloadend: null
onloadstart: null
onprogress: null
onreadystatechange: ƒ ()
ontimeout: null
readyState: 4
response: "....."
responseType: ""
responseURL: "http://47.106.132.253:8081/api/data"
responseXML: null
status: 200
statusText: "OK"
timeout: 0
upload: XMLHttpRequestUpload
onabort: null
onerror: null
onload: null
onloadend: null
onloadstart: null
onprogress: null
ontimeout: null
withCredentials: false
```
