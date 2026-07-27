# Assignment 5 — Bash Script Automation Drill (OPS Checklist)

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will practice Bash scripting by building a series of small automation scripts covering environment setup, variables, arrays, loops, file conditionals, if-else logic, and functions. These scripts form the foundation of real-world Linux automation used in DevOps, cloud, and production support environments.

---

# Task 1 — Bash Environment & Workspace Setup

## Goal

Verify that Bash is available on your system and create a clean workspace for this assignment.

### Evidence

#### Screenshot 1 — Output of `echo $SHELL` and `bash --version`

![alt text](<screenshots/Screenshot 1(Assignment 5 task1).png>)

---

#### Screenshot 2 — Output of `pwd` and `ls -lah` showing the scripts directory

![alt text](<screenshots/Screenshot 2 (Assignment 5 task1).png>)

---

### Notes

Answer the following in your own words:

**1. What is Bash?**

Bash is a command-line interpreter that allows users to interact with the Linux operating system.

---

**2. What is the difference between shell and Bash?**

A shell is a general program that allows users to communicate with the operating system while bash is a specific type of shell and is one of the most popular shells used in Linux. 

---

**3. Why is it important to confirm the Bash version before writing scripts?**

It is important because different versions support different features and syntax so confirming the version helps to make sure that the script will run correctly and avoids compatibility issues on the system.

---

# Task 2 — Your First Bash Script

## Goal

Create your first Bash script, make it executable, and run it from the terminal.

### Evidence

#### Screenshot 1 — Content of `first-script.sh`

![alt text](<screenshots/Screenshot 1(Assignment 5 task2).png>)

---

#### Screenshot 2 — Output of `./first-script.sh`

