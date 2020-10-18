---
layout: posts
title:  "Revisiting the Abstract Factory Pattern"
date:   2020-10-18
categories: designPatterns
---

The Abstract Factory pattern is one defined in the GoF design patterns book as a way to make groups of objects easy to swap out by creating concrete factories that implement the abstract factory's interface. To this you use both the abstract factory and the concrete factories, but also the abstract and concrete objects associated with the set of factories.

If you decide to go out to a restaurant, then the idea of 'restaurant' is going to be your abstract factory. `Restaurant` is a term used to define a lot of different things, but generally it is a place where you purchase food that has been prepared for you. The abstract objects produced by the `Restaurant` factory are going to be individual products. You could break those types up into different types of items, say main dish, side, desert, and drink. Those categories represent the abstract objects in this pattern.

Once you decide to go to a specific restaurant then you are going to the concrete factory that implements the `Restaurant` interface. Assuming you went to a Mexican restaurant, our four types of food items might be taco, refried beans, flan, and horchata.

<!---
UML DIAGRAM
-->

Of course this is a simplified example since a restaurant usually has more than one option in each category. In reality, we'd probably model a restaurant as an object instead of a factory and it would have a collection of products with different types. However, if we stick with our `Restaurant` factory for now, some of the benefits and problems become apparent.

## Benefits
The main reason for making use of this pattern is that it becomes very easy to change the type of restaurant to our system. One of the main reasons for using interfaces is to allow you to decouple specific implementations from the system asking for that implementation. A program that represents your visit to a restaurant could pick the specific type of restaurant at runtime and the rest of the program wouldn't care whether you decide to visit a Mexican or Italian restaurant. You would still do things like order, eat, and pay regardless of where you go.

## Negatives
While it's easy to change which concrete factory and related objects you are using, making changes becomes more difficult. Any time you create a new type of restaurant 

## When to Use It

## C# Example

### ASP.NET Framework

This sort of pattern is commonly found in dependency injection containers.`HttpClient` can be created using this pattern in ASP.NET Core

    public void ConfigureServices(IServiceCollection services)
    {
        services.AddHttpClient();
    }

### C# Implementation
