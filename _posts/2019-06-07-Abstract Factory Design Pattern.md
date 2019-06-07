---
layout: post
title: Abstract Factory
subtitle: Design Pattern学习笔记系列
date: 2019-06-07
author: Jalever
header-img: img/home_bg_tree.png
catalog: true
tags:
  - Design Pattern
---
## Introduction

Abstract Factory design pattern is one of the Creational pattern.

Abstract Factory patterns work around a super-factory which creates other factories.


```java
// Java Program to demonstrate the
// working of Abstract Factory Pattern

enum CarType {
	MICRO,
	MINI,
	LUXURY
}

enum Location {
    DEFAULT,
    USA,
    INDIA
}

abstract class Car {
	Car(CarType model, Location location) {
		this.model = model;
		this.location = location;
	}

	abstract void construct();

	CarType model = null;
	Location location = null;

	CarType getModel() {
		return model;
	}

	void setModel(CarType model) {
		this.model = model;
	}

	Location getLocation() {
		return location;
	}

	void setLocation(Location location) {
		this.location = location;
	}

	@Override
	public String toString() {
		return "CarModel - "+model + " located in "+location;
	}
}

class LuxuryCar extends Car {
	LuxuryCar(Location location) {
		super(CarType.LUXURY, location);
		construct();
	}
	@Override
	protected void construct(){
		System.out.println("Connecting to luxury car");
	}
}

class MicroCar extends Car {
	MicroCar(Location location) {
		super(CarType.MICRO, location);
		construct();
	}
	@Override
	protected void construct() {
		System.out.println("Connecting to Micro Car ");
	}
}

class MiniCar extends Car {
	MiniCar(Location location) {
		super(CarType.MINI,location );
		construct();
	}

	@Override
	void construct() {
		System.out.println("Connecting to Mini car");
	}
}


class INDIACarFactory {
	static Car buildCar(CarType model) {
		Car car = null;
		switch (model) {
			case MICRO:
				car = new MicroCar(Location.INDIA);
				break;

			case MINI:
				car = new MiniCar(Location.INDIA);
				break;

			case LUXURY:
				car = new LuxuryCar(Location.INDIA);
				break;

				default:
				break;

		}
		return car;
	}
}

class DefaultCarFactory {
	public static Car buildCar(CarType model) {
		Car car = null;
		switch (model) {
			case MICRO:
				car = new MicroCar(Location.DEFAULT);
				break;

			case MINI:
				car = new MiniCar(Location.DEFAULT);
				break;

			case LUXURY:
				car = new LuxuryCar(Location.DEFAULT);
				break;

				default:
				break;

		}
		return car;
	}
}


class USACarFactory {
	public static Car buildCar(CarType model) {
		Car car = null;
		switch (model) {
			case MICRO:
				car = new MicroCar(Location.USA);
				break;

			case MINI:
				car = new MiniCar(Location.USA);
				break;

			case LUXURY:
				car = new LuxuryCar(Location.USA);
				break;

				default:
				break;

		}
		return car;
	}
}



class CarFactory {
	private CarFactory() { 	}

	public static Car buildCar(CarType type) {
		Car car = null;

		// We can add any GPS Function here which
		// read location property somewhere from configuration
		// and use location specific car factory
		// Currently I'm just using INDIA as Location
		Location location = Location.INDIA;

		switch(location) {
			case USA:
				car = USACarFactory.buildCar(type);
				break;

			case INDIA:
				car = INDIACarFactory.buildCar(type);
				break;

			default:
				car = DefaultCarFactory.buildCar(type);

		}

		return car;

	}
}

class AbstractDesign {
	public static void main(String[] args)
	{
		System.out.println(CarFactory.buildCar(CarType.MICRO));
		System.out.println(CarFactory.buildCar(CarType.MINI));
		System.out.println(CarFactory.buildCar(CarType.LUXURY));
	}
}
```
