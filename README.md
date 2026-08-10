<h1 align="center">Windows Server Active Directory & IT Support Lab</h1>

<p align="center">
  <strong>Enterprise-style Windows Server Administration Portfolio Project</strong><br>
  Active Directory • DNS • Group Policy • File Server • NTFS • SMB • Access Control
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Platform-Windows%20Server-0078D4?style=flat-square" alt="Windows Server">
  <img src="https://img.shields.io/badge/Directory-Active%20Directory-0078D4?style=flat-square" alt="Active Directory">
  <img src="https://img.shields.io/badge/DNS-Configured-2EA44F?style=flat-square" alt="DNS">
  <img src="https://img.shields.io/badge/Virtualization-VirtualBox-183A61?style=flat-square" alt="VirtualBox">
</p>

<hr>

<h2>1. Project Overview</h2>

<p>
This project simulates a small-to-medium enterprise Windows IT environment using
<strong>Windows Server</strong>. The objective was to build and document a centralized
infrastructure for identity management, security policy enforcement, departmental
resource management, and file sharing.
</p>

<h3>Primary Goals</h3>

<ul>
  <li>Deploy and configure a Windows Server Domain Controller.</li>
  <li>Build the <code>corp.local</code> Active Directory domain.</li>
  <li>Configure DNS for the domain.</li>
  <li>Organize departments using Organizational Units (OUs).</li>
  <li>Manage users through department-based security groups.</li>
  <li>Apply centralized password and account-lockout policies.</li>
  <li>Configure departmental file storage and SMB shares.</li>
  <li>Control access using NTFS permissions.</li>
  <li>Verify the implemented configuration with evidence.</li>
</ul>

<hr>

<h2>2. Lab Environment</h2>

<table>
<tr><th>Component</th><th>Configuration</th></tr>
<tr><td><strong>Server</strong></td><td>Windows Server</td></tr>
<tr><td><strong>Server Name</strong></td><td><code>DC01</code></td></tr>
<tr><td><strong>Domain</strong></td><td><code>corp.local</code></td></tr>
<tr><td><strong>Directory Service</strong></td><td>Active Directory Domain Services</td></tr>
<tr><td><strong>DNS</strong></td><td>Windows DNS</td></tr>
<tr><td><strong>Virtualization</strong></td><td>Oracle VirtualBox</td></tr>
<tr><td><strong>File Sharing</strong></td><td>SMB</td></tr>
<tr><td><strong>Permissions</strong></td><td>NTFS</td></tr>
<tr><td><strong>Departments</strong></td><td>IT, HR, Finance, Sales, Management</td></tr>
</table>

<hr>

<h2>3. Architecture</h2>

<pre>
                         +----------------------+
                         |    Windows Server    |
                         |        DC01          |
                         |      corp.local      |
                         +----------+-----------+
                                    |
              +---------------------+---------------------+
              |                     |                     |
       Active Directory            DNS              Group Policy
              |
        +-----+------+
        |            |
       OUs      Security Groups
        |            |
   +----+----+----+----+
   |    |    |    |    |
  IT   HR Finance Sales Management
        |
        +------------------+
                           |
                      File Server
                           |
                  Departmental Shares
</pre>

<hr>

<h2>4. Implementation & Evidence</h2>

<p>
The following sections document the work in the order it was performed. Each
implementation is followed immediately by its corresponding evidence.
</p>

<h3>4.1 Windows Server Identity</h3>

<p><strong>What was done:</strong> Configured and verified the Windows Server that serves as the central infrastructure server for the lab.</p>

<p><strong>Why it matters:</strong> A clearly identified infrastructure server provides a consistent foundation for centralized Windows administration.</p>

<p><strong>Evidence:</strong></p>

<p align="center">
  <img src="./Evidence/01-DC01-Server-Identity.png" width="760" alt="DC01 Server Identity">
</p>
<p align="center"><em>Figure 1 — DC01 Server Identity</em></p>

<hr>

<h3>4.2 Static IP Configuration</h3>

