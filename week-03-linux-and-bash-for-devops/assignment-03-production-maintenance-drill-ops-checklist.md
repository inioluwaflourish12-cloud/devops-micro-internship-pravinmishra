# Assignment 3 — Production Maintenance Drill (OPS Checklist)

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will treat your already deployed React application (on Ubuntu VM with Nginx) as a live production system. You will perform structured operational checks covering network validation, service health, log analysis, resource monitoring, configuration verification, and incident simulation with recovery — mirroring real on-call DevOps responsibilities.

---

# Task 1 — Server Access & Networking Validation

## Goal

Verify that the deployed React application is reachable from the browser and confirm basic network connectivity of the Ubuntu VM.

### Evidence

#### Screenshot 1 — Browser showing the React app with your Full Name visible on the UI

![alt text](<screenshots/Screenshot 10 (Assignment 2 task8).png>)

---

#### Screenshot 2 — Output of `ip a`

![alt text](<screenshots/Screenshot 2(Assignment 3 task1).png>)

---

#### Screenshot 3 — Output of `sudo ss -tulpen`

![alt text](<screenshots/Screenshot 3 (Assignment 3 task1).png>)

---

#### Screenshot 4 — Output of `sudo ufw status`

![alt text](<screenshots/Screenshot 4 (Assignment 3 task 1).png>)

---

### Notes

Answer the following in your own words:

**1. What proves Nginx is listening on 0.0.0.0:80?**

The output of the network listening command showed that nginx is listening on 0.0.0:80, and that means it's accepting HTTP conections on port 80 for all network interface



**2. What proves SSH is active on port 22?**

The network listening output showed that the SSH service is listening on port 22, which confirms that SSH is active and available for remote connections 



**3. Did you find any unexpected open ports? Explain briefly.**

No i didn't, i only found the expected ports, including port 80 for nginx and port 22 for SSH. 

---

# Task 2 — Service Health & Systemd Validation (Nginx)

## Goal

Verify that Nginx is properly installed, running, enabled at boot, and safely configured.

### Evidence

#### Screenshot 1 — Output of `systemctl status nginx --no-pager`

![alt text](<screenshots/Screenshot 1 (Assignment 3 task 2).png>)

---

#### Screenshot 2 — Output of `sudo nginx -t`

![alt text](<screenshots/Screenshot 2 (Assignment 3 task2).png>)

---

#### Screenshot 3 — Output of `sudo ss -lptn '( sport = :80 )'`

![alt text](<screenshots/Screenshot 3 (Assignment 3 task1).png>)

---

### Notes

Answer the following in your own words:

**1. What happens if Nginx fails to restart in production?**

If Nginx fails to restart in production, then the web application may become unavailable to users because the web server is'nt running

---

**2. What's your basic rollback plan?**

If the changes cause any problems, i will restore the previous working configuration, restart Nginx and confirm that the application is working normally again.

---

# Task 3 — Logs & Request Trace

## Goal

Verify real traffic flow and analyze logs to understand system behavior and errors.

### Evidence

#### Screenshot 1 — Output of `sudo tail -n 30 /var/log/nginx/access.log`

![alt text](<screenshots/Screenshot 1 (Assignment 3 task 3).png>)

---

#### Screenshot 2 — Output of `sudo tail -n 30 /var/log/nginx/error.log`

![alt text](<screenshots/Screenshot 2(Assignment 3 task 3).png>)

---

#### Screenshot 3 — Output of `sudo journalctl -u nginx --no-pager -n 50`

![alt text](<screenshots/Screenshot 3(Assignment 3 task3).png>)

---

### Notes

Answer the following in your own words:

**1. Were there any errors in the logs?**

- If yes, mention 1–2 example error lines from the logs and explain what each one means in simple terms.
- If no, explain what it means if the error log is empty or shows no recent errors during your check.

No I didn't get an error in the logs. The Nginx error log did not show any recent errors, and that means the web server was running normally during my checks and there was no issues recorded at the same time.

---

**2. If there were no errors, what does that indicate about the system?**

It indicates that Nginx is working properly and the web server was stable during the checks.

---

**3. Based on the access logs, were your curl requests visible in the log entries? What does that prove about traffic flow?**

My curl request were visible in the access log and that proves that the requests successfully reached the Nginx server, processed and recorded in the logs.

