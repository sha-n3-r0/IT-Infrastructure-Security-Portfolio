# Day 1 Ticket: Cannot Access Marketing Shared Drive

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

## Ticket 3 Objective
Identify the cause of the office-wide printer outage and restore printing services for all users.

---

## Tasks Performed
- Investigated the reported issue to determine the root cause.
- Verified that all office printers were showing as offline.
- Checked the status of the print server.
- Identified that the print server service was degraded.
- Rebooted the print server.
- Verified that the print services were restored.
- Confirmed that users were able to print successfully.

---

## Root Cause

### Print Server Service Degraded

**Cause:**
- The print server service became degraded, causing all network printers to appear offline and preventing users from printing.

---

## Skills Learned
- Print Server Troubleshooting
- Root Cause Analysis
- Windows Server Administration
- Network Printing
- Service Recovery
- Incident Resolution

---

## Issues Encountered

### All Office Printers Offline

**Symptoms:**
- All printers across the office appeared offline.
- Print jobs were not processed.
- Users from multiple floors experienced the same issue.

**Resolution:**
- Investigated the issue and identified the print server as the source of the problem.
- Found that the print server service was degraded.
- Rebooted the print server to restore the service.
- Confirmed that the printers came back online and users were able to print normally.

---

## Learning Reflection

This ticket taught me the importance of checking the central print server when multiple users report printer issues. Instead of troubleshooting individual printers, I focused on identifying the root cause, which was a degraded print server. Rebooting the server restored the printing service for the entire office. This experience improved my understanding of centralized print management and efficient troubleshooting.

## Base Action

First, I investigated the root cause of the problem to determine why none of the office printers were working. After checking the print server, I found that the print service was degraded, which caused all printers to appear offline. I immediately rebooted the print server, and once it came back online, I confirmed that the printers were working normally again.

## Ticket 4 Objective
Correct the user's system time and time zone to restore accurate meeting schedules and file timestamps.

---

## Tasks Performed
- Connected to the user's computer remotely.
- Checked the system date, time, and time zone settings.
- Identified that the computer was configured to the wrong time zone.
- Changed the time zone from Eastern Time to the correct Central Time zone.
- Checked for pending Windows system updates.
- Installed the available system updates.
- Verified that the system time synchronized correctly.
- Confirmed that Team Chat meetings and file timestamps displayed the correct time.

---

## Root Cause

### Incorrect Time Zone Configuration

**Cause:**
- The computer was configured to the wrong time zone, causing incorrect meeting schedules and file timestamps.
- The system also had pending updates that could affect time synchronization.

---

## Skills Learned
- Remote Desktop Support
- Windows Date and Time Configuration
- Time Zone Troubleshooting
- Windows Update Management
- System Time Synchronization
- User Support

---

## Issues Encountered

### Incorrect System Time

**Symptoms:**
- Computer was set to Eastern Time instead of Central Time.
- System clock was a few minutes behind.
- Team Chat meetings appeared at the wrong times.
- File timestamps were incorrect.

**Resolution:**
- Connected to the user's computer remotely.
- Corrected the system time zone to Central Time.
- Checked for pending Windows updates and installed them.
- Verified that the system time synchronized correctly.
- Confirmed that meeting schedules and file timestamps were accurate.

---

## Learning Reflection

This ticket helped me understand the importance of verifying both the system time zone and Windows updates when troubleshooting time-related issues. I learned that an incorrect time zone can affect meetings, file timestamps, and other system functions. By correcting the time zone and installing pending updates, I was able to restore the system to the correct time and resolve the user's issue.

## Base Action

I remotely connected to the user's computer and checked the desktop's time zone settings. I corrected the time zone to the correct one and verified that the system time was accurate. I also checked for pending system updates and found that the desktop was not up to date, so I installed the available updates to ensure the system was running properly.

## Ticket 5 Objective
Restore the user's second monitor by identifying and resolving the cause of the display issue.

---

## Tasks Performed
- Reviewed the troubleshooting steps already performed by the user.
- Connected to the user's computer remotely.
- Checked the display settings and system status.
- Initially suspected that the display cable needed to be replaced.
- Determined that the issue was caused by pending system updates.
- Installed the required Windows updates.
- Restarted the computer.
- Verified that the second monitor was detected and functioning correctly.
- Informed the user that the issue had been resolved.

---

## Root Cause

### Pending System Updates

**Cause:**
- The computer had pending system updates that affected the display functionality.
- After installing the updates and restarting the computer, the second monitor was detected normally.

---

## Skills Learned
- Remote Desktop Support
- Multi-Monitor Troubleshooting
- Windows Update Management
- Display Configuration
- Root Cause Analysis
- User Communication

---

## Issues Encountered

### Second Monitor Not Detected

**Symptoms:**
- Monitor displayed **"No Signal."**
- Computer did not detect the second monitor.
- Monitor functioned correctly when tested on another laptop.

**Resolution:**
- Reviewed the user's troubleshooting steps.
- Checked the computer for pending system updates.
- Installed the updates and restarted the computer.
- Confirmed that the second monitor was detected and working properly.
- Notified the user that the issue had been resolved.

---

## Learning Reflection

At first, I assumed the issue was caused by a faulty display cable and considered replacing it. However, after reviewing the ticket more carefully, I found that the problem was resolved by installing the pending system updates and restarting the computer. This experience taught me the importance of reviewing all available information before making assumptions and following a structured troubleshooting process.

## Base Action

My first assumption was to replace the display cable, but I realized that I had misread the ticket. The issue only required a system update. After installing the update and restarting the computer, the monitor worked fine. I then informed Amanda Foster that the issue had been resolved and that the monitor was ready to use.
