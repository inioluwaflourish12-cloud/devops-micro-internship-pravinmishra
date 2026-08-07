# Assignment 5 — AI-Assisted Sprint Health Report via Jira MCP

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In this assignment, you will connect Claude Code to your Jira board through an MCP server, the same way you connected it to GitHub in Week 2, and build a read-only `/sprint-health` skill. The skill reads your current sprint through Jira's API and reports sprint velocity, stories at risk of missing the sprint, and items missing an estimate — but it must never create, edit, comment on, or transition a single ticket itself. You will prove that boundary holds by making a real change on the board yourself and confirming the skill only ever reports, never acts.

---

# Task 1 — Create a Jira API Token

## Goal

Generate an API token from your Atlassian account that the MCP server will use to authenticate with your Jira site. Do not screenshot the token value itself.

### Evidence

#### Screenshot 1 — Jira API token creation confirmation page showing the token name, with the token value not visible

![alt text](<screenshots/Screenshot 1 (Assignment 5 task1) - Copy.png>)

### Notes You Must Write (Very Important):

Why does the MCP server need your site URL and account email in addition to the token?

The site URL identifies the Jira workspace, the email identifies the user account, and the API token provides authentication. All three are required for the MCP server to securely connect to the correct Jira environment.

---

# Task 2 — Create .mcp.json at the Project Root

## Goal

Create or update `.mcp.json` at your project root with a Jira MCP server block, following the same shape as the GitHub MCP server you configured in Week 2.

### Evidence

#### Screenshot 2 — `.mcp.json` open in VS Code showing the Jira server configuration

![alt text](<screenshots/Screenshot 2 (Assignment 5 task2).png>)

### Notes You Must Write (Very Important):

Compare this jira block to the github block from Week 2 Assignment 5. The GitHub server ran via npx (a Node.js package); this one runs via uvx (a Python package) — what stays exactly the same shape despite that difference, and why doesn't Claude Code care which language a given MCP server is written in?

Both the GitHub and Jira MCP configurations use the same MCP structure: a server name, command, args, and env section. The only difference is that GitHub uses npx to run a Node.js package while Jira uses uvx to run a Python package. Claude Code does not care what programming language the MCP server is written in because it communicates with all MCP servers through the same standardized MCP protocol.

---

# Task 3 — Add Your Credentials to settings.local.json

## Goal

Add your Jira site URL, account email, and API token to `.claude/settings.local.json`, and confirm that file is listed in `.gitignore` so it is never committed.

### Evidence

#### Screenshot 3 — `settings.local.json` open in VS Code showing the `env` section, with the actual token value blurred or covered

![alt text](<screenshots/Screenshot 3 (Assignment 5 task3).png>)

### Notes You Must Write (Very Important):

Why must JIRA_API_TOKEN live in settings.local.json and never in .mcp.json?

JIRA_API_TOKEN must be stored in settings.local.json because it contains sensitive credentials. The settings.local.json file is local to my machine and should not be committed to Git. The .mcp.json file is for server configuration only and may be shared with others, so secrets should never be stored there.

---

# Task 4 — Verify the Connection with /mcp

## Goal

Restart Claude Code and confirm the Jira MCP server shows as connected.

### Evidence

#### Screenshot 4 — `/mcp` output showing `jira: connected`

![alt text](<screenshots/Screenshot 4 (Assignment 5 task4).png>)

---

# Task 5 — Run a Live Query to Prove Real Board Data

## Goal

Ask Claude to list the issues in your current active sprint through the Jira MCP connection, and confirm the result matches what you see on your live board in the browser.

### Evidence

#### Screenshot 5 — Claude's response showing the live sprint issue list retrieved via Jira MCP

![alt text](<screenshots/Screenshot 5 (Assignment 5 task5).png>)

### Notes You Must Write (Very Important):

How did you confirm this was real board data and not something Claude guessed?

I confirmed the data was real by comparing the issues, statuses, assignees, story points, sprint name, and sprint summary returned by the Jira MCP with the actual Jira board in my browser. The issue keys and sprint information matched exactly, proving the data came directly from Jira rather than being generated or guessed by Claude.

