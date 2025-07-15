## BMML Conditions

In Bizmanage we allow to set advanced condtions written in the following described syntax.

Currently we support the it with conditional rendering at the form setup.

### Syntax

The syntax is based on the following:

- '' - a string should be wrapped with single quotes
- `()` - a full condition or condition set should be wrapped with parenthesis
- `AND` - used to define AND conditions
- `OR` - used to define OR conditions
- `IS_EQUALS` - used to define equality (case insensitive and ignores sorrounding spaces)
- `IS_NOT_EQUALS` - used to define inequality (case insensitive and ignores sorrounding spaces)
- `BEGINS_WITH` - used to define that the value begins with the given string (case insensitive and ignores sorrounding spaces)
- `ENDS_WITH` - used to define that the value ends with the given string (case insensitive and ignores sorrounding spaces)
- `IS_EMPTY` - used to define that the value is empty (case insensitive and ignores sorrounding spaces)
- `IS_NOT_EMPTY` - used to define that the value is not empty (case insensitive and ignores sorrounding spaces)

Rules:
* variables are available based on context (in a form, all the fields are available)
* A condtion can be 3 words seperated by spaces. The first word is the field name, the second word is the operator and the third word is the value.
* When you combine conditions or condition groups you must use parenthesis.
* double spaces are ignored.
* a new line is considered as a space.
* An empty string is a valid condition, and it eveluates to true.
* We support strings (single quotes), numbers, booleans (true/false);


Example:

``(field1 IS_EQUALS 'value1')``

This means that the value of field1 is equal to 'value1'.


``(field1 IS_EQUALS true)``
This means that the value of field1 is equal to true.

``(field1 IS_EQUALS false)``
This means that the value of field1 is equal to false.

``(field1 IS_EQUALS 1)``
This means that the value of field1 is equal to 1.

``(field1 IS_EQUALS 'value1') AND (field2 IS_EQUALS 'value2')``

``(field1 IS_EQUALS 'value1') AND (field2 IS_NOT_EQUALS 'value2')``

This means that the value of field1 is equal to 'value1' and the value of field2 is not equal to 'value2'.

``(field1 IS_EQUALS 'value1') OR (field2 IS_NOT_EQUALS 'value2')``

This means that the value of field1 is equal to 'value1' or the value of field2 is not equal to 'value2'.

``(field1 IS_EQUALS 'value1') AND (field2 IS_NOT_EQUALS 'value2') AND (field3 IS_EQUALS 'value3')``

This means that the value of field1 is equal to 'value1' and the value of field2 is not equal to 'value2' and the value of field3 is equal to 'value3'.

``((field1 IS_EQUALS 'value1') AND (field2 IS_NOT_EQUALS 'value2')) OR (field3 IS_EQUALS 'value3')``
This means that the value of field1 is equal to 'value1' and the value of field2 is not equal to 'value2' or the value of field3 is equal to 'value3'.

``(field1 IS_EMPTY) AND (field2 IS_NOT_EMPTY)``
This means that the value of field1 is empty and the value of field2 is not empty.


Order of operations:
- `()` - parenthesis
- `AND` - AND
- `OR` - OR