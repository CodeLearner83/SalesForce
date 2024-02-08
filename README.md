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

###
