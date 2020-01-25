
# ServiceNow Incident to Salesforce Case Migration	

<!-- Header (start) -->

<!-- Header (end) -->
Moves a large set of Incidents from ServiceNow to Salesforce. Trigger with an HTTP call either manually or programmatically. Incidents are upserted so that the migration can be run multiple times without creating duplicate records. This template uses batch to efficiently process many records at a time.

# Use Case
<!-- Use Case (start) -->
**As a ServiceNow admin I want to migrate incidents to Salesforce**

This template should serve as a foundation for the process of migrating Incidents from a Workday instance to Salesforce. 

As implemented, this template leverages the [Batch Module](http://www.mulesoft.org/documentation/display/current/Batch+Processing).
Firstly will query the Workday for all the existing incidents that match the filtering criteria sent as a request parameter. The criteria is based on manipulations based on ServiceNow Incidents caller Id.
The last step of the Process stage will group the incidents and create them in Salesforce.
Finally, during the On Complete stage, the results of the batch execution will be presented with some statistics data.

# Considerations <a name="considerations"/>

1. **Migrated Cases in SalesForce:** For now, the migrated cases Subject field will be set as 'SFDC_MIGRATION_' + ServiceNow Incident Number. This will be used to check if the incident has been migrated to Salesforce or not. Make sure that the migrated case Subject field does not change after migration, or the incident will be migrated again.  

## Salesforce Considerations <a name="salesforceconsiderations"/>

In order to have this template working as expected, you should be aware of your own Salesforce field configuration.

## ServiceNow Considerations <a name="workdayconsiderations"/>

In order to have this template working as expected, you should be aware of your own ServiceNow field configuration.

### Running <a name="runonmuleesbstandalone"/>
Complete all properties in: mule-artifact.properties. 
After this, to trigger the use case you just need to hit the local http connector with the port you configured in the properties file, then you should hit: `http://localhost:8081/migrate?callerId=ServiceNow_Incidents_CallerId` and this will output a summary report.

## Properties to be configured (With examples) <a name="propertiestobeconfigured"/>
In order to use this Mule template you need to configure properties either in properties file or in CloudHub as Environment Variables. Detail list with examples:

#### ServiceNow Connector 
+ snow.user `snow_user1`
+ snow.password `ExamplePassword881`
+ snow.endpoint `https://instance.service-now.com`

#### Salesforce Connector
+ sfdc.username `user@company.com`
+ sfdc.password `secret`
+ sfdc.securityToken `1234fdkfdkso20kw2sd`
+ sfdc.url `https://login.salesforce.com/services/Soap/u/46.0`

**********************************************************************
* Application plugins:                                              
  - File Common Plugin : 1.2.0                              
  - ObjectStore : 1.1.3                                             
  - ServiceNow : 6.4.0                                              
  - Sockets : 1.1.5                                                 
  - File : 1.2.0                                                    
  - HTTP : 1.5.11                                                   
  - Salesforce : 9.7.10                                             
**********************************************************************