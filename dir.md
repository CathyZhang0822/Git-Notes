## Get all object attributes in Python?
Use the built-in function `dir()`.    
https://docs.python.org/3/library/functions.html#dir
```python
>>> dir(value1)
['__add__', '__class__', '__contains__', '__delattr__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__getitem__', '__getnewargs__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__iter__', '__le__', '__len__', '__lt__', '__module__', '__mul__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__rmul__', '__setattr__', '__sizeof__', '__slots__', '__str__', '__subclasshook__', '_asdict', '_field_defaults', '_fields', '_fields_defaults', '_make', '_replace', 'checksum', 'count', 'headers', 'index', 'key', 'offset', 'partition', 'serialized_header_size', 'serialized_key_size', 'serialized_value_size', 'timestamp', 'timestamp_type', 'topic', 'value']
```
