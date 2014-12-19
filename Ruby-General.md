# Methods


# Definitions
**[Module](http://www.tutorialspoint.com/ruby/ruby_modules.htm)**  a collection of methods and constants, may be instance methods or module methods .Modules define a namespace, a sandbox in which your methods and constants can play without having to worry about being stepped on by other methods and constants.  Can be included by a class.  Useful because though classes cannot inherit multiple classes, multiple modules can be included by a class.

**Instance methods** appear as methods in a class when the module is included, **module methods** do not. Conversely, module methods may be called without creating an encapsulating object, while instance methods may not.

**Class** describes a group of objects.  Can include modules.  Describes attributes, cannot inherit multiple parent classes, can have class methods.