---

# Task 4 — System Resource Health Check (Capacity Red Flags)

## Goal

Assess server capacity and detect potential performance or failure risks.

### Evidence

#### Screenshot 1 — Output of `uptime`

![alt text](<screenshots/Screenshot 1 (Assignment 3 task 4).png>)

---

#### Screenshot 2 — Output of `free -h`

![alt text](<screenshots/Screenshot 2 (Assignment 3 task4).png>)

---

#### Screenshot 3 — Output of `df -h`

![alt text](<screenshots/Screenshot 3 (Assignment 3 task 4).png>)

---

#### Screenshot 4 — Output of `sudo du -sh /var/* | sort -h`

![alt text](<screenshots/Screenshot 4 (Assignment 3 task4).png>)

---

### Notes

Answer the following in your own words:

**1. Which resource looks most critical right now? (CPU/load, memory, or disk) Explain why.**

None of the resources looked critical during my checks. T cpu load was 0.00, memory still has more than 500MiB available, and the disk also still had about 2.7GB free. 

---

**2. What happens if disk becomes 100% full in a production server?**

The server may stop working properly because of the low storage to store logs, files and application data. it could even cause Nginx to fail and users wont be able to access the website.

---

# Task 5 — Configuration & Deployment Verification

## Goal

Ensure the correct React build is deployed and Nginx is serving it properly.

### Evidence

#### Screenshot 1 — Output of `ls -lah /var/www/html | head -n 20`

![alt text](<screenshots/Screenshot 1 (Assignment 3 task 5).png>)

---

#### Screenshot 2 — Output of `grep -R "Deployed by" -n /var/www/html 2>/dev/null | head`

![alt text](<screenshots/Screenshot 2 (Assignment 3 task5).png>)

---

#### Screenshot 3 — Output of `grep -n "try_files" /etc/nginx/sites-available/default`

![alt text](<screenshots/Screenshot 3 (Assignment 3 task5).png>)

---

### Notes

Answer the following in your own words:

**1. How do you confirm that the correct version of the application is deployed?**

 T he files in /var/www/html matches the react build and my full name was visible "Welcome, Oyebajo Inioluwa Flourish". It was visible in the deployed application files. 

---

# Task 6 — Nginx Configuration Failure Simulation

## Goal

Simulate a real-world Nginx misconfiguration and recover the service safely.

### Evidence

#### Screenshot 1 — Output of `sudo nginx -t` showing the syntax error (broken config)

![alt text](<screenshots/Screenshot 1 (Assignment 3 task 6).png>)

---

#### Screenshot 2 — Output of `sudo nginx -t` showing syntax ok (fixed config)

![alt text](<screenshots/Screenshot 2(Assignment 3task6).png>)

---

#### Screenshot 3 — Output of `curl -I http://<public-ip>` confirming recovery (200 OK)

![alt text](<screenshots/Screenshot 3(Assignment 3task6).png>)

---

### Notes

Answer the following in your own words:

**1. What caused the configuration failure?**

The configuration failed because I removed the semicolon required from the Nginx configuration files. This caused a syntax error, so Nginx could not validate the configuration.

---

**2. How did you fix the issue?**

I restored the semicolon back into the configuration file. 

---

**3. How can you avoid this kind of issue in real production systems?**

I would carefully review any configuration changes and make a back up before editing the file.

---

# Task 7 — Web Application Failure Simulation

## Goal

Simulate missing deployment content and recover the application safely.

### Evidence

#### Screenshot 1 — Output of `curl -I http://<public-ip>` showing failure (non-200 response)

![alt text](<screenshots/Screenshot 1(Assignment 3 task7).png>)

---

#### Screenshot 2 — Output of `curl -I http://<public-ip>` confirming recovery (200 OK)

![alt text](<screenshots/Screenshot 2(Assignment 3 task7).png>)

---

### Notes

Answer the following in your own words:

**1. What caused the application to break in this scenario?**

The application broke because the web content directory was moved, so Nginx could no longer find the application files it was supposed to serve.

---

**2. How did you fix the issue and restore the application?**

I fixed the issue by restoring the original application files from the backup folder, restarting the Nginx service, and then checking that the application was working again by confirming it returned a 200 OK response.

---

