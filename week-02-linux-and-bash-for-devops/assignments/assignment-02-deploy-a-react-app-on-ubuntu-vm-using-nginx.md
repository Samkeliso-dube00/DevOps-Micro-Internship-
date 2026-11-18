# Assignment 2: Deploy a React App on Ubuntu VM Using Nginx

---

## Purpose

In this assignment, you will deploy a React application on an Ubuntu EC2 instance and serve it using Nginx. You will provision a Linux server, install the required tools, personalize the application with your details, and verify that it is publicly accessible via a browser.

---

## Task 1: Setup Environment (Node.js & npm)

## Goal

Install Node.js and npm on the Ubuntu VM and verify the installation.

## Evidence

**Screenshot 1: Output of `node -v && npm -v` showing installed versions**

![Task 1 - Environment setup and Node.js/npm versions](../screenshots/W02_T01_Environment_Setup.png)

---

## Task 2: Setup Environment (Nginx)

## Goal

Install Nginx, start the service, and confirm it is running.

## Evidence

**Screenshot 2: Output of `systemctl status nginx --no-pager` showing Active (running)**

![Task 2 - Nginx service status](../screenshots/W02_T02_Nginx_Service_Status.png)

---

## Task 3: Clone React Application

## Goal

Clone the project repository and verify the project files are present.

## Evidence

**Screenshot 3: Output of `ls` inside the `my-react-app` directory showing project files**

![Task 3 - React repository clone](../screenshots/W02_T03_React_Repository_Clone.png)

---

## Task 4 : Modify Application (Personalization)

## Goal

Update `App.js` with your full name and the current date.

## Evidence

**Screenshot 4 : `nano App.js` open showing your full name and date filled in**

![Task 4 - React app personalization](../screenshots/W02_T04_React_App_Personalization.png)

---

## Task 5 : Build React Application

## Goal

Install dependencies and generate the production build.

## Evidence

**Screenshot 5 : Output of `ls` inside `my-react-app` showing the `build/` folder generated**

![Task 5 - React production build](../screenshots/W02_T05_React_Production_Build.png)

---

## Task 6 : Deploy React Build to Nginx Web Root

## Goal

Copy the production build files to the Nginx web root directory.

## Evidence

**Screenshot 6 : Output of `ls /var/www/html/` showing the deployed build contents**

![Task 6 - Deploy React build to Nginx web root](../screenshots/W02_T06_Deploy_React_Build_to_Nginx.png)

---

## Task 7 : Configure Nginx for React Application

## Goal

Apply Nginx configuration for React routing and confirm the service is active.

## Evidence

**Screenshot 7: Output of `systemctl is-active nginx` showing `active`**

![Task 7 - Nginx service verification](../screenshots/W02_T07_Nginx_Service_Verification.png)

**Screenshot 8 : Output of `cat /etc/nginx/sites-available/default` showing the Nginx config**

![Task 7 - Nginx configuration](../screenshots/W02_T08_Nginx_Configuration.png)

---

## Task 8 : Test Deployment

## Goal

Verify the React application is publicly accessible via the server's public IP.

## Evidence

**Screenshot 9: Output of `curl ifconfig.me` showing the server's public IP address**

![Task 9 - EC2 public IP address](../screenshots/W02_T09_EC2_Public_IP_Address.png)

**Screenshot 10 : Browser showing the deployed React app at `http://<public-ip>` with your name and date visible**


![Task 10 - Live React application](../screenshots/W02_T10_Live_React_Application.png)

---

## LinkedIn Post (Required)

## Evidence

**LinkedIn Post URL**

[View LinkedIn Post](https://www.linkedin.com/posts/samkeliso-dube03_devops-cloudengineering-softwareengineering-activity-7419356690745237504-O23W/)

**Update:**

The original project link remains unchanged. I've since rebuilt the application deployment and updated the screenshots to reflect the latest version of the live application.

The updated screenshots provide more accurate evidence of the completed deployment.

Thank you!


---

## 👩🏽‍💻 Personal Reflection

This assignment gave me practical experience deploying a React application on an Ubuntu EC2 instance using Nginx. I learned how to set up the environment, install the required tools, clone the application repository, build the application, and configure Nginx to serve the React application.

Through this hands-on task, I gained a better understanding of how Linux servers and web servers work together to host applications. I also learned the importance of following deployment steps carefully and verifying that the application is accessible through a browser.

## 🎯 Conclusion

This assignment strengthened my understanding of deploying web applications on AWS EC2 using Nginx. It was a valuable opportunity to apply my knowledge practically and build confidence in working with Linux servers and cloud infrastructure.

Going forward, I want to continue practising application deployments and deepen my understanding of the tools and technologies used in DevOps.

---

**Author:** Samkeliso Dube  
**Role:** DevOps Engineer | Cloud Engineer  
**GitHub:** [Samkeliso-Dube](https://github.com/Samkeliso-dube00)  
**LinkedIn:** [Samkeliso Dube](https://www.linkedin.com/in/samkeliso-dube03/)
