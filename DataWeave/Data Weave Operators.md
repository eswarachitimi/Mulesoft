# Update Operator

DataWeave supports the `update` operator, which enables you to update specified fields of a data structure with new values.

The `update` operator simplifies the syntax:

```
%dw 2.0
var myInput = {
    "name": "Ken",
    "lastName":"Shokida",
    "age": 30
}
output application/json
---
myInput update {
    case age at .age -> age + 1
}
```

With `update`, casting or iterating through all the key-value pairs is not necessary.

The update syntax is as follows:

```
<value_to_update> update {
    case <variable_name> at <update_expression>[!]? [if(<conditional_expression>)]? -> <new value>
    ...
}
```
- `value_to_update` represents the original value to update.

- `update_expression` is the selector expression that matches a value in value_to_update.

- `variable_name` is the name of the variable to bind to the matched update_expression value.

- `new_value` is the expression with the new value.

- `[if(<conditional_expression>)]?` If conditional_expression returns true, the script updates the value. Use of a conditional expression is optional.

[!] marks the selector as an upsert. If the expression doesn’t find a match, the ! makes the update operator create all the required elements and insert the new value.

update_expression supports multiple case expressions.

The update operator doesn’t mutate the existing value. Instead, the operator creates a new value with the updated expressions.
