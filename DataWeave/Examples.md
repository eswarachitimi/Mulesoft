[{
"Fruit" : "apple",
"quantity" : "14"
},
{
"Fruit" : "orange",
"quantity" : "13"
},
{
"Fruit" : "apple",
"quantity" : "6"
},
{
"Fruit" : "orange",
"quantity" : "12"
}]


[
  {
    "Fruit": "apple",
    "quantity": 20
  },
  {
    "Fruit": "orange",
    "quantity": 25
  }
]

%dw 2.0

fun grouping (inputObj,dynmicString) = ((payload groupBy($.Fruit))[dynmicString])
output application/json
---
payload distinctBy ((item, index) -> item.Fruit) map {
    Fruit : $.Fruit,
    quantity : (grouping (payload,($.Fruit)))..quantity reduce ( $ + $$)
}


fun grouping (inputObj,dynmicString) = ((payload groupBy($.Fruit))[dynmicString])
output application/json
---
payload distinctBy ((item, index) -> item.Fruit) map {
    Fruit : $.Fruit,
    quantity : sum((grouping (payload,($.Fruit)))..quantity)
}
