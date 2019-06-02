---
layout: post
title: 21 Performance Optimization Techniques for React Apps
subtitle: Web Development学习笔记系列
date: 2019-06-02T00:00:00.000Z
author: Jalever
header-img: img/post-bg-js-version.jpg
catalog: true
tags:
  - Performance
---

- [Memoize React Components](#Memoize React Components)
- [Using Web Workers for CPU Extensive Tasks](#Using Web Workers for CPU Extensive Tasks)
- [Consider Server-side Rendering](#Consider Server-side Rendering)

## Using Immutable Data Structures

## Function/Stateless Components and React.PureComponent

## Multiple Chunk Files

## Using Production Mode Flag in Webpack

## Dependency optimization

## Use React.Fragments to Avoid Additional HTML Element Wrappers

## Avoid Inline Function Definition in the Render Function

## Throttling and Debouncing Event Action in JavaScript

## Avoid using Index as Key for map

## Avoiding Props in Initial States

## Spreading props on DOM elements

## Use Reselect in Redux Connect to Avoid Frequent Re-render

## Avoid Async Initialization in componentWillMount()

## Memoize React Components

Memoization is an optimization technique used primarily to speed up computer programs by storing the results of expensive function calls and returning the cached result when the same inputs occur again. A memoized function is usually faster because if the function is called with the same values as the previous one then instead of executing function logic it would fetch the result from cache.

```javascript
const UserDetails = ({user, onEdit}) =>{
    const {title, full_name, profile_img} = user;

    return (
        <div className="user-detail-wrapper">
            <img src={profile_img} />
            <h4>{full_name}</h4>
            <p>{title}</p>
        </div>
    )
}

export default React.memo(UserDetails)
```

## CSS Animations Instead of JS Animations

## Using a CDN

## Using Web Workers for CPU Extensive Tasks

Web Workers makes it possible to run a script operation in a web application's background thread, separate from the main execution thread. By performing the laborious processing in a separate thread, the main thread, which is usually the UI, is able to run without being blocked or slowed down.

Web Workers works best when executing computation extensive operation since it executes code independent of other scripts in a separate thread in the background. This means it doesn't affect the page's performance.

Sort Service for sort post by the number of comments:

```javascript
function sort(posts) {
    for (let index = 0, len = posts.length - 1; index < len; index++) {
        for (let count = index+1; count < posts.length; count++) {
            if (posts[index].commentCount > posts[count].commentCount) {
                const temp = posts[index];
                posts[index] = users[count];
                posts[count] = temp;
            }
        }
    }
    return posts;
}

export default Posts extends React.Component{

    constructor(props){
        super(posts);
    }

    state = {
        posts: this.props.posts
    }

    doSortingByComment = () => {
        if(this.state.posts && this.state.posts.length){
            const sortedPosts = sort(this.state.posts);
            this.setState({
                posts: sortedPosts
            });
        }
    }

    render(){
        const posts = this.state.posts;
        return (
            <React.Fragment>
                <Button onClick={this.doSortingByComment}>
                    Sort By Comments
                </Button>
                <PostList posts={posts}></PostList>
            </React.Fragment>
        )
    }
}
```

`sort.worker.js`:

```javascript
export default  function sort() {

    self.addEventListener('message', e =>{
        if (!e) return;
        let posts = e.data;

        for (let index = 0, len = posts.length - 1; index < len; index++) {
            for (let count = index+1; count < posts.length; count++) {
                if (posts[index].commentCount > posts[count].commentCount) {
                    const temp = posts[index];
                    posts[index] = users[count];
                    posts[count] = temp;
                }
            }
        }
        postMessage(posts);
    });
}
```

```javascript
export default Posts extends React.Component{

    constructor(props){
        super(posts);
    }
    state = {
        posts: this.props.posts
    }
    componentDidMount() {
        this.worker = new Worker('sort.worker.js');

        this.worker.addEventListener('message', event => {
            const sortedPosts = event.data;
            this.setState({
                posts: sortedPosts
            })
        });
    }

    doSortingByComment = () => {
        if(this.state.posts && this.state.posts.length){
            this.worker.postMessage(this.state.posts);
        }
    }

    render(){
        const posts = this.state.posts;
        return (
            <React.Fragment>
                <Button onClick={this.doSortingByComment}>
                    Sort By Comments
                </Button>
                <PostList posts={posts}></PostList>
            </React.Fragment>
        )
    }
}
```

## Virtualize Long Lists

## Analyzing and Optimizing Your Webpack Bundle Bloat

## Consider Server-side Rendering

## Enable Gzip Compression on Web Server
