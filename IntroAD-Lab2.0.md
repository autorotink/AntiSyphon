# Lab 004 - Add Client and Member Server to Domain
## Task 1 - Set Static DNS Server Address on Workstation
- Login to the Client machine (leave Domain blank). > Select `Yes` concerning network discoverability
- In the Control Panel > Under Network and Internet > Select `View network status and tasks` > Select `Change adapter settings`
- Right-click `Ethernet 3` > Select `Properties` > Select `Internet Protocol Version 4 (TCP/IPv4)` > Select Properties
  - (Note from lab: Normally for a client system it would receive IP addressing information including DNS servers via DHCP.)
- Manually configure the DNS servers (Lab Only).
- Select `Use the DNS server IP address` > Enter IP of the Domain Controller
  - (Run `ipconfig` in a command prompt on the Domain Controller, if needed)
- Select `OK` > Select `Close`    
## Task 2 - Join the Client to the Domain
- Start the Server Manager Machine
- Search for "About" > Select `Server Manager`
- Select `Local Server` > Select `WORKGROUP` > at the next popup, Select `Change`
- Select the `Domain` radio button > Enter "adlab.org" > Select `OK`
- Enter the username "Administrator" and the password set up earlier. > Select `OK` x2 > Select `Close` > Select `Restart Now`
- The system will reboot.
## Task 3 - Rename Computer (Lab environment only) 
- Login to the Client using the Domain Administrator credentials, domain "adlab.org" > Select `Continue`
- Popup appears > Select `Yes`
- Launch `About your PC` > Select `Rename this PC` > Enter the name for your member server (for the lab, we're using "client") > Select `Next` > Select `Restart now` > Select `Continue`
- Once rebooted, log back in.
## Task 4 - Verify
- Login to your domain controller
- Select `Start menu` > Type "Active Directory Users and Computers" and Enter
- In left pane Expand "adlab.org" > Select `Computers` in the right pane you should see the computer named "Client"
- Move the Client computer from the default Computers container to the "Computers-Clients" OU > Right-click the "Client" object > Select `Move` > Select `Computers-Clients` OU > Select `OK`
- Click on `Computers-Clients` OU > Observe the "Client" computer is in the OU in the right pane.
## Task 5 - Set Static DNS Server Address on Member Servers
- Login to the "Member Server" with Administrator credentials provided in the MetaCTF console (leave domain blank) > Pop appears, Select `Yes`
- Launch the Control Panel > Select `View network status and tasks` > Select `Change adapter settings` > Right-click `Ethernet0` > Select `Properties` > Select `Internet Protocol Version 4 (TCP/IPv4) > Select `Properties`
- Select `Use the following IP address` > Enter the IP of the Domain Controller > Select `OK` > Select `Close`
## Task 6 - Join Member Server to the Domain
- Launch the Server Manager, Select `Local Server` > Select `WORKGROUP` > Select `Change` > Select `Domain:` and enter "adlab.org" > Select `OK`
- Enter username Administrator and password set up from the Domain Controller > Select `OK` x2 > Select `Close` > Select `Restart Now`
- System will reboot
## Task 7 - Rename Computer (Lab environment only)
- Login to the Member Server using the Domain Administrator credentials, domain "adlab.org" > Select `Continue`
- Popup appears > Select `Yes`
- Launch `About your PC` > Select `Rename this PC` > Enter the name for your member server (for the lab, we're using "pki") > Select `Next` > Select `Restart now` > Select `Continue`
- Once rebooted, log back in.
## Task 8 - Verify
- Login to your domain controller
- Select `Start menu` > Type "Active Directory Users and Computers" and Enter
- In left pane Expand "adlab.org" > Select `Computers` in the right pane you should see the computer named "PKI"
- Move the Client computer from the default Computers container to the "Servers" OU > Right-click the "PKI" object > Select `Move` > Select `Servers` OU > Select `OK`
- Click on `Servers` OU > Observe the "PKI" computer is in the OU in the right pane.
## Task 9 - Enable Remote Logins (Lab environment only, do NOT perform in production environment!)
- Login to Client, using Domain Administrator credentials > Launch "Computer Management"
- Expand `Local Users and Groups` > Select `Groups` > Right-Click `Remote Desktop Users` > Select `Properties` > Select `Add` and add "Domain Users" > Select `OK` x2.
- Repeat this Task on Member Server machine.
Conclusion: "You've successfully joined your Client and Member Server to the Active Directory domain"
