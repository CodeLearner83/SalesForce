# SalesForce Learning

## Add New Record

> All data which were set in the below are mandatory fields for Student Object.

```
Date d = Date.valueOf('1990-01-01');
Student__c student = new Student__c();
student.Name = 'A1001';
student.Student_Id__c = 1001;
student.DOB__c = d;
student.Email_Id__c = 'A101@xyz.com';

insert student;
```
## SOQL


### Syntax

```
Select id, Name
from <standard-or-custom-object>
where <> Name='abc'
```

```
User u = [Select id, Name from User where Name='abc'];

Account ac = new Account();
ac.Name ='Test';
ac.OwnerId=u.id;

insert ac;
```

## Flow

<ul>
  <li>Fast Field Update - isBefore Operation</li>
  <li>Actions & Releated Records - isAfter Operation</li>
</ul>


## Apex Code


## Trigger
> Trigger executes automatically when ever any DML operations are performed
  > DML Operation : Create Record, Update Record, Delete Record, Undelete
> Are used to perform validation
  > Ex : user entered data is correct, Student Name should not contain any special chars
> Also used to perform automation
  > 

#### Trigger vs Flows

| Trigger   | Validation Rules/Flows |
| :---   | :--- | 
| All DML operation (including delete & undelete) | insert & update only | 
| Any object | one object & associated parent only | 
| write apex code | no apex code | 
| if requirement is not met with validation rules | simple requirements only |

#### Trigger Context Variables
> a group of variables that will be available which hold runtime/background information of the current trigger when it is running/executing
> Below table 

| Trigger Context Variables   | Data Type | Notes|
| :---   | :--- | :---: | 
| isInsert | Boolean| 
| isUpdate |Boolean| 
| isDelete |Boolean|
| isBefore |Boolean|
| isAfter |Boolean|
| old |List| <ul><li>Data Variables, which stored record information</li><li>data before DML operation</li></ul>
| new |List| <ul><li>Data Variables, which stored record information</li><li>data after/during DML operation</li></ul>
| oldmap |Map| <ul><li>Data Variables, which stored record information</li><li>Map key contains id, Map value contains old data</li></ul>
| newmap | Map|<ul><li>Data Variables, which stored record information</li><li>Map key contains id, Map value contains new data</li></ul>
| isExecuting |Boolean |
| size | integer |

```
- Insert Operation - Always have new data (new & newmap)
- Delete Operation - Always have old data (old & oldmap)
- Update Operation - Both old data & new data (old|oldmap & new|newmap) . Ex : Address Update - where old address will be in the old & oldmap, new address data will be new & newmap
```

#### Trigger Syntax

```
// 1 event type parameter
trigger <trigger-name> on <standard-or-custom-object> (<event-type>) {
  // loigc
}

// multiple events type parameter
trigger <trigger-name> on <standard-or-custom-object> (<event-type-01>, <event-type-02>, <event-type-03>) {
  // loigc
}
```

 > Event Type informatiom

```
- before insert - used for field validation & field updates
- after insert - multiple objects & automations. Ex : add into new other objects
```


#### Trigger Event Types

| #    | Event Name | Notes|
| :---   | :--- | :--- |
| 1   | beforeInsert |  |
| 2   | beforeUpdate |  |
| 3   | beforeDelete |  |
| 4   | afterInsert |  |
| 5   | afterUpdate |  |
| 6   | afterDelete |  |
| 7   | afterUndelete |  |



#### Example - Trigger Code
> Below trigger will be fired when user tries to insert new record into the system
> Note
  > Below trigger will change the user entered email id with the email mentioned in the trigger

```
trigger StudentTrigger on Student__c (before insert) {
    string emailId = 'trigger-before-insert@xyz.com';
    if(trigger.IsInsert && trigger.IsBefore) {
        for(Student__c sp:Trigger.new){
          sp.Email_Id__c = emailId;
        }
    }
}
```

#### Example - Trigger Test Code

```
Date d = Date.valueOf('1990-01-01');
Student__c student = new Student__c();
student.Name = 'A1001';
student.Student_Id__c = 1001;
student.DOB__c = d;
student.Email_Id__c = 'A101@xyz.com';

insert student;    
```


#### Testing in Dev Console

| #   | Step Name   | Code    |
| :---:   | :--- | :--- |
| 1 | Login to Developer Console  |    |
| 2 | Create Apex Trigger  | File ->  Apex Trigger  |
| 3 | Add Details in Popup Dialog  | Name = Any Name, sObject = Select the object on which you want to create the trigger  |
| 4 | Add Trigger Code  | Refer to the "Example - Trigger Code" section above |
| 5 | Save  | File -> Save |
| 6 | Test Step # 01  | File -> Debug -> Open Execute Anonymous Window|
| 7 | Test Step # 02  | Add Code to Test, refer tp "Example - Trigger Test Code" section above|
| 8 | Verify  | Goto Object and verify the record is present |







