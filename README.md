# How-to-Clone-Zoho-CRM-Records
A simple and effective Deluge script that lets you clone records (with or without some changes).

## Core Idea
Here's a quick, easy, no-frills method to clone/duplicate a Zoho CRM record via Deluge. The idea is to get the full JSON map of the record, make changes to the record map (if necessary), and create the new record.

## Tutorial
### Get Record Information
We use the `getRecordsbyId` Deluge task to get the complete map of the record information.
```javascript
record = zoho.crm.getRecordById("CRM_Module_Name","Record_ID");
info record;
```

### Make Changes to the Data if Necessary
We can modify the record data by using the `put` and `remove` function. 

#### To Modify the Value of Keys
In order to change the value of a key, use the `put` function to assign a new value to the key. 
For example, if your new record is to be called "{Record Name} - Copy", this is how the script would look like.
```javascript
record.put("Name",recordData.get("Name") + " - Copy";
```
You can replace the value of as many keys as you want.
```javascript
record.put("Stage","Closed Won");
record.put("Closing Date",today);  
```
You can also reassign lookup fields by reassigning the value of the lookup map with the new ID (the ID alone is sufficient).
```javascript
record.put("Account_Id",{"id","Replacement_Account_ID"});  
```
  
#### To Remove Fields
If you want to exclude certain fields from the cloned record, simply remove the key from the record map using the `remove` function.
```javascript
record.remove("Currency");
```

### Create the New "Cloned" Record
Once you are done modifying the record map, create the new "cloned" record using the `createRecord` Deluge task with the record map.
```javascript
newrecord = zoho.crm.createRecord("CRM_Module_Name", record);
info newrecord;
```

*Note: When creating clone/duplicate records, keep in mind that you may have unique field(s) set up in your module. To successfully create the cloned record, you need to make sure that you modify the value of the field(s).*
