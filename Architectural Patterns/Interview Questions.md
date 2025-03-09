Data Integration Patterns in MuleSoft?

 Data integration makes data agnostic — so it can be accessed and handled with ease. So, developers can use these data integration patterns to standardize the integration process.
 
Data Integration Patterns include:

 1. Migration.
 2. Broadcast.
 3. Aggregation.
 4. Bi-directional.
 5. correlation.
 6. Filtering.
 7. proxy.
 8. Transformation.
 9. Routing.
 10. Normalisation.
 
 #### Migration pattern.
 This pattern is used to create a migration flow where data is retrieved from one system and inserted into another system. Eg: retrieve data from salesforce and insert it into MySQL database. 

 
 #### Broadcast pattern:
 This pattern is used where data is retrieved from one system and inserted into multiple systems in the same time. Eg: Retrieve data from MySQL and insert it to Salesforce, AWS database, and SAP systems.

 
 #### Aggregation pattern:
 This pattern is used where data is retrieved from multiple systems and inserting it into one system. Eg: Customer details can retrieved from salesforce, AWS database, and SAP and then inserted into MySQL database.
 
 
 #### Bi-directional pattern:
 This pattern is used where data changes are synchronized in both directions. Eg: Transferring data between Marketo and Salesforce in a synchronized way. Updating customer data in both Salesforce and SAP.


 #### Correlation pattern: 
 Same as a bi-directional pattern, but only syncs when the same item exists in two systems naturally. Eg: Both Marketo and Salesforce has Account object, so it can synchronize easily using correlation pattern. Also, custom objects can be created to sync two systems manually using correlation patterns.
 

 #### Filtering pattern:
 Filtering involves selectively extracting specific data from a larger dataset based on defined criteria. This pattern is useful for retrieving relevant information without transferring unnecessary data. Eg: Using the filter in dwl to filter the particular ID data in DB, Salesforce.
