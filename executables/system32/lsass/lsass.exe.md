
## LSASS ASCII diagrams:

### User Authentication:

```
  User Input (Username, Password)
       |
  Winlogon.exe (User Interface)
       |
  LSASS.exe (Local Security Authority Subsystem Service)
       |-----------------> Authentication Protocols
       |                  |-----> Kerberos
       |                  |       |-----> Domain Controller (If Domain Account)
       |                  |       |-----> Local SAM Database (If Local Account)
       |                  |-----> NTLM
       |                  |       |-----> Domain Controller (If Domain Account)
       |                  |       |-----> Local SAM Database (If Local Account)
       |-----------------> LSA (Local Security Authority)
       |
  SAM (Security Account Manager)
       |
  Read User Info from Registry
       |
  Compare Hashed Password
       |
  Generate Access Token
       |-----> Include User's SID
       |-----> Include Group SIDs
       |-----> Include Privileges
       |
  Create User Session
       |
  Access Granted/Denied (Logon or Error Message)

```

### Password Change:

```
  User Input (Ctrl+Alt+Del, Old Password, New Password)
       |
  Application (Change Password Dialog)
       |
  LSASS.exe (Local Security Authority Subsystem Service)
       |-----------------> Authentication Protocols
       |                  |-----> Validate Old Password
       |                  |-----> Generate New Password Hash
       |-----------------> LSA (Local Security Authority)
       |
  SAM (Security Account Manager)
       |
  Update Password Hash in Database
       |
  Synchronize with Domain (If Domain Account)
       |-----> Notify Domain Controller
       |-----> Update in Active Directory
       |
  Confirmation/Error Message

```

### Access Token Creation:

```
  User Login (Successful Authentication)
       |
  LSASS.exe (Local Security Authority Subsystem Service)
       |
  Create Access Token
       |-----> Include User's SID (Security Identifier)
       |-----> Include Group SIDs (Security Groups)
       |-----> Include Privileges (User Rights)
       |-----> Include Logon Session Data
       |-----> Include Other Attributes (e.g., Session Type)
       |
  Assign to Process (e.g., Explorer.exe)
       |
  Process Runs with User's Security Context
       |
  Monitor and Manage User Session
       |-----> Handle Permissions
       |-----> Monitor Session Activities
```

### Kerberos Authentication (in a domain environment):

```
  User Input (Username, Password)
       |
  Winlogon.exe (User Interface)
       |
  LSASS.exe (Local Security Authority Subsystem Service)
       |
  Kerberos.dll (Kerberos Protocol)
       |-----> AS Request to Domain Controller (Authentication Service)
       |       |-----> Include Pre-Authentication Data
       |       <---- AS Response (TGT - Ticket Granting Ticket)
       |
       |-----> TGS Request to Domain Controller with TGT (Ticket Granting Service)
       |       |-----> Include Service Request Information
       |       <---- TGS Response (Service Ticket)
       |
  Validate Service Ticket
       |
  Generate Access Token
       |-----> Include User's SID
       |-----> Include Group SIDs
       |-----> Include Privileges
       |
  Create User Session
       |
  Access Granted/Denied (Logon or Error Message)
```

### Interaction with Third-party Authentication:

```
  User Input (Custom Credentials)
       |
  Winlogon.exe (User Interface)
       |
  LSASS.exe (Local Security Authority Subsystem Service)
       |
  Third-party Authentication Package (Custom Protocol)
       |-----------------> Custom Verification Process (e.g., Biometrics, Smart Card)
       |                  |-----> Hardware/Software Interaction
       |                  |-----> Custom Security Checks
       |                  |-----> Additional Verification Steps (e.g., Multi-Factor)
       |                  <---- Verification Result (Success/Failure)
       |
  Generate Access Token (If Successful)
       |-----> Include User's SID
       |-----> Include Group SIDs
       |-----> Include Privileges
       |
  Create User Session (If Successful)
       |
  Access Granted/Denied (Logon or Error Message)
```

## LSASS detailed diagram:

![image](https://github.com/mthcht/Windows-Learning-Diagrams/assets/75267080/e05b92e6-d3f0-4b41-9567-9a01c7e3dce2)

![image](https://github.com/mthcht/Windows-Learning-Diagrams/assets/75267080/2b12ae1d-335d-4ae4-904d-bddf2db1fede)

## LSASS microsoft diagrams:

ref: https://learn.microsoft.com/en-us/windows-server/security/windows-authentication/credentials-processes-in-windows-authentication

![image](https://github.com/mthcht/Windows-Learning-Diagrams/assets/75267080/b11e4faa-22ef-4556-867f-9c1b80d708fa)

![image](https://github.com/mthcht/Windows-Learning-Diagrams/assets/75267080/a1978a1f-37ff-4092-95fb-f54e8f7d177c)

![image](https://github.com/mthcht/Windows-Learning-Diagrams/assets/75267080/ee0dc0b7-223b-48f6-a52f-e9cc7d3a5b69)

Windows Hello:
ref:https://learn.microsoft.com/en-us/windows/security/identity-protection/hello-for-business/hello-how-it-works-authentication

![image](https://github.com/mthcht/Windows-Learning-Diagrams/assets/75267080/b6e6770b-4b6d-49b5-9efe-c11fd47f0fb1)


## LSASS to a 5-year-old:
![lsass_winlogon](https://github.com/mthcht/Windows-Learning-Diagrams/assets/75267080/5decfb34-122b-4b63-b2e7-4214df16744c)
