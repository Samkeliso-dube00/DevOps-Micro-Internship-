# SOP: Deploying a React Application on an Ubuntu EC2 Instance Using Nginx

**Prepared by:** Samkeliso Dube  
**Program:** DevOps Micro Internship  
**Cohort:** 2  
**Date:** 28 October 2026

---

Introduction

This document provides step-by-step instructions for deploying a React application to an AWS EC2 Ubuntu instance using Nginx. This procedure is intended for DevOps engineers and learners performing web application deployments on AWS as part of coursework or hands-on practice.

---

## Tools and Requirements

The following tools are required before starting:

- AWS Account 
- Ubuntu EC2 instance 
- SSH client 
- Web browser 
- Basic Linux command knowledge

---

## Step 1: Connect to the Ubuntu EC2 Instance

### Step 1.1: Access AWS Console

Open your browser and go to:

👉 https://console.aws.amazon.com

Sign in to your AWS account.

### Step 1.2: Navigate to EC2 Instances

In the search bar at the top, type:

👉 EC2

Click on EC2 to open the console.

### Step 1.3: Select Your Instance

From the Instances list, click your Ubuntu instance:

👉 react-app-vm (or your instance name)

### Step 1.4: Copy the Public IP Address

On the instance details page, locate the **Public IPv4 address** field.

Copy the IP address (e.g., `35.192.100.45`).

### Step 1.5: Open Terminal and Connect via SSH

Open your terminal (Mac/Linux) or Git Bash (Windows).

Run the SSH command:

```bash
ssh -i /path/to/your-key.pem ubuntu@<your-public-ip>
```

Replace:
- `/path/to/your-key.pem` with the path to your private key file
- `<your-public-ip>` with the IP you copied in Step 1.4

**Example:**
```bash
ssh -i ~/Downloads/my-key.pem ubuntu@35.192.100.45
```

### Step 1.6: Accept the Security Prompt

If prompted:

```
Are you sure you want to continue connecting (yes/no)?
```

Type:

```bash
yes
```

**Expected Outcome:**

You will see a prompt like:

```
ubuntu@ip-172-31-xx-xx:~$
```

**Explanation:** You are now connected to the Ubuntu instance.

---

## Step 2: Install Required Packages

### Step 2.1: Update System Packages

After connecting, run:

```bash
sudo apt update && sudo apt upgrade -y
```

**Explanation**

This command updates the package list and upgrades installed packages to the latest versions.

**Why it is needed**

- Ensures the system is up to date
- Prevents compatibility issues during installation
- Improves system security

**Expected Outcome:**

The terminal displays progress messages. After completion, you see:

```
ubuntu@ip-172-31-xx-xx:~$
```

---

### Step 2.2: Install Node.js, npm, and Git

Run the following command:

```bash
sudo apt install -y nodejs npm git
```

**Explanation**

This installs three critical tools:

- **Node.js** → JavaScript runtime environment
- **npm** → Package manager for JavaScript dependencies
- **Git** → Version control system for cloning repositories

**Why it is needed**

- Node.js and npm are required to build the React application
- Git is required to clone the React application source code from GitHub

**Meaning of the command**

- `sudo` runs with administrative privileges
- `apt install` installs packages
- `-y` automatically answers "yes" to prompts

**Expected Outcome:**

Installation completes and displays:

```
Setting up nodejs...
Setting up npm...
Setting up git...
ubuntu@ip-172-31-xx-xx:~$
```

---

### Step 2.3: Verify Installation

Check the installed versions:

```bash
node -v
npm -v
git --version
```

**Expected Outcome:**

You should see version numbers displayed:

```
v18.x.x
9.x.x
git version 2.x.x
```

**Explanation:** Version numbers confirm successful installation.

---

### Step 2.4: Install Nginx

Run:

```bash
sudo apt install -y nginx
```

**Explanation**

Nginx is a lightweight web server that serves static files and acts as a reverse proxy.

**Why it is needed**

- Serves the built React application files to users
- Handles HTTP requests on port 80
- Provides routing support for React single-page applications

**Expected Outcome:**

```
Setting up nginx...
ubuntu@ip-172-31-xx-xx:~$
```

---

### Step 2.5: Start and Enable Nginx

Run:

```bash
sudo systemctl start nginx
sudo systemctl enable nginx
systemctl status nginx
```

