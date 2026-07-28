# Assignment 6 — Build an AI-Assisted Linux Health Check (AI-Assisted Linux Incident Triage)

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will build a read-only Bash triage script that checks the health of your Ubuntu server and Nginx application, connect it to Claude Code as a reusable `/linux-triage` skill, simulate a controlled Nginx incident, use the skill to gather and analyze evidence, recover the service manually, and verify recovery. The workflow follows the Agentic Loop: Gather → Analyze → Human Act → Verify.

---

# Task 1 — Confirm the Healthy Baseline and Create the Workspace

## Goal

Confirm that Nginx and the React application are healthy before building the automation.

### Evidence

#### Screenshot 1 — Output of `systemctl is-active nginx`, `ss -ltn | grep ':80'`, and `curl -I http://localhost`

![alt text](<screenshots/Screenshot 1 (Assignment 6 task1).png>)

---

#### Screenshot 2 — Output of `pwd` and `find . -maxdepth 4 -type d | sort` showing the workspace folder structure

![alt text](<screenshots/Screenshot 2 (Assignment 6 task1).png>)

---

### Notes

Answer the following in your own words:

**1. What proves that Nginx is running?**

The command systemctl is-active nginx returned active, which confirms that the Nginx service is running properly.

---

**2. What proves that the server is listening for HTTP traffic?**

The command ss -ltn | grep ':80' showed that port 80 is in the LISTEN state.

---

**3. Why must you capture a healthy baseline before simulating an incident?**

A healthy baseline lets you know what the system looks like when everything is working correctly. 

---

# Task 2 — Create Project Context and Safety Rules in CLAUDE.md

## Goal

Tell Claude exactly what this project does and what it is not allowed to do.

### Evidence

#### Screenshot 3 — CLAUDE.md open in VS Code showing all four sections (Project Overview, Incident Workflow, Safety Rules, Output Rules)

![alt text](<screenshots/Screenshot 3 (Assignment 6 task2).png>)

---

### Notes

Answer the following in your own words:

**1. Why should Claude receive project-specific operational rules?**

Project-specific operational rules tell Claude what it is allowed and not allowed to do. This helps it analyze incidents safely, follow the correct workflow, and avoid making changes that could damage the system.

---

**2. Why is the human required to execute the recovery command?**

The human must execute the recovery command because Claude is only allowed to recommend recovery steps, not perform them. This ensures that a person reviews and approves any changes before they are made.

---

**3. Which rule prevents Claude from making an unsupported diagnosis?**

The rule that says "Do not claim a root cause unless the report contains supporting evidence." 

---

# Task 3 — Use Agentic AI to Plan Before Writing the Script

## Goal

Use Claude Code to inspect the environment and produce a read-only plan before creating any Bash code.

### Evidence

#### Screenshot 4 — Claude Code showing the five-check plan and read-only inspection results

![alt text](<screenshots/Screenshot 4 (Assignment 6 task3).png>)

---

### Notes

Answer the following in your own words:

**1. Which part of this task represents the Gather phase?**

The gather phase is when Claude checked the system and collected information, like the Nginx status, port 80, disk space, memory, and HTTP response, before making the conclusions.

---

**2. Did Claude follow the instruction not to create files? How did you verify this?**

 Yes, it did. Claude only read the CLAUDE.md file and gave me a plan of the checks to perform. It didn't create or edit any files, so I knew it followed the instructions.

---

**3. Why is planning before coding useful in DevOps automation?**

Planning first helps me know exactly what needs to be done before writing any code. It makes the script easier to build, helps avoid mistakes, and keeps the automation process organized.

---

# Task 4 — Build the Linux Triage Bash Script

## Goal

Create one Bash script that gathers consistent Linux and Nginx health evidence.

### Evidence

#### Screenshot 5 — Top section of `linux-triage.sh` showing variables, thresholds, and the checks array

