# 🧱 1: Provisioning the Linux Server

To begin this project, I provisioned a cloud-based Linux server using **Amazon EC2 (Elastic Compute Cloud)**. This gave me a secure, scalable environment to host and serve my dynamic landing page.

---

## ✅ 1.1 Created an AWS EC2 Instance

I logged into the Amazon Management Console (AWS) and performed the following steps to launch a virtual server:

1. **Navigated to EC2 Dashboard**:  
   [https://console.aws.amazon.com/ec2/](https://console.aws.amazon.com/ec2/)

2. **Clicked "Launch Instance"** in **eu-north-1** region to create a new virtual machine.

3. **Named the instance**:  
   `altschool-cloud`

4. **Selected the OS Image (AMI)**:  
   - Ubuntu Server 22.04 LTS (HVM), SSD Volume Type (Free tier eligible)

5. **Instance Type**:  
   - `t2.micro` (1 vCPU, 1 GB RAM — fits within free tier)

6. **Created a new key pair**:  
   - Name: `lnd-key`
   - Format: `.pem`
   - I downloaded and stored it securely on my local machine (used for SSH access).

7. **Left storage at default**: 8 GiB (EBS)

8. **Launched the instance** and set it to `running`


## ✅ 1.2 Configured the network settings (Security Group)

Opened the altschool-cloud EC2 instance ID, scrolled down and navigated to security. I then clicked on **`Edit Inbound Rules`**

- The inbound rules allow traffic for:
     - SSH (Port 22) — restricted to my private IP
     - HTTP (Port 80) — open to all (0.0.0.0/0)
     - HTTPS (Port 443) — open to all (0.0.0.0/0)


## 🌐 1.3 Allocating and Associating an Elastic IP

To ensure the server retains a consistent public IP address even after reboots, I allocated and attached an **Elastic IP**:

1. **EC2 Dashboard > Elastic IPs**
2. **“Allocate Elastic IP”** and confirm.
3. After creation, **“Actions > Associate Elastic IP”**
4. Selected the running EC2 instance and clicked **Associate**

📝 My server’s permanent public IP is:
**`3.8.225.151`**


## 🛠️ 1.4 SSH Access via Termius

To access the server from my local terminal using SSH:

1. On my local machine (Termius), I created a folder named `altschool`
2. I moved the downloaded key pair `lnd-key.pem` file into the `altschool` folder.
3. I opened a terminal and navigated into the folder:

   ```bash
   mkdir ~/altschool
   mv ~/Downloads/lnd-key.pem ~/altschool/

4. I then connected securely using the terminal

    ```bash
    chmod 400 "lnd-key.pem"
    ssh -i "lnd-key.pem" ubuntu@ec2-3-8-225-151.eu.west-2.compute.amazonaws.com

5. I was greeted with the AWS EC2 cloud instance on my local machine showing the hostname (ubuntu), my private IP and the prompt (~).

![SSH'd into EC2 Server on Local Machine](assets/cloud1.JPG)
---

