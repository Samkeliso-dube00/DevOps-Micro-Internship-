# Assignment 4 — Deploy EpicReads Portfolio Website via Nginx

Part of the DevOps Micro Internship (DMI) with Agentic AI

---

## Purpose

In this assignment, I deployed the provided portfolio website on an Ubuntu EC2 instance using Nginx. I downloaded and extracted the source code, added my ownership details to the footer, copied the website into the Nginx document root, and checked that the site was responding over HTTP.

The screenshots below show the work carried out and the results I observed on the server.

---

# Task 0 — Pre-flight Check

## Goal

Verify that the Ubuntu instance and Nginx are ready before deploying the website.

I checked the Nginx service with:

```bash
sudo systemctl status nginx --no-pager
```

The service was active and running. The output also showed that Nginx was enabled, meaning it is configured to start automatically when the instance boots.

### Evidence

#### Screenshot 0 — Nginx service status

![Nginx service status showing active and running](../screenshots/W02_A04_T00_Nginx_Status.png)

---

# Task 1 — Get the Website Source Code

## Goal

Download and extract the portfolio website template.

I downloaded the template archive as `site.zip` and extracted it in the Ubuntu user's home directory. I then used `ls -la` to check the contents of the directory.

The extracted project folder was:

`Pravin-Mishra-Portfolio-main`

The listing also showed the downloaded `site.zip` archive, confirming that the source files were available before customisation.

### Evidence

#### Screenshot 1 — Extracted project folder

![Extracted portfolio project folder and site.zip](../screenshots/W02_A04_T01_Extracted_Project.png)

---

# Task 2 — Add Ownership Proof (Anti-Copy Change)

## Goal

Personalise the website footer so that it identifies my deployment.

I opened the website's `index.html` file in Nano and added the ownership information to the footer. The captured footer shows:

- DMI Cohort 2
- Samkeliso Dube
- Group 2
- Week 3

The screenshot confirms that the footer was edited in Nano. The date is not included in the captured footer yet, so I still need to add it and capture updated evidence to fully meet this requirement.

### Evidence

#### Screenshot 2 — Ownership footer in Nano

![Nano editor showing the personalised ownership footer](../screenshots/W02_A04_T02_Ownership_Footer.png)

---

# Task 3 — Deploy Website via Nginx

## Goal

Copy the customised website files into Nginx's document root and check the deployment.

I inspected the Nginx web root before copying the site. The original `/var/www/html` directory had been removed, so I recreated it before deploying the files.

I copied the contents of `Pravin-Mishra-Portfolio-main` into `/var/www/html/`, set the ownership to `www-data:www-data`, and applied the required permissions.

I then ran `sudo nginx -t`. Nginx reported that the configuration syntax was OK and that the configuration test was successful.

The final directory listing showed the deployed website content, including `index.html`, `style.css`, the images directory, and the other HTML files. The listing also showed the deployed files owned by `www-data`.

### Evidence

#### Screenshot 3 — Successful Nginx configuration test

![Nginx configuration syntax check completed successfully](../screenshots/W02_A04_T03_Nginx_Config_Test.png)

#### Screenshot 4 — Website files in the Nginx web root

![Deployed website files in /var/www/html](../screenshots/W02_A04_T03_Deployed_Website_Files.png)

---

# Task 4 — Verify Website is Live

## Goal

Check that the website can be reached through the EC2 instance's public IP address and that the personalised footer is displayed.

I used `curl ifconfig.me` to check the public IP address seen by an external service. The command returned:

`3.90.243.189`

I then used that address to test the website over HTTP. The terminal returned `HTTP/1.1 200 OK`. I also opened the address in a browser and confirmed that the portfolio website loaded.

The browser screenshot shows the site and the ownership details in the footer. The date still needs to be added to the footer, as noted in Task 2.

### Evidence

#### Screenshot 5 — Public IP check

![Terminal showing the public IP address returned by ifconfig.me](../screenshots/W02_A04_T04_Public_IP.png)

#### Screenshot 6 — Live portfolio website

![Portfolio website loaded in the browser with the ownership footer visible](../screenshots/W02_A04_T04_Live_Website.png)

---

# Task 5 — Mini Real DevOps Operational Check

## Goal

Carry out a couple of basic checks to confirm that Nginx is enabled at boot and responds to local HTTP requests.

I ran:

```bash
systemctl is-enabled nginx
```

