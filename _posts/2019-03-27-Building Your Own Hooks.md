---
layout: post
title: Building Your Own Hooks
subtitle: React Hooks学习笔记系列
date: 2019-03-27
author: Jalever
header-img: img/post_2019_react_bg_shadow.jpg
catalog: true
tags:
  - React
  - React Hooks
---

When we were learning about using the Effect Hook, we saw this component from a chat application that displays a message indicating whether a friend is online or offline:

```javascript
import React, { useState, useEffect } from "react";

function FriendStatus(props) {
  const [isOnline, setIsOnline] = useState(null);

  useEffect(() => {
    function handleStatusChange(status) {
      setIsOnline(status.isOnline);
    }

    ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
    return () => {
      ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
    };
  });

  if (isOnline === null) {
    return "Loading...";
  }
  return isOnline ? "Online" : "Offline";
}
```

Now let’s say that our chat application also has a contact list, and we want to render names of online users with a green color.<br>
We could copy and paste similar logic above into our `FriendListItem` component but it wouldn’t be ideal:

```javascript
import React, { useState, useEffect } from "react";

function FriendListItem(props) {
  const [isOnline, setIsOnline] = useState(null);

  useEffect(() => {
    function handleStatusChange(status) {
      setIsOnline(status.isOnline);
    }

    ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
    return () => {
      ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
    };
  });

  return (
    <li style={{ color: isOnline ? "green" : "black" }}>{props.friend.name}</li>
  );
}
```

Traditionally in `React`, we’ve had two popular ways to share stateful logic between components: `render props` and `higher-order components`.

- [Extracting a Custom Hook](#extracting-a-custom-hook)
- [Using a Custom Hook](#using-a-custom-hook)
    - [Is this code equivalent to the original examples?](#is-this-code-equivalent-to-the-original-examples)
    - [Do I have to name my custom Hooks starting with “use”?](#do-i-have-to-name-my-custom-hooks-starting-with-use)
    - [Do two components using the same Hook share state?](#do-two-components-using-the-same-hook-share-state)
    - [How does a custom Hook get isolated state?](#how-does-a-custom-hook-get-isolated-state)
- [useYourImagination()](#useyourimagination)

## Extracting a Custom Hook

There’s nothing new inside of it — the logic is copied from the components above.
The purpose of our `useFriendStatus` Hook is to subscribe us to a friend’s status. This is why it takes `friendID` as an argument, and returns whether this friend is online:

```javascript
function useFriendStatus(friendID) {
  const [isOnline, setIsOnline] = useState(null);

  // ...

  return isOnline;
}
```

## Using a Custom Hook

we’ve extracted this logic to a `useFriendStatus` hook, we can just use it:

```javascript
function FriendStatus(props) {
  const isOnline = useFriendStatus(props.friend.id);

  if (isOnline === null) {
    return "Loading...";
  }
  return isOnline ? "Online" : "Offline";
}
```

or

```javascript
function FriendListItem(props) {
  const isOnline = useFriendStatus(props.friend.id);

  return (
    <li style={{ color: isOnline ? "green" : "black" }}>{props.friend.name}</li>
  );
}
```

#### Is this code equivalent to the original examples?
Yes, it works in exactly the same way.<br>
`Custom Hooks` are a convention that naturally follows from the design of `Hooks`, rather than a `React` feature.

#### Do I have to name my custom Hooks starting with “use”?
Please do.<br>
Without it, we wouldn’t be able to automatically check for violations of rules of `Hooks` because we couldn’t tell if a certain function contains calls to Hooks inside of it.

#### Do two components using the same Hook share state?
No. <br>
All state and effects inside of `Hooks` are fully isolated.

#### How does a custom Hook get isolated state?
Each call to a `Hook` gets isolated state.<br>
We can call `useState` and `useEffect` many times in one component, and they will be completely independent. 

## useYourImagination()
You can write `custom Hooks` that cover a wide range of use cases like `form handling`, `animation`, `declarative subscriptions`, `timers`, and probably many more we haven’t considered.<br>