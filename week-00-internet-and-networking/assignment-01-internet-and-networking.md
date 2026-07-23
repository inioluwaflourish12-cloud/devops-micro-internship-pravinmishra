# Week 00 - Internet and Networking

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

# 🧑‍💻 Task 1: Using ChatGPT as Your Learning Assistant

## Scenario

You're new to DevOps and will frequently encounter technical questions. ChatGPT can be your learning companion.

## Your Task

Write a clear ChatGPT prompt to help you understand:

> "What is a protocol in networking? Explain with a simple real-life example."

Take a screenshot of your interaction showing:

* Your detailed prompt (with clear expectations)
* ChatGPT's simplified response with an example

## Screenshot

Save your screenshot in the `screenshots` folder and update the file name below.

![alt text](<screenshots/Task1 Chatgpt.jpeg>)


Replace `task-1-chatgpt.png` with your actual screenshot file name.

---

## What I Learned (2–3 lines)

I learned that a networking protocol is a set of rules that devices follow to communicate with each other over a network. Just like people need to follow certain rules to have a clear conversation, computers also use protocols to exchange information correctly. This helped me understand why protocols are important for reliable communication on the internet.

---

# 🌐 Task 2: Internet and Networking

## Scenario

Your friend is launching an online bookstore named **EpicReads**.

He asked you to explain how users globally can access his website hosted in Finland.

## Your Task

Write a short explanation (**100–150 words**) that includes:

* Packet Switching
* IP Address
* TCP/IP
* HTTP/HTTPS

💡 **Tip:** You may use ChatGPT (as demonstrated in Task 1) to refine your explanation.

## Answer

EpicReads is hosted on a server in Finland, but users from different countries can still access it
through the internet. Every device connected to the internet has an IP address, which helps
identify where data should be sent.
When a user opens the EpicReads website, the browser uses HTTP/HTTPS to request
information from the server. HTTPS keeps the connection secure and protects user data. The
internet also uses TCP/IP protocols to make sure the data is delivered correctly between the
user and the website.
Information is transferred using packet switching, where data is divided into small packets and
sent through different routes before being combined again at the destination. These networking
technologies allow people around the world to use EpicReads quickly and safely.

---

# 🏗️ Task 3: Application Architecture & Stack

## Scenario

EpicReads bookstore has two application versions:

### Two-Tier Application

* Frontend
* Database

### Three-Tier Application

* Frontend
* Backend
* Database

## Your Task

* Draw simple diagrams (hand-drawn or tool-based such as draw.io)
* Label each layer clearly
* List at least two common technologies or tools used for each layer
* Submit a screenshot or photo clearly showing your own drawing

## Diagram Screenshot / Photo

Save your diagram image in the `screenshots` folder and update the file name below.

![alt text](<screenshots/Task3 diagram.jpeg>)


Replace `task-3-diagram.png` with your actual diagram file name.

---

## Technologies Used

### Frontend

* Next.js
* Tailwind.css

### Backend

* JWT
* Bcrypt.js

### Database

* MySQL
* MongoDB

---

# 🌍 Task 4: Domain Name & DNS (Basic Concepts)

## Scenario

Your friend's bookstore **EpicReads** is currently accessible through:

```text
52.172.142.222:3000
```

He purchased the domain:

```text
epicreads.com
```

## Your Task

In **50–100 words**, explain in your own words:

1. What is DNS (Domain Name System)?
2. Which DNS record type should be used to connect the domain to the given IP, and why?

## Answer

DNS (Domain Name System) is like the phonebook of the internet. It helps users access
websites using easy-to-remember domain names instead of typing complicated IP addresses.
When someone enters epicreads.com into a web browser, DNS translates the domain name
into the server’s IP address, which in this case is 52.172.142.222. The :3000 part represents a
port number used by the application running on the server.
To connect the domain name to the server’s IP address, an A Record should be used because
it maps a domain name to an IPv4 address. This makes it easier for users worldwide to visit the
EpicReads website quickly, conveniently, and without needing to memorize numerical IP
addresses.

---

# 💻 Task 5: Visual Studio Code Setup (Hands-on)

## Your Task

Install Visual Studio Code (if not already installed).

Take a screenshot of your VS Code environment showing:

* Terminal open inside VS Code
* Running a basic command:

### Windows

```powershell
dir
```

### Linux / macOS

```bash
pwd
ls
```

* Your selected VS Code theme clearly visible