![alt text](<screenshots/Screenshot 2 (Assignment 5 task2.png>)

---

#### Screenshot 3 — Output of `ls -l first-script.sh` showing executable permission

![alt text](<screenshots/Screenshot 3 (Assignment 5 task2).png>)

---

### Notes

Answer the following in your own words:

**1. What is the purpose of `#!/bin/bash`?**

The #!/bin/bash tells the operating system to use the Bash shell to run the script.

---

**2. Why do we use `chmod +x` before running a script?**

We do that to make the script executable. Without executable permission, the operating system will not allow the script to be run directly.


---

**3. What is the difference between running a script using `./script.sh` and `bash script.sh`?**

Running a script with ./script.sh executes the script directly, so it must have executable permission and a valid shebang line. Running bash script.sh tells Bash to execute the script directly, so the script can run even if it is not marked as executable.

---

# Task 3 — Variables: User Information Script

## Goal

Use variables to store and display user-related information.

### Evidence

#### Screenshot 1 — Content of `user-info.sh`

![alt text](<screenshots/Screenshot 1 (Assignment 5 task3).png>)

---

#### Screenshot 2 — Output of `./user-info.sh`

![alt text](<screenshots/Screenshot 2 (Assignment 5 task 3).png>)

---

### Notes

Answer the following in your own words:

**1. What is a variable in Bash?**

A variable in Bash is used to store information, such as text or numbers, that can be used later in a script. It makes scripts more flexible and easier to update.

---

**2. Why should we avoid spaces around the `=` sign when creating variables?**

If spaces are added, Bash treats them as separate commands or arguments, which can cause an error.

---

**3. How do you access the value stored inside a Bash variable?**

You access the value of a Bash variable by putting a dollar sign ($) before the variable name. For example, if the variable is name, you can access its value using $name

---

# Task 4 — Arrays & Loops: Tools Checklist Script

## Goal

Use arrays and loops to print a checklist of tools used in Bash scripting.

### Evidence

#### Screenshot 1 — Content of `tools-checklist.sh`

![alt text](<screenshots/Screenshot 1 (Assignment 5 task 4).png>)

---

#### Screenshot 2 — Output of `./tools-checklist.sh`

![alt text](<screenshots/Screenshot 2 (Assignment 5 task 4).png>)

---

### Notes

Answer the following in your own words:

**1. What is an array in Bash?**

An array in Bash is a variable that stores multiple values under one variable name.

---

**2. Why are arrays useful in scripts?**

Arrays are useful for storing and processing multiple related values and maintaining scripts.

---

**3. What does `"${tools[@]}"` mean?**

It refers to all the elements in the tools array, allowing the script to access each item one by one.

---

**4. What is the purpose of the `for` loop in this script?**

The for loop goes through each item in the tools array and performs the same action for every item, which in this script is printing each tool name

---

# Task 5 — Loops: Number Counter Script

## Goal

Use loops to repeat a task multiple times.

### Evidence

#### Screenshot 1 — Content of `counter.sh`

![alt text](<screenshots/Screenshot 1 (Assignment 5 task5).png>)

---

#### Screenshot 2 — Output of `./counter.sh`

![alt text](<screenshots/Screenshot 2 (Assignment 5 task5).png>)

---

### Notes

Answer the following in your own words:

**1. What is a loop?**

A loop is a programming structure that repeats a block of code multiple times until a condition is met or all items have been processed.

---

**2. Why do we use loops in Bash scripting?**

We use loops in Bash scripting to automate repetitive tasks, reduce duplicate code, and make scripts more efficient.

---

**3. How many times did the loop run in your script?**

The loop ran 5 times.

---

**4. What would you change if you wanted the loop to run 10 times?**

I would change the loop's range or condition so that it counts from 1 to 10 instead of 1 to 5.

---

# Task 6 — Files & Conditionals: File Validation Script

## Goal

Use file checks and conditionals to verify whether files and directories exist.

### Evidence

#### Screenshot 1 — Output of `ls -lah ../test-folder`

![alt text](<screenshots/Screenshot 1 (Assignment 5 task6).png>)

---

#### Screenshot 2 — Content of `file-check.sh`

![alt text](<screenshots/Screenshot 2(Assignment 5 task6).png>)

---

#### Screenshot 3 — Output of `./file-check.sh`

![alt text](<screenshots/Screenshot 3 (Assignment 5 task6).png>)

---

### Notes

Answer the following in your own words:

**1. What does `-d` check in Bash?**

-d checks whether a specified path exists and is a directory.

---

**2. What does `-f` check in Bash?**

-f checks whether a specified path exists and is a regular file

---

**3. Why should file and directory paths be stored in variables?**

Storing file and directory paths in variables makes scripts easier to read, update, and reuse. You only need to change the path in one place if it changes.

---

**4. What happens if the file does not exist?**

If the file does not exist, the -f test returns false, and the script can display a message or take another action, such as creating the file or exiting.

---

# Task 7 — Conditionals: Pass or Retry Script

## Goal

Use if-else conditionals to make decisions based on a variable value.

### Evidence

#### Screenshot 1 — Content of `score-check.sh` with `score=85`

![alt text](<screenshots/Screenshot 1 (Assignment 5 task7).png>)

---

#### Screenshot 2 — Output showing `Result: Pass`

![alt text](<screenshots/Screenshot 2 (Assignment 5 task 7).png>)

---

#### Screenshot 3 — Content of `score-check.sh` with `score=55`

![alt text](<screenshots/Screenshot 3 (Assignment 5 task7).png>)

---

#### Screenshot 4 — Output showing `Result: Retry`

![alt text](<screenshots/Screenshot 4 (Assignments 5 task7).png>)

---

### Notes

Answer the following in your own words:

**1. What is the purpose of if-else in Bash?**

The if-else statement allows a script to make decisions by running different commands depending on whether a condition is true or false.

---

**2. What does `-ge` mean?**

-ge means greater than or equal to. It is used to compare two numbers in Bash.

---

**3. Why should conditions be tested with different values?**

Conditions should be tested with different values to make sure the script works correctly in all situations and handles different inputs properly.

---

**4. How can conditionals help in automation scripts?**

Conditionals help automation scripts make decisions automatically, such as checking for errors, validating input, or choosing the correct action based on different conditions.

---

# Task 8 — Functions: Final Bash Automation Script

## Goal

Create a final Bash script using functions to organize reusable code.

### Evidence

#### Screenshot 1 — Content of `final-automation.sh`

![alt text](<screenshots/Screenshot 1 (Assignment 5 task8).png>)

---

#### Screenshot 2 — Output of `./final-automation.sh`

![alt text](<screenshots/Screenshot 2 (Assignment 5 task8).png>)

---

#### Screenshot 3 — Output of `ls -lah` showing all created scripts

![alt text](<screenshots/Screenshot 3 (Assignment 5 task8).png>)

---

### Notes

Answer the following in your own words:

**1. What is a function in Bash?**

A function in Bash is a reusable block of code that performs a specific task. 
---

**2. Why are functions useful in scripts?**

Functions help organize code, reduce repetition, and make scripts easier to read, maintain, and update.

---

**3. Which functions did you create in this script?**

I created the print_header(), print_user_details(), and check_files() functions.

---

**4. How does this final script combine variables, arrays, loops, conditionals, files, and functions?**

The script uses variables to store information, arrays to hold multiple values, loops to repeat tasks, conditionals to make decisions, file checks to verify files and directories, and functions to organize the code into reusable sections.

---

# LinkedIn Post (Required)

## Evidence

#### LinkedIn Post URL

https://www.linkedin.com/posts/inioluwa-oyebajo-486437398_devops-linux-bashscripting-ugcPost-7486090721876180993-0IjN/?utm_source=share&utm_medium=member_android&rcm=ACoAAGGYlOYBOn_PsB7jgFY6vcn0UKQqKg7ZS4M


<<<<<<< HEAD
=======
`Add your URL here`
>>>>>>> upstream/main

---

#### Screenshot — Published LinkedIn post

![alt text](<screenshots/Assignment 5 linkedin post.jpeg>)

---

# Submission Instructions

- Add all required screenshots in your submission
- Full name must be visible in required screenshots
- All script files must be created and run successfully
- Required notes must be answered clearly for every task
- Do not expose sensitive information (keys, passwords, credentials)

---

# Completion Checklist

- [ ] Task 1: Environment setup verified, workspace created (Screenshots 1–2, Notes answered)
- [ ] Task 2: First script created, executed, permissions verified (Screenshots 1–3, Notes answered)
- [ ] Task 3: Variables script created and run (Screenshots 1–2, Notes answered)
- [ ] Task 4: Arrays and loops script created and run (Screenshots 1–2, Notes answered)
- [ ] Task 5: Counter loop script created and run (Screenshots 1–2, Notes answered)
- [ ] Task 6: File validation script created and run (Screenshots 1–3, Notes answered)
- [ ] Task 7: Pass/Retry conditional script tested with both values (Screenshots 1–4, Notes answered)
- [ ] Task 8: Final automation script created and run (Screenshots 1–3, Notes answered)
- [ ] All scripts run without errors
- [ ] Full Name visible in all required screenshots
- [ ] LinkedIn post published and URL submitted
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