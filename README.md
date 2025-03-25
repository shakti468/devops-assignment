# Task 1: System Monitoring Setup

## 📌 Overview
This task involves setting up system monitoring tools to track CPU, memory, process usage, and disk utilization. Additionally, we configure automatic logging for resource monitoring.

---

## 📂 Steps to Implement

### **1️⃣ Install Monitoring Tools**
We install `htop` and `nmon` for real-time system monitoring.

```bash
sudo apt update
sudo apt install -y htop nmon
```

👉 **Installed `htop` and `nmon` successfully.**

---

### **2️⃣ Check CPU, Memory, and Process Usage**
We use the following commands to track system resources:

```bash
htop        # Interactive process monitoring
nmon        # Real-time system performance
free -m     # Memory usage
df -h       # Disk space usage
du -sh /    # Total disk usage
ps aux --sort=-%cpu | head -5   # Top 5 CPU-intensive processes
```

📉 **Outputs:**
#### **🔹 htop Output**
![image](https://github.com/user-attachments/assets/72a93632-78a4-494d-ac27-8df44ee7541f)


#### **🔹 nmon Output**
![image](https://github.com/user-attachments/assets/b339ab63-4c05-4cd7-8741-5ca24fe7347c)


#### **🔹 Memory Usage (`free -m`)**

![image](https://github.com/user-attachments/assets/1821648b-d4dc-4dad-ba82-2c1e903b58a1)



#### **🔹 Disk Usage (`df -h` and `du -sh /`)**

![image](https://github.com/user-attachments/assets/f85d4b0c-40fe-420e-96a4-595b1b79c862)


#### **🔹 Top 5 CPU-Intensive Processes**

![image](https://github.com/user-attachments/assets/27f52933-9b28-4932-b028-f975634d1611)



---

### **3️⃣ Log System Metrics Every 5 Minutes**
We set up a cron job to log system metrics automatically.

```bash
crontab -e
```
Add this line to log CPU, memory, and disk usage every 5 minutes:

```bash
*/5 * * * * (date; free -m; df -h; ps aux --sort=-%cpu | head -5) >> /var/log/system_monitor.log
```

👉 **Cron job configured successfully.**

---

### **4️⃣ Verify Log File**
To check the system monitoring log:

```bash
cat /var/log/system_monitor.log
```

📉 **Output:**
#### **🔹 System Monitoring Log (`cat /var/log/system_monitor.log`)**
![image](https://github.com/user-attachments/assets/34f61ce1-4367-48d8-b6b8-206807615a06)


---

## 📌 Conclusion
- **✅ Installed and configured system monitoring tools (`htop`, `nmon`).**  
- **✅ Tracked system performance (CPU, memory, disk usage).**  
- **✅ Configured cron job to log system metrics every 5 minutes.**  
- **✅ Verified the logs to ensure proper monitoring.**  

---

# Task 2: User Management and Access Control

## 📌 Overview
This task involves creating user accounts for Sarah and Mike, setting up secure directories with proper permissions, and enforcing password policies for enhanced security.

---

## 📂 Steps to Implement

### **1️⃣ Create User Accounts**
We create user accounts for Sarah and Mike with secure passwords.

```bash
sudo useradd -m -s /bin/bash sarah
sudo useradd -m -s /bin/bash mike
sudo passwd sarah
sudo passwd mike
```

👉 **Users `sarah` and `mike` created successfully.**

#### **🔹 User Accounts Creation Output**
![image](https://github.com/user-attachments/assets/ed840deb-5df9-42d8-9ef2-2c027411ca49)


---

### **2️⃣ Create Isolated Directories**
We set up separate workspace directories for each user and restrict access.

```bash
sudo mkdir -p /home/sarah/workspace
sudo mkdir -p /home/mike/workspace
```

Assign ownership:
```bash
sudo chown sarah:sarah /home/sarah/workspace
sudo chown mike:mike /home/mike/workspace
```

Set permissions:
```bash
sudo chmod 700 /home/sarah/workspace
sudo chmod 700 /home/mike/workspace
```

👉 **Each user now has an isolated and secured workspace.**

---

### **3️⃣ Enforce Password Expiration and Complexity**
To enforce security policies, we configure password expiration and complexity rules.

Install password policy package:
```bash
sudo apt install libpam-pwquality -y  # Ubuntu/Debian
sudo yum install pam_pwquality -y     # CentOS/RHEL
```

Edit password policy:
```bash
sudo nano /etc/security/pwquality.conf
```
Modify or add the following rules:
```
minlen = 12
dcredit = -1
ucredit = -1
lcredit = -1
ocredit = -1
retry = 3
```

Set password expiration to 30 days:
```bash
sudo chage -M 30 sarah
sudo chage -M 30 mike
```

👉 **Password policy applied successfully.**

#### **🔹 Password Policy Configuration Output**
![image](https://github.com/user-attachments/assets/5002f6d4-3f7b-4db7-a9c3-c204262507d7)


---

### **4️⃣ Verify User Permissions**
To confirm that only the respective user can access their workspace:
```bash
ls -ld /home/sarah/workspace
ls -ld /home/mike/workspace
```

👉 **Permissions verified successfully.**

#### **🔹 User Permissions Verification Output**
![image](https://github.com/user-attachments/assets/c59f128d-14f4-434e-9105-a167173748b8)

---

## 📌 Conclusion
- **✅ Created user accounts for Sarah and Mike.**  
- **✅ Set up isolated directories with secure permissions.**  
- **✅ Implemented password complexity and expiration policies.**  
- **✅ Verified access control and security configurations.**  

---

# **Task 3: Backup Configuration for Web Servers**

## **Objective**
To configure automated backups for Sarah’s Apache server and Mike’s Nginx server, ensuring data integrity and disaster recovery readiness.

---

## **1. Steps to Implement**

### **Step 1: Create Backup Directory**
```bash
sudo mkdir -p /backups
sudo chmod 700 /backups
```

### **Step 2: Create Backup Scripts**
#### **For Sarah’s Apache Backup:**
```bash
sudo nano /usr/local/bin/apache_backup.sh
```
**Add the following:**
```bash
#!/bin/bash
DATE=$(date +'%Y-%m-%d')
tar -czf /backups/apache_backup_$DATE.tar.gz /etc/httpd/ /var/www/html/
```
Save and exit, then make the script executable:
```bash
sudo chmod +x /usr/local/bin/apache_backup.sh
```

#### **For Mike’s Nginx Backup:**
```bash
sudo nano /usr/local/bin/nginx_backup.sh
```
**Add the following:**
```bash
#!/bin/bash
DATE=$(date +'%Y-%m-%d')
tar -czf /backups/nginx_backup_$DATE.tar.gz /etc/nginx/ /usr/share/nginx/html/
```
Save and exit, then make the script executable:
```bash
sudo chmod +x /usr/local/bin/nginx_backup.sh
```

### **Step 3: Schedule Cron Jobs**
Edit the crontab:
```bash
crontab -e
```
Add the following lines to schedule backups every Tuesday at 12:00 AM:
```bash
0 0 * * 2 /usr/local/bin/apache_backup.sh
0 0 * * 2 /usr/local/bin/nginx_backup.sh
```

### **Step 4: Verify Backup Creation**
Manually trigger the backup scripts:
```bash
sudo /usr/local/bin/apache_backup.sh
sudo /usr/local/bin/nginx_backup.sh
```
Check if backup files exist:
```bash
ls -lh /backups/
```

### **Step 5: Verify Backup Integrity**
```bash
tar -tzf /backups/apache_backup_$(date +'%Y-%m-%d').tar.gz
tar -tzf /backups/nginx_backup_$(date +'%Y-%m-%d').tar.gz
```

### **Step 6: Generate Verification Logs**
```bash
tar -tzf /backups/apache_backup_$(date +'%Y-%m-%d').tar.gz > /backups/apache_backup_log.txt
tar -tzf /backups/nginx_backup_$(date +'%Y-%m-%d').tar.gz > /backups/nginx_backup_log.txt
```

---

## **2. Expected Output**

### **✅ Cron Job Configuration**
```bash
crontab -l
```
*Expected Output:*
```
0 0 * * 2 /usr/local/bin/apache_backup.sh
0 0 * * 2 /usr/local/bin/nginx_backup.sh
```

### **✅ Backup Files in `/backups/`**
```bash
ls -lh /backups/
```
*Expected Output:*
```
-rw-r--r-- 1 root root 2.5M Mar 22 00:00 apache_backup_2025-03-22.tar.gz
-rw-r--r-- 1 root root 3.1M Mar 22 00:00 nginx_backup_2025-03-22.tar.gz
```

### **✅ Backup Integrity Verification**
```bash
tar -tzf /backups/apache_backup_$(date +'%Y-%m-%d').tar.gz
tar -tzf /backups/nginx_backup_$(date +'%Y-%m-%d').tar.gz
```

### **✅ Screenshot of Terminal Outputs**
![image](https://github.com/user-attachments/assets/db23160b-0338-4625-8b0f-1fead6f9c6e6)
![image](https://github.com/user-attachments/assets/1d94a018-d7e7-4641-9c6a-61f6515a5970)
![image](https://github.com/user-attachments/assets/54a1d4dc-c88d-48ee-9457-dbbc0ea641e6)





---









  

