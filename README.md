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

### Part 5: Secure Policy Creation

Now that the users and groups were all setup, I could now create specific policies for the groups so that they could only access and modify things that pertain to their specifc role. This is the concept of least privlege. 
1. **CREATING POLICY.** The policy I created was for the Developer group. This policy would allow them to only view/read and download objects from S3 Buckets, but they wouldn't be able to modify or make any changes to those buckets (like deleting or adding buckets). This would only allow them what they need from these buckets and nothing more. To create it, I went to AWS Console → IAM → Policies → Create Policy. I wrote the policy in JSON format (IM21). In the policy was the line for either allow or deny (Allow), a couple lines for the service affected by the policy ("s3:GetObject," which allows reading of files in bucket and "s3:ListBucket" which allowed veiwing bucket contents ), and line for what resources within S3 would be affected ("Resource": "*" which means all). Normally in a real environment a policy would only affect specific buckets. I then named the policy "Developer-S3-Read-Policy." (IM22)
2. **ATTACHING POLICY TO DEVELOPERS GROUP.** Now that I created the policy, I needed to to attach it to the correct group that that it would apply. To do this, I went to the developers group, and then under permissions, clicked "add permissions" then "Attach policies (IM23)." I then clicked the policy I created for the Developers group and attached it (IM24&25).
3. **TESTING POLICY.** I wanted to see if the policy I made actually worked, so I logged on to the developer account and attempted to create a bucket. When I tried, it gave me a message saying I didn't have permission to do so, confirming that the policy was working as intended (IM26).

<img width="805" height="248" alt="Screenshot 2026-06-22 183057" src="https://github.com/user-attachments/assets/53b820ac-aabd-49ca-ac92-dcd8fef8d21d" />

IM21: Creating Custom Policy in JSON Format

<img width="827" height="344" alt="Screenshot 2026-06-22 183150" src="https://github.com/user-attachments/assets/dbbbcfc5-4bb5-4a86-be9a-ea92654e09cb" />

IM22: Configuring Custom Policy

<img width="803" height="259" alt="image" src="https://github.com/user-attachments/assets/f6b94e72-dd6b-43df-99b1-72480e1a692e" />

IM23: Attaching Policy to Developers Group

<img width="814" height="167" alt="Screenshot 2026-06-22 183309" src="https://github.com/user-attachments/assets/d8ca5edc-52c8-4d0b-bc34-9f4a8f5706cf" />
<img width="797" height="230" alt="Screenshot 2026-06-22 183359" src="https://github.com/user-attachments/assets/cd47efba-6b92-4f27-9687-7a6c5d8a7752" />

IM24&25: Policy Attached to Developers Group

<img width="812" height="96" alt="Screenshot 2026-06-25 103131" src="https://github.com/user-attachments/assets/af1663ba-bb08-4f83-9f0c-b789a4bbd311" />

IM26: Confirming Policy is Working 

### Part 6: Insecure Policy Creation

Now that I created a policy that securly restrics roles, I wanted to create a policy that did the opposite, allow access for all users to have full control of AWS. This is very problematic because if the policy is applied, any standard user could change anything they want, or have maximum permissions. To create this policy, I went to AWS Console → IAM→ Policies → Create Policy. I did it in JSON format again (IM27). This policy is essentialy saying allow any action for any resource. This give essentaily full administrative access to AWS. I named it "Dangerous-FullAccess" and created the policy (IM28&29). 

<img width="785" height="151" alt="Screenshot 2026-06-22 183631" src="https://github.com/user-attachments/assets/dc6ea8a3-8f6d-419a-a924-1fb0b098795b" />

IM27: Creaing Insecure Policy in JSON format

<img width="833" height="347" alt="Screenshot 2026-06-22 183718" src="https://github.com/user-attachments/assets/329d422b-8824-47e1-a481-86fb44231972" />
<img width="786" height="222" alt="Screenshot 2026-06-22 184038" src="https://github.com/user-attachments/assets/9d3986b8-5298-4caa-a88a-10e2b7dab24d" />

IM28&29: Insecure policy creating with full admin access. 

### Part 7: IAM Security Audit

I now wanted to perform a security audit like a security analyst would too see how secure my "environemnt" was and what to improve on. I asked myself a couple of questions too see my current standing. 
1. **REVIEWING ALL CURRENT USERS.** First I reviewed all the current users and what current group they were in as well as what permissions they had as well (IM30-33)
2. **WHO HAS ADMINISTRATIVE STATUS?** The only current user that that administrative status was the Admin-User
3. **WHO LACKS MFA?** Of the four users, two users did not have MFA, the developer-user and the auditor-user.
4. **WHICH PERMISSIONS ARE EXCESSIVE?** I currently had two custom made permissions/policies. "Developer-S3-Read-Policy" which was not excessive and was a secure policy. The other policy "Dangerous-FullAccess" was not secure and very exccesive.
5. **SHOULD ANY PERMISSIONS BE REMOVED?** The one permission that should be removed was the Dangerous-FullAccess policy. I went to that policy and then deleted it (IM34).

After doing these audits and findings, I a small table listing these findings with three sections: Finding, Risk, and Severity (TB1)

| Finding                     | Risk                 | Severity |
| --------------------------- | -------------------- | -------- |
| developer-user lacks MFA    | Account compromise   | High     |
| auditor-user lacks MFA      | Account compromise   | High     |
| Dangerous-FullAccess policy | Privilege escalation | Critical |
| Wildcard permissions (*)    | Excessive access     | Critical |
| Full administrative access  | Potential misuse (if associated with wrong account)    | High     |

Table1: Findings Post-Security Audit

<img width="796" height="272" alt="Screenshot 2026-06-22 184229" src="https://github.com/user-attachments/assets/dacc81a1-2f84-49ae-afa4-2fc84be86b45" />
<img width="788" height="277" alt="Screenshot 2026-06-22 184255" src="https://github.com/user-attachments/assets/0892daf3-ec15-4571-a240-72175fd579dc" />
<img width="792" height="271" alt="Screenshot 2026-06-22 184320" src="https://github.com/user-attachments/assets/a7c36c4c-b7e8-46e2-8a70-75471e45f882" />
<img width="790" height="278" alt="Screenshot 2026-06-22 184458" src="https://github.com/user-attachments/assets/49a65a8d-ed27-4c4d-b79a-5752457807b9" />

IM30-33: Current Configuration of all IAM Users

<img width="802" height="205" alt="Screenshot 2026-06-22 184634" src="https://github.com/user-attachments/assets/6a93e34b-3faa-40e9-8a67-35e638f9bb91" />

IM34: Deleting Dangerous-FullAccess Policy






































