# Day 2 Ticket: Cannot Access Marketing Shared Drive

## Objective
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