---

# Task 6 — Build the /sprint-health Skill

## Goal

Create a `/sprint-health` skill restricted to read-only Jira tools plus `Read`, with no issue-mutating tools and no `Write`. Run it and confirm it produces a report covering sprint velocity, at-risk stories, and items missing an estimate.

### Evidence

#### Screenshot 6 — `SKILL.md` frontmatter showing `allowed-tools` limited to read-only Jira tools plus `Read`, with `disable-model-invocation: true`

![alt text](<screenshots/Screenshot 6 (Assignment 5 task6).png>)

#### Screenshot 7 — `/sprint-health` output showing the full triage report against your real sprint

![alt text](<screenshots/Screenshot 7 (Assignment 5 task6).png>)

### Notes You Must Write (Very Important):

1. Which Jira MCP tools does this skill's allowed-tools list include, and which mutating tools (create issue, update issue, transition issue, add comment) does it deliberately exclude?

The skill includes only Jira read tools: mcp__jira__jira_search, mcp__jira__jira_get_issue, mcp__jira__jira_get_sprint, mcp__jira__jira_get_board, and Read. These tools allow the skill to retrieve and analyze sprint information without making any changes. It deliberately excludes mutating tools such as create issue, update issue, transition issue, and add comment, ensuring the skill remains read-only and cannot modify the Jira board.

2. Why does a Scrum Master need this restriction more than almost any other role in this course?

A Scrum Master needs this restriction because their role is to monitor progress, identify risks, and facilitate discussions rather than directly changing work items. A read-only skill prevents accidental updates to issues, comments, estimates, or workflow statuses. This maintains transparency and ensures that decisions and changes are made by the team members responsible for the work, not automatically by the tool.

---

# Task 7 — Prove the Skill Never Mutates the Board

## Goal

Manually update one ticket on your board in the browser (for example, move a story to "Done" or add a missing estimate), then run `/sprint-health` again and confirm the new report reflects your change — proving the skill only ever reads live state and never wrote to the board itself.

### Evidence

#### Screenshot 8 — Second `/sprint-health` run showing the report now reflects your manual board change

![alt text](<screenshots/Screenshot 8 (Assignment 5 task7).png>)

### Notes You Must Write (Very Important):

Map this assignment to Gather → Analyze → Human Act → Verify from Week 3 Assignment 6. Which step did you perform manually in the browser, and why must that step stay human?

Gather: The /sprint-health skill retrieved live sprint data from Jira using read-only MCP tools.
Analyze: The skill analyzed sprint progress, calculated velocity, identified risks, and checked for missing estimates or acceptance criteria.
Human Act: I manually moved a Jira story to Done in the browser. This step must remain human-controlled because changing issue status affects project records, sprint tracking, and team commitments. A tool should not make those decisions automatically.
Verify: I ran /sprint-health again and confirmed that the report changed from 0/5 points completed to 2/5 points completed (40%), proving that the skill reads the live board state but does not modify it.

---

# Submission Instructions

Complete all tasks in sequence.

Your submission must include:
- All 8 required screenshots
- All the required notes

---

# Completion Checklist

- [ ] Task 1: Jira API token created, value never screenshotted (Screenshot 1)
- [ ] Task 2: `.mcp.json` has the Jira server block (Screenshot 2)
- [ ] Task 3: Credentials stored in `settings.local.json`, token blurred, file gitignored (Screenshot 3)
- [ ] Task 4: `/mcp` shows the Jira server connected (Screenshot 4)
- [ ] Task 5: Live query returned real sprint data, verified against the browser (Screenshot 5)
- [ ] Task 6: `/sprint-health` skill created with correct read-only `allowed-tools`, and produced a full report (Screenshots 6–7)
- [ ] Task 7: A manual board change was reflected in a second `/sprint-health` run (Screenshot 8)
- [ ] Skill never created, edited, transitioned, or commented on any issue
- [ ] Reflection answered (Notes)
- [ ] No API token value exposed

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
