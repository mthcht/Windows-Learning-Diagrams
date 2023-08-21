
## LSASS ASCII diagrams:

### User Authentication:

```
  User Input (Username, Password)
       |
  Winlogon.exe (User Interface)
       |
  LSASS.exe (Local Security Authority Subsystem Service)
       |-----------------> Kerberos/NTLM (Authentication Protocols)
       |                  |-----> Domain Controller (If Domain Account)
       |                  |-----> Local SAM Database (If Local Account)
       |-----------------> LSA (Local Security Authority)
       |
  SAM (Security Account Manager)
       |
  Read User Info from Registry
       |
  Compare Hashed Password
       |
  Generate Access Token
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
       |-----------------> Kerberos/NTLM (Authentication Protocols)
       |                  |-----> Validate Old Password
       |                  |-----> Generate New Password Hash
       |-----------------> LSA (Local Security Authority)
       |
  SAM (Security Account Manager)
       |
  Update Password Hash in Database
       |
  Synchronize with Domain (If Domain Account)
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
       |-----------------> Include User's SID (Security Identifier)
       |-----------------> Include Group SIDs (Security Groups)
       |-----------------> Include Privileges (User Rights)
       |-----------------> Include Logon Session Data
       |
  Assign to Process (e.g., Explorer.exe)
       |
  Process Runs with User's Security Context
       |
  Monitor and Manage User Session
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
       |       <---- AS Response (TGT - Ticket Granting Ticket)
       |
       |-----> TGS Request to Domain Controller with TGT (Ticket Granting Service)
       |       <---- TGS Response (Service Ticket)
       |
  Validate Service Ticket
       |
  Generate Access Token
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
       |                  <---- Verification Result (Success/Failure)
       |
  Generate Access Token (If Successful)
       |
  Create User Session (If Successful)
       |
  Access Granted/Denied (Logon or Error Message)
```

## LSASS detailed diagram:

## LSASS to a 5-year-old:
![lsass_winlogon](https://github.com/mthcht/Windows-Learning-Diagrams/assets/75267080/5decfb34-122b-4b63-b2e7-4214df16744c)
