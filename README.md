# Object Oriented Programming
- What is Procedural Programming?
- What is OOP?
- 4 Pillars of OOP

# What is Procedural Programming?

Procedural programming is a style in which a program is constructed as a linear sequence of instructions. It emphasizes breaking down a task into smaller, manageable procedures (also known as functions or methods). This is what we normally do.

Procedural Example in C#

*Program.cs*
```cs
int number1 = 10;
int number2 = 5;

int result = AddNumbers(number1, number2);
Console.WriteLine("The sum is: " + result);

static int AddNumbers(int num1, int num2)
{
    return num1 + num2;
}
```

As programs grow, it gets harder to manage all the procedures and methods.

# What is OOP?

OOP is a technique for structuring programs. The idea is that programs consist of "objects" that use each other to perform tasks.

That in itself sounds a lot like procedural programming, where we have methods to perform different tasks. But there is a difference:

Objects are *instances* of classes.

The concept of a "class" in C# pretty much corresponds to how we categorize "objects" or "concepts" or "types" in the real world in our heads. For example we can think about Dogs, People, Cars, Newspapers as objects, with some similarities and differences in attributes and functionalities. 

*Car.cs*
```cs
class Car
{
    // Attributes (properties) describing the car
    public string Color { get; set; }
    public int NumDoors { get; set; }
    public int NumWheels { get; set; }

    // Methods (behaviors) representing what the car can do
    public void StartEngine() { /* Code to simulate engine starting */ }
    public void StopEngine() { /* Code to simulate engine stopping */ }
    public void Steer(string direction) { /* Code to simulate turning */ }

    // Constructors etc...
}
```
*Microwave.cs*
```cs
class Microwave
{
    // Attributes (properties) describing the microwave
    public string Color { get; set; }
    public int NumDoors { get; set; }

    // Methods (behaviors) representing what the microwave can do
    public void Start() { /* Code to simulate microwave heating */ }
    public void Stop() { /* Code to simulate microwave heating stopping */ }

    // Constructors etc...
}
```

So this Car class serves as a "blueprint" for Car objects (instances), while the Microwave class for instances of microwaves. This helps us create some hierarchy, there are certain things one class can do that another cannot.

An employee can also be a class

```cs
class Employee
{

    private string firstName;

    public string FirstName
    {
        get { return firstName; }
        set { firstName = value; }
    }

    public Employee()
    {

    }

    public void PerformWork()
    {

    }
}
```

In .net 5 categories of CTS (.net Common Type System types)

- Classes (most useful)
- Enumerations (useful to give readable names to constant-codes. Enums are value types)
- Structs (can be described as lightweight classes. Structs are value types)
- Interface (similar to class but it contains only "the contract" that must be implemented by the class it is an interface for, the inteface does not contain the implementation, just the specification (contract).)
- Delegate (types that point to a method with parameter list and return type. Typicly used to pass methods as parameters to other methods.)
- Record (internally treated as classes. Only used in special cases. Records support "value-based" equality checks.)

Examples of these:

```cs

enum Weekdays { Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday }

struct Point
{
    public int X { get; set; }
    public int Y { get; set; }
}

interface ICar
{
    void StartEngine();
    void StopEngine();
}

delegate void DisplayMessage(string message);

public record Person(string FirstName, string LastName);

// usage

DisplayMessage display = message => Console.WriteLine(message);
display("Hello from a delegate!");

var point = new Point { X = 10, Y = 20 };
```

Object oriented programming relies on a few principles to help structure code. One of them is the 4 pillars of OOP.


# 4 Pillars of OOP

1. Abstraction
2. Encapsulation
3. Inheritance
4. Polymorphism

## Abstraction

When we're asked in real life to think about something abstractly, we focus on its essential characteristics and behaviors, ignoring specific details. For example, if we think of the concept of driving a car. We interact with an abstract interface (steering wheel, pedals), but the underlying mechanics (engine, transmission) are hidden.

In object-oriented programming (OOP), abstraction works similarly. We create blueprints called **classes** that define the essential features and behaviors of objects.  This allows us to work with a simplified representation of the object without needing to worry about the underlying implementation details.

Abstraction is about focusing on what an object does rather than how it does it. Imagine it like putting a simplified interface on top of a complex system. You provide the essential controls and information needed to interact with the object, while hiding the messy details behind the scenes.

In C#, we use classes to model objects. With abstraction, we design classes that only expose public methods to represent the actions an object can take. These methods act like the "handles" of the object. The inner workings of the class – the private variables and intricate logic –  are hidden from the user. This makes it easier to use and reason about the object.

Abstraction can feel a bit tricky to understand at first, and that's okay!  The key is to think about objects in terms of their capabilities and interactions, not the nitty-gritty details of their inner code.

## Thinking in Abstraction

Imagine we are asked to create an application that allows employees to "perform work".

We start by thinking about "employee" entity in our system as a class in our code. An emplyee will have a number of characteristics what an employee might do or might contain. An employee will have a name, an age, their weight, their address, their hair color, and so on.