![alt text](<screenshots/Screenshot 5 (Assignment 6 task4).png>)

---

#### Screenshot 6 — Middle section showing check functions and conditionals

![alt text](<screenshots/Screenshot 6 (Assignment 6 task4).png>)

---

#### Screenshot 7 — Bottom section showing the loop, summary function, and exit behavior

![alt text](<screenshots/Screenshot 7 (Assignment 6 task4).png>)

---

#### Screenshot 8 — Output of `bash -n scripts/linux-triage.sh` (no syntax errors) and `ls -l scripts/linux-triage.sh` showing executable permission

![alt text](<screenshots/Screenshot 8 (Assignment 6 task4).png>)

---

### Notes

Answer the following in your own words:

**1. What is stored in the checks array?**

The checks array stores the list of system checks the script needs to perform, including service status, port, HTTP response, disk usage, and memory.

---

**2. How does the `for` loop use that array?**

The for loop reads each function name from the checks array and runs it one after another until all the checks are completed.

---

**3. Why are the health checks separated into functions?**

The checks are separated into functions to keep the script organized, reusable, and easier to maintain. 

---

**4. What is the purpose of `$(...)` in this script?**

Its used to run a command and save it's output into a variable.

---

**5. Why does the script use different exit codes for HEALTHY, WARN, and FAIL?**

Different exit codes help show whether the system is healthy orhas failed.

---

# Task 5 — Run and Understand the Healthy-State Report

## Goal

Run the Bash script against the healthy server and verify that it creates a report.

### Evidence

#### Screenshot 9 — Output of `./scripts/linux-triage.sh` showing your Full Name and all five check results

![alt text](<screenshots/Screenshot 9 (Assignment 6task5).png>)

---

#### Screenshot 10 — Output showing the captured exit code and final summary

![alt text](<screenshots/Screenshot 10 (Assignment 6 task5).png>)

---

### Notes

Answer the following in your own words:

**1. What is the overall status of your healthy baseline?**

The overall status of my health baseline is HEALTHY because all five checks passed, with no warnings or failures.

---

**2. Which exact Linux evidence proves the application is serving traffic?**

The evidence is the line [PASS] Local HTTP check returned status 200. This shows that the application is responding successfully to HTTP requests.

---

**3. Did your script return exit code 0 or 1? Explain why.**

My script returned exit code 0 because all the health checks passed successfully, so the system was healthy and no errors were detected.

---

**4. What is the difference between a warning and a failure in this script?**

A warning means there is a potential issue that should be monitored, but the system is still working. A failure means there is a serious problem that needs immediate attention because it can affect the system or application.

---

# Task 6 — Create and Run the /linux-triage Skill

## Goal

Turn the Bash script into a reusable, manually invoked Agentic AI workflow.

### Evidence

#### Screenshot 11 — `SKILL.md` showing the frontmatter, allowed tool restrictions, and safety rules

![alt text](<screenshots/Screenshot 11 (Assignment 6 task6).png>)

---

#### Screenshot 12 — `/linux-triage` output for the healthy server

![alt text](<screenshots/Screenshot 12 (Assignment 6 task6).png>)

---

### Notes

Answer the following in your own words:

**1. Why does this skill have Bash, Read, and Grep, but not Write?**

The skill is designed to inspect the server without making any changes. Bash, Read, and Grep are enough to collect and search for information, while Write is not included to prevent accidental changes to the system.

---

**2. Why is `disable-model-invocation: true` useful for this skill?**

It makes sure the skill only collects evidence and doesn't let the AI make its own assumptions.

---

**3. What part is performed by Bash, and what part is performed by Claude?**

Bash runs the Linux commands and gathers the system information. Claude reads the results, explains what they mean, and helps interpret the evidence without changing anything on the server.

---

**4. Why is this better than asking Claude "Is my server healthy?" without giving it evidence?**

It's better because Claude is making its decision based on real system evidence instead of guessing.

---

