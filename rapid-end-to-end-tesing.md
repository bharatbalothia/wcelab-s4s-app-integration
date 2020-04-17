#End to End Testing Flow and Test Cases

## 1. Component and Component Owners

| Components  | Component Owners |
| ------------- | ------------- |
| Inventory Visibility Application | Prithi Krishnaswamy |
| OMS Business User Control (BUC) | Shishir Saha |
| App Connect Flow | Bharat Balothia & Hari Krishna Kothamasam  |
| SCBN Flow | Neil Hubbard & Venkat Potluri & Amit Saini |

## 2. Testing Guidelines

  1.	Component Owner will develop the test cases or get it done by developer and review.
  1.	Test cases should be tested by someone other than the person who coded or own the component. The test case should be reproduced by the tester based on the document provided by the test case writer.
    
1. ###App Connect Test Cases

>Note: Currently App Connect is not protected with any Authentication Mechanism, so there is no need of passing any authetication bearer token etc.
1. Call App Connect flow using Postman Client with 
1. Malformed CSV inside the JSON Payload so CSV Parser can be failed in that case.
1. Mailslot ID is not present in the payload
1. Customer ID (First Row, First Column of the CSV payload) not present in the payload
1. Token generation NodeJS Services is down
1. Supplier ID (First Row, Second Column of the CSV payload) is supploed correctly but that is no onboarded in MongoDB Expected Result (HTTP 400 "Supplier ID not found in Token service. Please onboard supplier")
1. Supplier ID returned by Token Service is not matching with the Supplier ID (first row Second Column value) present in CSV payload. Expected Result (HTTP 400 "Supplier ID from token service. is not matching with Supplier ID in Payload)
1. Provide mailformed date in any of the date column of any of the row in CSV payload while calling the App Connect API
1. Validate data in IV either manually or by calling IV API to check that App Connect is inserting the data correctly for following conditions
  "available from" Is greater than current date then set type = WIP else ONHAND"
  "available from" is less than current date then set eta = "1900-01-01T00:00:00Z" else "available from"
      
What if:
1.	When the invalid / incomplete rows are present in CSV payload and missing mandatory data fields like:
  1.	Item ID
  1.	Quantity
  1.	Location ID
  1.	Available From
  1.	Supplier ID
1.	When Token Generation Service returns the Supplier ID based on the Mailslot input but does not return URL or Bearer Token or both?
1.	When IV is down or a wrong / malformed IV URL supplied by Token Service?
	 

   __Sample JSON Data which SCBN pushes to App Connect__
   
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
   [App Connect Dev API](https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/3e595d26cea339a4f91ccb59b8eda6b8204c53eee08371b9e68d47967bfa21e6/NOIW5t/SCBNtoIV)
   

<h3>Supplier Onboarding Test Cases:</h3>

End to End Test Cases:

Call App Connect Flow to Post the to IV using Postman

Onboarding Test Cases:
Onboarding using Scripts and Manually.

__1. Happy Path:__

   1. Upload a Solution Defined Formatted CSV file from SCBN's and the Quantities of all the SKU's for all the Ship Nodes should be reflected in BUC UI.
   2. Upload a Solution Defined Formatted CSV from SCBN with one Line Item and with one 


#### Resources:
  
1. [Mindmap and Test Cases Spreadsheet](https://ibm.ent.box.com/file/647930438099)
1. [Demo Data](https://github.ibm.com/wcelab/S4S-PerformanceTesting/tree/master/demo_data)




