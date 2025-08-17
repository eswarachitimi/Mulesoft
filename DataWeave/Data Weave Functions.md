# DataWeave Functions

You can define your own DataWeave functions using the `fun` declaration in the header of a DataWeave script.

<img width="978" height="601" alt="image" src="https://github.com/user-attachments/assets/fa316740-0945-4c0e-83c1-1bc586797e9f" />

<img width="1007" height="745" alt="image" src="https://github.com/user-attachments/assets/bac382e2-3555-45e2-8e6f-d71043c5b010" />

<img width="1012" height="509" alt="image" src="https://github.com/user-attachments/assets/dd41e708-07fc-4934-8eef-0ccfff7f3689" />

<img width="1005" height="968" alt="image" src="https://github.com/user-attachments/assets/6ddffde9-501e-4c75-8ea0-760b7ba6dfae" />

There are several ways to import a module or elements in it:

- Import the module, for example: `import modules::MyModule`. In this case, you must include the name of the module when you call the element (here, a function) in it, for example: `MyModule::myFunc`.

- Import all elements from the module, for example: `import * from modules::MyModule`. In this case, you do not need to include the name of the module when you call the element. For example: `myFunc("dataweave") ++ "name"` works.

- Import specific elements from a module, for example: `import myFunc from modules::MyModule`. In this case, you do not need to include the name of the module when you call the element. For example: `myFunc("dataweave") ++ "name"` works. You can import multiple elements from the module like this, for example: `import myFunc someOtherFunction from modules::MyModule` (assuming both myFunc and someOtherFunction are defined in the module).
