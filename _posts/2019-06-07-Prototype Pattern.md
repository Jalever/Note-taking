---
layout: post
title: Prototype Factory
subtitle: Design Pattern学习笔记系列
date: 2019-06-07
author: Jalever
header-img: img/home_bg_tree.png
catalog: true
tags:
  - Design Pattern
---

## Introduction
The prototype pattern is a creational design pattern.

The concept is to copy an existing object rather than creating a new instance from scratch, something that may include costly operations.

Prototype allows us to hide the complexity of making new instances from the client.

The existing object acts as a prototype and contains the state of the object.

The newly copied object may change same properties only if required.

This approach saves costly resources and time, especially when the object creation is a heavy process.

Prototype patterns is required, when object creation is time consuming, and costly operation, so we create object with existing object itself.

One of the best available way to create object from existing objects are clone() method.

#### Prototype Design Participants

- Prototype
This is the prototype of actual object.

- Prototype registry
This is used as registry service to have all prototypes accessible using simple string parameters.

- Client
Client will be responsible for using registry service to access prototype instances.

#### Advantages
- Adding and removing products at run-time
Prototypes let you incorporate a new concrete product class into a system simply by registering a prototypical instance with the client.

That’s a bit more flexible than other creational patterns, because a client can install and remove prototypes at run-time.

- Specifying new objects by varying values
Highly dynamic systems let you define new behavior through object composition by specifying values for an object’s variables and not by defining new classes.

- Specifying new objects by varying structure
Many applications build objects from parts and subparts.

For convenience, such applications often let you instantiate complex, user-defined structures to use a specific subcircuit again and again.

- Reduced subclassing
Factory Method often produces a hierarchy of Creator classes that parallels the product class hierarchy.

The Prototype pattern lets you clone a prototype instead of asking a factory method to make a new object. Hence you don’t need a Creator class hierarchy at all.


#### Disadvantages
- Overkill for a project that uses very few objects and/or does not have an underlying emphasis on the extension of prototype chains.

- It also hides concrete product classes from the client

- Each subclass of Prototype must implement the clone() operation which may be difficult, when the classes under consideration already exist. Also implementing clone() can be difficult when their internals include objects that don’t support copying or have circular references.

```java
// A Java program to demonstrate working of
// Prototype Design Pattern with example
// of a ColorStore class to store existing objects.

import java.util.HashMap;
import java.util.Map;


abstract class Color implements Cloneable {

	protected String colorName;

	abstract void addColor();

	public Object clone()
	{
		Object clone = null;
		try
		{
			clone = super.clone();
		}
		catch (CloneNotSupportedException e)
		{
			e.printStackTrace();
		}
		return clone;
	}
}

class blueColor extends Color {
	public blueColor() {
		this.colorName = "blue";
	}

	@Override
	void addColor() {
		System.out.println("Blue color added");
	}

}

class blackColor extends Color {

	public blackColor() {
		this.colorName = "black";
	}

	@Override
	void addColor() {
		System.out.println("Black color added");
	}
}

class ColorStore {

	private static Map<String, Color> colorMap = new HashMap<String, Color>();

	static {
		colorMap.put("blue", new blueColor());
		colorMap.put("black", new blackColor());
	}

	public static Color getColor(String colorName) {
		return (Color) colorMap.get(colorName).clone();
	}
}


// Driver class
class Prototype {
	public static void main (String[] args) {
		ColorStore.getColor("blue").addColor();
		ColorStore.getColor("black").addColor();
		ColorStore.getColor("black").addColor();
		ColorStore.getColor("blue").addColor();
	}
}
```
