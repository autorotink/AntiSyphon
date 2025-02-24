Lab (cont.)
# Lab 003 - Create OUs, users, and groups
## Task 1 Creating Organizational Units (OUs)
- Launch `Active Directory Users and Computers`
- Right-click the domain > Hover over `New` > Select `Organizational Unit`
- Create six OUs: Computers-Clients, Servers, Finance, HR, IT, and Sales.
## Task 2 Creating Groups
- Right-click on a OU > Hover over `New` > Select `Group`
  - Group name, Group Scope: Global, Group Type: Security
  - The lab provides specifics names, etc., for this step.
  - Instead of clicking around, you can use `alt` to try to navigate the menus using just your keyboard.
## Task 3 Creating Users
- Right-click on a OU > Hover over `New` > Select `User`
<img width="265" alt="image" src="https://github.com/user-attachments/assets/234f764b-a4e7-4644-b21f-183f469a463b" />

- The lab provides specific information.  But you're filling out the above!  After you complete the information Select `Next`
- Enter a password, leave `User must change password at next logon` selected. (🐿️ Still can't be something "easy")
- Review the information and Select `Finish`
- The lab continues with more users to add.
- These users will now appear in the right panel of the select OU.
<img width="452" alt="image" src="https://github.com/user-attachments/assets/84b52214-badd-471f-b9b9-b9258963c113" />

- There are plenty more users to add for this lab (in the different OUs, etc), so I'm going to get to it!  You should definiately get your `tab` game on during this, so you can be faster!
## Task 4 Populating Groups
- Select an OU > Right-click on the desired group > Select `Properties`
- Click on the `Members` tab > Select `Add`
- In the dialog box, Enter a name > Click `Check Names` which should return a login for a User > Select `OK` and `OK`
- 🐿️ You can also do this same action by selecting the User and adding them to a group.
- (You have to know the name of the group and/or the name of the user)
- You can double-check your work 
- The lab continues with what group users are part of.
- Nest Groups within other groups!  Complete the same way as above, but instead of User Names, enter the group name and `Check Names` to return the group information.
- 🐿️ Separate different entities with a semi-colon `;`, if needed.
- 🐿️ Should you happen to have created a OU, and left the "Protect object from accidental deletion" on, and you want to delete it:
  - Go to the "View" menu > Select `Advanced Features` > Right-Click the desired object > Select `Properties` > Select the `Object` tab > Deselect `Protect object from accidental deletion`
  - After you're done deleting the unwanted items > Go to the `View` menu > Deselect `Advanced Features` > And you'll be back to your old view!
- Having knowledge about the Organizational Layout for your Organization will certainly help with setting up all the necessary groups and OUs!
## Conclusion
"You’ve successfully created Organizational Units, users, and groups in Active Directory! You can now manage these entities as needed, applying policies and permissions based on your organizational structure."
