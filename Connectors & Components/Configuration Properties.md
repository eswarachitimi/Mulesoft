MuleSoft has the ability to configure properties that can be used throughout your integration flows. Properties are key-value pairs that can be used to store configuration data such as database connection details, API keys, and more.

#### Points to remember before creating Configuration Files -

- It is advisable to create any configuration file under `src/main/resources/`. I prefer keeping all the configuration files under separate folders and I use the following path `src/main/resources/config/`.
- It is advised that we should separate all the plain text properties and encrypted properties into different files for different environments.
- `dev.yaml` will contain all dev-related properties which are in plain text format.
- `dev-secure.yaml` will contain all dev-related encrypted properties.
- The above points are similar for different environments and `.properties` files as well.
- Any common properties among all environments need to go into a separate common configuration file. I prefer them in `common.yaml` or `common.properties` (Name can be anything that makes sense).

![image](https://github.com/user-attachments/assets/af65d441-a26a-4e4d-8b7c-812492b7a768)

- While configuring the Configuration Properties in global elements, make sure the reference to the common configuration file is at last in order of elements.

![image](https://github.com/user-attachments/assets/eb17b66f-5a56-438d-82a2-b13e583b86a4)

- This order allows mule runtime to properly override any property which is declared in both common & environment-specific files and consider the value only from env specific configuration file.

#### Setup Properties in YAML File -

YAML is a popular human-readable data serialization format that can be used to configure properties in MuleSoft. To create a YAML file for your properties, follow these steps:

- Create a new file with an `.yaml` extension in your MuleSoft project.
- Define your properties in the YAML format, using the `key: value` notation. For example

 ``` 
database:
  host: "localhost"
  port: "3306"
  username: "admin"
```

- Save the YAML file.

> **_⚠ Note :_** Make sure you provide a space after : before writing a value.

#### Setup Properties in the Properties File -

Another way to configure properties in MuleSoft is by using a `.properties` file. To create a properties file for your properties, follow these steps:

- Create a new file with an `.properties` extension in your MuleSoft.
- Define your properties using the key=value notation. For example:

```
database.host=localhost
database.port=3306
database.username=admin
```

- Save the properties file.

#### Adding .yaml or .properties files to Global Elements -

- Navigate to Global Elements Tab in Mule XML file. It is advisable to create a separate XML file just for configuring Global elements.
- Click on Create and choose Configuration Properties and choose the file you want to refer to.

![image](https://github.com/user-attachments/assets/a681d7cc-21a0-4344-848c-6f8cc68d81f2)

  Steps to follow to create Configuration Properties Type

![image](https://github.com/user-attachments/assets/22b477cb-be70-4646-b878-7fb489db4b8c)

![image](https://github.com/user-attachments/assets/4dcbad1d-2f47-4793-b3a0-c433e998ce02)

  - But, we need to dynamically assign the configuration file. So, we need to add the mule.env placeholder instead of dev in the path and the File location looks like this

- Dynamic location for Plain Properties

![image](https://github.com/user-attachments/assets/5c77f24d-ca1f-4415-b55b-0506042df7c2)

- Dynamic location for Secure Properties

![image](https://github.com/user-attachments/assets/9a8f7ce4-c239-4df1-8c6c-07f04ef9424b)

> The similar kind of configuration will be done even for `.properties` files.

#### Accessing Properties in Mule flows -

Once all required global elements are declared we can use any of the following ways to access properties in a properties file:

- Properties can be used by referencing the key of the property enclosed in ${}. This will work only if Expression Mode is turned OFF. Here is an example of how to access the host property from the database section of our properties file:

> ${database.host}

- Using Dataweave and the p() function from Mule module. This should be used when Expression mode is turned ON. Here is an example of how to access the host property from the database section of our properties file:
  
> #[p('database.host')]

> #[Mule::p('database.host')]

- Both of the above will return the value localhost. The only difference is the Mule module is by default imported into Dataweave and we need not to explicitly mention it in the function call p() unless you want to create another function with the name p(). But, It’s always a best practice to use the function with Module Name as runtime will understand where to get this function from.

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

#### Accessing Secure Properties -

In some cases, you may need to store sensitive data 🤐 such as passwords, API keys, or other secrets. To keep this data secure, you can use the MuleSoft Secure Property Placeholder (SPP). The SPP allows you to encrypt your properties and access them securely in your integration flows.

Consider the following `mule.key` as a Secret key for Dev, which we use to encrypt the values. The following values will be passed as Runtime Arguments when deploying the Mule Application.

```
mule.env=dev
mule.key=MySuperSecretKey
```

> Note that you should replace `MySuperSecretKey` it with your secret key in your application.

> `mule.key & mule.env` are used for general represetation of secret key and environment name. You can use any variable name you wish and pass them as runtime arguments.

- Encrypt your properties by following the instructions given on the below page.

> If you use the $ character in your key, you must precede it with \. For example, to use key myKey#$%123, you must specify the <key> parameter as myKey#\$%123.

![image](https://github.com/user-attachments/assets/0af3503f-62c1-480b-9508-87a4cbd68647)

1. By using the Blowfish method and CBC state we will get `5BhrtU8SGibB5mE5P0m27w==` for `db.password=password`.
2. Save the encrypted property value in your file. For example:

#### YAML File:

```
database:
  password: "![5BhrtU8SGibB5mE5P0m27w==]"
```

#### Properties File:

```
database.password=![5BhrtU8SGibB5mE5P0m27w==]
```

- Access your encrypted property in your integration flows using the `secure::` prefix. For example:

```
${secure::database.password}
or
#[p('secure::database.password')]
or
#[Mule::p('secure::database.password')]
```

This will decrypt the database.password as password.
