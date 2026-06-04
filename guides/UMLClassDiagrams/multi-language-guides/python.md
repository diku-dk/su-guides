# What do the arrows mean in Python?
This guide relates Python code to the arrows found in UML class diagrams. This guide is not intended as a way to learn UML class diagrams, it is just meant as a supplement to other resources. An alternative resource to understand UML class diagrams can be found [here](https://www.visual-paradigm.com/guide/uml-unified-modeling-language/uml-class-diagram-tutorial/).

# Inheritance
An example of when an inheritance relationship can occur is.
```python
class ClassA:
    pass


class ClassB(ClassA):
    pass
```
The inheritance arrow is used since `ClassB` inherits from `ClassA`, which can be expressed as a UML class diagram below.

<p align="center">
  <img src="../diagrams/inheritance.png" />
</p>

# Aggregation
An example of when an aggregation relationship can occur is.
```python
class ClassA:
    def __init__(self):
        self.class_b = None


class ClassB:
    pass
```
The aggregation arrow is used if `ClassB` is part of `ClassA`, but they have separate life spans. This means that `ClassA` can stop existing while `ClassB` can keep existing. So if you consider the following piece of code.
```python
a = ClassA()
b = ClassB()
a.class_b = b
a = None
```
Then, executing the last line of the code, the instance of `ClassA` has been dereferenced and is inaccessible using the variable `a`, but the instance of `ClassB` is still available through the variable `b`. This relation can be expressed using the following arrow.

<p align="center">
  <img src="../diagrams/aggregation.png" />
</p>

# Multiplicity
An example of when multiplicity can occur is.
```python
class ClassA:
    def __init__(self):
        self.bs = []


class ClassB:
    pass
```
Multiplicity is used to denote the quantities of classes in the relationships. In the above example a single `ClassA` has many `ClassB` instances. In the diagram below you can see how this is shown.

<p align="center">
  <img src="../diagrams/multiplicity.png" />
</p>

# Composition
An example of when a composition relationship can occur is.
```python
class ClassA:
    def __init__(self):
        self._class_b = ClassB()


class ClassB:
    pass
```
The composition arrow is used if `ClassB` is part of `ClassA` and they have the same life span. This means that if an instance of `ClassA` stops existing then its instance of `ClassB` will stop existing. If a public attribute were used then they would not necessarily have the same life span. An example of this piece of code expressed as a UML class diagram can be seen below.

<p align="center">
  <img src="../diagrams/composition.png" />
</p>

# Dependency
An example of when a dependency relationship can occur is.
```python
class ClassA:
    def print(self):
        print("test")


class ClassB:
    def use_print(self, a):
        a.print()
```
The dependency arrow is used when a class is dependent on another class without storing the class in a field. In the example above, `ClassB` depends on `ClassA` in the sense that if you changed `ClassA` such that `print` did not exist then `ClassB` would break. Also, since `ClassB` does not store an instance of `ClassA`, the dependency is less strong than an aggregation or a composition. Below is a diagram expressing the code.

<p align="center">
  <img src="../diagrams/dependency.png" />
</p>

# Realization
An example of when a realization relationship can occur is.
```python
from abc import ABC


class InterfaceA(ABC):
    pass


class ClassB(InterfaceA):
    pass
```
The realization arrow is used when a class implements some blueprint. As an example, the blueprint can specify a set of methods that must be implemented such that the implementation is fulfilled for that class. Python does not use interfaces in the same way as Java or C#, but abstract base classes can be used to express a similar blueprint. In the code above, `ClassB` implements the blueprint represented by `InterfaceA`. The diagram below shows a UML class diagram expressing the code.

<p align="center">
  <img src="../diagrams/realization.png" />
</p>
