Create a unit test for a simple Apex trigger.
Install a simple Apex trigger, write unit tests that achieves 100% code coverage for the trigger, and run your Apex tests.
The Apex trigger to test is called 'RestrictContactByName', and the code is available here. Copy and paste this trigger into your Developer Edition via the Developer Console.
'RestrictContactByName' is a trigger which blocks inserts and updates to any contact with a last name of 'INVALIDNAME'.
The unit tests must be in a separate Apex class called 'TestRestrictContactByName'.
The unit tests must cover scenarios for all lines of code included in the Apex trigger, resulting in 100% code coverage.
Run your test class at least once (via 'Run All' tests the Developer Console) before attempting to verify this challenge.

Solution:

1.RestrictContactByName.apxc
```
	trigger RestrictContactByName on Contact (before insert, before update) {
	
	//check contacts prior to insert or update for invalid data
	For (Contact c : Trigger.New) {
		if(c.LastName == 'INVALIDNAME') {	//invalidname is invalid
			c.AddError('The Last Name "'+c.LastName+'" is not allowed for DML');
		}

	}

}
```
2.TestRestrictContactByName.apxc

```
@isTest
public class TestRestrictContactByName {
static testMethod void  Test() 
    {
    
        List<Contact> listContact= new List<Contact>();
        Contact c1 = new Contact(FirstName='Raam', LastName='Leela' , email='ramleela@test.com');
        Contact c2 = new Contact(FirstName='gatsby', LastName = 'INVALIDNAME',email='gatsby@test.com');
        listContact.add(c1);
        listContact.add(c2);
        
        Test.startTest();
            try
            {
                insert listContact;
            }
            catch(Exception ee)
            {
            }
        
        Test.stopTest(); 
        
    }
}
```
