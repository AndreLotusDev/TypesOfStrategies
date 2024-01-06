# Strategy Design Pattern in C#

## Overview
The Strategy Design Pattern is a behavioral design pattern that allows you to define a family of algorithms, encapsulate each one, and make them interchangeable. The strategy pattern lets the algorithm vary independently from clients that use it. This is particularly useful for applications that need to dynamically swap out algorithms or behaviors at runtime.

## Purpose
- To define a set of interchangeable algorithms or strategies.
- To enable a client to choose the most suitable algorithm at runtime.
- To extend a class behavior without altering its structure.

## Example Usage

### Scenario
Imagine an application for a logistics company that calculates the cost of shipping goods. The shipping cost can vary based on different factors like the distance, weight of goods, and the type of transportation (air, road, sea).

### Implementing Strategy Pattern
We create a `IShippingStrategy` interface that defines the `Calculate` method. Then, we implement different shipping strategies like `AirShippingStrategy`, `RoadShippingStrategy`, and `SeaShippingStrategy` that implement the `IShippingStrategy` interface. The `ShippingCostCalculator` class uses the `IShippingStrategy` to calculate the shipping cost.

## Code Example in C#

```csharp
// Strategy Interface
public interface IShippingStrategy
{
    double Calculate(double weight, double distance);
}

// Concrete Strategies
public class AirShippingStrategy : IShippingStrategy
{
    public double Calculate(double weight, double distance)
    {
        return weight * distance * 0.25;
    }
}

public class RoadShippingStrategy : IShippingStrategy
{
    public double Calculate(double weight, double distance)
    {
        return weight * distance * 0.15;
    }
}

public class SeaShippingStrategy : IShippingStrategy
{
    public double Calculate(double weight, double distance)
    {
        return weight * distance * 0.05;
    }
}

// Context
public class ShippingCostCalculator
{
    private IShippingStrategy _strategy;

    public ShippingCostCalculator(IShippingStrategy strategy)
    {
        _strategy = strategy;
    }

    public double CalculateShippingCost(double weight, double distance)
    {
        return _strategy.Calculate(weight, distance);
    }
}

// Usage
public class Program
{
    public static void Main(string[] args)
    {
        var calculator = new ShippingCostCalculator(new AirShippingStrategy());
        double cost = calculator.CalculateShippingCost(10, 100); // Example usage
        Console.WriteLine("Shipping Cost: " + cost);
    }
}
```
