### Differences in Extracting property values using $​{ } and p('​ '​) | Mule 4 

We all know that we can extract property values from property file or vault by two ways . either by ${} or p(' ') .

**_Note :_**  Either of the cases , we have to restart the application if there are any changes made in property file to get the new values reflected

##### _Difference 1 :_

- ${} can be used any where at any place , either in configuration or in dataweave etc.
- p(' ') can only be used in DataWeave expression Language scope. i.e, within #[]

> For eg : Check the Connection idle Timeout field :

> It doesn't support expression language . So, ${} alone will work

![image](https://github.com/user-attachments/assets/c43a732d-4617-43e6-a184-de2e78ebffce)

> p(' ') doesn't work :

![image](https://github.com/user-attachments/assets/cc21b2d1-0672-4607-9f12-a5be8f14e96f)

##### _Difference 2 :_

If you are extracting a key using ${} which is not present in property file, then your application will fail to deploy saying couldn't find config property..

If you are extracting a key using p(' ') which is not present in property file, then your application will NOT fail to deploy . Instead it treats as null value .

> For eg: I have a config.properties file where i have a key called "message"

![image](https://github.com/user-attachments/assets/abfaeb82-a7cb-4235-9abf-aab6c73cf3ab)

> If i try to extract a key "message1" which is not actually present in config file, then it fails to deploy

![image](https://github.com/user-attachments/assets/37611395-3e92-4a09-81ce-d6e8c564f26a)

![image](https://github.com/user-attachments/assets/6f70fabe-da36-410d-815a-2f665b29055e)

> If you use p(' ') to extract a key which is not present , the application will deploy but a null value is shown.

![image](https://github.com/user-attachments/assets/e029fa56-d150-4e5e-b309-25ea333bcf81)

![image](https://github.com/user-attachments/assets/ece68027-bfef-40ae-a119-c33cd3133a8b)

When you give proper key names then both behaves in same way. p(' ') is nothing but a function . (Usually whatever functions we write in Dataweave, we notate it with functionName(arguments).

This p(' ') is also a function which accepts a string as an argument .It returns null when no value is found.