# Task 7 — Simulate an Nginx Incident and Let the Skill Diagnose It

## Goal

Create a controlled service failure, gather evidence through Bash, and let Claude analyze the evidence without taking recovery action.

### Evidence

#### Screenshot 13 — Output showing Nginx is inactive and the HTTP request fails

![alt text](<screenshots/Screenshot 13 (Assignment 6 task7).png>)

---

#### Screenshot 14 — `/linux-triage` output showing failed evidence, most likely cause, and a suggested recovery command

![alt text](<screenshots/Screenshot 14 (Assignment 6 task 7).png>)

---

#### Screenshot 15 — `incident-failure-report.txt` showing the failed checks and your Full Name

![alt text](<screenshots/Screenshot 15 (Assignment 6 task7).png>)

---

### Notes

Answer the following in your own words:

**1. Which three checks failed?**

- Nginx service is not active.
- Port 80 is not listening.
- The local HTTP check returned status 000.

---

**2. What evidence supports the conclusion that Nginx is unavailable?**

The report shows that the Nginx service is inactive, port 80 is not listening, and the local HTTP request returned status 000, meaning the web server can not be reached.

---

**3. Did Claude execute the recovery command? Why is that important?**

No. Claude only recommended the recovery command and did not run it. It's important because it keeps the system safe by allowing the user to review and approve any recovery action before making changes.

---

**4. Which phase of the Agentic Loop is represented by the Bash report?**

The Bash report represents the Observe phase of the agentic loop. 
---

**5. Which phase is represented by Claude's explanation?**

Claude's explanation represents the Reason phase of the agentic loop.

---

# Task 8 — Recover Manually, Verify Again, and Write the Incident Summary

## Goal

Recover the service as the human operator and prove that the system is healthy again.

### Evidence

#### Screenshot 16 — Output showing Nginx is active and `curl -I http://localhost` returns 200 OK

![alt text](<screenshots/Screenshot 16 (Assignment 6 task8).png>)

---

#### Screenshot 17 — Second `/linux-triage` output showing successful recovery with no FAIL results

![alt text](<screenshots/Screenshot 17 (Assignment6 task8).png>)

---

#### Screenshot 18 — Output of `ls -lah reports` showing both `incident-failure-report.txt` and `recovery-report.txt`

![alt text](<screenshots/Screenshot 18 (Assignment 6 task8).png>)

---

#### Screenshot 19 — `incident-summary.md` showing all required sections and your Full Name

![alt text](<screenshots/Screenshot 19 (Assignment 6 task8).png>)

---

### Notes

Answer the following in your own words:

**1. What action did you execute manually?**

I manually stopped and restarted the Nginx service by running sudo systemctl start nginx after reviewing Claude's recommendation

---

**2. What evidence proves that the service recovered?**

The service recovered because systemctl is-active nginx returned active

---

**3. Why is the second triage run necessary?**

The second triage run confirms that the recovery worked.

---

**4. What could go wrong if an AI agent automatically restarted every failed service?**

An AI agent could restart the wrong service or interrupt a system that was intentionally stopped.

---

**5. In one sentence, explain the difference between using AI as a chatbot and using AI in this agentic workflow.**

A chatbot mainly answers questions, while an AI agent gathers evidence, analyzes the results, and guides the user through a structured workflow without making unauthorized changes.

---

# Incident Summary

Fill in all seven sections below in your own words.

**Full Name:** Oyebajo Inioluwa Flourish

**Date:** 24/07/2026

---

**1. Reported Symptom**

Nginx was unavailable after the service was stopped so the web sever couldn't be reached.

---

**2. Evidence Collected**

Nginx service was not active.

---

**3. Most Likely Cause**

The Nginx service was manually stopped which caused port 80 to stop listening and prevented the local HTTP request from connecting.

---

**4. Human-Approved Recovery Action**

I ran the recommended recovery command and manually executed sudo systemctl start nginx to restart the Nginx service.

