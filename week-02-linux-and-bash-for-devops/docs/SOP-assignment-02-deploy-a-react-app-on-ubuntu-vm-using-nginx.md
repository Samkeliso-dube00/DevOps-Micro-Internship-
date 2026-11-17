# 📘 SOP: Deploying a React Application on an Ubuntu EC2 Instance Using Nginx

**Prepared by:** Samkeliso Dube  
**Program:** DevOps Micro Internship  
**Cohort:** 2  
**Date:** 28 October 2026

---

## 📖 Introduction

This Standard Operating Procedure (SOP) outlines the process of deploying a React application on an Ubuntu EC2 instance using Nginx.

The procedure covers the steps required to prepare the server, install the necessary software, obtain the application source code, build the application for production, and configure Nginx to serve the application over HTTP.

It is intended for learners and junior DevOps engineers who want practical experience with Linux server administration and deploying web applications on AWS.

By following this procedure, the user should be able to access the deployed React application through the EC2 instance's public IP address.

---

## 🛠️ Tools and Requirements

Before starting the deployment, ensure that the following tools and resources are available.

### ☁️ AWS Resources
- An active AWS account.
- An Ubuntu EC2 instance running in your selected AWS region.
- A public IPv4 address assigned to the EC2 instance.
- An EC2 security group configured with the following inbound rules:
  - **SSH (TCP port 22):** Allow access from your own public IP address.
  - **HTTP (TCP port 80):** Allow access from anywhere (`0.0.0.0/0`) so visitors can access the application.

### 💻 Local Machine
- An SSH client for connecting to the EC2 instance.
- A web browser for accessing the deployed application.
- The EC2 private key file (`.pem`) used when launching the instance.

### 📦 Software Requirements
The following software is installed on the EC2 instance during this procedure:
- Node.js
- npm
- Git
- Nginx

### 📚 Basic Knowledge
- Basic Linux command-line operations.
- Basic understanding of SSH and EC2 instances.
- Familiarity with React application structure.

---

## 🚀 Deployment Procedure

Follow the steps below to deploy the React application on an Ubuntu EC2 instance using Nginx.

### Step 1: 🔐 Connect to the Ubuntu EC2 Instance

1. Sign in to the AWS Management Console.
2. Navigate to EC2 → Instances.
3. Select the Ubuntu EC2 instance.
4. Copy its public IPv4 address.
5. Open a terminal on your local machine.
6. Navigate to the directory containing your EC2 private key (`.pem`).
7. Connect to the instance using SSH:

```bash
ssh -i /path/to/your-key.pem ubuntu@<your-public-ip>
```

> Replace `/path/to/your-key.pem` with the actual path to your private key and `<your-public-ip>` with the instance's public IPv4 address.

**8. When prompted, confirm the connection by typing `yes`.**

**Expected Result:** A successful SSH connection opens a terminal session on the Ubuntu EC2 instance.

---

### Step 2: 🔄 Update Ubuntu and Install Required Software

After connecting to the EC2 instance, update the Ubuntu package lists and install the required software for the deployment.

**1. Update the package lists**

Run:

```bash
sudo apt update
```

> This command refreshes the list of available packages from the configured Ubuntu repositories.

**2. Upgrade installed packages**

```bash
sudo apt upgrade -y
```

> This command installs available updates for packages already installed on the Ubuntu instance. The -y option automatically confirms the installation prompts.

**3. Install Node.js, npm and Git**

```bash
sudo apt install -y nodejs npm git
```

> These tools are required for working with the React application:

- **Node.js:** Provides the JavaScript runtime environment.
- **npm:** Manages project dependencies and build scripts.
- **Git:** Downloads the application source code from GitHub.

**4. Verify the installations**

```bash
node -v
npm -v
git --version
```

**5. Install Nginx**

```bash
sudo apt install -y nginx
```

> This command installs Nginx, a web server that serves the React application's production files to users through a web browser.

**6. Start and enable Nginx**

```bash
sudo systemctl start nginx
sudo systemctl enable nginx

```

> The start command starts the Nginx service immediately, while enable configures it to start automatically when the EC2 instance reboots.

**7. Verify Nginx is running**

```bash
sudo systemctl status nginx --no-pager
```

> This command displays the current status of the Nginx service. Confirm that it shows Active: active (running).

**Expected Result:** Nginx should display `Active: active (running)`.

---

### Step 3: 📥 Clone the React Application from GitHub

Download the React application source code from its GitHub repository.

**1. Clone the repository**

```bash
git clone https://github.com/pravinmishraaws/my-react-app.git
```

**2. Navigate into the project directory**

```bash
cd my-react-app
```

**3. List the project files**

```bash
ls
```

> The project directory should contain files and folders such as:

- `package.json`
- `package-lock.json`
- `src/`
- `public/`
- `README.md`

**4. Inspect the project configuration**

```bash
cat package.json
```