**Explanation**

- `systemctl start nginx` starts the Nginx service immediately
- `systemctl enable nginx` configures Nginx to start automatically on reboot
- `systemctl status nginx` checks the current status

**Expected Outcome:**

The status output displays:

```
● nginx.service - A high performance web server...
   Loaded: loaded (/lib/systemd/system/nginx.service...)
   Active: active (running)
```

**Meaning of the code**

- `Active: active (running)` confirms Nginx is running
- Green indicator shows the service is healthy

---

## Step 3: Clone the React Application

### Step 3.1: Clone the Repository

Run:

```bash
git clone https://github.com/pravinmishraaws/my-react-app.git
cd my-react-app
ls
```

**Explanation**

- `git clone` downloads the React application source code
- `cd my-react-app` navigates into the project folder
- `ls` lists the project contents

**Why it is needed**

- Obtains the React application source code
- Prepares the project for build and deployment

**Expected Outcome:**

You see the project structure:

```
package.json  package-lock.json  src/  public/  README.md  vite.config.js
```

**Explanation:** These files are part of a React project. `package.json` lists dependencies and build commands.

---

## Step 4: Personalize the React Application

### Step 4.1: Navigate to the Source Folder

Run:

```bash
cd src
```

**Explanation:** The `src/` folder contains the React component files.

---

### Step 4.2: Open the App.js File

Run:

```bash
nano App.js
```

**Explanation**

This opens the file in the nano text editor, allowing you to edit it directly in the terminal.

**Why it is needed**

The App.js file contains the main React component. You need to add your name and deployment date.

---

### Step 4.3: Add Your Name and Date

Inside the nano editor, find a suitable location in the JSX (the HTML-like code) and add:

```jsx
<h2>Deployed by: <strong>Your Full Name</strong></h2>
<p>Date: <strong>DD/MM/YYYY</strong></p>
```

**Example:**

```jsx
<h2>Deployed by: <strong>Samkeliso Dube</strong></h2>
<p>Date: <strong>28/10/2026</strong></p>
```

---

### Step 4.4: Save and Exit the Editor

Press:

```
CTRL + O
```

This prompts "File name to write:" - just press:

```
Enter
```

Then press:

```
CTRL + X
```

**Explanation**

- `CTRL + O` opens the save dialog
- `Enter` confirms the filename
- `CTRL + X` exits the editor

**Expected Outcome:**

You return to the terminal prompt:

```
ubuntu@ip-172-31-xx-xx:~/my-react-app/src$
```

---

### Step 4.5: Verify Your Changes

Run:

```bash
cat App.js | grep -A 2 "Deployed by"
```

**Expected Outcome:**

You see your name and date displayed:

```
<h2>Deployed by: <strong>Samkeliso Dube</strong></h2>
<p>Date: <strong>28/10/2026</strong></p>
```

---

## Step 5: Install Dependencies and Build

### Step 5.1: Return to Project Root

Run:

```bash
cd ..
```

**Explanation:** This takes you back to the main project folder.

---

### Step 5.2: Install Dependencies

Run:

```bash
npm install
```

**Explanation**

This reads `package.json` and downloads all required JavaScript libraries and dependencies into a `node_modules/` folder.

**Why it is needed**

- React and related libraries must be installed before building
- npm resolves all dependency versions and compatibility

**Expected Outcome (after 2-5 minutes):**

```
up to date, audited 150 packages in 45s
5 packages are looking for funding...
```

---

### Step 5.3: Create the Production Build

Run:

```bash
npm run build
```

**Explanation**

This command compiles the React source code into optimized, minified files ready for production.

**Why it is needed**

- Converts JSX to JavaScript
- Minifies code for smaller file sizes
- Optimizes assets for web delivery
- Generates a `build/` folder with deployment-ready files

**Expected Outcome (after 1-2 minutes):**

```
> npm run build

Creating an optimized production build...
Compiled successfully.

File sizes after gzip:
  build/static/js/main.js
  build/static/css/main.css
```

---

### Step 5.4: Verify the Build

Run:

```bash
ls
```

**Expected Outcome:**

You see a `build/` directory in the listing:

```
build/  node_modules/  package.json  src/  ...
```

---

## Step 6: Deploy to Nginx