⚠️ **Important:** The screenshot must show your username or another identifiable detail to confirm it is your environment.

## Screenshot

Save your screenshot in the `screenshots` folder and update the file name below.

![alt text](<screenshots/Task5 vscode.jpeg>)


Replace `task-5-vscode.png` with your actual screenshot file name.

---

# 🔗 Task 6: Publish Your Assignment as a LinkedIn Post

## Objective

Publishing on LinkedIn helps you:

* Build your professional online presence
* Reinforce your learning
* Document your DevOps journey publicly

## Your Task

Summarize your answers from Tasks 1–5 into a LinkedIn post.

Clearly structure your post into the following sections:

* ChatGPT
* Internet & Networking
* App Architecture
* DNS
* VS Code Setup

Add the following credit note at the end of your post:

> **P.S. This post is a part of DevOps Micro Internship with Agentic AI Cohort-3 by Pravin Mishra. You can start your DevOps journey by joining this Discord community: https://discord.pravinmishra.com/**

---

## LinkedIn Post URL



```text
https://www.linkedin.com/posts/inioluwa-oyebajo-486437398_im-really-excited-to-share-that-ive-been-activity-7463973360469852161-KfKi?utm_source=share&utm_medium=member_android&rcm=ACoAAGGYlOYBOn_PsB7jgFY6vcn0UKQqKg7ZS4M
```

---

## LinkedIn Post Backup Copy


I'm excited to share that I’ve been learning the fundamentals of DevOps through practical tasks and hands-on exercises 🚀

Here are some of the topics I worked on:

🔹 ChatGPT
Learned how AI tools like ChatGPT can help simplify technical concepts, improve understanding, and assist with assignments and learning.

🔹 Internet & Networking
Studied how websites are accessed globally using concepts like Packet Switching, IP Addresses, TCP/IP, and HTTP/HTTPS.

🔹 App Architecture
Learned the difference between Two-Tier and Three-Tier architectures, including the roles of Frontend, Backend, and Database layers.

🔹 DNS
Understood how DNS works like the phonebook of the internet by converting domain names into IP addresses. Also learned about DNS records like the A Record used for IPv4 addresses.

🔹 VS Code Setup
Installed Visual Studio Code, explored the integrated terminal, and practiced basic commands while setting up my development environment.

This journey has been a great introduction to DevOps concepts, and I’m excited to keep learning and building more skills 💻🔥

P.S. This post is part of the FREE DevOps Micro Internship Cohort run by Pravin Mishra. You can start your DevOps journey for free from his YouTube Playlist.

---

# Reflection – Week 0

### What did you find easy?

I found it easy to understand the basic networking concepts because the explanations and examples made them simple to follow

---

### What was difficult?

I found it a little difficult to understand some of the technical terms at first, especially DNS records and application architecture, but with more reading and practice, I understood them better.

---

### What will you improve next week?

Next week, I will improve by practicing more, asking questions whenever I'm unsure, and spending more time learning about DevOps tools and concepts.

---

## 📌 About DMI & CloudAdvisory

DevOps Micro Internship (DMI) is a project-based DevOps program run by Pravin Mishra (The CloudAdvisory) focused on real-world execution, systems thinking, and career readiness.

It helps learners build strong DevOps foundations with hands-on experience.


## 📌 Resources

- 🌐 **DMI Official Website:** https://pravinmishra.com/dmi  
- 🎓 **DevOps for Beginners (Udemy):** https://www.udemy.com/course/devops-for-beginners-docker-k8s-cloud-cicd-4-projects/  
- 🎓 **Ultimate Agentic AI DevOps with Clude Code** https://www.udemy.com/course/ultimate-agentic-ai-devops-with-claude-code/?referralCode=448389767BC96284087B
- 🎓 **DevOps with Claude Code: Terraform, EKS, ArgoCD & Helm** https://www.udemy.com/course/devops-with-claude-code-terraform-eks-argocd-helm/?referralCode=1C5B734505D65A010FA3
- ▶️ **YouTube Playlist (DMI Cohort 3):** https://www.youtube.com/playlist?list=PLFeSNDtI4Cho  
- 🔗 **Pravin Mishra (LinkedIn):** https://www.linkedin.com/in/pravin-mishra-aws-trainer/  
- 🏢 **CloudAdvisory (LinkedIn):** https://www.linkedin.com/company/thecloudadvisory/

---

*This submission is part of DevOps Micro Internship (DMI) Cohort 3 — Agentic AI Track*