<p><strong>What was done:</strong> Configured and verified a static IP configuration for DC01.</p>

<p><strong>Why it matters:</strong> Infrastructure services such as DNS and Active Directory should be reachable through a predictable server address.</p>

<p><strong>Evidence:</strong></p>

<p align="center">
  <img src="./Evidence/02-DC01-Static-IP-Verification.png" width="760" alt="DC01 Static IP Verification">
</p>
<p align="center"><em>Figure 2 — Static IP Verification</em></p>

<hr>

<h3>4.3 Active Directory Domain</h3>

<p><strong>What was done:</strong> Configured the Active Directory domain <code>corp.local</code>.</p>

<p><strong>Why it matters:</strong> The domain provides centralized identity, authentication, and policy management.</p>

<p><strong>Evidence:</strong></p>

<p align="center">
  <img src="./Evidence/03-DC01-Domain-Joined.png" width="760" alt="DC01 Domain Configuration">
</p>
<p align="center"><em>Figure 3 — Domain Configuration</em></p>

<hr>

<h3>4.4 Domain Controller & Active Directory</h3>

<p><strong>What was done:</strong> Configured Active Directory Domain Services and the server as the Domain Controller.</p>

<p><strong>Why it matters:</strong> The Domain Controller provides centralized directory services and authentication for the Windows domain.</p>

<p><strong>Evidence:</strong></p>

<p align="center">
  <img src="./Evidence/04-Active-Directory-Domain-Controller.png" width="760" alt="Active Directory Domain Controller">
</p>
<p align="center"><em>Figure 4 — Active Directory Domain Controller</em></p>

<hr>

<h3>4.5 DNS Configuration</h3>

<p><strong>What was done:</strong> Configured and verified the <code>corp.local</code> DNS zone.</p>

<p><strong>Why it matters:</strong> DNS is a critical dependency of Active Directory because domain services rely on name resolution to locate resources and services.</p>

<p><strong>Evidence:</strong></p>

<p align="center">
  <img src="./Evidence/05-DNS-Corp-Local-Zone.png" width="760" alt="DNS corp.local Zone">
</p>
<p align="center"><em>Figure 5 — DNS corp.local Zone</em></p>

<hr>

<h3>4.6 Organizational Units</h3>

<p><strong>What was done:</strong> Created department-based Organizational Units.</p>

<pre>
corp.local
├── IT
├── HR
├── Finance
├── Sales
└── Management
</pre>

<p><strong>Why it matters:</strong> OUs provide logical organization and make future administration and Group Policy management easier.</p>

<p><strong>Evidence:</strong></p>

<p align="center">
  <img src="./Evidence/06-AD-Organizational-Units.png" width="760" alt="AD Organizational Units">
</p>
<p align="center"><em>Figure 6 — Departmental Organizational Units</em></p>

<hr>

<h3>4.7 Security Groups & Group Membership</h3>

<p><strong>What was done:</strong> Created department-based security groups and assigned users to the appropriate groups.</p>

<pre>
GG-IT-Users
GG-HR-Users
GG-Finance-Users
GG-Sales-Users
GG-Management-Users
</pre>

<p><strong>Why it matters:</strong> Group-based permissions scale better than assigning resource permissions individually to every employee.</p>

<p><strong>Access model:</strong></p>

<pre>
User
  ↓
Department Security Group
  ↓
Department Resource
</pre>

<p><strong>Evidence A — IT Group Membership:</strong></p>

<p align="center">
  <img src="./Evidence/07-AD-IT-Security-Group-Membership.png" width="760" alt="IT Security Group Membership">
</p>
<p align="center"><em>Figure 7 — IT Security Group Membership</em></p>

<p><strong>Evidence B — Security Groups:</strong></p>

<p align="center">
  <img src="./Evidence/08-AD-Security-Groups.png" width="760" alt="AD Security Groups">
</p>
<p align="center"><em>Figure 8 — Department Security Groups</em></p>

<hr>

<h3>4.8 Domain Password Policy</h3>

