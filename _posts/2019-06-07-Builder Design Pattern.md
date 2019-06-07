---
layout: post
title: Builder Pattern
subtitle: Design Pattern学习笔记系列
date: 2019-06-07
author: Jalever
header-img: img/home_bg_tree.png
catalog: true
tags:
  - Design Pattern
---

Builder pattern aims to “Separate the construction of a complex object from its representation so that the same construction process can create different representations.”

It is used to construct a complex object step by step and the final step will return the object.

The process of constructing an object should be generic so that it can be used to create different representations of the same object.

```java
interface HousePlan {
	public String getBasement();
	public void setBasement(String basement);

	public String getStructure();
	public void setStructure(String structure);

	public String getRoof();
	public void setRoof(String roof);

	public String getInterior();
	public void setInterior(String interior);
}

class House implements HousePlan {
	private String basement;
	private String structure;
	private String roof;
	private String interior;

	public String getBasement() {
	    return this.basement;
	};

	public void setBasement(String basement) {
		this.basement = basement;
	}

	public String getStructure() {
	    return this.structure;
	};

	public void setStructure(String structure) {
		this.structure = structure;
	}

	public String getRoof() {
	    return this.roof;
	};

	public void setRoof(String roof) {
		this.roof = roof;
	}

	public String getInterior() {
	    return this.interior;
	};

	public void setInterior(String interior) {
		this.interior = interior;
	}
}


interface HouseBuilder {
	public void buildBasement();

	public void buildStructure();

	public void bulidRoof();

	public void buildInterior();

	public void getHouse();
}

class IglooHouseBuilder implements HouseBuilder {
	private House house;

	public IglooHouseBuilder() {
		this.house = new House();
	}

	public void buildBasement()	{
		house.setBasement("Ice Bars");
	}

	public void buildStructure() {
		house.setStructure("Ice Blocks");
	}

	public void buildInterior()	{
		house.setInterior("Ice Carvings");
	}

	public void bulidRoof()	{
		house.setRoof("Ice Dome");
	}

	public void getHouse()	{
	    String basement = house.getBasement();
	    String structure = house.getStructure();
	    String roof = house.getRoof();
	    String interior = house.getInterior();

		System.out.print("  -Basement: " + basement + "\n");
		System.out.print("  -structure: " + structure + "\n");
		System.out.print("  -roof: " + roof + "\n");
		System.out.print("  -interior: " + interior + "\n");
	}
}

class TipiHouseBuilder implements HouseBuilder {
	private House house;

	public TipiHouseBuilder() {
		this.house = new House();
	}

	public void buildBasement() {
		house.setBasement("Wooden Poles");
	}

	public void buildStructure() {
		house.setStructure("Wood and Ice");
	}

	public void buildInterior() {
		house.setInterior("Fire Wood");
	}

	public void bulidRoof() {
		house.setRoof("Wood, caribou and seal skins");
	}

	public void getHouse()	{
		String basement = house.getBasement();
	    String structure = house.getStructure();
	    String roof = house.getRoof();
	    String interior = house.getInterior();

		System.out.print("  -Basement: " + basement + "\n");
		System.out.print("  -structure: " + structure + "\n");
		System.out.print("  -roof: " + roof + "\n");
		System.out.print("  -interior: " + interior + "\n");
	}
}

class CivilEngineer {
	private HouseBuilder houseBuilder;

	public CivilEngineer(HouseBuilder houseBuilder) {
		this.houseBuilder = houseBuilder;
	}

	public void getHouse()	{
		this.houseBuilder.getHouse();
	}

	public void constructHouse() {
		this.houseBuilder.buildBasement();
		this.houseBuilder.buildStructure();
		this.houseBuilder.bulidRoof();
		this.houseBuilder.buildInterior();
	}
}

class Builder {
	public static void main(String[] args) 	{
		HouseBuilder iglooBuilder = new IglooHouseBuilder();
		CivilEngineer engineer = new CivilEngineer(iglooBuilder);
		engineer.constructHouse();
		System.out.println("Builder constructed: \n");
		engineer.getHouse();

	}
}
```

#### Advantages of Builder Design Pattern
- The parameters to the constructor are reduced and are provided in highly readable method calls.

- Builder design pattern also helps in minimizing the number of parameters in constructor and thus there is no need to pass in null for optional parameters to the constructor.

- Object is always instantiated in a complete state
Immutable objects can be build without much complex logic in object building process.

#### Disadvantages of Builder Design Pattern

- The number of lines of code increase at least to double in builder pattern, but the effort pays off in terms of design flexibility and much more readable code.

- Requires creating a separate ConcreteBuilder for each different type of Product.
