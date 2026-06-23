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









