They can also perform work, they can walk, they can talk, and more.

Now not all of this is relevant to our application, so out of these, we pick the ones we need in our application, so probably the name and the ability to perform work. That will become the public interface of our employee entity. 

Other internal functionalities may be included internally in the class, but won't be exposed to the user of the class. For example a check if they perform more work than allowed may be included in the classs, but not publicly exposed.

We are abstracting away all that isn't relevant to what we are creating at the design level, and that's what the abstraction is all about.

```cs
class Employee
{
    public string Name;
    public void PerformWork()
    {

    }
}
```

## Encapsulation

Encapsulation means bundling an object's data (its state) and the methods (behaviors) that operate on that data into a single unit: the class. This allows us to control how the object's data is accessed and modified.

By keeping data and its related logic together, we make our code more organized and maintainable. Changes to an object's internal implementation are less likely to break other parts of the code.

We protect the object's data by making it private and providing controlled access through public methods or properties. This ensures the data is changed in predictable ways, maintaining the object's integrity.

## Encapsulation applied on a Car

Think of a car as an encapsulated object. It holds data like its current speed, fuel level, and engine temperature. It also has operations (methods) like accelerate, brake, and adjust climate control.  All this functionality is bundled together within the car itself.

Encapsulation also means hiding complex details from the driver (the user).  You don't directly manipulate the fuel injection or engine timing. Instead, you interact with the car through a well-defined interface: the gas pedal, brake pedal, and dashboard controls.  These elements trigger internal processes in a safe and controlled manner.

Similarly, in a C# class, encapsulation lets us define a public interface of methods and properties for interacting with an object.  A lot of the inner workings remain hidden, ensuring that the object's data is used and modified in intended ways.

## Inheritance

The third pillar of object‑oriented programming is inheritance. In real life a dog is a type of animal, and a poodle is a more specific type of a dog just like a golden retriever is. We implicitly are putting these in a hierarchy, going from more generic to more specific, and we understand that all dogs are animals, and poodles are dogs, and thus they will inherit features from their parent or parents. This is where inheritance comes into play.

We will be able to, in our code, define this hierarchy and define the functionality on a higher level, therefore, being able to reuse code on the parent or on their child instead of having to duplicate the code.

The child class will typically build on what the parent has already defined, and will also typically extend this with its own functionality and data. 

So inheritance will allow us to define common functionality on a higher level, thereby allowing inheritors to reuse that functionality and extend when needed.

We can define a car which wraps the data and functionality of the concept of a car. It may define the speed, the max speed, the color, the age as data, and functionality such as drive, brake, and park. 

```cs
class Car
{
    private int maxSpeed;
    public int MaxSpeed { get => maxSpeed; set => maxSpeed = value; }
    public void Drive()
    {

    }
}
```

Just like with dogs, more specific types of cars exist. 

A minivan is a car, but it will typically have more specific features, while still being a car. Through inheritance, the minivan inherits the data and functionalities of the parent car, but might extend it with the functionality, openSlideDoor. 

Similarly, a sports car with an open roof might define 'isRoofOpen' and 'closeRoof', while benefiting from the drive, brake, and park method which are defined on the parent Car class. And an ElectricCar class might define a charge method. 

```cs
class SportsCar : Car
{
    private bool isRoofOpen;
}
```

Having these functionalities on the parent class will really help with code reuse. If there's a bug in the Drive method defined on the Car class, we only need to change that in one place, and all of the classes will benefit from that. 

## Polymorphism

The final pillar is polymorphism. One issue we'll get with just plain inheritance is that in the hierarchy some classes will define the same behavior, but they will need a different implementation. The Drive method will be available on all the cars in the hierarchy, but driving a sports car is a different experience than driving a minivan. This is what polymorphism is all about. The same method must be able to execute in different forms, hence, the word polymorph, so multiple forms.

Within the hierarchy, we can still define a base implementation, but inheritors can decide they'll need a different implementation. In C#, this is  possible using the **virtual** and **override** keywords. Example:

```cs
class Car
{
    public virtual void Drive()
    {
        Console.WriteLine("Driving...");
    }
}
```
We can define the Drive method on the base class to be virtual, thereby saying that inheriting classes can provide their own implementation. 
The ElectricCar class is opting to do so by adding the override keyword, and then it gives its own implementation. 

```cs
class ElectricCar : Car
{
    public override void Drive()
    {
        base.Drive();
    }
}
```
For consumers of this class, nothing changes. We can still invoke the Drive method, but different versions, different forms of the same method now exist.

The override keyword replaces the original Drive method, but if needed it's possible to call the Car's Drive-method from within the ElectriCar's class using base.Drive() which is what we're doing here.

Those are the 4 pillars of OOP.


## There are few additional access modifiers in C# that are useful in relation to OOP:

- **sealed class** cannot be used as a base class.
- **abstract class** cannot be instantiated, it is ment to serve as base class for another class or interface.
