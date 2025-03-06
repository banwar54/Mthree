# Understanding Object-Oriented Programming (OOP) in Python

### 1. **Classes and Objects**
   - A **class** is a blueprint for creating objects. It defines attributes (data) and methods (functions) that describe the behavior of the objects.
   - An **object** is an instance of a class with its own unique attribute values.

### 2. **Instance and Class Attributes**
   - **Instance Attributes**: These are attributes unique to each instance (object) of a class. They are defined using `self.attribute_name` inside the constructor (`__init__`).
   - **Class Attributes**: These are attributes shared by all instances of a class and are defined outside any instance method.

### 3. **Methods**
   - **Instance Methods**: Defined inside a class and operate on instance-specific data. They use `self` as the first parameter.
   - **Magic Methods** (`__init__`, `__str__`, etc.): Special methods that define behavior for class instances.

### 4. **Inheritance**
   - A mechanism that allows one class (child) to inherit attributes and methods from another class (parent).
   - The child class can override parent methods or introduce new methods.
   - `super()` is used to call methods from the parent class.

---

## Code Explanation

### 1. **Basic Class Definition**
```python
class Dog:
    """
    A simple class representing a dog.
    
    This demonstrates the most basic class definition in Python.
    """
    # Class attribute - shared by all instances
    species = "Canis familiaris"

    def __init__(self, name, age):
        """Initialize a new Dog object.
        
        Args:
            name (str): The dog's name
            age (int): The dog's age in years
        """
        # Instance attributes
        self.name = name
        self.age = age

    def bark(self):
        """The dog makes a sound."""
        return f"{self.name} says Woof!"
    
    def get_info(self):
        """Return a string with the dog's information."""
        return f"{self.name} is {self.age} years old."
```

### 2. **Creating Instances**
```python
# Creating objects (instances) of the Dog class
fido = Dog("Fido", 3)
bella = Dog("Bella", 5)
```

- `fido` and `bella` are objects of the `Dog` class with unique `name` and `age` attributes.

### 3. **Accessing Attributes and Methods**
```python
print(fido.name)        # Output: Fido
print(bella.age)        # Output: 5
print(fido.species)     # Output: Canis familiaris
print(fido.bark())      # Output: Fido says Woof!
print(bella.get_info()) # Output: Bella is 5 years old.
```

- `fido.name` and `bella.age` access instance attributes.
- `species` is a shared class attribute.
- `bark()` and `get_info()` are instance methods called on objects.

---

## **Inheritance**

### **Concept of Inheritance**
Inheritance allows us to define a new class that retains characteristics of an existing class.

- `Pet` is the base class.
- `Cat` is a subclass that inherits from `Pet` and extends its functionality.

### **Parent Class: `Pet`**
```python
class Pet:
    """A base class for all pets."""
    
    def __init__(self, name, age):
        """Initialize a Pet object.
        
        Args:
            name (str): The pet's name
            age (int): The pet's age in years
        """
        self.name = name
        self.age = age
    
    def speak(self):
        """The sound the pet makes (to be overridden by subclasses)."""
        return "Some generic pet sound"
    
    def __str__(self):
        """Return a string representation of the pet."""
        return f"{self.name}, age {self.age}"
```

### **Child Class: `Cat` (Inheriting from `Pet`)**
```python
class Cat(Pet):  # Cat inherits from Pet
    """A class representing a cat, inheriting from Pet."""
    
    species = "Felis catus"
    
    def __init__(self, name, age, color):
        """Initialize a Cat object.
        
        Args:
            name (str): The cat's name
            age (int): The cat's age in years
            color (str): The cat's fur color
        """
        super().__init__(name, age)  # Call the parent class's __init__ method
        self.color = color
    
    def speak(self):
        """Override the speak method from the parent class."""
        return f"{self.name} says Meow!"
    
    def purr(self):
        """A method specific to cats."""
        return f"{self.name} purrs contentedly."
```

### **Instance Creation and Method Calls**
```python
# Creating instances
whiskers = Cat("Whiskers", 4, "gray")
```

### **Verifying Inheritance**
```python
print(isinstance(whiskers, Cat))   # Output: True
print(isinstance(whiskers, Pet))   # Output: True
```

### **Accessing Attributes and Methods**
```python
print(whiskers.name)   # From Pet
print(whiskers.color)  # From Cat
print(whiskers)         # Calls __str__ from Pet, Output: Whiskers, age 4
print(whiskers.speak()) # Calls overridden speak method, Output: Whiskers says Meow!
print(whiskers.purr())  # Calls Cat-specific method, Output: Whiskers purrs contentedly.
```

---