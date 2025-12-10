# Azure Static Website Deployment 🚀

This project demonstrates how to deploy a static website to an **Azure Linux Virtual Machine** using **Nginx** as the web server and **GitHub** for version-controlled deployments.

---

## 🧩 Project Overview

A simple static website built using **HTML & CSS**, hosted on an **Ubuntu VM (Azure)** with **Nginx** serving the content.  
Deployment is managed through **Git & GitHub** — any website updates are pushed from local machine to GitHub, then pulled into the VM for instant changes.

This project helped me learn the **end-to-end web deployment lifecycle** on Azure using Linux.

---

## 🏗️ Architecture

Local Machine (VS Code)
│
├── Git Push (code updates)
│
GitHub Repository
│
├── Git Pull (on VM)
│
Azure Ubuntu VM (Public IP)
│
Nginx Web Server
│
Serves static files from:
→ /var/www/azure-static-site



**Access** → `http://<Public-IP>` (Only active while VM is running)

---

## 🛠️ Tech Stack Used

| Layer | Technology |
|------|------------|
| Cloud | Microsoft Azure |
| OS | Ubuntu Server (Linux) |
| Web Server | Nginx |
| Version Control | Git & GitHub |
| Frontend | HTML, CSS |
| Remote Access | SSH |

---

## 📂 Project Structure

azure-static-site/
│
├── index.html
├── about.html
├── contact.html
│
└── assets/
└── styles.css


---

## 🚀 Deployment Steps (What I Implemented)

### 1️⃣ Local Setup

```bash
git init
git add .
git commit -m "Initial static site"

2️⃣ GitHub Setup
git remote add origin https://github.com/<username>/azure-static-site.git
git push -u origin main

3️⃣ Azure VM Setup

Created Ubuntu VM on Azure

Opened Port 22 (SSH) & Port 80 (HTTP)

SSH into VM:

ssh azureuser@<Public-IP>

4️⃣ Install Web Server
sudo apt update
sudo apt install nginx git -y

5️⃣ Clone Code to VM
sudo mkdir -p /var/www/azure-static-site
sudo chown -R $USER:$USER /var/www/azure-static-site
git clone https://github.com/<username>/azure-static-site.git .

6️⃣ Configure Nginx
sudo nano /etc/nginx/sites-available/azure-static-site


Server block:

server {
    listen 80;
    listen [::]:80;
    server_name _;
    root /var/www/azure-static-site;
    index index.html;
    location / {
        try_files $uri $uri/ =404;
    }
}


Enable config & reload:

sudo ln -s /etc/nginx/sites-available/azure-static-site /etc/nginx/sites-enabled/
sudo rm /etc/nginx/sites-enabled/default
sudo nginx -t
sudo systemctl reload nginx

🔁 Deployment Workflow (Update Process)

1️⃣ Edit code in VS Code
2️⃣ Commit & push changes:

git add .
git commit -m "update"
git push


3️⃣ On VM:

cd /var/www/azure-static-site
git pull


4️⃣ Refresh browser → updated site live ✔️

🎯 What I Learned

✔ Hosting static websites on Linux VM
✔ Managing deployments via Git and GitHub
✔ Nginx configuration basics
✔ Working with Azure networking (NSG inbound rules)
✔ SSH access & Linux server operations
✔ Deployment workflow used in real cloud environments

📌 Future Improvements

Add HTTPS with Let's Encrypt SSL

Use CI/CD for automated deployment

Convert site into a dynamic weather dashboard (my next project)

👤 Author

Nayan B
Cloud & Linux Learner
