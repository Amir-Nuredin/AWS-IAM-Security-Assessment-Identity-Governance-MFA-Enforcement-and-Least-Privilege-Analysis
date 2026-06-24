# AWS IAM Security Assessment: RBAC, MFA, Least Privilege, and Access Governance Review

## Objective

This lab/project aims to develop foundational skills in Identity and Access Management (IAM), access governance, and cloud security auditing using AWS. In this lab, I explored AWS IAM by reviewing users, groups, authentication methods, and permission management practices. I created multiple IAM users representing different organizational roles and implemented Role-Based Access Control (RBAC) through the use of IAM groups. To strengthen account security, I configured Multi-Factor Authentication (MFA) for privileged accounts and evaluated the importance of authentication controls in protecting cloud environments. Additionally, I designed and analyzed both secure and insecure IAM policies to understand the principle of least privilege and the risks associated with excessive permissions. I created a custom read-only Amazon S3 policy for developers, then compared it against a deliberately over-permissive policy to identify potential privilege escalation and security risks. Finally, I conducted a formal IAM security assessment by reviewing user permissions, MFA compliance, administrative access, and policy configurations to identify governance issues and recommend security improvements. This project provided hands-on experience with AWS IAM, Role-Based Access Control (RBAC), Multi-Factor Authentication (MFA), least-privilege access management, identity governance, policy analysis, and cloud security auditing while demonstrating how security teams evaluate and secure access controls within AWS environments.

### Skills Learned

This project provided hands-on experience with the following cloud security, identity management, and access governance skills:

- AWS Identity and Access Management (IAM) administration
- IAM user, group, and permission management
- Role-Based Access Control (RBAC) implementation
- Least-privilege access control design and enforcement
- Security auditing of IAM users, groups, and permissions
- Cloud security risk analysis and remediation planning

### Tools Used

- AWS Free Tier Account
- AWS Management Console
- AWS Identity and Access Management (IAM)

## Current Lab Environment Architecture/Setup

Below are screenshots of my lab Architecture before and after this week's lab/project (IM1&2). All the work for this weeks lab was done in the cloud, so no new hardware of VM additions.

<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/a3414b91-40bd-4b4d-a676-94ea8d3630f4" />
<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/8a5e0964-9f5b-4ec1-be64-9e7b88e98818" />

IM1&2: Current Lab Environment/Architecture Before and After this Week's Lab/Project

## Steps/Procedure

### Step 1: IAM Exploration

Since all of the work for this weeks project would be in AWS IAM, I wanted to quickly look at what was already in there so I could move forward knowing what I have to work with. I went to the IAM dashboard to get a general sense of what was going on, and everything looked good there (IM3). I first looked at the users section of IAM. I currently had one user (Admin-User) and it had MFA configured (IM4). I then looked at the Groups section of IAM. I currently had no groups created, but in this project I will later be creating different groups (IM5). Lastly I looked at the Policies section of IAM. Listed there were all the policies in AWS (IM6). The only policies I had currently was the AdministratorAccess policy for my Admin-User account. Later more would be created. 

<img width="949" height="342" alt="Screenshot 2026-06-22 095440" src="https://github.com/user-attachments/assets/816b6c70-fd88-4b25-a073-fe76bd20287a" />

IM3: IAM Dashboard in AWS

<img width="791" height="149" alt="Screenshot 2026-06-22 095528" src="https://github.com/user-attachments/assets/ce71848f-5ac1-4e7b-9a86-e2235048647f" />

IM4: Users Section in IAM (currently only one user)

<img width="781" height="121" alt="Screenshot 2026-06-22 095548" src="https://github.com/user-attachments/assets/efe03b37-4327-4e7b-be65-7c4259d83c69" />

IM5: Groups Section in IAM (none currently created)

<img width="771" height="295" alt="Screenshot 2026-06-22 095612" src="https://github.com/user-attachments/assets/91484131-fa87-4514-81aa-48eff9e71197" />

IM6: Policies Section in IAM

### Part 2: User Creation

Now that I confirmed everything, the first thing to do was to create the users for this project. I would be creating four users, an administator user (Admin-User this user wasn already created from a different project), a developer user for cloud development (developer-user), a security analyst user for monitoring and security (security-analyst), and lastly an auditor user for auditing and review (auditor user). to create these users, I went to IAM → Users → Create User and then configured each user. I named the user, allowed it access to the AWS Console, and created a custom password as well. I did the same for all three users (IM7-9). 

