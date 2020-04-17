<h1>End to End Testing Flow and Test Cases</h1>

| Components  | Component Owners |
| ------------- | ------------- |
| Inventory Visibility Application | Prithi Krishnaswamy |
| OMS Business User Control (BUC) | Shishir Saha |
| App Connect Flow | Bharat Balothia & Hari Krishna Kothamasam  |
| SCBN Flow | Neil Hubbard & Venkat Potluri & Amit Saini |

<h2>Testing Guidelines:</h2>
	1.	Component Owner will develop the test cases or get it done by developer and review.
	2.	Test cases should be tested by someone other than the person who coded or own the component. The test case should be reproduced by the tester based on the document provided by the test case writer.


End to End Test Cases:

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
	1.	When the invalid / incomplete rows are present in CSV payload and missing mandatory data fields like:
		1.	Item ID
		2.	Quantity
		3.	Location ID
		4.	Available From
		5.	Supplier ID
	2.	When Token Generation Service returns the Supplier ID based on the Mailslot input but does not return URL or Bearer Token or both?
	3.	When IV is down or a wrong / malformed IV URL supplied by Token Service?
	 

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

<h3>Supplier Onboarding Test Cases:</h3>
  
 Mindmap and a spreadsheet. https://ibm.ent.box.com/file/647930438099
 
 Also put the link the demo data which might be useful to you. https://github.ibm.com/wcelab/S4S-PerformanceTesting/tree/master/demo_data
 
   https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/3e595d26cea339a4f91ccb59b8eda6b8204c53eee08371b9e68d47967bfa21e6/NOIW5t/SCBNtoIV


