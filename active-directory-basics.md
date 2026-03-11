# TryHackMe - Active Directory Basics Write-Up
**Category**: Active Directory / Networking

*This room will introduce the basic concepts and functionality provided by Active Directory.*


## Overview 

This room is where you learn about the basics of Active Directory. Active Directory is a part of how companies manage their computers and users. The lab teaches you about the parts of Active Directory like domain controllers and users and groups and organizational units. You will see how Active Directory helps keep track of who can do what on the computers, in a company using something called a Windows domain environment with Active Directory. 

## Task 2 - Windows Domains 
A **Windows Domain** is a group of users, computers, and resources that are centrally managed and resources that are centrally managed within an organization. Instead of each computer having its own separate user accounts, authentication and access control are managed through central systems. 

For example, in a domain such as `github.example.com`, users can log into any computer on the network using a ceneralized account like 
`github\jdoe` - This allows organizations to manage authentication and permissions more efficiently across many machines. 

A **Domain Controller (DC)** – is a server that runs Active Directory services and is reponsible for authenticating users, managing directory data, and enforcing security policies across the domain. The Domain Controller acts as the central authority for identity management within the network. 

**Advantages of a Windows Domain**
- **Centralized Identity management**: Administrators can manage all user accounts from a central location using Active Directory, allowing users to access multiple systems across the network with a single set of credentials.
- **Managing security policies**: Security policies can be configured through Active Directory and applied to users and computers across the network using Group Policy. This ensures consistent security configurations throughout the organization.

## Task 3 - Active Directory
The core component of any Windows domain is Active Directory Domain Services (AD DS). AD DS functions as a direcotry service that stores information about all objects within a network environment. These objects include users, computers, groups, and other resources. 

**Users**: are one of the most common object types in a Active Directory. Users are considered security principals, meaning they can be authenticated by the domain and granted access to resources such as files, folders, printers, and applications. These users can be represented as employees within an organization who require accesss to the network. 

**Machines (or Computers)** that join the domain are also represented as objects in a Active Directory. Each computer recieves a machine account similar to user acctount which allows the system to authenticate itself to the domain. Similar to users, machines are also considered security principles. 

---

<img width="468" height="414" alt="image" src="https://github.com/user-attachments/assets/ff0488bc-0fdc-40b4-b076-6f733d9109be" />

While examining the domain environment, an Organizational Unit named THM was identified.

Within this OU, there were five departmental child OUs:
- IT
- Management
- Marketing
- Research & Development (R&D)
- Sales

*This structure reflects how organizations typically separate departments for easier management and policy enforcement.*

In Active Directory, objects such as users, computers, and groups are organized into Organizational Units (OUs). OUs act as containers that help administrators logically organize resources within the domain. This structure makes it easier to manage permissions and apply security policies. Administrators can apply Group Policies to specific OUs to control system settings, security configurations, and user permissions.

For example: 
- Employees in the Sales department may require different system configurations than employees in IT. 
- By placing users into department-specific OUs, administrators can efficiently apply appropriate policies.

---

<img width="468" height="442" alt="image" src="https://github.com/user-attachments/assets/6f6f250a-41cd-43a3-8983-46a74d7e5405" />

Windows automatically creates several default containers within Active Directory, including **Builtin** which contains default groups available on all Windows systems, **Computers** which are any machine that joins the domain is placed here by default, **Domain Controllers** which are the default Organizational Unit that contains all domain controllers, **Users** which contains default domain users and groups, and finally **Managed Service Accounts** which stores accounts used by services running within the Windows domain.

---

## Task 4 Managing Users in Active Directory

<img width="468" height="440" alt="image" src="https://github.com/user-attachments/assets/cdc586d3-eb8c-4507-8a30-b3d679db86c9" />

During this task, users and Organizational Units were managed to match an organizational structure. 

Some departments contained users that did not match the organizational chart. The inconsistencies were corrected by: 
- Creating new user accoutns
- Deleting unnecessary users
- Adjusting the OU strcture where necessary

If an Organizational Unit needs to be removed, the "Protect object from accidental deletion" option must first be unchecked. Once this portection is disabled, the OU and any contained objects can be deleted after confirmation. 

--- 

<img width="468" height="415" alt="image" src="https://github.com/user-attachments/assets/6ffad1f6-11d3-4c2e-aafa-ac793ab070eb" />

One poweful feature of Active Directory is delegation of control. Delegation allows administratiors to grant specific users limited adminstrative privileges over particular organizational units without giving them full Domain Admnistrator access. A common use case is allowing IT support staff to reset passwoards for standard users. 

