🐘 There were quite a few people in the class, so the labs were lagging.  I decided to do the lab after the weekend (hopefully everyone else already did their's!).  The lab instructions are very thorough, with ALL the screenshots!  I'm looking to make this as a quick(-er) reference.

# Lab 001 - Virtual Machine Setup
- I connected to the [MetaCTF Cloud Labs Infrastructure](https://metactf.com/).  Registering was easy, and Antisyphon provided a class code for us to use.
- When using MetaCTF, you don't want to run the labs continuously.  Credits are associated with hours.  So if you run the labs, you'll run out of credits.  You can always [buy more credits](https://app.metactf.com/billing), if you need to!  
- Our particular lab has three different computers:
  - Domain Controller: Manages network security and user authentication within a Windows domain via Active Directory.
  - Member Server: Part of a Windows domain, relies on domain controllers for authentication, and provides services like file sharing.
  - Client: A computer or device that connects to the network and accesses resources provided by domain controllers and member servers.
- Following the lab instructions, I started the lab, and the machines are getting created.
  - I completed this step during class, but the machines are destroyed after 48 hours, so I had to recreate them (it's actually a safeguard in place by MetaCTF to prevent unintended costs.
  - After the machines are created, you select the button: Connect via browser (RDP)
    - There are starting credentials provided, which you can change once you're in the machine.
# Lab 002 - Installing the Domain Controller
## Task 1: Set Static IP Address (Reference Only)
- This is a reference only task for setting up a Static IP address.  (I've actually done this in my Home Lab before!)
## Task 2: Rename Computer
- Log into the Domain Controller
- Search "About your PC"
- Select `Rename this PC` - enter desired name
- Select `Restart now`
## Task 3: Install Active Directory Domain Services
- Log into the Domain Controller
- Launch the Server Manager (this may take a little bit of time!)
  - There was a info popup referencing Azure Arc and Windows Admin Center (aka.ms/ManageWindowsServer).  Maybe, one day, I'll do this!
- From here there we are at a Dahsboard and we'll be selecting `Add Rolls and Features`
  - It's a wizard! 🧙🏾‍♂️ > Select `Next`
  - We're rolling with `Role-based or feature based installation` > Select `Next`
  - Server Selection > `Select a server from the server pool` > Select `Next`
  - Server Roles > Check `Active Directory Domain Services` > Select `Next` > Next Pop-up Select `Add Features` > Select `Next`
  - Features > Leave the Default Features > Select `Next`
  - AD DS Description > Select `Next`
  - <img width="590" alt="image" src="https://github.com/user-attachments/assets/9e74e0ea-6c31-42cf-880f-d44b73acf998" />
  - Confirmation > Review the roles and features > Select `Install` (This may take a few minutes!)
  - When installation is completed, select `Close`
## Task 4 Promote the Server to Domain Controller
- After the installation, there's a flag with a warning triangle in the top right corner of the Server Manager.  Click on it a select `Promote this server to a domain controller`
- Another Wizard 🧙🏾‍♂️ will appear!
- Deployment Configuration:
  - Select `Add a new forest` and provide a Root domain name > Select `Next`
  - From here, we can select functional levels for the forest and domain.  (We're just sticking to the default of Windows Server 2016).
  - Specify the Directory Services Restore Mode (DSRM) passoword > Select `Next`
  - Delegation warning appears > Select `Next`
  - The NetBIOS name should automagically populate > Select `Next`
  - Set locations for the Database, Log Files, and SYSVOL (we're sticking to the default locations) > Select `Next`
  - Review all configurations > Select `Next`
  - The wizard will perform a prerequisite check (this is where I stopped during the class).  The warnings are expected behavior when setting up a new domain.  If the prerequisite checks pass, Select `Install`
- After installation, the server will automatically restart
- Login...again!  When I tried to login without the domain specified, it stalled on getting group policies.  So I input the domain of `adlab` and it logged me in.
- Launch the `Windows Administrative Tools` > Select `Active Directory Users and Computers`
- Expand the domain name (`adlab.org`) and click on Users
- Right-click on `Administrator` select `Reset Password`
- Enter the desired password, ensure `User must change password at logon` is NOT selected. (🐿️ You have to pick a "real" password.  It won't let you pick something "easy".)
- Popup will appear, indicating that the password has been changed > Select `OK`
- Log out and back in with the Domain Administrator account (and that new password!)
## Task 5 Log In and Verify
"You’ve successfully installed and configured a default installation of Active Directory on Windows Server! You can now start creating user accounts, groups, and organizational units as needed." 

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
_🐘 It's breaktime!  Also, the lab is getting ready to go into the other machines!_

