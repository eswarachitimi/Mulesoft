# DataWeave Functions

You can define your own DataWeave functions using the `fun` declaration in the header of a DataWeave script.

## DataWeave Function Definition Syntax

<img width="966" height="482" alt="image" src="https://github.com/user-attachments/assets/9823eff2-6dcb-4401-b3f4-460c7071807a" />

## Example Function Definitions

<img width="969" height="494" alt="image" src="https://github.com/user-attachments/assets/01e66030-f1c0-46a6-a554-a9d3377d2511" />

## Type Constraint Definition

<img width="987" height="595" alt="image" src="https://github.com/user-attachments/assets/b3f6d604-2d54-4140-9040-0c6ab1a7de3a" />

## Custom Modules

In addition to using the built-in DataWeave function modules (such as `dw::Core` and `dw::Crypto`), you can also create and use custom modules and mapping files. The examples demonstrate common data extraction and transformation approaches.

You write modules and mapping files in a DataWeave Language (.dwl) file and import into your Mule app through DataWeave scripts in Mule components. Both modules and mapping files are useful when you need to reuse the same functionality or feature over and over again.

- Custom modules can define functions, variables, types, and namespaces. You can import these modules into a DataWeave script to use the features.

## Creating and Using DataWeave Mapping Files

<img width="1014" height="650" alt="image" src="https://github.com/user-attachments/assets/c6184927-da2a-4ca2-8590-c3d8f4c930ae" />

<img width="1005" height="968" alt="image" src="https://github.com/user-attachments/assets/6ddffde9-501e-4c75-8ea0-760b7ba6dfae" />

## Creating and Using a Custom Module

A custom module file can only contain `var`, `fun`, `type`, and `ns` declarations, for example:

```
%dw 2.0
var name = "MyData"
fun myFunc(myInput: String) = myInput ++ "_"
type User = {
    name: String,
    lastname: String
}
ns mynamespace http://acme.com/bar
```

When you import a custom module into another DataWeave script, any functions, variables, types, and namespaces defined in the module become available for use in the DataWeave body. In the next example, a DataWeave script:

Imports the module `MyModule` through the import directive in the header. In this case, the imported module is stored in a Studio project path `src/main/resources/modules/MyModule.dwl`

Calls a function in MyModule by using `MyModule::myFunc("dataweave")`.

Example: Importing and Using a Custom DataWeave Module

```
%dw 2.0
import modules::MyModule
output application/json
---
MyModule::myFunc("dataweave") ++ "name"
```

There are several ways to import a module or elements in it:

- Import the module, for example: `import modules::MyModule`. In this case, you must include the name of the module when you call the element (here, a function) in it, for example: `MyModule::myFunc`.

- Import all elements from the module, for example: `import * from modules::MyModule`. In this case, you do not need to include the name of the module when you call the element. For example: `myFunc("dataweave") ++ "name"` works.

- Import specific elements from a module, for example: `import myFunc from modules::MyModule`. In this case, you do not need to include the name of the module when you call the element. For example: `myFunc("dataweave") ++ "name"` works. You can import multiple elements from the module like this, for example: `import myFunc someOtherFunction from modules::MyModule` (assuming both myFunc and someOtherFunction are defined in the module).

## Refer below image for Function over riding, function overloading and  passing function as parameter to function examples -

<img width="1175" height="521" alt="image" src="https://github.com/user-attachments/assets/6f9ba1b9-942e-4881-8d4a-93ea8e8037e7" />
