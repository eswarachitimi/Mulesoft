* DataWeave is a programming language designed for transforming data. It is MuleSoft’s primary language for data transformation, as well as the expression language used to configure components and connectors within Mule.

![image](https://github.com/user-attachments/assets/9ff87642-4e95-452c-a0b0-0101bb2b10fd)

* DataWeave allows you to easily read, manipulate, and write data in any format.

* Inputs and outputs are critical in DataWeave.

* DataWeave scripts act on data (payload ) in the Mule event.

Notice in the dw script that there are three lines, a line with three dashes, then one more line. The first three lines of the script contain *directives*. The first directive, which is in every DataWeave file, defines which version the script is using.

The second and third lines contain the input and output directives. They each have their own form, which allows naming the inputs and defining reader and writer properties:

`input <var_name> <mime_type> [<reader_properties>]`

`output <mime_type> [<writer_properties>]`

After the first three lines of the script there is a line only containing three dashes. This is to separate your declarations from your script output logic, sometimes called the header and the body of the script respectively.

Finally, the last line of the script is the output section. Whatever the output section evaluates to is what gets sent to the writer, and is ultimately serialized into the specified output format.

![image](https://github.com/user-attachments/assets/0704e88e-267a-41e6-9e52-01afb12a760a)

![image](https://github.com/user-attachments/assets/595e9f0c-7210-45f6-89a9-a033d1cd2b80)

![image](https://github.com/user-attachments/assets/fb4e81b3-6cde-41fd-94b8-570f46cf378b)

![image](https://github.com/user-attachments/assets/8c0a8615-1f29-479f-aad6-a831a0eba473)

![image](https://github.com/user-attachments/assets/b7fdd884-79b3-4ea1-b448-e53aee582681)

![image](https://github.com/user-attachments/assets/c08d50ef-944a-4fea-a4e6-b4d7c9bd4fa7)

