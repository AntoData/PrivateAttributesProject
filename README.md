# PrivateAttributesProject
 Module to increase encapsulation in Python, not allowing the access to private members outside their classes


## Installation

Use the package manager [pip](https://pip.pypa.io/en/stable/) to install PrivateAttributesProject.

```bash
pip3 install PrivateAttributesDecorator
```

## Usage

```python
    from PrivateAttributesDecorator import private_attributes_decorator
    # We add the attributes we want to make private, also optionally we can add the keyword
    # parameter allow_deep_copy and set it to True in case we want to allow our class to create
    # deep copies of its objects. By default, it is set to False
    @private_attributes_decorator.private_attributes_dec("a")
    class Example:
        def __init__(self):
            self.a: int = 12
            self.b: int = 12
            self.c: int = 12
            self.__d: int = 12
            self.__e: int = 12
    e: Example = Example()
    # Case 1.1: Trying to access the private attribute outside the class -> We will raise an AttributeError
    try:
        print(e._Example__d)
    except AttributeError:
        assert True
        print("The attribute __d (_Example__d) can't be accessed outside the class")
    else:
        assert False
    # Case 2.1: We try to access a public attribute that we altered to make private using the arguments in the decorator
    # -> We raise an AttributeError
    try:
        print(e.a)
    except AttributeError:
        assert True
        print("The attribute a can't be accessed outside the class")
    else:
        assert False
    # Case 6: We try to do a deepcopy of an object, but we set some parameters as private in its class and did not
    # set the attribute allow_deep_copy to True
    @private_attributes_decorator.private_attributes_dec("arg1")
    class NewExample:
        def __init__(self,arg1: int, arg2: int, arg3: int):
            self.arg1: int = arg1
            self__arg2: int = arg2
            self.arg3: int = arg3
    import copy

    ne: NewExample = NewExample(1,2,3)
    # Case 6.1: We try to do a deepcopy of an object, but we set some parameters as private in its class and did not
    # set the attribute allow_deep_copy to True -> deepcopy raises a copy.Error Exception
    try:
        nec = copy.deepcopy(ne)
    except copy.Error:
        print("We did not allow for deep copies so the method raised a copy.Error Exception")
        assert True
    else:
        print("We did not allow for deep copies, but the deep copy was produced. Something is not right here")
        assert False
    # Case 7: We allowed deep copies in our class and we try to do a deepcopy of an object, we set the some parameters
    # as private in its class
    @private_attributes_decorator.private_attributes_dec("arg1",allow_deep_copy=True)
    class NewExampleAllowDeepCopy:
        def __init__(self,arg1: int, arg2: int, arg3: int):
            self.arg1: int = arg1
            self__arg2: int = arg2
            self.arg3: int = arg3


    ned: NewExampleAllowDeepCopy = NewExampleAllowDeepCopy(1, 2, 3)
    # Case 7.1: We allowed deep copies in our class and we try to do a deepcopy of an object, we set the some parameters
    # as private in its class. We try to create a deepcopy of the object -> The copy is created
    try:
        nedc = copy.deepcopy(ned)
    except copy.Error:
        print("We allowed for deep copies but the method raised a copy.Error Exception, something is wrong")
        assert False
    else:
        print("The copy was created without issues")
        print(nedc)
        assert True
    # For more examples and information check the tests in the source file
```

## Contributing
For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.

## License
[MIT](https://choosealicense.com/licenses/mit/)
