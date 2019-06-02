---
layout: post
title: Strategy Pattern
subtitle: Design Pattern学习笔记系列
date: 2019-06-02
author: Jalever
header-img: img/home_bg_tree.png
catalog: true
tags:
  - Design Pattern
---

## Definition
In computer programming, the strategy pattern (also known as the policy pattern) is a software design pattern that enables an algorithm’s behavior to be selected at runtime. The strategy pattern
- defines a family of algorithms,
- encapsulates each algorithm, and
- makes the algorithms interchangeable within that family.

## Origins
Suppose we are building a game “Street Fighter”. For simplicity assume that a character may have four moves that is kick, punch, roll and jump. Every character has kick and punch moves, but roll and jump are optional. How would you model your classes? Suppose initially you use inheritance and abstract out the common features in a Fighter class and let other characters subclass Fighter class.

Fighter class will we have default implementation of normal actions. Any character with specialized move can override that action in its subclass.

What if a character doesn’t perform jump move? It still inherits the jump behavior from superclass. Although you can override jump to do nothing in that case but you may have to do so for many existing classes and take care of that for future classes too. This would also make maintenance difficult. So we can’t use inheritance here.

We took out some actions (which some characters might not perform) out of Fighterclass and made interfaces for them. That way only characters that are supposed to jump will implement the JumpBehavior.

The main problem with the above design is code reuse. Since there is no default implementation of jump and roll behavior we may have code duplicity. You may have to rewrite the same jump behavior over and over in many subclasses.

What if we made JumpBehavior and RollBehavior classes instead of interface? Well then we would have to use multiple inheritance that is not supported in many languages due to many problems associated with it.

Here strategy pattern comes to our rescue. We will learn what the strategy pattern is and then apply it to solve our problem.

## Summary
#### Advantages
1. A family of algorithms can be defined as a class hierarchy and can be used interchangeably to alter application behavior without changing its architecture.

2. By encapsulating the algorithm separately, new algorithms complying with the same interface can be easily introduced.

3. The application can switch strategies at run-time.

4. Strategy enables the clients to choose the required algorithm, without using a “switch” 1. statement or a series of “if-else” statements.

5. Data structures used for implementing the algorithm are completely encapsulated in Strategy classes. Therefore, the implementation of an algorithm can be changed without affecting the Context class.

#### Disadvantages
1. The application must be aware of all the strategies to select the right one for the right situation.

2. Context and the Strategy classes normally communicate through the interface specified by the abstract Strategy base class. Strategy base class must expose interface for all the required behaviours, which some concrete Strategy classes might not implement.

3. In most cases, the application configures the Context with the required Strategy object. Therefore, the application needs to create and maintain two objects in place of one.

```js
var Shipping = function() {
    this.company = "";
};

Shipping.prototype = {
    setStrategy: function(company) {
        this.company = company;
    },

    calculate: function(package) {
        return this.company.calculate(package);
    }
};

var UPS = function() {
    this.calculate = function(package) {
        // calculations...
        return "$45.95";
    }
};

var USPS = function() {
    this.calculate = function(package) {
        // calculations...
        return "$39.40";
    }
};

var Fedex = function() {
    this.calculate = function(package) {
        // calculations...
        return "$43.20";
    }
};

// log helper

var log = (function() {
    var log = "";

    return {
        add: function(msg) { log += msg + "\n"; },
        show: function() { alert(log); log = ""; }
    }
})();

function run() {
    var package = { from: "76712", to: "10012", weigth: "lkg" };

    // the 3 strategies

    var ups = new UPS();
    var usps = new USPS();
    var fedex = new Fedex();

    var shipping = new Shipping();

    shipping.setStrategy(ups);
    log.add("UPS Strategy: " + shipping.calculate(package));
    shipping.setStrategy(usps);
    log.add("USPS Strategy: " + shipping.calculate(package));
    shipping.setStrategy(fedex);
    log.add("Fedex Strategy: " + shipping.calculate(package));

    log.show();
}
```
