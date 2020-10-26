---
layout: posts
title:  "Revisiting the Abstract Factory Pattern"
date:   2020-10-25
categories: designPatterns
---

The Abstract Factory pattern is one defined in the GoF design patterns book as a way to make groups of objects easy to swap out by creating concrete factories that implement the abstract factory's interface. To this you use both the abstract factory and the concrete factories, but also the abstract and concrete objects associated with the set of factories.

If you decide to go out to a restaurant, then the idea of 'restaurant' is going to be your abstract factory. `Restaurant` is a term used to define a lot of different things, but generally it is a place where you purchase food that has been prepared for you. The abstract objects produced by the `Restaurant` factory are going to be individual products. You could break those types up into different types of items, say main dish, side, desert, and drink. Those categories represent the abstract objects in this pattern.

Once you decide to go to a specific restaurant then you are going to the concrete factory that implements the `Restaurant` interface. Assuming you went to a Mexican restaurant, our four types of food items might be taco, refried beans, flan, and horchata.

![Abstract Factory Diagram](/assets/images/AbstractFactoryUML.png)

Of course this is a simplified example since a restaurant usually has more than one option in each category. In reality, we'd probably model a restaurant as an object instead of a factory and it would have a collection of products with different types. However, if we stick with our `Restaurant` factory for now, some of the benefits and problems become apparent.

## Benefits
The main reason for making use of this pattern is that it becomes very easy to change the type of restaurant to our system. One of the main reasons for using interfaces is to allow you to decouple specific implementations from the system asking for that implementation. A program that represents your visit to a restaurant could pick the specific type of restaurant at runtime and the rest of the program wouldn't care whether you decide to visit a Mexican or Italian restaurant. You would still do things like order, eat, and pay regardless of where you go.

## Negatives
While it's easy to change which concrete factory and related objects you are using, making changes becomes more difficult. Any time you create a new type of restaurant you have to implement all the methods in the factory and each of the models.

## When to Use It
This pattern is particularly useful when you know you will need a set of objects that follow a particular pattern, but don't want to choose the specific implementation until runtime. It can also be used in situations where you don't want to expose the underlying implementation, such as in the ASP.NET example below.


## .NET Core Example

This sort of pattern is commonly found in dependency injection containers. [`HttpClient`](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/http-requests?view=aspnetcore-3.1) can be created using this pattern in ASP.NET Core. It doesn't look like much with the default setup:
```c#
public void ConfigureServices(IServiceCollection services)
{
    services.AddHttpClient();
}
```

Behind the scenes the `AddHttpClient()` method creates the [`DefaultHttpClientFactory`](https://github.com/aspnet/HttpClientFactory/blob/master/src/Microsoft.Extensions.Http/DefaultHttpClientFactory.cs) as a singleton and registers it with the DI container. This is a concrete factory. Where this becomes an abstract factory is that the `DefaultHttpClientFactory` class is internal to the System.Net.Http namespace. The part you as the developer can access is the abstract version `IHttpClientFactory`.

It is not quite a perfect example as there is no abstract `IHttpClient` interface. Instead the `HttpClient` acts as a default model and you can create specific implementations of that class to be handled by the factory.

## C# Implementation
```c#
//Interfaces
public interface IRestaurantFactory {
    IMainDish CreateMainDish();
    IDrink CreateDrink();
}

public interface IMainDish {
    string Name;
    float Price;
    List<string> Ingredients;
    string Description;
}

public interface IDrink {
    string Name;
    float Price;
    float Size;
    string Description;
}

//Classes
public class MesicanRestaurantFactory: IRestaurantFactory {
    public IMainDish CreateMainDish() {
        return new Taco();
    }

    public IDrink CreateDrink() {
        return new Horchata();
    }
}

public class Taco: IMainDish {

    public Taco() {
        Name = "Taco";
        Price = .99;
        Ingredients = new List<string>() {
            "Tortilla",
            "Ground Beef",
            "Shredded Cheese"
        };
        Description = "It's a basic taco.";
    } 

    public string Name { get; }
    public float Price { get; }
    public List<string> Ingredients { get; }
    public string Description { get; }
}

public class Horchata: IDrink {

    public Horchata() {
        Name = "Horchata";
        Price = 1.99;
        Size = 16;
        Description = "Rice milk with vanilla and cinnamon";
    }

    public string Name { get; }
    public float Price { get; }
    public float Size { get; }
    public string Description { get; }
}
```