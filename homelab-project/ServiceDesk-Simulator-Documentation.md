# Day 2 Ticket: Cannot Access Marketing Shared Drive

## Ticket 1 Objective
Diagnose and resolve a remote user's inability to access files on the Marketing shared drive while working from home.

---

## Tasks Performed
- Connected to the user's computer remotely.
- Performed initial troubleshooting and analyzed the reported issue.
- Verified that the user's VPN connection was disconnected.
- Confirmed that the mapped network drives were showing as **Disconnected**.
- Checked the existing documentation to verify the correct Marketing file server path.
- Reconnected the VPN.
- Verified that the file server path was accessible.
- Confirmed that the Marketing shared drive was successfully restored.

---

## Root Cause

### VPN Disconnected

**Cause:**
- The user was working remotely without an active VPN connection.
- Since the Marketing file server is hosted on the internal network, the disconnected VPN prevented access, resulting in the error:
  > "The network path was not found."

---

## Skills Learned
- Remote Desktop Support
- VPN Troubleshooting
- Network Drive Troubleshooting
- File Server Path Verification
- Documentation Review
- Root Cause Analysis

---

## Issues Encountered

### Unable to Access Marketing Shared Drive

**Symptoms:**
- Error message: **"The network path was not found."**
- Mapped drives displayed as **Disconnected**.
- Internet and email were working normally.

**Resolution:**
- Connected to the user's computer remotely.
- Identified that the VPN connection was disconnected.
- Verified the correct Marketing file server path using internal documentation.
- Reconnected the VPN.
- Confirmed that the mapped drives reconnected successfully and the user regained access to the Marketing shared drive.

---

## Learning Reflection

This ticket reinforced the importance of checking VPN connectivity when remote users cannot access internal company resources. I also learned how to verify network file server paths using documentation and troubleshoot disconnected mapped drives. Although I am still learning the service desk workflow, this experience improved my confidence in identifying the root cause and resolving similar connectivity issues efficiently.

## Base Action

First, I connected to the user remotely and performed an analysis to determine the root cause of the problem. I found that the VPN was disconnected, and the user's file server was unreachable. I checked the existing documentation to verify the correct path for the Marketing file server. After resolving the issue, I realized that I am still grasping the workflow, but I know I will become more comfortable and efficient with it in no time.

---

## Ticket 2 Objective
Restore the user's access by resetting their expired password and verifying their identity according to company security procedures.

---

## Tasks Performed
- Verified the user's identity by asking for the required account details.
- Confirmed that the password had expired after the user had been away for three weeks.
- Sent a verification code to the user's registered contact method.
- Asked the user to provide the verification code for identity confirmation.
- Reset the user's password and provided a temporary password.
- Instructed the user to log in using the temporary password and create a new password.

---

## Root Cause

### Expired Password

**Cause:**
- The user's password expired while they were away on vacation.
- The password could not be changed from the Windows login screen, preventing access to the computer.

---

## Skills Learned
- Identity Verification
- Password Reset Procedures
- Account Security
- User Authentication
- Help Desk Support
- Security Best Practices

---

## Issues Encountered

### User Unable to Log In

**Symptoms:**
- Password expired message appeared at login.
- Unable to change the password from the login screen.
- User could not access their development environment.

**Resolution:**
- Verified the user's identity before performing the password reset.
- Sent a verification code and confirmed it with the user.
- Reset the account password and issued a temporary password.
- Instructed the user to change the temporary password after successfully logging in.

---

## Learning Reflection

The first procedure I performed was to verify the user's identity because password resets require strict security procedures. After confirming the user's identity through a verification code, I reset the expired password and provided a temporary password so the user could log in and create a new one. This ticket helped me understand the importance of following security policies during account recovery while providing timely support to the user.

## Base Action

First, I verified the employee's identity by asking for her details because password resets require careful verification. She informed me that her password had expired. Before resetting it, I sent a verification code to her registered contact and asked her to send it back to confirm her identity. After the verification was completed, I provided her with a temporary password so she could log in and create a new password.