**3. What steps would you take to prevent this kind of issue in real production systems?**

I would always back up the application before making changes, test any changes in a staging environment first, and verify that everything is working before deploying to the live server. 

---

# Task 8 — Security & Reliability Review

## Goal

Review and reflect on the security and reliability practices applied during this assignment.

### Security & Reliability Notes

Answer the following in your own words:

**1. Why is SSH key-based authentication more secure than sharing passwords?**

SSH key-based authentication is more secure because it uses encrypted keys instead of passwords, which are easier to guess or steal. 

---

**2. Why should only required ports be open on a production server?**

Only the necessary ports should be open to reduce security risks. Open ports can be entry points for attackers, so limiting them helps protect the server from unauthorized access.

---

**3. Why is it important for Nginx to be enabled on boot?**

It is important because if the server restarts, Nginx will start automatically without manual intervention. 
---

**4. What are the risks of sharing secrets, keys, or credentials publicly?**

It can allow unauthorized people to access servers, applications, or cloud resources and this can lead to data loss, security breaches, or misuse of resources

---

**5. Why should cloud resources be stopped or terminated when they are no longer needed?**

Cloud resources should be stopped or terminated when they are no longer needed to avoid unnecessary costs. Unused resources can still be targeted by attackers if they remain running.


---

# LinkedIn Post (Required)

## Evidence

#### LinkedIn Post URL

https://www.linkedin.com/posts/inioluwa-oyebajo-486437398_devops-aws-linux-ugcPost-7485681860971479041-jgfL/?utm_source=screenshot_social_share&utm_medium=android_app&rcm=ACoAAGGYlOYBOn_PsB7jgFY6vcn0UKQqKg7ZS4M&utm_campaign=copy_link

`__________________________`

---

#### Screenshot — Published LinkedIn post

![alt text](<screenshots/Linkedin screenshot.jpeg>)

---

# Submission Instructions

- Add all required screenshots in your submission
- Full name must be visible in required screenshots
- Do not expose sensitive information (keys, passwords, account IDs)

---

# Completion Checklist

- [ ] Task 1: Screenshots (browser, ip a, ss -tulpen, ufw status) + Notes answered
- [ ] Task 2: Screenshots (nginx status, nginx -t, ss port 80) + Notes answered
- [ ] Task 3: Screenshots (access log, error log, journalctl) + Notes answered
- [ ] Task 4: Screenshots (uptime, free -h, df -h, du -sh) + Notes answered
- [ ] Task 5: Screenshots (ls html, grep deployed by, grep try_files) + Notes answered
- [ ] Task 6: Screenshots (nginx -t fail, nginx -t pass, curl recovery) + Notes answered
- [ ] Task 7: Screenshots (curl failure, curl recovery) + Notes answered
- [ ] Task 8: Security & Reliability Notes answered
- [ ] LinkedIn post published and URL submitted
- [ ] Full Name visible in all required screenshots
- [ ] No sensitive data exposed

---

## 📌 About DMI & CloudAdvisory

DevOps Micro Internship (DMI) is a project-based DevOps program run by Pravin Mishra (The CloudAdvisory) focused on real-world execution, systems thinking, and career readiness.

It helps learners build strong DevOps foundations with hands-on experience.

---

## 📌 Resources

- 🌐 DMI Official Website: https://pravinmishra.com/dmi  
- 🎓 DevOps for Beginners (Udemy): https://www.udemy.com/course/devops-for-beginners-docker-k8s-cloud-cicd-4-projects/  
- 🎓 Agentic AI DevOps with Claude Code: https://www.udemy.com/course/ultimate-agentic-ai-devops-with-claude-code/  
- 🎓 DevOps with Claude Code: Terraform, EKS, ArgoCD & Helm: https://www.udemy.com/course/devops-with-claude-code-terraform-eks-argocd-helm/  
- ▶️ YouTube Playlist: https://www.youtube.com/playlist?list=PLFeSNDtI4Cho  
- 🔗 Pravin Mishra (LinkedIn): https://www.linkedin.com/in/pravin-mishra-aws-trainer/  
- 🏢 CloudAdvisory (LinkedIn): https://www.linkedin.com/company/thecloudadvisory/

---

*This submission is part of DevOps Micro Internship (DMI) Cohort 3 — Agentic AI Track.*