<p><strong>What was done:</strong> Configured centralized password controls including minimum password length, password complexity, and maximum password age.</p>

<p><strong>Why it matters:</strong> Centralized policy ensures authentication requirements are consistently enforced across the domain.</p>

<p><strong>Evidence:</strong></p>

<p align="center">
  <img src="./Evidence/09-Domain-Password-Policy.png" width="760" alt="Domain Password Policy">
</p>
<p align="center"><em>Figure 9 — Domain Password Policy</em></p>

<hr>

<h3>4.9 Account Lockout Policy</h3>

<p><strong>What was done:</strong> Configured account-lockout controls to protect domain accounts from repeated failed authentication attempts.</p>

<p><strong>Why it matters:</strong> Account lockout is a basic defensive control against password guessing and repeated authentication attempts.</p>

<p><strong>Evidence:</strong></p>

<p align="center">
  <img src="./Evidence/10-Account-Lockout-Policy.png" width="760" alt="Account Lockout Policy">
</p>
<p align="center"><em>Figure 10 — Account Lockout Policy</em></p>

<hr>

<h3>4.10 Departmental File Server</h3>

<p><strong>What was done:</strong> Created a centralized departmental storage structure.</p>

<pre>
C:\CompanyData
├── IT
├── HR
├── Finance
├── Sales
└── Management
</pre>

<p><strong>Why it matters:</strong> Departmental separation provides a structured foundation for controlling access to organization-specific data.</p>

<hr>

<h3>4.11 NTFS Permissions</h3>

<p><strong>What was done:</strong> Configured NTFS permissions using security groups.</p>

<pre>
GG-IT-Users
      ↓
IT Department Folder
      ↓
Required Access
</pre>

<p><strong>Why it matters:</strong> Group-based permissions improve scalability and support the principle of least privilege.</p>

<p><strong>Evidence:</strong></p>

<p align="center">
  <img src="./Evidence/11-NTFS-IT-Group-Permissions.png" width="760" alt="NTFS IT Group Permissions">
</p>
<p align="center"><em>Figure 11 — NTFS IT Group Permissions</em></p>

<hr>

<h3>4.12 SMB File Share</h3>

<p><strong>What was done:</strong> Configured the IT departmental folder as an SMB network share.</p>

<pre>
\\DC01\IT
</pre>

<p><strong>Why it matters:</strong> SMB allows authorized Windows users to access shared departmental resources over the network.</p>

<p><strong>Evidence:</strong></p>

<p align="center">
  <img src="./Evidence/12-File-Server-IT-Share.png" width="760" alt="IT File Server Share">
</p>
<p align="center"><em>Figure 12 — IT File Server Share</em></p>

<hr>

<h3>4.13 Share Access Verification</h3>

<p><strong>What was done:</strong> Verified the IT share locally using <code>\\localhost\IT</code>.</p>

<p><strong>Why it matters:</strong> This confirms that the configured SMB share is reachable from the server.</p>

<p><strong>Evidence:</strong></p>

<p align="center">
  <img src="./Evidence/13-IT-Share-Access-Verification.png" width="760" alt="IT Share Access Verification">
</p>
<p align="center"><em>Figure 13 — IT Share Access Verification</em></p>

<hr>

<h3>4.14 Test User & Group Assignment</h3>

<p><strong>What was done:</strong> Verified the IT test user's membership in the IT security group.</p>

<pre>
IT Test User
      ↓
GG-IT-Users
      ↓
IT Department Resources
</pre>

<p><strong>Why it matters:</strong> This demonstrates the relationship between user identity, security-group membership, and department-level resource access.</p>

<p><strong>Evidence:</strong></p>

<p align="center">
  <img src="./Evidence/14-IT-TestUser-Group-Membership.png" width="760" alt="IT Test User Group Membership">
</p>
<p align="center"><em>Figure 14 — IT Test User Group Membership</em></p>

<hr>

<h2>5. Security Controls Demonstrated</h2>

