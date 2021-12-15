# Rule of Three
If a class manages resources, it has a **non-trivial** [destructor](Constructors%20and%20Destructors.md#Destructor). 

Rule of 3: If you have to manage how an object is destroyed, you should also manage how it is copied.
- Technical version: If you have a non-trivial destructor, you should also define a  [copy constructor](Overloading.md#Copy%20constructor) and [assignment operator](Overloading.md#Assignment%20Operator).
- Another perspective: if your class has a non-trivial destructor, you probably don't want shallow copying. 

\
Also consider whether or not you need equality operator (design decision).