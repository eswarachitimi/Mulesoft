## Example -1

![image](https://github.com/user-attachments/assets/418bf7a0-be55-463c-be5e-18c98a667e78)

## Example -2

![image](https://github.com/user-attachments/assets/2367cfee-d4f6-4b88-a123-0e97ed4cb677)

## Example -3

![image](https://github.com/user-attachments/assets/7431129b-a974-4ed0-868a-a839ff15484a)

%dw 2.0

fun grouping (inputObj,dynmicString) = ((payload groupBy($.Fruit))[dynmicString])
output application/json
---
payload distinctBy ((item, index) -> item.Fruit) map {
    Fruit : $.Fruit,
    quantity : (grouping (payload,($.Fruit)))..quantity reduce ( $ + $$)
}

## Example -4
