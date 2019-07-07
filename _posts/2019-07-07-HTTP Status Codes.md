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
