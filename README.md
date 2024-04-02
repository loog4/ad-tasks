<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Common Tasks in Active Directory</h1>
Unlike other projects showcased, this page mainly shows different things done in an Active Directory Lab.
I will be adding more tasks to this in the future.

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Users and Computers
- Active Directory DNS
- Network File Share
- Group Policy Management
- Powershell

<h2>Task Overview:</h2>

- Unlock and reset account password using either GUI or Powershell
- Setup Network File Shares and configuring permissions to different people
- Setup Remote Desktop for non-admins using Group Policy
- DNS Exercise (Creating A-Records, CNAMEs, and flushing cache)

<h2>Account Unlock and Reset</h2>

![image](https://github.com/loog4/ad-tasks/assets/80493463/d135a574-edbf-45b2-818e-94ef8283b568)

<p>The user account of Bob Smith has forgotten their password and now has their account locked out.</p>

![image](https://github.com/loog4/ad-tasks/assets/80493463/6efd3af9-e2fe-4900-9907-2f4bb7af5f69)
![image](https://github.com/loog4/ad-tasks/assets/80493463/4392a3b4-8b94-45b3-a268-c1f43dcf97cc)
![image](https://github.com/loog4/ad-tasks/assets/80493463/248a7235-dd44-42f8-8613-cede255084f7)

First way to fix this is to go Active Directory Users and Computers and unlock and reset their password.

![image](https://github.com/loog4/ad-tasks/assets/80493463/002fcc89-0e5e-45a8-8ff6-d252f528544f)

<p>Another way is to input these commands into Powershell</p>
<p>(You can change the password to whatever you wish by editing the text between the quotation marks)</p>

<h2>Remote Desktop for Non-Admins</h2>

![image](https://github.com/loog4/ad-tasks/assets/80493463/e019f677-fc03-43e0-87f0-1b1faa63e47d)

<p>Bob tries login to his account now but finds out he does not have access to Remote Desktop</p>

![image](https://github.com/loog4/ad-tasks/assets/80493463/b299d7f2-3259-4a6a-b32d-3f3bfc52e4f6)
![image](https://github.com/loog4/ad-tasks/assets/80493463/56496ee8-621f-4ebe-89de-faa39c482aa1)

<p>We solve this by using Group Policy to allow users to use Remote Desktop</p>

![image](https://github.com/loog4/ad-tasks/assets/80493463/5924cba0-bff2-424d-ba01-7173b959eb80)

<p>Log in to the Client PC and update its Group Policy</p>

![image](https://github.com/loog4/ad-tasks/assets/80493463/76c1837a-3acb-4912-896f-256de67a1c06)

<p>Bob can now remote login into the pc</p>

<h2>Network File Share</h2>

![image](https://github.com/loog4/ad-tasks/assets/80493463/7659f14f-a1e3-4d40-9842-1481907cde74)

<p>We want to share these 4 folders across the network but have different permissions for each one</p>
<p>The following permissions for all Domain Users are:</p>

- FolderA has Read-Access
- FolderB has Read/Write Access
- FolderC has No Access

<p>The "IMPORTANT" folder will be used later</p>

![image](https://github.com/loog4/ad-tasks/assets/80493463/bd976385-9830-432c-b167-d71a64e26618)
![image](https://github.com/loog4/ad-tasks/assets/80493463/3d920141-7d01-4fcb-ad45-b75da79d36c1)

<p>FolderA</p>

![image](https://github.com/loog4/ad-tasks/assets/80493463/1adc3575-4dd1-42d7-afac-bdba526040aa)

<p>FolderB</p>

![image](https://github.com/loog4/ad-tasks/assets/80493463/803542a4-9ef1-4873-a255-35ef876ed89d)

<p>FolderC</p>
<p>Go into each folder's properties and edit their share permissions</p>

![image](https://github.com/loog4/ad-tasks/assets/80493463/a9a26667-5dfe-42dc-a5fe-51192bab561b)

<p>If we login as another user and search in file explorer "\\DC-1" we can see the folders shared</p>
<p>With the permissions in place, a regular account will be able to read both Folders A and B but only be able write anything on B</p>
<p>And should have no access to Folder C</p>

<h3>Security Group Folder</h3>

![image](https://github.com/loog4/ad-tasks/assets/80493463/fa0cb6e6-f7e6-4fbd-9dc8-23c78a5e0a38)

<p>We will make the "IMPORTANT" folder exclusive for a specific security group shown above</p>

![image](https://github.com/loog4/ad-tasks/assets/80493463/38efd0f1-d5d2-4cdd-b947-2f43acabd9f4)

<p>Give the security group read and write permissions</p>

![image](https://github.com/loog4/ad-tasks/assets/80493463/80daeea2-896f-4777-aa8c-beb36958ff9b)

<p>Trying to access the Folder as a normal user is not possible</p>

![image](https://github.com/loog4/ad-tasks/assets/80493463/c09006cb-4ed7-4d5d-aa56-227d80d34e79)
![image](https://github.com/loog4/ad-tasks/assets/80493463/a076bf84-8528-4ee1-ab97-e47a8aba3de7)

<p>Adding Bob Smith to the Security Group will now allow us to access the folder</p>

<h2>DNS Exercises</h2>

<h3>A Record</h3>
<p>We can assign an IP address to a human readable name using A records</p>

![image](https://github.com/loog4/ad-tasks/assets/80493463/c4cf774f-8b85-4bb1-877b-fd1fa0bf787a)
![image](https://github.com/loog4/ad-tasks/assets/80493463/2c9c57f7-f0f2-4af2-9296-af16e9e9a1f2)

<h3>CNAME Record</h3>
<p>A CNAME Record allows us to assign a new name to an already existing dns address</p>

![image](https://github.com/loog4/ad-tasks/assets/80493463/7f16c662-447c-4537-8949-abf8ecd11f37)
![image](https://github.com/loog4/ad-tasks/assets/80493463/ea2f1e11-1c81-4354-b32e-c303fbb0af49)
![image](https://github.com/loog4/ad-tasks/assets/80493463/d98b2f7a-66d6-4bde-8507-e05a9afbe006)

<h3>DNS Flushing</h3>
<p>If we want to assign a new IP address to a DNS record or have issues with connecting to one</p>
<p>Flushing the DNS cache will reset the records and allow new IP address assigned to them</p>

![image](https://github.com/loog4/ad-tasks/assets/80493463/d99b79f7-dafc-469a-9c7e-a775125ec15b)
![image](https://github.com/loog4/ad-tasks/assets/80493463/3764345c-866b-49e7-88fe-7048095bdd09)

<p>That concludes this list for now. I will add more in the future</p>

