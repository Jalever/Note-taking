---
layout: post
title: Scroll Restoration
subtitle: React Router Guides学习笔记系列 5
date: 2019-04-10
author: Jalever
header-img: img/post_2019_react_bg_shadow.jpg
catalog: true
tags:
  - React
  - React Router
---


## Table of Contents
- [Table of Contents](#table-of-contents)
- [Scroll to Top](#scroll-to-top)




Most of the time all you need is to “scroll to the top” because you have a long content page, that when navigated to, stays scrolled down.
## Scroll to Top
`<ScrollToTop>` component that will scroll the window up on every navigation, make sure to wrap it in `withRouter` to give it access to the router’s props:
```javascript
content page, that when navigated to, stays scrolled down. This is straightforward to handle with a <ScrollToTop> component that will scroll the window up on every navigation, make sure to wrap it in withRouter to give it access to the router’s props:

class ScrollToTop extends Component {
  componentDidUpdate(prevProps) {
    if (this.props.location.pathname !== prevProps.location.pathname) {
      window.scrollTo(0, 0);
    }
  }

  render() {
    return this.props.children;
  }
}

export default withRouter(ScrollToTop);

```
Then render it at the top of your app, but below `Router`
```javascipt
function App() {
  return (
    <Router>
      <ScrollToTop>
        <App />
      </ScrollToTop>
    </Router>
  );
}
```
just render it bare anywhere you want, but just one
```javascript
<ScrollToTop />;
```
If you have a ***tab interface*** connected to the router, then you probably don’t want to be scrolling to the top when they switch tabs. 
```javascript
class ScrollToTopOnMount extends Component {
  componentDidMount() {
    window.scrollTo(0, 0);
  }

  render() {
    return null;
  }
}

class LongContent extends Component {
  render() {
    <div>
      <ScrollToTopOnMount />
      <h1>Here is my long content page</h1>
    </div>;
  }
}
```
somewhere else
```javascript
<Route path="/long-content" component={LongContent} />;

```

