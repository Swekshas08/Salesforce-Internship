Create a contact test factory.
Create an Apex class that returns a list of contacts based on two incoming parameters: one for the number of contacts to generate, and the other for the last name. The list should NOT be inserted into the system, only returned. The first name should be dynamically generated and should be unique for each contact record in the list.
The Apex class must be called 'RandomContactFactory' and be in the public scope.
The Apex class should NOT use the @isTest annotation.
The Apex class must have a public static method called 'generateRandomContacts' (without the @testMethod annotation).
The 'generateRandomContacts' method must accept an integer as the first parameter, and a string as the second. The first parameter controls the number of contacts being generated, the second is the last name of the contacts generated.
The 'generateRandomContacts' method should have a return type of List<Contact>.
The 'generateRandomContacts' method must be capable of consistently generating contacts with unique first names.
For example, the 'generateRandomContacts' might return first names based on iterated number (i.e. 'Test 1','Test 2').
The 'generateRandomContacts' method should not insert the contact records into the database.


Solution: 

1.RandomContactFactory.apxc
```
public class RandomContactFactory {
public static List<Contact> generateRandomContacts(Integer numContactsToGenerate, String FName) {
        List<Contact> contactList = new List<Contact>();
        
        for(Integer i=0;i<numContactsToGenerate;i++) {
            Contact c = new Contact(FirstName=FName + ' ' + i, LastName = 'Contact '+i);
            contactList.add(c);
            System.debug(c);
        }
        //insert contactList;
        System.debug(contactList.size());
        return contactList;
    }

}
```
OR
```
public class RandomContactFactory {
    public static List<Contact> generateRandomContacts(Integer NumberofContacts, String lName){
        List<Contact> con = new List<Contact>();
        for(Integer i=0; i<NumberofContacts; i++){
            lName = 'Test'+i;
            Contact c = new Contact(FirstName=lName, LastName=lName);
            con.add(c);
        }
        return con;
    }

}
```
