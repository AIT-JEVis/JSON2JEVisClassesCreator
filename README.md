# JSON2JEVisClassesCreator
Automatically create JEVis-classes as given by json-file

## Structure
There must always be a rootnode given in the JSON-file under which the classes are described to be.

See [create_test_classes.json](create_test_classes.json) for an example on how to create classes.


## Operations
The following commands can be given (default is `0`). The commands are given in the `"operation"` field of the JSON-file

```
private interface OPERATIONS {
        final long CREATE = 0; // or update
        final long IGNORE = -1;
        final long DELETE = -2;
        final long DELETE_RECURSIVE = -3;
        final long RENAME = -4;
    }
```

Note: the operation `RENAME` is not implemented. Pull requests are quite welcome.


### Ignore
Operation `IGNORE` with the value `-1` can be used to describe the structure under which to later create a new class (or delete one).

### Create
the default operation if none is described. Tries to create the described class with all its attributes (keyword `type`), primitive types (keyword `primitiveType`) and valid parents (keyword `validParents`). Other classes under this class can be given in the keyword `children`.

Note: if the class already exists then the creator bails out and processes the next class, thus nothing is changed. Pull requests for update-functionality are welcome.

### Delete
Operation `-2` deletes the described class. Children of this class are then automatically moved to the root.

To delete a class and all sub-classes under the described class use Operation `-3`.

See [delete_test_classes.json](delete_test_classes.json) for an example on how to delete classes.
