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



  

