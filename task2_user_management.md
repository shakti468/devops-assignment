#Task 2

## User Management and Access Control

## Creating User Accounts
sudo useradd -m -s /bin/bash sarah
sudo useradd -m -s /bin/bash mike
sudo passwd sarah
sudo passwd mike

## Terminal output 
Everything up-to-date
root@e409703:~/batch10/devops-assignment# sudo useradd -m -s /bin/bash sarah
root@e409703:~/batch10/devops-assignment# sudo passwd sarah
New password:
Retype new password:
passwd: password updated successfully
root@e409703:~/batch10/devops-assignment# sudo useradd -m -s /bin/bash mike
root@e409703:~/batch10/devops-assignment# sudo passwd mike
New password:
Retype new password:
passwd: password updated successfully

## Creating Isolated Directories
sudo mkdir -p /home/sarah/workspace
sudo mkdir -p /home/mike/workspace
sudo chown sarah:sarah /home/sarah/workspace
sudo chown mike:mike /home/mike/workspace
sudo chmod 700 /home/sarah/workspace
sudo chmod 700 /home/mike/workspace

## Terminal output 
root@e409703:~/batch10/devops-assignment# sudo mkdir -p /home/mike/workspace
root@e409703:~/batch10/devops-assignment# sudo chown sarah:sarah /home/sarah/workspace
root@e409703:~/batch10/devops-assignment# ls -ld /home/sarah/workspace
drwxr-xr-x 2 sarah sarah 4096 Mar 24 23:56 /home/sarah/workspace
root@e409703:~/batch10/devops-assignment# sudo chown mike:mike /home/mike/workspace
root@e409703:~/batch10/devops-assignment# ls -ld /home/mike/workspace
drwxr-xr-x 2 mike mike 4096 Mar 24 23:59 /home/mike/workspace
root@e409703:~/batch10/devops-assignment# sudo chmod 700 /home/sarah/workspace
root@e409703:~/batch10/devops-assignment# sudo chmod 700 /home/mike/workspac
chmod: cannot access '/home/mike/workspac': No such file or directory
root@e409703:~/batch10/devops-assignment# sudo chmod 700 /home/mike/workspac
chmod: cannot access '/home/mike/workspac': No such file or directory
root@e409703:~/batch10/devops-assignment# sudo chmod 700 /home/mike/workspace
root@e409703:~/batch10/devops-assignment# sudo apt install libpam-pwquality -y


##  Enforcing Password Policy
sudo nano /etc/security/pwquality.conf


## Modified
minlen = 12
dcredit = -1
ucredit = -1
lcredit = -1
ocredit = -1
retry = 3


## Set password expiration:
sudo chage -M 30 sarah
sudo chage -M 30 mike

## Terminal output 
root@e409703:~/batch10/devops-assignment# sudo chage -M 30 sarah
root@e409703:~/batch10/devops-assignment# sudo chage -l sarah
Last password change                                    : Mar 24, 2025
Password expires                                        : Apr 23, 2025
Password inactive                                       : never
Account expires                                         : never
Minimum number of days between password change          : 0
Maximum number of days between password change          : 30
Number of days of warning before password expires       : 7
root@e409703:~/batch10/devops-assignment# sudo chage -M 30 mike
root@e409703:~/batch10/devops-assignment# sudo chage -l mike
Last password change                                    : Mar 24, 2025
Password expires                                        : Apr 23, 2025
Password inactive                                       : never
Account expires                                         : never
Minimum number of days between password change          : 0
Maximum number of days between password change          : 30
Number of days of warning before password expires       : 7

## Check user directories
ls -ld /home/sarah/workspace /home/mike/workspace


## Terminal output 
root@e409703:~/batch10/devops-assignment# ls -ld /home/sarah/workspace /home/mike/workspace
drwx------ 2 mike  mike  4096 Mar 24 23:59 /home/mike/workspace
drwx------ 2 sarah sarah 4096 Mar 24 23:56 /home/sarah/workspace
