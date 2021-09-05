# PrivateAttributesProject
 Module to increase encapsulation in Python, not allowing the access to private members outside their classes


## Installation

Use the package manager [pip](https://pip.pypa.io/en/stable/) to install PrivateAttributesProject.

```bash
pip3 install PrivateAttributesProject
```

## Usage

```python
    @private_attributes_dec("a")
    class Example:
        def __init__(self):
            self.a: int = 12
            self.b: int = 12
            self.c: int = 12
            self.__d: int = 12
            self.__e: int = 12
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
        print(e._Example__d)
    except AttributeError:
        assert True
        print("The attribute __d (_Example__d) can't be accessed outside the class")
    else:
        assert False
```

## Contributing
For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.

## License
[MIT](https://choosealicense.com/licenses/mit/)