# Assignment 6 — Building an AI-Assisted Git Safety Net (PR Ready Check)

Part of the DevOps Micro Internship (DMI) Cohort 3 with Agentic AI

---

## Purpose

In Week 2 you built Claude Code hooks that block a dangerous action *before* it happens (`PreToolUse`), and a restricted skill that could look but not touch (`allowed-tools` without `Write`). In this assignment you will discover that Git has the exact same idea, decades older: a **pre-commit hook** that blocks a commit before it's created.

You will build both halves of a real "PR Ready" workflow:

1. A **Git hook that follows fixed rules** — scans staged changes for hardcoded secrets and oversized files and refuses the commit. No AI involved, no guessing, just a rule that gives the same answer every time.
2. A **restricted Claude Code skill** (`/pr-ready`) that reads your staged diff and drafts a Pull Request title, description, and a short list of things worth a second look — the kind of judgment a fixed rule can't make (mixed changes, missing context, unclear intent). The skill never commits, pushes, or opens the PR. You do that yourself, using its draft as a starting point.

This mirrors the Agentic Loop from Week 3's Linux triage assignment: **Gather → Analyze → Human Act → Verify**. The hook and the skill both gather and analyze; only you act.

---

# Task 0 — Confirm Your Fork and Create a Feature Branch

## Goal

Confirm you are working in your own fork, then create a dedicated branch for this assignment.

### Evidence

#### Screenshot 1 — Output of git remote -v and git branch showing the new branch

![alt text](<screenshots/Screenshot 1 (Assignment 6 task0).png>)

---

### Notes

**1. Why create a dedicated branch instead of doing this work on main?**

A dedicated branch keeps new changes isolated from the main branch, making it safer to develop,test and review work before mergong. It also prevents accidental changes from affecting the stable version of the project.

---

# Task 1 — Stage a Change With Realistic Risk

## Goal

