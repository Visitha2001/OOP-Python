Object-Oriented Programming (OOP) is a programming paradigm that organizes software design around objects and data, rather than functions and logic. Python supports OOP principles like classes, objects, inheritance, polymorphism, encapsulation, and abstraction.

Here’s an overview of OOP concepts in Python with examples:

### 1. **Classes and Objects**

- **Class**: A blueprint for creating objects.
- **Object**: An instance of a class.

```python
# Defining a class
class Dog:
    # Constructor to initialize an object
    def __init__(self, name, age):
        self.name = name  # Instance variable
        self.age = age    # Instance variable
    
    # Method
    def bark(self):
        return f"{self.name} says Woof!"
    
# Creating an object (instance of Dog)
my_dog = Dog("Buddy", 5)

# Accessing properties and methods
print(my_dog.name)       # Accessing instance variable
print(my_dog.bark())     # Calling method
```

### 2. **Encapsulation**

Encapsulation is the concept of restricting access to some of an object’s components and only allowing access through methods.

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.__age = age  # Private variable (name mangling)

    # Getter method
    def get_age(self):
        return self.__age

    # Setter method
    def set_age(self, age):
        if age > 0:
            self.__age = age
        else:
            print("Age must be positive")

# Creating an object
person = Person("John", 25)

# Accessing private variable through getter
print(person.get_age())

# Trying to directly access a private variable (raises error)
# print(person.__age)  # This will result in an AttributeError
```

### 3. **Inheritance**

Inheritance allows one class (child class) to inherit attributes and methods from another class (parent class).

```python
# Parent class
class Animal:
    def __init__(self, name):
        self.name = name

    def speak(self):
        return f"{self.name} makes a sound"

# Child class inherits from Animal
class Dog(Animal):
    def speak(self):  # Overriding the speak method
        return f"{self.name} barks"

class Cat(Animal):
    def speak(self):  # Overriding the speak method
        return f"{self.name} meows"

# Creating objects of Dog and Cat
dog = Dog("Buddy")
cat = Cat("Whiskers")

# Calling overridden methods
print(dog.speak())  # Output: Buddy barks
print(cat.speak())  # Output: Whiskers meows
```

### 4. **Polymorphism**

Polymorphism allows you to use a method in multiple ways. It can refer to method overriding (as shown in inheritance) or method overloading (though Python does not support traditional method overloading).

```python
class Bird(Animal):
    def speak(self):  # Overriding the speak method
        return f"{self.name} chirps"

# Creating a list of animals
animals = [Dog("Rex"), Cat("Luna"), Bird("Tweety")]

# Polymorphism in action
for animal in animals:
    print(animal.speak())  # Each animal calls its own speak method
```

### 5. **Abstraction**

Abstraction allows you to hide complex implementation details and only show the necessary features of an object.

In Python, abstraction can be achieved using abstract classes and methods (using the `abc` module).

```python
from abc import ABC, abstractmethod

class Animal(ABC):
    @abstractmethod
    def speak(self):
        pass  # Abstract method (to be implemented by subclass)

class Dog(Animal):
    def speak(self):
        return "Woof!"

class Cat(Animal):
    def speak(self):
        return "Meow!"

# Creating objects of Dog and Cat
dog = Dog()
cat = Cat()

print(dog.speak())  # Output: Woof!
print(cat.speak())  # Output: Meow!
```

### 6. **Class Methods and Static Methods**

- **Class methods**: Operate on the class itself, not on an instance.
- **Static methods**: Do not operate on the class or the instance.

```python
class Calculator:
    @staticmethod
    def add(x, y):
        return x + y

    @classmethod
    def description(cls):
        return f"This is a {cls.__name__} class that performs calculations."

# Using static method
print(Calculator.add(5, 3))  # Output: 8

# Using class method
print(Calculator.description())  # Output: This is a Calculator class that performs calculations.
```

### 7. **Magic Methods (Dunder Methods)**

Python provides special methods (called "magic" or "dunder" methods) that enable the use of operators and other Python features like object comparisons, string representations, and more.

```python
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    # __str__ method is used for string representation
    def __str__(self):
        return f"Point({self.x}, {self.y})"

    # __add__ method is used to define the behavior of the + operator
    def __add__(self, other):
        return Point(self.x + other.x, self.y + other.y)

# Creating Point objects
p1 = Point(2, 3)
p2 = Point(4, 5)

# Using __str__ method implicitly
print(p1)  # Output: Point(2, 3)

# Using __add__ method to add two Point objects
p3 = p1 + p2  # Calls p1.__add__(p2)
print(p3)  # Output: Point(6, 8)
```

### Summary of OOP Concepts:

- **Classes**: Blueprint for creating objects.
- **Objects**: Instances of classes.
- **Encapsulation**: Hiding internal states and requiring methods to access them.
- **Inheritance**: Ability to create a new class from an existing class.
- **Polymorphism**: The ability to use the same method name but have different behaviors.
- **Abstraction**: Hiding complex details and only exposing the essentials.
- **Magic Methods**: Special methods that allow Python objects to behave like built-in types (e.g., `__str__`, `__add__`).

### Final Example: A Complete OOP Program

```python
class BankAccount:
    def __init__(self, account_holder, balance=0):
        self.account_holder = account_holder
        self.__balance = balance  # Private variable
    
    def deposit(self, amount):
        if amount > 0:
            self.__balance += amount
            print(f"Deposited {amount}. New balance: {self.__balance}")
        else:
            print("Deposit amount must be positive.")
    
    def withdraw(self, amount):
        if 0 < amount <= self.__balance:
            self.__balance -= amount
            print(f"Withdrew {amount}. Remaining balance: {self.__balance}")
        else:
            print("Insufficient funds or invalid amount.")
    
    def get_balance(self):
        return self.__balance

# Create an object of BankAccount
account = BankAccount("Alice", 1000)
account.deposit(500)
account.withdraw(300)
print(f"Account balance: {account.get_balance()}")
```

This complete program illustrates how to use OOP to model a **BankAccount** with features such as deposit, withdrawal, and balance checking.
