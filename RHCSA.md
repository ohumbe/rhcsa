# RHCSA Material

## SELinux

### Goal
Learn to protect and manage the security of a server by using SELinux.

### Objectives
- Describe how SELinux works and how to switch a server between its various enforcment modes.

- Adjust the SELinux type of a file in order to control which processes can access it.

- Change the accesses allowed by the SELinux policy by setting tunable parameters called SELinux boolean.

- Perform basic investigation and troubleshooting of accesses blocked by SELinux.


#### What is SELinux?

- SELinux: Security Enhanced Linux

- Originally created by the NSA as a series of patches to the Linux kernel using Linux Security Modules.

- How does SELinux provide additional security to Linux?

  - How do we provide security to our system (or files) at the moment?

    - Providing ownership or group association to files/directories

    - Allowing users into particular groups and giving those groups access to something through ACLs

    - Modifying rwx permissions to our files/directories

    - All these are examples of discretionary access controls (DAC), where the user has discretion over access controls