### Step 6.1: Clear the Nginx Web Root

Run:

```bash
sudo rm -rf /var/www/html/
```

**Explanation**

This removes the default Nginx files to make room for the React application.

**Why it is needed**

- `/var/www/html/` is the default Nginx web directory
- Clearing it prevents conflicts between old and new files
- Ensures a clean deployment

**⚠️ Warning:** This command deletes files permanently.

---

### Step 6.2: Copy the Build Files

Run:

```bash
sudo cp -r build/* /var/www/html/
```

**Explanation**

This copies all the production-ready React files into the Nginx web root.

**Why it is needed**

- Nginx serves files from `/var/www/html/`
- Copying the build here makes the application publicly accessible

**Meaning of the command**

- `sudo` runs with admin privileges
- `cp -r` copies recursively (includes folders)
- `build/*` is the source (all files in build/)
- `/var/www/html/` is the destination (Nginx web root)

---

### Step 6.3: Set Ownership

Run:

```bash
sudo chown -R www-data:www-data /var/www/html
```

**Explanation**

This changes the owner of all files to the `www-data` user, which is the Nginx process user.

**Why it is needed**

- Nginx runs as the `www-data` user
- The files must be owned by this user for Nginx to read them

---

### Step 6.4: Set Permissions

Run:

```bash
sudo chmod -R 755 /var/www/html
```

**Explanation**

This sets read and execute permissions for all files and folders.

**Why it is needed**

- Nginx needs permission to read files
- Users need permission to download and view the application

---

### Step 6.5: Verify Deployment

Run:

```bash
ls -la /var/www/html/
```

**Expected Outcome:**

You see the deployed files:

```
-rw-r--r-- 1 www-data www-data  2345 Oct 28 10:35 index.html
drwxr-xr-x 2 www-data www-data  4096 Oct 28 10:35 assets
drwxr-xr-x 2 www-data www-data  4096 Oct 28 10:35 static
```

---

## Step 7: Configure Nginx for React Routing

### Step 7.1: Update the Nginx Configuration

Run:

```bash
echo 'server {
    listen 80;
    server_name _;
    root /var/www/html;
    index index.html;

    location / {
        try_files $uri /index.html;
    }

    error_page 404 /index.html;
}' | sudo tee /etc/nginx/sites-available/default > /dev/null
```

**Explanation**

This replaces the default Nginx configuration with one optimized for React routing.

**Why it is needed**

React is a single-page application (SPA). All routes are handled by JavaScript in the browser. Without this configuration:
- Navigating directly to a route like `/products` would return 404
- The `try_files` rule redirects all unknown URLs to `index.html`
- React's JavaScript then renders the correct component

**Meaning of the code**

- `listen 80` - Nginx listens on port 80 (HTTP)
- `server_name _` - Accept requests for any domain
- `root /var/www/html` - Serve files from this directory
- `index index.html` - Default file for `/`
- `try_files $uri /index.html` - Try the requested file, fall back to `index.html`
- `error_page 404 /index.html` - Serve `index.html` for missing files

---

### Step 7.2: Test the Configuration

Run:

```bash
sudo nginx -t
```

**Expected Outcome:**

```
nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful
```

**Explanation:** Both lines confirm the configuration is correct.

---

### Step 7.3: Restart Nginx

Run:

```bash
sudo systemctl restart nginx
systemctl is-active nginx
```

**Expected Outcome:**

```
active
```

**Explanation:** Nginx is running with the new configuration.

---

## Step 8: Test the Deployment

### Step 8.1: Get Your Public IP Address

Run:

```bash
curl ifconfig.me
```

**Expected Outcome:**

```
35.192.100.45
```

(Your IP address will be different.)

**Explanation:** This is your instance's public-facing IP address.

---

### Step 8.2: Open in Browser

On your local computer, open a web browser.

Navigate to:

```
http://<your-public-ip>
```

Replace `<your-public-ip>` with the IP from Step 8.1.

**Example:**

```
http://35.192.100.45
```

**Expected Outcome:**

- The React application loads
- Your full name is visible
- The deployment date is visible
- The page has styling (colors, fonts, layout)
- Navigation works without 404 errors

---

## Step 9: Verify Successful Deployment

### Checklist

