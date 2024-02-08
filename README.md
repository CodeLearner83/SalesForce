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
#### Example
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