The output was `enabled`, confirming that Nginx is configured to start automatically during system boot.

I then tested the local HTTP endpoint using:

```bash
curl -I http://localhost
```

The response contained `HTTP/1.1 200 OK`. This confirms that Nginx returned a successful HTTP response to a request made from the EC2 instance itself.

### Evidence

#### Screenshot 7 — Nginx enabled status

![systemctl is-enabled nginx returning enabled](../screenshots/W02_A04_T05_Nginx_Enabled.png)

#### Screenshot 8 — Local HTTP response

![curl request to localhost returning HTTP 200 OK](../screenshots/W02_A04_T05_HTTP_200_OK.png)

---

## 📌 About DMI & CloudAdvisory

DevOps Micro Internship (DMI) is a project-based DevOps program run by Pravin Mishra (The CloudAdvisory), focused on practical execution, systems thinking, and career readiness.

## 📌 Resources

- 🌐 DMI Official Website: https://dmi.pravinmishra.com?utm_source=github&utm_medium=readme
- 🎓 University: https://university.pravinmishra.com?utm_source=github&utm_medium=readme
- 💬 Discord Community: https://discord.pravinmishra.com?utm_source=share&utm_medium=member_desktop&rcm=ACoAAFWazFgBljBJn82yruDlPYI5eQTyv705bh4
- 📝 Blog: https://dmi.pravinmishra.com/blog?utm_source=github&utm_medium=readme
- ▶️ YouTube Playlist: https://www.youtube.com/playlist?list=PLFeSNDtI4Cho
- 🔗 Pravin Mishra (LinkedIn): https://www.linkedin.com/in/pravin-mishra-aws-trainer/
- 🏢 CloudAdvisory (LinkedIn): https://www.linkedin.com/company/thecloudadvisory/

---

# LinkedIn Evidence

I shared this deployment on LinkedIn to document the practical work and the lessons I picked up while deploying a static website with Nginx on an AWS EC2 instance.

**Published post:** [Deploying a portfolio website using AWS EC2 and Nginx](https://www.linkedin.com/posts/samkeliso-dube03_devops-aws-nginx-activity-7420453917274103808--AT9)

---

# Submission Summary

The deployment procedure is documented above, with the nine task screenshots stored in the repository's `screenshots/` directory and embedded under their corresponding tasks. The LinkedIn post URL is also included above.

## Completion Checklist

- [x] Screenshot 0: Nginx service status shows active/running
- [x] Screenshot 1: Website source code downloaded and extracted
- [x] Screenshot 2: Ownership footer edited in Nano
- [x] Screenshot 3: Nginx configuration test successful
- [x] Screenshot 4: Website files present in `/var/www/html`
- [x] Screenshot 5: Public IP retrieved
- [x] Screenshot 6: Live website opened in the browser
- [x] Screenshot 7: Nginx enabled at boot
- [x] Screenshot 8: Local HTTP response returns 200 OK
- [x] LinkedIn post published and URL included
- [ ] Ownership footer includes the deployment date

---

# Reflection

This assignment gave me practical experience with the steps involved in putting a website online using Nginx. I started by checking the server and the Nginx service, then downloaded and extracted the website files before preparing the web root and deploying the content.

One thing that stood out was the importance of inspecting the environment before making changes. The original `/var/www/html` directory was not present, so I recreated it before copying the website files. I also learned to use different checks for different purposes: `nginx -t` validates the configuration, a directory listing confirms that the files are in the expected location, and `curl` helps verify the HTTP response.

The exercise also reminded me not to treat one successful check as proof of everything. A local HTTP 200 response confirms that Nginx can respond locally, while opening the public IP in a browser checks access from outside the instance. In future deployments, I want to keep improving how I document changes and capture evidence, especially when personalising a site before making it publicly accessible.

# Conclusion

I deployed the portfolio website on an Ubuntu EC2 instance and served it through Nginx. The evidence included in this assignment shows that the Nginx service was running, the website files were placed in the document root, the Nginx configuration test passed, the website loaded through the instance's public IP address, and a local HTTP request returned `200 OK`. Nginx was also enabled to start automatically at boot.

The deployment and its verification steps are documented with the corresponding screenshots, and the LinkedIn post is linked as evidence of sharing the work. The remaining improvement is to add the deployment date to the website's ownership footer and update its relevant evidence.

---

*This submission is part of DevOps Micro Internship (DMI) — Agentic AI Track.*