<img width="803" height="284" alt="Screenshot 2026-06-22 100519" src="https://github.com/user-attachments/assets/7a4876b3-711f-4068-944f-661b96e3cf90" />
<img width="799" height="278" alt="Screenshot 2026-06-22 100537" src="https://github.com/user-attachments/assets/8850379d-721a-4d90-9d8f-4965ba6a80e5" />
<img width="793" height="276" alt="Screenshot 2026-06-22 100744" src="https://github.com/user-attachments/assets/c53b6abf-bdb1-4928-92d6-ef5092f51f86" />

IM7-9: IAM User Accounts Created for Developer, Security Analyst, & Auditor

### Part 3: Creating Groups and Assigning Users to Groups

Now that I created the users, I wanted to assign them to different groups based on their roles. This is better than assigning permissions to each user individually because if you assign permissions to a specific group, you can then put that user in that group that matches the permissions that you want to give it. To do this, I went to IAM → User Groups → Create Group. 
1. **ADMINISTRATORS GROUP.** First I wanted to create a group for the Administrators. This group would have anyone with Admin access. I created the group and added the "Admin-User" user to the group as well (IM10&11).
2.  **DEVELOPERS GROUP.** Next I wanted to create a group for the Developers. This group would have any developers with different roles in it. I created the group and added the "developer-user" user to the group as well (IM12&13).
3.   **SECURITYTEAM GROUP.** I then wanted to create a group for the Security Team. This group would have any Security Analyst or anyone with a security role. I created the group and added the "security-analyst" user to the group as well (IM14&15).
4.    **AUDITORS GROUP.** Lastly I wanted to create a group for the Auditors. This group would any auditors in it. I created the group and added the "auditor-user" to the group as well (IM16&17).

<img width="791" height="218" alt="Screenshot 2026-06-22 100919" src="https://github.com/user-attachments/assets/6c088f69-d599-44d3-9160-4982bca2b5d4" />
<img width="807" height="242" alt="Screenshot 2026-06-22 100955" src="https://github.com/user-attachments/assets/f246db06-99b8-4980-b860-0732a023db31" />

IM10&11: Creaing Administrators Group and Adding Admin-User

<img width="797" height="283" alt="Screenshot 2026-06-22 101019" src="https://github.com/user-attachments/assets/0e85b653-e22d-4861-9b9c-2291848608a3" />
<img width="802" height="244" alt="Screenshot 2026-06-22 101118" src="https://github.com/user-attachments/assets/37ec91bd-8773-4b4c-867a-84a117319548" />

IM12&13: Creating Developer Group and Adding developer-user


<img width="790" height="285" alt="Screenshot 2026-06-22 101216" src="https://github.com/user-attachments/assets/cabd8074-ef60-4657-a337-aa0120b7f7de" />
<img width="799" height="234" alt="Screenshot 2026-06-22 101237" src="https://github.com/user-attachments/assets/8ac3b887-825f-412b-9a6d-b1ab78d8bac3" />

IM14&15: Creating SecurityTeam Group and Adding security-analyst User

<img width="796" height="278" alt="Screenshot 2026-06-22 101311" src="https://github.com/user-attachments/assets/d38874d0-d53b-41ee-8646-4c12a977f5df" />
<img width="804" height="245" alt="Screenshot 2026-06-22 101424" src="https://github.com/user-attachments/assets/8dabf2d5-487e-4776-b1f7-6d58166af20d" />

IM16&17: Creating Auditors Group and Adding auditor-user

### Part 4: MFA Deployment for Privleged Users

Next I wanted to configure MFA for users with higher levels of access, which were the "Admin-User" and "security-analyst." I already configured MFA access for the Admin-User in a previous project, so all I had to do was configure it for the security-analyst account. To do this, I went to the security-analyst user and then the "Security credentials" tab. I then went throught the MFA proccess and successfully configured MFA for the security-analyst account (IM18). To confirm that it was working, I logged in to the security-analyst account and it asked me for a MFA code. I typed it in (IM19), then I was able to login to the AWS console as the security-analyst account, confirming successfull deployment of MFA (IM20). 

<img width="619" height="254" alt="image" src="https://github.com/user-attachments/assets/5551258f-e307-45c2-a044-472054dc76ec" />

IM18: Assinging MFA to security-analyst account

<img width="257" height="319" alt="Screenshot 2026-06-22 102246" src="https://github.com/user-attachments/assets/9093a834-294c-4aa9-b29b-94689fceb889" />

IM19: MFA Code to Login to security-analyst Account 

<img width="862" height="389" alt="Screenshot 2026-06-22 102331" src="https://github.com/user-attachments/assets/47fea029-b510-483a-ae63-c5b384ac6047" />

IM20: AWS Console for security-analyst Account







