---

**5. Verification**

After restarting Nginx, systemctl is-active nginx returned active.

---

**6. Safety Decision**

The AI was only allowed to collect and analyze system information. It was not allowed to restart the service automatically, so a human could review and approve the recovery action before making any changes.

---

**7. Agentic Loop Mapping**

Gather: Bash collected evidence about the system.
Verify: Claude verified the evidence and explained the problem.
Act: I manually restarted Nginx using the recommended command.

---

# LinkedIn Post (Required)

## Evidence

#### LinkedIn Post URL

https://www.linkedin.com/posts/inioluwa-oyebajo-486437398_dmibypravinmishra-linux-bash-ugcPost-7486487532021510144-AQFi/?utm_source=share&utm_medium=member_android&rcm=ACoAAGGYlOYBOn_PsB7jgFY6vcn0UKQqKg7ZS4M


---

#### Screenshot — Published LinkedIn post

![alt text](<screenshots/Assignment 6 linkedin post.jpeg>)

---

# GitHub Repository URL

https://github.com/inioluwaflourish12-cloud/devops-micro-internship-pravinmishra.git


---

# Submission Instructions

- Add all required screenshots in your submission
- Full Name must be visible in required screenshots and the Bash report
- All written answers must be in your own words
- Do not expose sensitive information (keys, passwords, AWS account IDs, tokens)
- GitHub URL must be included in this document

---

# Completion Checklist

- [ ] Task 1: Healthy baseline confirmed, workspace created (Screenshots 1–2, Notes answered)
- [ ] Task 2: CLAUDE.md created with all four sections (Screenshot 3, Notes answered)
- [ ] Task 3: Five-check plan produced by Claude using read-only tools (Screenshot 4, Notes answered)
- [ ] Task 4: `linux-triage.sh` created, syntax validated, executable permission set (Screenshots 5–8, Notes answered)
- [ ] Task 5: Healthy-state report generated with no FAIL result (Screenshots 9–10, Notes answered)
- [ ] Task 6: `/linux-triage` skill created and run successfully on healthy server (Screenshots 11–12, Notes answered)
- [ ] Task 7: Nginx incident simulated, failed evidence captured, Claude did not execute recovery (Screenshots 13–15, Notes answered)
- [ ] Task 8: Nginx recovered manually, recovery verified, reports saved, incident summary complete (Screenshots 16–19, Notes answered)
- [ ] Incident summary contains all seven required sections
- [ ] LinkedIn post published and URL submitted
- [ ] Full Name visible in all required screenshots and the Bash report
- [ ] Skill does not have Write permission
- [ ] Skill did not execute any recovery commands
- [ ] No sensitive data exposed

---

## 📌 About DMI & CloudAdvisory

DevOps Micro Internship (DMI) is a project-based DevOps program run by Pravin Mishra (The CloudAdvisory) focused on real-world execution, systems thinking, and career readiness.

It helps learners build strong DevOps foundations with hands-on experience.

---

## 📌 Resources

- 🌐 DMI Official Website: https://dmi.pravinmishra.com?utm_source=github&utm_medium=readme  
- 🎓 University: https://university.pravinmishra.com?utm_source=github&utm_medium=readme  
- 💬 Discord Community: https://discord.pravinmishra.com?utm_source=github&utm_medium=readme  
- 📝 Blog: https://dmi.pravinmishra.com/blog?utm_source=github&utm_medium=readme  
- ▶️ YouTube Playlist: https://www.youtube.com/playlist?list=PLFeSNDtI4Cho  
- 🔗 Pravin Mishra (LinkedIn): https://www.linkedin.com/in/pravin-mishra-aws-trainer/  
- 🏢 CloudAdvisory (LinkedIn): https://www.linkedin.com/company/thecloudadvisory/

---

*This submission is part of DevOps Micro Internship (DMI) Cohort 3 — Agentic AI Track.*