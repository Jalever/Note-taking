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

- [Router](#router)
    - [BrowserRouter](#browserrouter)
        - [getUserConfirmation](#getuserconfirmation)
        - [forceRefresh](#forcerefresh)
        - [keyLength](#keylength)
        - [children](#children)
        - [basename](#basename)
        - [basename](#basename)
    - [HashRouter](#hashrouter)
        - [basename](#basename)
        - [getUserConfirmation](#getuserconfirmation)
        - [hashType](#hashtype)
        - [children](#children)
    - [MemoryRouter](#memoryrouter)
        - [initialEntries](#initialentries)
        - [initialIndex](#initialindex)
        - [getUserConfirmation](#getuserconfirmation)
        - [keyLength](#keylength)
        - [children](#children)
    - [StaticRouter](#staticrouter)
        - [basename](#basename)
        - [location](#location)
        - [location](#location)
        - [context](#context)
        - [children](#children)
- [Switch](#switch)
    - [location](#location)
    - [children](#children)
- [Link](#Link)
    - [to](#to)
    - [to](#to)
    - [to](#to)
    - [replace](#replace)
    - [innerRef](#innerRef)
    - [innerRef](#innerRef)
- [Route](#route)
    - [Route render methods](#route-render-methods)
        - [Route component](#route-component)
        - [Route render](#route-render)
        - [Route children](#route-children)
    - [Route props](#route-props)
        - [match](#match)
        - [location](#location)
        - [history](#history)
    - [path](#path)
    - [exact](#exact)
    - [strict](#strict)
    - [sensitive](#sensitive)

## Router
The common low-level interface for all router components. Typically apps will use one of the high-level routers instead:
- &lt;BrowserRouter&gt;
- &lt;HashRouter&gt;
- &lt;MemoryRouter&gt;
- &lt;NativeRouter&gt;
- &lt;StaticRouter&gt;

The most common use-case for using the low-level &lt;Router&gt; is to synchronize a custom history with a state management lib like `Redux` or `Mobx`. Note that this is not required to use state management libs alongside `React Router`, it’s only for deep integration.
![egCNz8.png](https://s2.ax1x.com/2019/08/05/egCNz8.png)

<strong>history</strong><br/>
data type: <strong>object</strong>

A <strong>history</strong> object to use for navigation.
![egCfL4.png](https://s2.ax1x.com/2019/08/05/egCfL4.png)

<strong>children</strong><br/>
data type: <strong>node</strong>

A single child element to render.
![egC5w9.png](https://s2.ax1x.com/2019/08/05/egC5w9.png)

#### &lt;BrowserRouter&gt;
A &lt;Router&gt; that uses the HTML5 history API (pushState, replaceState and the popstate event) to keep your UI in sync with the URL.
![egCzTA.png](https://s2.ax1x.com/2019/08/05/egCzTA.png)

###### basename
data type: <strong>string</strong>

The base URL for all locations. If your app is served from a sub-directory on your server, you’ll want to set this to the sub-directory. A properly formatted basename should have a leading slash, but no trailing slash.
![egPnkn.png](https://s2.ax1x.com/2019/08/05/egPnkn.png)

###### getUserConfirmation
data type: <strong>func</strong>

A function to use to confirm navigation. Defaults to using `window.confirm`.
![egPY79.png](https://s2.ax1x.com/2019/08/05/egPY79.png)

###### forceRefresh
data type: <strong>bool</strong>

If true the router will use full page refreshes on page navigation. You probably only want this in browsers that don’t support the HTML5 history API.
![egPB6O.png](https://s2.ax1x.com/2019/08/05/egPB6O.png)

###### keyLength
data type: <strong>number</strong>

The length of `location.key`. Defaults to 6.
![egPbAs.png](https://s2.ax1x.com/2019/08/05/egPbAs.png)

###### children
data type: <strong>node</strong>

A single child element to render.

#### &lt;HashRouter&gt;
A &lt;Router&gt; that uses the hash portion of the URL (i.e. `window.location.hash`) to keep your UI in sync with the URL.  
> Hash history does not support `location.key` or `location.state`.

![egFkZQ.png](https://s2.ax1x.com/2019/08/05/egFkZQ.png)

###### basename
data type: <strong>string</strong>

The base URL for all locations. A properly formatted basename should have a leading slash, but no trailing slash.
![egF8o9.png](https://s2.ax1x.com/2019/08/05/egF8o9.png)

###### getUserConfirmation
data type: <strong>func</strong>

A function to use to confirm navigation. Defaults to using `window.confirm`.
![egFyFA.png](https://s2.ax1x.com/2019/08/05/egFyFA.png)

###### hashType
data type: <strong>string</strong>

The type of encoding to use for `window.location.hash`. Available values are:
- <strong>slash</strong> - Creates hashes like `#/` and `#/sunshine/lollipops`
- <strong>noslash</strong> - Creates hashes like `#` and `#sunshine/lollipops`
- <strong>hashbang</strong> - Creates `ajax crawlable`(deprecated by Google) hashes like `#!/` and `#!/sunshine/lollipops`

Defaults to <strong>slash</strong>.

###### children
data type: <strong>node</strong>

A single child element to render.

#### &lt;MemoryRouter&gt;
A &lt;Router&gt; that keeps the history of your “URL” in memory (does not read or write to the address bar). Useful in tests and non-browser environments like `React Native`.
![egmCfH.png](https://s2.ax1x.com/2019/08/05/egmCfH.png)

###### initialEntries
data type: <strong>array</strong>

An array of <strong>locations</strong> in the history stack. These may be full-blown location objects with `{ pathname, search, hash, state }` or simple string URLs.
![egmutg.png](https://s2.ax1x.com/2019/08/05/egmutg.png)

###### initialIndex
data type: <strong>number</strong>

The initial location’s index in the array of <strong>initialEntries</strong>.

###### getUserConfirmation
data type: <strong>func</strong>

A function to use to confirm navigation. You must use this option when using &lt;MemoryRouter&gt; directly with a &lt;Prompt&gt;.

###### keyLength
data type: <strong>number</strong>

The length of <strong>location.key</strong>. Defaults to 6.
![egmah4.png](https://s2.ax1x.com/2019/08/05/egmah4.png)

###### children
data type: <strong>node</strong>

A single child element to render.

#### &lt;StaticRouter&gt;
A &lt;Router&gt; that never changes location.

This can be useful in server-side rendering scenarios when the user isn’t actually clicking around, so the location never actually changes. Hence, the name: static. It’s also useful in simple tests when you just need to plug in a location and make assertions on the render output.

Here’s an example node server that sends a 302 status code for <strong>&lt;Redirect&gt;</strong>s and regular HTML for other requests:
![egnzJe.png](https://s2.ax1x.com/2019/08/05/egnzJe.png)
![eguSRH.png](https://s2.ax1x.com/2019/08/05/eguSRH.png)

###### basename
data type: <strong>string</strong>

The base URL for all locations. A properly formatted basename should have a leading slash, but no trailing slash.
![egu50P.png](https://s2.ax1x.com/2019/08/05/egu50P.png)

###### location
data type: <strong>string</strong>

The URL the server received, probably `req.url` on a node server.
![egKip4.png](https://s2.ax1x.com/2019/08/05/egKip4.png)

###### location
data type: <strong>object</strong>

A location object shaped like `{ pathname, search, hash, state }`
![egKKhD.png](https://s2.ax1x.com/2019/08/05/egKKhD.png)

###### context
data type: <strong>object</strong>

A plain JavaScript object. During the render, components can add properties to the object to store information about the render.
![egKa4S.png](https://s2.ax1x.com/2019/08/05/egKa4S.png)
When a &lt;Route&gt; matches, it will pass the context object to the component it renders as the `staticContext` prop.

After the render, these properties can be used to to configure the server’s response.
![egKbE6.png](https://s2.ax1x.com/2019/08/05/egKbE6.png)

###### children
data type: <strong>node</strong>  

A single child element to render.

---------------------------------------------------------------------------------------

## Switch
Renders the first child &lt;Route&gt; or &lt;Redirect&gt; that matches the location.

&lt;Switch&gt; is unique in that it renders a route exclusively. In contrast, every &lt;Route&gt; that matches the location renders inclusively. Consider this code:
![eg8i9K.png](https://s2.ax1x.com/2019/08/05/eg8i9K.png)
If the URL is `/about`, then &lt;About&gt;, &lt;User&gt;, and &lt;NoMatch&gt; will all render because they all match the path. This is by design, allowing us to compose &lt;Route&gt;s into our apps in many ways, like sidebars and breadcrumbs, bootstrap tabs, etc.

Occasionally, however, we want to pick only one &lt;Route&gt; to render. If we’re at `/about` we don’t want to also match `/:user` (or show our “404” page). Here’s how to do it with Switch:
![eg8VnH.png](https://s2.ax1x.com/2019/08/05/eg8VnH.png)
Now, if we’re at `/about`, &lt;Switch&gt; will start looking for a matching &lt;Route&gt;. <strong>&lt;Route path="/about"/&gt;</strong> will match and &lt;Switch&gt; will stop looking for matches and render &lt;About&gt;. Similarly, if we’re at `/michael` then &lt;User&gt; will render.

This is also useful for animated transitions since the matched &lt;Route&gt; is rendered in the same position as the previous one.
![eg8R4x.png](https://s2.ax1x.com/2019/08/05/eg8R4x.png)

#### location
data type: <strong>object</strong>

A <strong>location</strong> object to be used for matching children elements instead of the current history location (usually the current browser URL).

#### children
data type: <strong>node</strong>

All children of a <strong>&lt;Switch&gt;</strong> should be <strong>&lt;Route&gt;</strong> or <strong>&lt;Redirect&gt;</strong> elements. Only the first child to match the current location will be rendered.

<strong>&lt;Route&gt;</strong> elements are matched using their <strong>path</strong> prop and <strong>&lt;Redirect&gt;</strong> elements are matched using their <strong>from</strong> prop. A <strong>&lt;Route&gt;</strong> with no <strong>path</strong> prop or a <strong>&lt;Redirect&gt;</strong> with no <strong>from</strong> prop will always match the current location.

When you include a <strong>&lt;Redirect&gt;</strong> in a <strong>&lt;Switch&gt;</strong>, it can use any of the <strong>&lt;Route&gt;</strong>'s location matching props: <ins>path</ins>, <ins>exact</ins>, and <ins>strict</ins>. <strong>from</strong> is just an alias for the <strong>path</strong> prop.

If a <strong>location</strong> prop is given to the <strong>&lt;Switch&gt;</strong>, it will override the <strong>location</strong> prop on the matching child element.
---------------------------------------------------------------------------------------
## Link
Provides declarative, accessible navigation around your application.
![egadeS.png](https://s2.ax1x.com/2019/08/05/egadeS.png)

#### to
data type: <strong>string</strong>

A string representation of the Link location, created by concatenating the location’s pathname, search, and hash properties.
![egasWn.png](https://s2.ax1x.com/2019/08/05/egasWn.png)

#### to
data type: <strong>object</strong>

An object that can have any of the following properties:
- <strong>pathname</strong>: A string representing the path to link to.
- <strong>search</strong>: A string representation of query parameters.
- <strong>hash</strong>: A hash to put in the URL, e.g. #a-hash.
- <strong>state</strong>: State to persist to the location.

![egdP6P.png](https://s2.ax1x.com/2019/08/05/egdP6P.png)

#### to
data type: <strong>function</strong>

A function to which current location is passed as an argument and which should return location representation as a string or as an object
![egdq9s.png](https://s2.ax1x.com/2019/08/05/egdq9s.png)

#### replace
data type: <strong>bool</strong>

When <strong>true</strong>, clicking the link will replace the current entry in the history stack instead of adding a new one.
![egwZDK.png](https://s2.ax1x.com/2019/08/05/egwZDK.png)

#### innerRef
data type: <strong>function</strong>

Allows access to the underlying <strong>ref</strong> of the component
![egwB2n.png](https://s2.ax1x.com/2019/08/05/egwB2n.png)

#### innerRef
data type: <strong>RefObject</strong>

Get the underlying <strong>ref</strong> of the component with React.createRef()
![egw2aF.png](https://s2.ax1x.com/2019/08/05/egw2aF.png)


---------------------------------------------------------------------------------------
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
When you use <strong>component</strong> (instead of <strong>render</strong> or <strong>children</strong>) the router uses <strong>React.createElement</strong> to create a new <strong>React element</strong> from the given component. That means if you provide an inline function to the <strong>component</strong> prop, you would create a new component every render. This results in the existing component unmounting and the new component mounting instead of just updating the existing component. When using an inline function for inline rendering, use the <strong>render</strong> or the <strong>children</strong> prop.

###### &lt;Route render&gt;
This allows for convenient inline rendering and wrapping without the undesired remounting explained above.

Instead of having a new <strong>React element</strong> created for you using the <strong>component</strong> prop, you can pass in a function to be called when the location matches. The <strong>render</strong> prop function has access to all the same <strong>route props</strong> (<strong>match</strong>, <strong>location</strong> and <strong>history</strong>) as the component render prop.
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

###### location
Locations represent where the app is now, where you want it to go, or even where it was. It looks like this:
![er4Dk6.png](https://s2.ax1x.com/2019/08/03/er4Dk6.png)
The router will provide you with a location object in a few places:
- <strong>Route component</strong> as `this.props.location`
- <strong>Route render</strong> as `({ location }) => ()`
- <strong>Route children</strong> as `({ location }) => ()`
- <strong>withRouter</strong> as `this.props.location`

It is also found on <strong>history.location</strong> but you shouldn’t use that because its mutable. You can read more about that in the <strong>history</strong> doc.

A location object is never mutated so you can use it in the lifecycle hooks to determine when navigation happens, this is really useful for data fetching and animation.
![er4XBn.png](https://s2.ax1x.com/2019/08/03/er4XBn.png)
You can provide locations instead of strings to the various places that navigate:
- Web Link to
- Native Link to
- Redirect to
- history.push
- history.replace

Normally you just use a string, but if you need to add some “location state” that will be available whenever the app returns to that specific location, you can use a location object instead. This is useful if you want to branch UI based on navigation history instead of just paths (like modals).
![er5eN6.png](https://s2.ax1x.com/2019/08/03/er5eN6.png)

Finally, you can pass a location to the following components:
- Route
- Switch

This will prevent them from using the actual location in the router’s state. This is useful for animation and pending navigation, or any time you want to trick a component into rendering at a different location than the real one.

###### history
The term “history” and "history object" in this documentation refers to <ins>the history package</ins>[a NPM Package], which is one of only 2 major dependencies of React Router (besides <strong>React</strong> itself), and which provides several different implementations for managing session history in JavaScript in various environments.

The following terms are also used:
- <strong>browser history</strong> - A DOM-specific implementation, useful in web browsers that support the HTML5 history API
- <strong>hash history</strong> - A DOM-specific implementation for legacy web browsers
- <strong>memory history</strong> - An in-memory history implementation, useful in testing and non-DOM environments like React Native

history objects typically have the following properties and methods:

- <strong>length</strong> - (number) The number of entries in the history stack
- <strong>action</strong> - (string) The current action (PUSH, REPLACE, or POP)
- <strong>location</strong> - (object) The current location. May have the following properties:
- <strong>pathname</strong> - (string) The path of the URL
- <strong>search</strong> - (string) The URL query string
- <strong>hash</strong> - (string) The URL hash fragment
- <strong>state</strong> - (object) location-specific state that was provided to e.g. push(path, state) when this location was pushed onto the stack. Only available in browser and memory history.
- <strong>push(path, [state])</strong> - (function) Pushes a new entry onto the history stack
- <strong>replace(path, [state])</strong> - (function) Replaces the current entry on the history stack
- <strong>go(n)</strong> - (function) Moves the pointer in the history stack by n entries
- <strong>goBack()</strong> - (function) Equivalent to go(-1)
- <strong>goForward()</strong> - (function) Equivalent to go(1)
- <strong>block(prompt)</strong> - (function) Prevents navigation

<strong>history is mutable.</strong>

The <strong>history</strong> object is mutable. Therefore it is recommended to access the <strong>location</strong> from the render props of &lt;Route&gt;, not from <strong>history.location</strong>. This ensures your assumptions about React are correct in lifecycle hooks. For example:
![er5O2D.png](https://s2.ax1x.com/2019/08/03/er5O2D.png)

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

> <strong>strict</strong> can be used to enforce that a <strong>location.pathname</strong> has no trailing slash, but in order to do this both <strong>strict</strong> and <strong>exact</strong> must be true.

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

When <strong>true</strong>, will match if the path is <strong>case sensitive</strong>.
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
