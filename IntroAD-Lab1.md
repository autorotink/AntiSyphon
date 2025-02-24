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