> Check the available scripts and build tool before proceeding.

**Expected Result:** The React application source code is available inside the `my-react-app` directory.

---

### Step 4: ✏️ Personalise the React Application

Modify the application to display your name and the deployment date.

**1. Navigate to the source directory**

```bash
cd src
```

**2. Open the App.js file**

```bash
nano App.js
```

**3. Add your deployment information**

Insert the following JSX inside the main application component:

```jsx
<h2>Deployed by: <strong>Samkeliso Dube</strong></h2>
<p>Date: <strong>28/10/2026</strong></p>
```

**4. Save the changes**

- Press `CTRL + O` to save.
- Press `ENTER` to confirm the filename.
- Press `CTRL + X` to exit.

**5. Verify the changes**

```bash
grep -n "Deployed by" App.js
```

**Expected Result:** Your name and deployment date should appear in the application source code.

---

### Step 5: 🏗️ Build the React Application

Navigate back to the project root directory and install the application dependencies.

**1. Return to the project root**

```bash
cd ..
```

> This command moves one directory level up, from the src directory to the project root.

**2. Install project dependencies**

```bash
npm install
```

> This command reads the package.json file and installs the dependencies required by the application.

**3. Build the application for production**

```bash
npm run build
```

> This command runs the build script defined in package.json and generates optimised production files.

**4. Verify the build output**

```bash
ls
```

> Check the build tool's configuration and output. Vite normally generates a `dist/` directory, while Create React App normally generates a `build/` directory.

**Expected Result:** A production build directory containing the application's static files should be generated successfully.

---

### Step 6: 📂 Deploy the Build Files to the Nginx Web Root

Copy the generated production files into Nginx's default web directory.

**1. Identify the build directory**

For a Create React App application:

```bash
ls build/
```

Use the directory that was generated in Step 5.

**2. Back up the existing Nginx web root if it contains files**

```bash
sudo cp -a /var/www/html /var/www/html-backup
```

> This command creates a backup of the existing web root before deploying the new application files. If the directory is empty or does not contain anything you need to preserve, a backup may not be necessary.

**3. Copy the production files**

For Create React App:

```bash
sudo cp -r build/. /var/www/html/
```

> These commands copy the contents of the production build directory into Nginx's web root.

**4. Verify the deployed files**

```bash
ls -la /var/www/html/
```

> This command lists the files copied into the Nginx web root.

**Expected Result:** The Nginx web root should contain the React application's production files, including `index.html`.

---

### Step 7: ⚙️ Configure Nginx for the React Application

Configure Nginx to serve the React application and support client-side routing.

**1. Open the default Nginx configuration**

```bash
sudo nano /etc/nginx/sites-available/default
```

> This command opens the default Nginx configuration file for editing.

**2. Replace the existing server configuration with:**

```nginx
server {
    listen 80;
    server_name _;

    root /var/www/html;
    index index.html;

    location / {
        try_files $uri $uri/ /index.html;
    }
}
```

> This configuration instructs Nginx to serve the React application's files from /var/www/html. The try_files directive also redirects requests for application routes that do not match physical files to index.html, allowing client-side routing to work.

**3. Save the configuration**

- Press `CTRL + O` to save.
- Press `ENTER` to confirm.
- Press `CTRL + X` to exit.

**4. Test the Nginx configuration**

```bash
sudo nginx -t
```

**Expected Result:** Nginx should report that the configuration syntax is okay and the test is successful.

**5. Restart Nginx**

```bash
sudo systemctl restart nginx
```

> This command restarts Nginx so that it applies the updated configuration.

**6. Verify the service status**

```bash
sudo systemctl is-active nginx
```

> This command checks whether the Nginx service is running.

**Expected Result:** The command should return:

```text
active
```
---

### Step 8: 🌐 Verify the Deployment

Confirm that the React application is accessible through the EC2 instance's public IPv4 address.

**1. Retrieve the public IP address**

```bash
curl -4 ifconfig.me
```

> This command retrieves the public IPv4 address used by the EC2 instance for outbound internet access. Confirm that it matches the instance's public IPv4 address in the AWS Console.

**2. Check the EC2 security group**

Ensure that the inbound rules allow:

- HTTP : TCP port 80 - Source: `0.0.0.0/0`.
- SSH : TCP port 22 - Source: your public IP address.

**3. Open the application in a web browser**

Enter the following address, replacing the placeholder with your EC2 public IPv4 address:

```text
http://<your-public-ip>
```

**4. Verify the application**

Confirm that:

- The React application loads successfully.
- Your full name is displayed.
- The deployment date is visible.
- The application styling and content display correctly.
- Navigation works as expected, if the application has multiple routes.

**Expected Result:** The React application should be publicly accessible through the EC2 instance's public IPv4 address.

---

## 🎉 Deployment Complete!

The React application has been built, deployed to the Nginx web root and made accessible through the EC2 instance's public IP address.



