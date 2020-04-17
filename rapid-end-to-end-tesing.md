<h1>End to End Testing Flow and Test Cases</h1>

| Components  | SPOCs / Owners |
| ------------- | ------------- |
| Inventory Visibility Application | Prithi Krishnaswamy |
| OMS Business User Control (BUC) | Shishir Saha |
| App Connect Flow | Bharat Balothia & Hari Krishna Kothamasam  |
| SCBN Flow | Neil Hubbard & Venkat Potluri & Amit Saini |


Test Cases:
App Connect to IV

Call App Connect Flow to Post the to IV using Postman

Onboarding Test Cases:
Onboarding using Scripts and Manually.

__1. Happy Path:__

   1. Upload a Solution Defined Formatted CSV file from SCBN's and the Quantities of all the SKU's for all the Ship Nodes should be reflected in BUC UI.
   2. Upload a Solution Defined Formatted CSV from SCBN with one Line Item and with one 
   
   
<h3>App Connect Test Cases:</h3>

__Note: Currently App Connect is not protected with any Authentication Mechanism, so there is no need of passing any authetication bearer token etc.__

   1. Call App Connect flow using Postman Client with 
   2. Malformed CSV inside the JSON Payload so CSV Parser can be failed in that case.
   3. Mailslot ID is not present in the payload
   4. Customer ID (First Row, First Column of the CSV payload) not present in the payload
   5. Token generation NodeJS Services is down
   6. Supplier ID (First Row, Second Column of the CSV payload) is supploed correctly but that is no onboarded in MongoDB Expected Result (HTTP 400 "Supplier ID not found in Token service. Please onboard supplier")
   7. Supplier ID returned by Token Service is not matching with the Supplier ID (first row Second Column value) present in CSV payload. Expected Result (HTTP 400 "Supplier ID from token service. is not matching with Supplier ID in Payload)
   8. Provide mailformed date in any of the date column of any of the row in CSV payload while calling the App Connect API
   9. Validate data in IV either manually or by calling IV API to check that App Connect is inserting the data correctly for following conditions
      "available from" Is greater than current date then set type = WIP else ONHAND"
      "available from" is less than current date then set eta = "1900-01-01T00:00:00Z" else "available from"

      
What if:
When The item rows are present but missing some mandatory data fields like:
Item ID
Quantity
Location ID
Available From
Supplier ID
When Token Generation Service Returns the Supplier ID based on the Mailslot ID Input but does not respond wither URL or Bearer Token
When IV is down or a wrong / malformed IV URL supplied by Token Service
 

   
   
   ```json
      
   {
      "MSlotID": "SJNG7A01",
      "Payload": "supplier id, customer id, location id, item id,product class, quantity,uom,available from
      KC,scbn_3,DALLAS,46827,NEW,15,UNIT,1900-01-01T00:00:00
      KC,scbn_3,DALLAS,46828,NEW,33,UNIT,1900-01-01T00:00:00
      KC,scbn_3,DALLAS,46867,NEW,23,CASE,1900-01-01T00:00:00
      KC,scbn_3,DALLAS,47424,NEW,24,UNIT,1900-01-01T00:00:00
      KC,scbn_3,DALLAS,62126,NEW,25,UNIT,2020-04-12T00:00:00
      KC,scbn_3,DALLAS,62355,NEW,26,UNIT,1900-01-01T00:00:00"
   }
   
   ```

  
   https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/3e595d26cea339a4f91ccb59b8eda6b8204c53eee08371b9e68d47967bfa21e6/NOIW5t/SCBNtoIV


