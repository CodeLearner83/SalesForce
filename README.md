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

## Trigger

#### Syntax

```
trigger <trigger-name> on <standard-or-custom-object> (<trigger-type>) {
  // loigc
}
```
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