- [ ] You connected to the EC2 instance via SSH
- [ ] Node.js, npm, and Git are installed
- [ ] Nginx is running
- [ ] React application was cloned and customized
- [ ] npm install and npm run build completed successfully
- [ ] Build files were copied to `/var/www/html/`
- [ ] Nginx configuration was tested and restarted
- [ ] Application loads at the public IP address
- [ ] Your name and date are visible on the page
- [ ] All 10 screenshots captured (if required for assignment)

---

## Step 10: Troubleshooting

### Problem: Website Cannot Be Reached

**Symptom:** Browser shows "ERR_CONNECTION_REFUSED" or times out.

**Steps to debug:**

1. Verify the EC2 instance is running:

Open the AWS Console, navigate to EC2 → Instances, and check the instance state.

```bash
Expected state: Running
```



2. Check the Nginx service.

```bash
systemctl status nginx
```
If Nginx is not running, start it:

```
sudo systemctl start nginx
```

3. Check the EC2 security group.
   - AWS Console → Security Groups → Inbound Rules → Port 80 should be present

4. Test locally on the instance:

```bash
curl -I http://localhost
```

Expected: `HTTP/1.1 200 OK`

---

### Problem: npm install Fails

**Symptom:** Error messages during `npm install`

**Steps to resolve:**

1. Check available disk space:

```bash
df -h
```

If nearly full, the instance may be out of space.

2. Check memory:

```bash
free -h
```

3. Clear npm cache and retry:

```bash
npm cache clean --force
npm install
```

---

### Problem: Nginx Config Test Fails

**Symptom:** `sudo nginx -t` shows syntax errors.

**Steps to resolve:**

1. Check the exact error message
2. Correct the syntax in the configuration file:

```bash
sudo nano /etc/nginx/sites-available/default
```

3. Save and test again:

```bash
sudo nginx -t
```

---

### Problem: React Routes Return 404

**Symptom:** Navigating to `/products` or other routes shows 404.

**Steps to resolve:**

1. Verify the `try_files` rule is present:

```bash
cat /etc/nginx/sites-available/default | grep try_files
```

2. If missing, reapply the configuration from Step 7.1

3. Restart Nginx:

```bash
sudo systemctl restart nginx
```

---

## Step 11: Cleanup (After Testing)

### When finished, stop the EC2 instance to save costs:

1. Open AWS Console
2. Go to EC2 → Instances
3. Select your instance
4. Click Instance State → Stop

**Explanation:** Stopped instances incur minimal charges (storage only) but no compute costs.

---

## What I Learned

Document what you learned after completing this deployment:

- How to connect to an EC2 instance via SSH
- How to install system packages using `apt`
- How to manage Linux services with `systemctl`
- How to clone and customize a React application
- How `npm install` and `npm run build` work
- How to deploy to Nginx and configure web server routing
- How React single-page applications require special Nginx configuration
- How to troubleshoot deployment issues systematically

---

## Issues Faced and How I Solved Them

Record only issues you actually encountered:

| Issue | Cause | How I Fixed It |
|-------|-------|----------------|
| | | |
| | | |
| | | |

---

## Screenshots Required for Assignment

| No. | What to Capture | Command/Action |
|-----|-----------------|----------------|
| 1 | Node.js and npm versions | `node -v && npm -v` |
| 2 | Nginx running | `systemctl status nginx` |
| 3 | Repository cloned | `ls` in my-react-app folder |
| 4 | App.js updated | Editor showing your name and date |
| 5 | Build directory created | `ls` showing build/ folder |
| 6 | Files deployed to Nginx | `ls /var/www/html/` |
| 7 | Nginx active | `systemctl is-active nginx` |
| 8 | Nginx configuration | `cat /etc/nginx/sites-available/default` |
| 9 | Public IP address | `curl ifconfig.me` output |
| 10 | Application in browser | Screenshot showing app with name/date visible |

---

## Final Checklist

- [ ] All steps completed successfully
- [ ] React application accessible at public IP
- [ ] Your full name visible on the page
- [ ] Deployment date visible on the page
- [ ] All 10 screenshots captured and clean
- [ ] No passwords, keys, or secrets in screenshots
- [ ] Google Doc created with all evidence
- [ ] Google Doc link tested in incognito window
- [ ] LinkedIn post created with explanation and screenshot (if required)

---





**Happy learning!!!**