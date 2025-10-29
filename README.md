# Automating-User-Role-Management-in-Microsoft-Entra-ID-with-PowerShell

In this lab, I automated identity lifecycle tasks inside my Microsoft Entra ID (Azure AD) tenant using PowerShell 7 and the Microsoft Graph module.
The automation created users from a CSV file, organized them into security groups, assigned departments, and delegated administrative roles — simulating how IAM engineers use scripting to manage users at scale instead of relying only on the Azure portal.

This lab builds on the secure tenant created previously and focuses on PowerShell-based automation for provisioning and access management.

## Objectives

By the end of this lab, I completed the following:

-Imported user data from a .csv file into Entra ID using PowerShell
-Automatically created 10 cloud-only users with custom passwords
-Created and organized department-based security groups (HR, IT, Finance)
-Added users to their respective groups using conditional logic
-Updated user department attributes programmatically
-Created a static and dynamic security group for Finance users
-Assigned the User Administrator role to the Helpdesk Admin account using Microsoft Graph

---

<img width="1400" height="808" alt="image" src="https://github.com/user-attachments/assets/b8bfc939-bbfb-4c12-9c53-c97d23b31919" />


# Tools Used

-PowerShell 7
-Microsoft Graph PowerShell module
-Azure Portal (Microsoft Entra ID)
-CSV user data file
-Microsoft Graph API endpoints (via PowerShell)

---

### Created a brand-new Azure AD tenant

To start the lab, I signed in to the Azure Portal and created a brand-new Entra ID (Azure AD) tenant instead of using my personal account. I went to Azure Active Directory → Manage tenants → Create, selected Azure AD as the tenant type, and entered the organization name, domain (onmicrosoft.com), and region. After deployment finished, I switched into the new tenant using the “Switch tenant” option. This gave me an isolated identity environment where I could configure users, MFA, and admin settings without mixing anything with a personal account.  

<img width="963" height="326" alt="image" src="https://github.com/user-attachments/assets/0345d0c7-341b-4a6b-b91a-5fa64bef3caf" />


---

### Added a Global Administrator account

To secure and manage the new tenant properly, I created a cloud-only Global Administrator account instead of using my personal Microsoft identity. From the Entra ID portal, I went to Users → New user → Create new user, entered the name and username in the tenant’s domain, and let Azure generate a temporary password. After creating the account, I confirmed it showed up under the tenant’s user list and made sure it was recognized as a directory-native identity instead of an external account. This account became the primary admin for all future IAM configuration and security tasks.

<img width="1357" height="607" alt="image" src="https://github.com/user-attachments/assets/0dbe7da0-0fde-4ad0-a3e3-23cf6cccdeee" />

---

### Enabled MFA for the admins

After creating the Global Administrator account, I immediately enabled MFA to protect high-privilege access. In the Entra ID portal, I went to Users → Per-user MFA settings, selected the admin account, and enforced MFA. When I signed in with the new credentials, Azure prompted me to register the Microsoft Authenticator app and complete verification. Enabling MFA at this stage ensures that even if someone gains the admin password, they still can’t access the tenant without the second authentication factor.

<img width="1423" height="357" alt="image" src="https://github.com/user-attachments/assets/c349a75a-b236-43bd-86f6-ec3f987a7d28" />


---

###  Installed PowerShell 7 and connected with Connect-MgGraph

To start managing the tenant through the command line, I installed PowerShell 7 and set it as my default shell. After launching it, I installed the Microsoft Graph PowerShell module using Install-Module Microsoft.Graph and then authenticated with the tenant using Connect-MgGraph. This allowed me to connect directly to Entra ID from PowerShell instead of relying only on the Azure portal, which is how IAM engineers manage users, roles, and policies at scale in real environments.

<img width="1240" height="608" alt="image" src="https://github.com/user-attachments/assets/6e8a90eb-1658-4afd-b494-d3bd246c25d8" />

<img width="1144" height="464" alt="image" src="https://github.com/user-attachments/assets/3fb162c2-d91e-4e58-8c7e-b4081e2f831a" />

---

### Installed and used Azure CLI (az login)

To enable command-line management of my Azure tenant, I installed the Azure CLI and authenticated using az login with my tenant ID. This allowed me to securely access and manage Azure resources from the terminal instead of relying solely on the web portal. After logging in, I confirmed the connection with az account show, which returned my tenant context and verified that the CLI was properly authenticated.

<img width="1027" height="599" alt="image" src="https://github.com/user-attachments/assets/3d063494-8e76-4d22-bbd0-9b515e6838ac" />

<img width="1387" height="325" alt="image" src="https://github.com/user-attachments/assets/03bbf66a-7ab9-43fb-a509-06bdfcd33142" />


---

### Reflection 

To build a secure and isolated cloud identity environment, I first created a brand-new Azure AD tenant to separate organizational identities from any personal Microsoft accounts. I then added a dedicated Global Administrator account to manage the directory with full control, rather than relying on default or external identities. To strengthen access security from the start, I enabled MFA on the admin account so that privileged login attempts require a second factor. After that, I installed PowerShell 7 and connected using the Microsoft Graph module via Connect-MgGraph, which allowed me to verify access and prepare for scripting and automation tasks. Finally, I installed the Azure CLI and authenticated with az login to confirm command-line access to the tenant, ensuring I could manage identities and configurations using both portal and CLI-based tooling.