On your own fork of this repository (the one you've been submitting your DMI work in since onboarding), create a new branch and stage a change that a real reviewer should catch: a hardcoded-looking secret and a leftover debug statement.

### Evidence

#### Screenshot 1 — Output of  `git status` showing the staged file on feature/ai-pr-ready

![alt text](<screenshots/Screenshot 1 (Assignment 6 task 1).png>)

---

### Notes

**1. Why does this assignment use an obviously fake key instead of a real one?**

If a real key were used it could create a serious security risk and allow unauthorized access to resources.

---

# Task 2 — Write a Real Git Pre-Commit Hook

## Goal

Create a tracked, shareable pre-commit hook that blocks a commit containing secret-like patterns or files over 1MB.

### Evidence

#### Screenshot 2 — `hooks/pre-commit` open in VS Code showing the full script

![alt text](<screenshots/Screenshot 2 (Assignment 6 task2).png>)

---

#### Screenshot 3 — Output of `git config core.hooksPath` confirming it points to `hooks`

![alt text](<screenshots/Screenshot 3 (Assignment 6 task2).png>)

---

### Notes

**1. Why is `hooks/pre-commit` tracked in the repo instead of living only in `.git/hooks/`?**

Tracking hooks/pre-commit in the repository allows the hook to be shared with all contributors and version controlled. If it lived only in .git/hooks/, each developer would have to create and maintain it manually, making it harder to enforce consistent checks across the team.

---

**2. Compare this to `PreToolUse` from Week 2 Assignment 6. What does each one intercept, and what do they have in common?**

The pre-commit hook intercepts Git commits before they are recorded, while the PreToolUse hook we configured in Week 2 intercepted Claude's tool usage before a command was executed, and both act as preventive controls that enforce rules and stop unsafe actions before they can happen.

---

# Task 3 — Prove the Hook Blocks the Risky Commit

## Goal

Attempt to commit the staged file from Task 1 and show the hook rejecting it.

### Evidence

#### Screenshot 4 — Terminal showing `git commit` rejected with the hook's "BLOCKED" message naming the exact file

![alt text](<screenshots/Screenshot 4 (Assignment 6 task3).png>)

---

### Notes

**1. Which line in `hooks/pre-commit` matched your fake key, and why did it match?**

The line containing grep -qE 'AKIA[0-9A-Z]{16}|-----BEGIN (RSA|OPENSSH|PRIVATE) KEY-----' matched the fake key because the value AKIAABCDEFGHIJKLMNOP follows the pattern of an AWS access key ID, which starts with AKIA followed by 16 uppercase letters or numbers.

---

**2. Could this hook have caught a poorly-named variable that stores a secret without the `AKIA` prefix? What does that tell you about the limits of a fixed rule like this?**



---

# Task 4 — Build the `/pr-ready` Skill

## Goal

Create a manually invoked Claude Code skill that reads your staged changes and produces a PR-readiness report and a draft PR description — without writing, committing, or pushing anything itself.

### Evidence

#### Screenshot 5 — `SKILL.md` frontmatter showing `allowed-tools: Bash, Read, Grep` (no `Write`) and `disable-model-invocation: true`

![alt text](<screenshots/Screenshot 5 (Assignment 6 task4).png>)

---

#### Screenshot 6 — `/pr-ready` output while the risky file is still staged, showing it flagged the secret and/or debug statement

![alt text](<screenshots/Screenshot 6 (Assignment 6 task 4).png>)

---

### Notes

**1. Why does `/pr-ready` have `Bash` and `Read` but not `Write`?**

/pr-ready only needs to inspect the staged changes and generate a review report, so it requires Bash and Read to view Git information but does not need Write because it should never modify files, create commits, or change the repository.

---

**2. The pre-commit hook and `/pr-ready` both looked at the same staged diff. Did they flag the same things? What did one catch that the other didn't?**

Both identified the hardcoded key in the staged file, but the pre-commit hook automatically blocked the commit based on pattern matching, while /pr-ready provided a more detailed review by identifying the debug statement and explaining the risks in a human-readable report.

---

# Task 5 — Fix the Issues and Re-Verify

## Goal

Remove the secret and debug statement, then prove both gates now pass clean.

### Evidence

#### Screenshot 7 — `git commit` succeeding after the fix (no BLOCKED message)

![alt text](<screenshots/Screenshot 7 (Assignment 6 task 5).png>)

---

#### Screenshot 8 — Second `/pr-ready` run showing a clean risk report and a drafted PR title + description

![alt text](<screenshots/Screenshot 8(Assignment 6 task5).png>)

---

### Notes

**1. What exactly did you change to satisfy the pre-commit hook?**

I removed the hardcoded AWS access key and deleted the debug echo statement that exposed the key value. After removing both lines and re-staging the file, the pre-commit hook no longer detected a secret-like pattern and allowed the commit to proceed.

---

# Task 6 — Push and Open a Pull Request Using the AI Draft

## Goal

Push your branch and open a real Pull Request, using `/pr-ready`'s drafted title and description as your starting point — read it critically and edit before you use it.

**Important:** Open this Pull Request with base repository set to **your own fork** — not the shared upstream `pravinmishraaws/devops-micro-internship-pravinmishra` repository. This assignment's hook and skill files are your own practice work, not a change meant for the shared class repo.

### Evidence

#### Screenshot 9 — Your Pull Request showing the base repository is your own fork, plus the title and description, with the `/pr-ready` draft visible for comparison (paste it in the PR conversation or your notes below)

![alt text](<screenshots/Screenshot 9 (Assignment 6 task6).png>)

---

#### PR Link

https://github.com/inioluwaflourish12-cloud/devops-micro-internship-interviews/pull/1

---

### Notes

**1. What, if anything, did you edit in the AI's drafted PR description before using it? Why?**

I reviewed the AI-generated description and adjusted it to accurately reflect the changes I actually made. I removed anything that was unclear or inaccurate and added details about fixing the credential-shaped string and debug statement.

---

**2. If you had blindly copy-pasted the AI's draft without reading it, what could go wrong?**

The description could contain incorrect information, miss important details, or misrepresent the purpose of the changes. Reviewing it helps ensure the PR accurately describes the work performed.
---

**3. Why does this PR need to target your own fork instead of the shared upstream repository?**

The internship workflow requires contributors to work in their own forks. Opening the PR against my fork prevents accidental changes to the shared upstream repository and allows my work to be reviewed safely before any upstream contribution.

---

# Task 7 — Map the Workflow to the Agentic Loop

## Goal

Explain this assignment's workflow using the same Gather → Analyze → Human Act → Verify structure from Week 3.

### Notes

**1. Which step(s) represent Gather?**

Task 1 and Task 2 represent Gather because the workflow collected the information needed for review. The pre-commit hook gathered the staged files and changes, while /pr-ready gathered the staged diff using Git commands like git diff --cached and git status.

---

**2. Which step(s) represent Analyze?**

Task 4 represents Analyze because the /pr-ready Claude Code skill reviewed the staged changes, identified risks like the credential-shaped string and debug statement, and generated recommendations and a PR draft.

---

**3. Which step is Human Act, and why must a human — not Claude — run `git commit`, `git push`, and open the PR?**

Task 6 represents Human Act because a human must review the AI suggestions, decide what changes are acceptable, run git commit, git push, and create the Pull Request. Claude can assist with analysis, but a human must remain responsible for actions that change repository history or share code with others.

---

**4. Which step is Verify?**

Task 3 and Task 5 represent Verify because the pre-commit hook tested whether the risky commit was blocked and later confirmed that the corrected file passed successfully. The /pr-ready skill also provided another verification layer by reviewing the changes before the Pull Request was created.

---

**5. In one or two sentences: why do you need *both* the fixed-rule pre-commit hook and the AI skill? Isn't one enough?**

Both are needed because they serve different purposes. The pre-commit hook automatically enforces security rules and blocks unsafe commits, while the AI skill provides a deeper review, explains risks, and helps prepare a better Pull Request.

---

# Task 8 — LinkedIn Post

## Goal

Publish a LinkedIn post summarizing what you built and what you learned about combining fixed-rule safety checks with AI-assisted review.

### Evidence

#### LinkedIn Post URL

https://lnkd.in/p/eKzpyMxz

---

## Key Learnings

Add 3-5 bullet points on what you learned this week.

- I learned how to work with forks, branches and pull requests
- I understood why humans should remain resposible for git actions like committing,pushing and pull request even when AI is involved
- I learned how git pre-commit hooks help enforce security rules bly automatically blocking risky commits before they reach a repository.

---

# Submission Instructions

- Ensure `hooks/pre-commit` and `.claude/skills/pr-ready/SKILL.md` are committed to your GitHub repository
- Add all required screenshots to your submission
- All written answers must be in your own words
- Do not use a real secret or credential anywhere in your submission — the fake key in Task 1 is intentional and must stay clearly fake
- Open your Pull Request against your own fork, not the shared upstream repository
- Push your final changes to your forked repository
- Include your PR link and LinkedIn post URL

---

## GitHub Repository URL

Paste your forked repository URL here:

`Add your URL here`

---

# Completion Checklist

- [ ] Branch `feature/ai-pr-ready` created with a staged file containing a fake secret and a debug statement
- [ ] `hooks/pre-commit` created and tracked in the repo (not only in `.git/hooks/`)
- [ ] `core.hooksPath` configured to point at `hooks/`
- [ ] Pre-commit hook shown blocking the risky commit
- [ ] `.claude/skills/pr-ready/SKILL.md` created with correct `allowed-tools` (no `Write`) and `disable-model-invocation: true`
- [ ] `/pr-ready` run against the risky diff and shown flagging issues
- [ ] Risky file fixed; `git commit` succeeds cleanly
- [ ] `/pr-ready` re-run showing a clean report and drafted PR title/description
- [ ] Pull Request opened using the AI draft as a starting point, with your own fork as the base repository (not upstream), PR link included
- [ ] Agentic Loop mapping (Task 7) completed in your own words
- [ ] LinkedIn post published and URL submitted
- [ ] All required screenshots added
- [ ] GitHub repository URL provided

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