<table>
<tr><th>Security Control</th><th>Implementation</th></tr>
<tr><td><strong>Centralized Identity</strong></td><td>Active Directory Domain Services</td></tr>
<tr><td><strong>Group-Based Access Control</strong></td><td>Department security groups</td></tr>
<tr><td><strong>Least Privilege</strong></td><td>Department-specific NTFS permissions</td></tr>
<tr><td><strong>Password Security</strong></td><td>Domain password policy</td></tr>
<tr><td><strong>Account Protection</strong></td><td>Account lockout policy</td></tr>
<tr><td><strong>Resource Separation</strong></td><td>Departmental folders and shares</td></tr>
<tr><td><strong>Centralized Administration</strong></td><td>Active Directory and Group Policy</td></tr>
</table>

<hr>

<h2>6. Troubleshooting Experience</h2>

<h3>6.1 VirtualBox Driver / Service Issue</h3>

<p>
A VirtualBox host-driver/service error prevented virtual machines from starting correctly.
The issue was investigated using Windows command-line and service checks and resolved so
the virtual machines could run again.
</p>

<h3>6.2 Windows Client Deployment</h3>

<p>
The Windows client VM encountered boot and installation problems involving UEFI,
Secure Boot, and Windows setup requirements. The client deployment was not counted
as a completed project feature; the completed project focuses on the Windows Server
infrastructure.
</p>

<hr>

<h2>7. Technologies & Tools</h2>

<table>
<tr><th>Technology / Tool</th><th>Purpose</th></tr>
<tr><td>Windows Server</td><td>Core server infrastructure</td></tr>
<tr><td>Active Directory Domain Services</td><td>Centralized identity and directory management</td></tr>
<tr><td>DNS</td><td>Domain name resolution</td></tr>
<tr><td>Group Policy</td><td>Centralized security policy</td></tr>
<tr><td>NTFS</td><td>File-system access control</td></tr>
<tr><td>SMB</td><td>Windows network file sharing</td></tr>
<tr><td>PowerShell</td><td>Windows administration and troubleshooting</td></tr>
<tr><td>Command Prompt</td><td>System and network troubleshooting</td></tr>
<tr><td>Oracle VirtualBox</td><td>Virtual lab environment</td></tr>
</table>

<hr>

<h2>8. Skills Demonstrated</h2>

<ul>
  <li>Windows Server Administration</li>
  <li>Active Directory Administration</li>
  <li>DNS Management</li>
  <li>User & Security Group Management</li>
  <li>Organizational Unit Design</li>
  <li>Group Policy Configuration</li>
  <li>File Server Administration</li>
  <li>NTFS Permission Management</li>
  <li>SMB Share Configuration</li>
  <li>Access Control</li>
  <li>Infrastructure Troubleshooting</li>
  <li>Technical Documentation</li>
</ul>

<hr>

<h2>9. Real-World Relevance</h2>

<ol>
  <li>Centralize employee identity with Active Directory.</li>
  <li>Organize employees by department using OUs.</li>
  <li>Manage resource access through security groups.</li>
  <li>Enforce authentication security policies centrally.</li>
  <li>Provide departmental shared storage.</li>
  <li>Apply NTFS permissions according to job requirements.</li>
  <li>Verify access and infrastructure configuration.</li>
  <li>Troubleshoot Windows infrastructure issues.</li>
</ol>

<hr>

<h2>10. Project Scope</h2>

<p>
This is a self-built lab environment created for hands-on learning and portfolio demonstration.
Only configurations and results that were actually completed and verified during the lab are
presented as implemented.
</p>

<p>
The unfinished bulk PowerShell user-provisioning automation and unsuccessful Windows client
deployment are intentionally not presented as completed features.
</p>

<hr>

<h2>11. Author</h2>

<p>
<strong>Mohammed Aleem Hasan</strong><br>
BCA Student • Aspiring IT Support / System & Network Administrator
</p>

<hr>

<p align="center">
  <strong>Windows Server • Active Directory • DNS • Group Policy • File Server • Access Control</strong>
</p>
