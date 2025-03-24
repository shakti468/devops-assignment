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





  

