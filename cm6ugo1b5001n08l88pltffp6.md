---
title: "Project: DevOps Linux Server Monitoring & Automation"
datePublished: Fri Feb 07 2025 07:44:44 GMT+0000 (Coordinated Universal Time)
cuid: cm6ugo1b5001n08l88pltffp6
slug: project-devops-linux-server-monitoring-automation
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1738914124170/5c7a0d6e-879b-40e0-8209-7c98d1c2f222.png
tags: devops, 90daysofdevops, tws

---

Imagine you're managing a **Linux-based production server** and need to ensure that **users, logs, and processes** are well-managed. You will perform real-world tasks such as **log analysis, volume management, and automation** to enhance your DevOps skills.

## 📌 Tasks

### **1️⃣ User & Group Management**

* Learn about Linux **users, groups, and permissions** (`/etc/passwd`, `/etc/group`).
    
* **Task:**
    
    * Create a user `devops_user` and add them to a group `devops_team`.
        
    * Set a password and grant **sudo** access.
        

Restrict SSH login for certain users in `/etc/ssh/sshd_config`.

Answer : Run following command

1. Create devops\_user
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1738739362262/e3687847-19ce-4e65-b053-6babf40f475c.png align="center")

2. Create group devops\_team
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1738739548826/fe2b0168-60bb-4366-a979-2885fdf8634c.png align="center")

3.Add User devops\_user to Group Devops\_team

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1738739893528/e9e3cd3a-22fb-4086-b58a-aae3522a60ec.png align="center")

4. Set Password for devops\_user
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1738740131666/3c3b4b1e-848e-46ce-92d4-29ada8565920.png align="center")

5. Set Password to groups
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1738740386214/18626676-4592-4e01-b704-0d36fec29a01.png align="center")

6. Grant sudo access to user and group
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1738741378727/9d6ed40d-43eb-42dc-9e30-ec5bd215e6c5.png align="center")
    
7. Edit Visudo file
    
    ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1738741405284/868d47cf-8ff6-4db2-a3ca-32d2980804b4.png align="center")
    
    8. Check grand sudo access to user
        
        ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1738741707199/1e9ca81e-cadb-4f6d-a9a8-b0aa6f4dc3ef.png align="center")
        

9. restrict ssh user to login
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1738903643490/68328175-cf79-42ff-b972-8068a361ba11.png align="center")

### **2️⃣ File & Directory Permissions**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1738903940233/10bb37b3-9f25-494b-b76e-b1beb613f915.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1738904043381/ec55b69f-bae1-4b16-b764-3e9c115e8baa.png align="center")

### **3️⃣ Log File Analysis with AWK, Grep & Sed**

Logs are crucial in DevOps! You’ll analyze logs using the **Linux\_2k.log** file from **LogHub** ([GitHub Repo](https://github.com/logpai/loghub/blob/master/Linux/Linux_2k.log)).

* **Task:**
    
    * **Download the log file** from the repository.
        
    * **Extract insights using commands:**
        
        * Use `grep` to find all occurrences of the word **"error"**.
            
        * Use `awk` to extract **timestamps and log levels**.
            
        * Use `sed` to replace all IP addresses with **\[REDACTED\]** for security.
            

**Bonus:** Find the most frequent log entry using `awk` or `sort | uniq -c | sort -nr | head -10`.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1738904878827/5c8a9106-e316-46db-b0c0-481a531d0e31.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1738905457040/edfaf0f5-0ee8-43e4-a5c6-228a43f6c704.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1738906700810/97d1dad3-0a6a-469c-94d3-327a474b4de7.png align="center")

### **4️⃣ Volume Management & Disk Usage**

* **Task:**
    
    * Create a directory `/mnt/devops_data`.
        
    * Mount a new volume (or loop device for local practice).
        

Verify using `df -h` and `mount | grep devops_data`.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1738907984534/62b0b618-c7e0-4a62-9174-375ea2751e60.png align="center")

### **5️⃣ Process Management & Monitoring**

* **Task:**
    
    * Start a background process (`ping` [`google.com`](http://google.com) `> ping_test.log &`).
        
    * Use `ps`, `top`, and `htop` to monitor it.
        

Kill the process and verify it's gone.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1738908303805/a1ce2d9e-9722-4dbe-ac3b-ec4036613413.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1738908362014/1df9c4da-a1ac-447b-9095-d87a486c2129.png align="center")

  

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1738908438937/d657a604-0edc-4e01-bd54-2cb05465e6a6.png align="center")

## **6️⃣ Automate Backups with Shell Scripting**

* **Task:**
    
    * Write a shell script to back up `/devops_workspace` as `backup_$(date +%F).tar.gz`.
        
    * Save it in `/backups` and schedule it using `cron`.
        
    * Make the script display a success message in **green text** using `echo -e`.
        

  

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1738912881457/7feb646b-72ce-4177-92c4-0dd9c159ae53.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1738912966321/ba2afe15-4ca9-421e-8c4f-e1b0ce9d802b.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1738913257462/594864fa-0ede-4c30-a7ab-2ae059a74e2a.png align="center")