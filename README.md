
## Phase 1 – Group Infrastructure

### 1. Create devops_interns
Command:
groupadd -g 4000 devops_interns


### 2. Create temporary_admins
Command:
groupadd temporary_admins



### 3. Rename Group and Change GID
Command:
groupmod -n sysadmins -g 5000 temporary_admins


### 4. Verify Groups
Command:
tail -n 5 /etc/group


## Phase 2 – User Provisioning

### 1. Create sysadmin1
Command:
useradd -u 2001 -s /bin/sh sysadmin1


### 2. Create sysadmin2
Command:
useradd -u 2002 -g sysadmins sysadmin2


### 3. Create sysadmin3
Command:
useradd sysadmin3



### 4. Set Password
Command:
passwd sysadmin3


### 5. Verify Users
Command:
grep -E 'sysadmin1|sysadmin2|sysadmin3' /etc/passwd


## Phase 3 – Account Modification & Membership

### 1. Change GECOS
Command:
usermod -c "Senior System Admin" sysadmin1


### 2. Change Login Name
Command:
usermod -l lead_admin sysadmin1

### 3. Add Secondary Group
Command:
usermod -aG devops_interns sysadmin2


### 4. Change Primary Group
Command:
usermod -g sysadmins sysadmin3


### 5. Remove Secondary Group
Command:
gpasswd -d sysadmin2 devops_interns


## Phase 4 – Verification & Cleanup

### 1. Verify User IDs
Command:
id lead_admin
id sysadmin2
id sysadmin3


### 2. Check Group Membership
Command:
grep '^sysadmins:' /etc/group


### 3. Delete sysadmin3
Command:
userdel -r sysadmin3


### 4. Final Verification
Command:
grep '^sysadmin3:' /etc/passwd
