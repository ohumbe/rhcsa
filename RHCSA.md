# RHCSA Material

## SELinux

### Goal
Learn to protect and manage the security of a server by using SELinux.

### Objectives
- Describe how SELinux works and how to switch a server between its various enforcment modes.

- Adjust the SELinux type of a file in order to control which processes can access it.

- Change the accesses allowed by the SELinux policy by setting tunable parameters called SELinux boolean.

- Perform basic investigation and troubleshooting of accesses blocked by SELinux.

### Content
#### What is SELinux?

- SELinux: Security Enhanced Linux

- Originally created by the NSA as a series of patches to the Linux kernel using Linux Security Modules.

- How does SELinux provide additional security to Linux?

  - How do we provide security to our system (or files) at the moment?

    - Providing ownership or group association to files/directories

    - Allowing users into particular groups and giving those groups access to something through ACLs

    - Modifying rwx permissions to our files/directories

    - All these are examples of discretionary access controls (DAC), where the user has discretion over access controls

  - What does SELinux add?

    - SELinux defines a set of security rules that determine which process can access which files, directories, and ports.

    - Every file, process, directory, and port has a special security label called an SELinux context.  While SELinux labels have several contexts (e.g. user, role, type, and sensitivity), what we really care most about for the RHCSA is the type.

    - How do we view these SELinux labels?
      
      A: `ls -lZ`; `ps -efZ`; etc.

- What are the different SELinux modes and how do you change them?

  - Enforcing, Permissive, Disabled

  - Check them using `getenforce`, set them (temporarily) using `setenforce`, and change the permanent setting in /etc/selinux/config

- How do you Control SELinux file contexts?

  - `semanage fcontext` && `chcon`

  - ports: `semanage port -a -t http_port_t -p tcp`

- Booleans

  - What are booleans?

    Booleans are simple on/off settings for SELinux, e.g. "do we allow the http server to access home directories?"; "do we allow haproxy to access any port available?"

  - How do you adjust SELinux policy with booleans?

    - First you could see a list of booleans and values with `getsebool`

    - The `semanage boolean -l` gives you more information

    - To list booleans in which the current state differs from the default state, run semanage boolean -l -C

    - You could temporarily change a boolean value with `setsebool httpd_enable_homedirs on` & make sure to add -P for permanent


- How do you troubleshoot SELinux issues?

  - First, install setroubleshoot & setroubleshoot-server; then restart the auditd service - this is the recommended way to go


## Logging

#### Intro: rsyslog service (persists through reboot) + systemd-journald (temp)

#### /var/log; which is also used for services that are not logged using syslog

#### Configuring logging events to the system

- facility & priority

- man rsyslog.conf

- logrotate; example /var/log/messages-$DATE

#### Example: humbe.log & HAProxy

humbe.log:
- edit /etc/rsyslog.conf:
*.info                                                  /var/log/humbe.log


haproxy.conf in /etc/rsyslog.d/:
local0.*  /var/log/haproxy-traffic.log
local0.info /var/log/haproxy-admin.log


#### journalctl

- example: two terminals; test `journalctl -xf` while sshing, logging in as root, changing somehting, etc.
- journalctl --since "-1 hour"
