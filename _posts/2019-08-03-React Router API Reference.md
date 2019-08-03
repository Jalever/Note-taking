---
layout: post
title: (React Router)Getting started with React Router
subtitle: React Router API Reference
date: 2019-08-03
author: Jalever
header-img: img/post_2019_react_bg_shadow.jpg
catalog: true
tags:
  - React
---

## Route
The Route component is perhaps the most important component in React Router to understand and learn to use well. Its most basic responsibility is to render some UI when a location matches the route’s path.

Consider the following code:
![eD2fSA.png](https://s2.ax1x.com/2019/08/03/eD2fSA.png)
If the location of the app is `/` then the UI hierarchy will be something like:
![eD2hQI.png](https://s2.ax1x.com/2019/08/03/eD2hQI.png)
And if the location of the app is `/news` then the UI hierarchy will be:
![eDRElR.png](https://s2.ax1x.com/2019/08/03/eDRElR.png)

#### Route render methods
There are 3 ways to render something with a <Route>:
- &lt;Route component&gt;
- &lt;Route render&gt;
- &lt;Route children&gt;

Each is useful in different circumstances. You should use only one of these props on a given <Route>.

###### &lt;Route component&gt;
A React component to render only when the location matches. It will be rendered with route props.
![eDWSgA.png](https://s2.ax1x.com/2019/08/03/eDWSgA.png)
When you use <strong>component (instead of <strong>render or <strong>children) the router uses <strong>React.createElement to create a new <strong>React element from the given component. That means if you provide an inline function to the <strong>component prop, you would create a new component every render. This results in the existing component unmounting and the new component mounting instead of just updating the existing component. When using an inline function for inline rendering, use the render or the children prop.

###### &lt;Route render&gt;
This allows for convenient inline rendering and wrapping without the undesired remounting explained above.

Instead of having a new <strong>React element created for you using the <strong>component</strong> prop, you can pass in a function to be called when the location matches. The render prop function has access to all the same <strong>route props</strong> (<strong>match</strong>, <strong>location</strong> and <strong>history</strong>) as the component render prop.
![eDfGeP.png](https://s2.ax1x.com/2019/08/03/eDfGeP.png)

> <strong>&lt;Route component&gt;</strong> takes precedence over <strong>&lt;Route render&gt;</strong> so don’t use both in the same &lt;Route&gt;.

###### &lt;Route children&gt;
Sometimes you need to render whether the path matches the location or not. In these cases, you can use the function <strong>children</strong> prop. It works exactly like <strong>render</strong> except that it gets called whether there is a match or not.

The <strong>children</strong> render prop receives all the same <strong>route props</strong> as the <strong>component</strong> and <strong>render</strong> methods, except when a route fails to match the URL, then <strong>match</strong> is <strong>null</strong>. This allows you to dynamically adjust your UI based on whether or not the route matches. Here we’re adding an active class if the route matches
![eDhp0P.png](https://s2.ax1x.com/2019/08/03/eDhp0P.png)
This could also be useful for animations:
![eD7FhV.png](https://s2.ax1x.com/2019/08/03/eD7FhV.png)

> Both <strong>&lt;Route component&gt;</strong> and <strong>&lt;Route render&gt;</strong> take precedence over <strong>&lt;Route children&gt;</strong> so don’t use more than one in the same <strong>&lt;Route&gt;</strong>.

#### Route props
All three <strong>render methods</strong> will be passed the same three route props
- match
- location
- history

###### match
A <strong>match</strong> object contains information about how a &lt;Route path&gt; matched the URL. <strong>match</strong> objects contain the following properties:
- <strong>params</strong> - (object) Key/value pairs parsed from the URL corresponding to the dynamic segments of the path
- <strong>isExact</strong> - (boolean) true if the entire URL was matched (no trailing characters)
- <strong>path</strong> - (string) The path pattern used to match. Useful for building nested <Route>s
- <strong>url</strong> - (string) The matched portion of the URL. Useful for building nested <Link>s

You’ll have access to match objects in various places:
- <strong>Route component</strong> as `this.props.match`
- <strong>Route render</strong> as `({ match }) => ()`
- <strong>Route children</strong> as `({ match }) => ()`
- <strong>withRouter</strong> as `this.props.match`
- <strong>matchPath</strong> as the return value

If a Route does not have a path, and therefore always matches, you’ll get the closest parent match. Same goes for <strong>withRouter</strong>.

<strong>null matches</strong><br/>
A &lt;Route&gt; that uses the children prop will call its children function even when the route’s path does not match the current location. When this is the case, the match will be null. Being able to render a &lt;Route&gt;'s contents when it does match can be useful, but certain challenges arise from this situation.

The default way to “resolve” URLs is to join the match.url string to the “relative” path.
![errP6f.png](https://s2.ax1x.com/2019/08/03/errP6f.png)

If you attempt to do this when the match is null, you will end up with a <strong>TypeError</strong>. This means that it is considered unsafe to attempt to join “relative” paths inside of a &lt;Route&gt; when using the children prop.

A similar, but more subtle situation occurs when you use a pathless <Route> inside of a &lt;Route&gt; that generates a null match object.
![err3BF.png](https://s2.ax1x.com/2019/08/03/err3BF.png)
Pathless &lt;Route&gt;s inherit their <strong>match</strong> object from their parent. If their parent match is <strong>null</strong>, then their match will also be <strong>null</strong>. This means that<br/>
a) any child routes/links will have to be absolute because there is no parent to resolve with and<br/>
b) a pathless route whose parent <strong>match</strong> can be <strong>null</strong> will need to use the <strong>children</strong> prop to render.

#### path
data type: `string` | `string[]`

Any valid URL path or array of paths that <strong>path-to-regexp@^1.7.0</strong> understands.
![eDbJwd.png](https://s2.ax1x.com/2019/08/03/eDbJwd.png)
Routes without a <strong>path</strong> always match.

#### exact
data type: `bool`

When true, will only match if the path matches the <strong>location.pathname</strong> exactly.
<table>
    <thead>
        <tr>
            <td>path</td>
            <td>location.pathname</td>
            <td>exact</td>
            <td>matches?</td>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>/one</td>
            <td>/one/two</td>
            <td>true</td>
            <td>no</td>
        </tr>
        <tr>
            <td>/one</td>
            <td>/one/two</td>
            <td>false</td>
            <td>yes</td>
        </tr>
    </tbody>
</table>

#### strict
data type: `bool`

When true, a path that has a trailing slash will only match a <strong>location.pathname</strong> with a trailing slash. This has no effect when there are additional URL segments in the <strong>location.pathname</strong>.
![eDLMrD.png](https://s2.ax1x.com/2019/08/03/eDLMrD.png)
<table>
    <thead>
        <tr>
            <td>path</td>
            <td>location.pathname</td>
            <td>matches?</td>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>/one</td>
            <td>/one</td>
            <td>no</td>
        </tr>
        <tr>
            <td>/one</td>
            <td>/one/</td>
            <td>yes</td>
        </tr>
        <tr>
            <td>/one</td>
            <td>/one/two</td>
            <td>yes</td>
        </tr>
    </tbody>
</table>

> <strong>strict can be used to enforce that a <strong>location.pathname has no trailing slash, but in order to do this both <strong>strict and <strong>exact must be true.

![eDLE5R.png](https://s2.ax1x.com/2019/08/03/eDLE5R.png)
<table>
    <thead>
        <tr>
            <td>path</td>
            <td>location.pathname</td>
            <td>matches?</td>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>/one</td>
            <td>/one</td>
            <td>yes</td>
        </tr>
        <tr>
            <td>/one</td>
            <td>/one/</td>
            <td>no</td>
        </tr>
        <tr>
            <td>/one</td>
            <td>/one/two</td>
            <td>no</td>
        </tr>
    </tbody>
</table>

#### sensitive
data type: `bool`

When <strong>true, will match if the path is <strong>case sensitive.
![eDLxdH.png](https://s2.ax1x.com/2019/08/03/eDLxdH.png)
<table>
    <thead>
        <tr>
            <td>path</td>
            <td>location.pathname</td>
            <td>sensitive</td>
            <td>matches?</td>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>/one</td>
            <td>/one</td>
            <td>true</td>
            <td>yes</td>
        </tr>
        <tr>
            <td>/One</td>
            <td>/one</td>
            <td>true</td>
            <td>no</td>
        </tr>
        <tr>
            <td>/One</td>
            <td>/one</td>
            <td>false</td>
            <td>no</td>
        </tr>
    </tbody>
</table>
