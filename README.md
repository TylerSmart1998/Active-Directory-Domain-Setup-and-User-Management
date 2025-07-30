# Active Directory Lab Guide

## Part 1: Install Active Directory and Setup Domain

1. **Login to DC-1** and install **Active Directory Domain Services**.
2. Promote DC-1 as a Domain Controller:
   - Setup a new forest: `mydomain.com` (replace with your domain name).
3. Restart DC-1 and log in as: `mydomain.com\labuser`.
4. Open **Active Directory Users and Computers (ADUC)**:
   - Create Organizational Units (OUs):
     - `_EMPLOYEES`
     - `_ADMINS`
   - Create user:
     - Name: Jane Doe
     - Username: `jane_admin`
     - Password: 
   - Add `jane_admin` to the **Domain Admins** security group.
5. Log out and log back in as `mydomain.com\jane_admin`.  
   From now on, use `jane_admin` as your admin account.
6. **Join Client-1 to the domain**:
   - Log in to Client-1 locally as `labuser`.
   - Join domain: `mydomain.com`.
   - Restart Client-1.
7. On DC-1, verify **Client-1** shows in ADUC.
8. Create a new OU: `_CLIENTS`.
9. Move the Client-1 computer object into the `_CLIENTS` OU.

---

## Part 2: Remote Desktop Setup & Bulk User Creation

1. Power on DC-1 and Client-1 VMs if off.
2. On Client-1, logged in as `mydomain.com\jane_admin`:
   - Open **System Properties**.
   - Go to **Remote Desktop** tab.
   - Enable Remote Desktop.
   - Allow **Domain Users** group remote desktop access.
3. On DC-1, log in as `jane_admin`.
4. Open **PowerShell ISE** as Administrator.
5. Create and run a script to bulk-create users in the `_EMPLOYEES` OU.
6. Verify new users in ADUC under `_EMPLOYEES`.
7. Test logging into Client-1 with one of the new users (use the script’s password).

---

## Part 3: Account Lockout Policy

1. Log into DC-1 as `jane_admin`.
2. Pick a user and try logging in with a bad password 10 times.
3. Configure **Group Policy** to lock out accounts after **5** failed login attempts:
   - Open Group Policy Management.
   - Edit Default Domain Policy or create a new GPO.
   - Navigate to: `Computer Configuration -> Policies -> Windows Settings -> Security Settings -> Account Policies -> Account Lockout Policy`.
   - Set **Account lockout threshold** to 5 invalid attempts.
4. Try logging in 6 times with a bad password.
5. Verify the user is locked out in Active Directory.
6. Unlock the user account.
7. Reset the user’s password.
8. Attempt login with the correct password.

---

## Part 4: Enable/Disable Accounts & Logs

1. Disable the test user account in Active Directory.
2. Attempt to log in with the disabled account (expect failure).
3. Re-enable the user account.
4. Attempt to log in again (should succeed).
5. Review Event Logs:
   - On **Domain Controller (DC-1)**: check Security logs for account lockouts and logins.
   - On **Client-1**: check logs for Remote Desktop and login events.
