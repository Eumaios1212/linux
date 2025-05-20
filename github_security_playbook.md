## Beginner-Friendly GitHub Organization Security Playbook

### (Team Plan • CodeQL Add-On • Code Rabbit Enabled • **Linux-Only Edition**)

> **Audience**  
> First-time GitHub **Team** org owners running **Linux workstations** who want a hardened security 
> baseline **and** AI pull-request reviews from **Code Rabbit**.
> 
> **What you need**  
> 
> 1. Org **Owner** role (or repo **Admin** for repo-level steps).  
> 2. **Advanced Security / CodeQL add-on** already active.  
> 3. **Code Rabbit** GitHub App installed for **All repositories**.  
> 4. About **45 minutes** (first repo) · **10 minutes** per additional repo.
> 
### Verify Prerequisites
> **GitHub → Org → Settings → Billing and Licensing → Licensing  
> Advanced Security/CodeQL**:  
> Confirm Secret Protection and Code Security are active.  
> **GitHub Team**:  
> Confirm active numbers of Seats.
> 
><img alt="Screenshot" src="/images/licenses.png" width="60%"/>  

> **Code Rabbit**:  
> **GitHub → Org → Settings → Third-party access → GitHub Apps → Configure**  
> Confirm "Code Rabbit" is listed with "All 
> repositories" access.  
> 
> <img alt="Screenshot" src="/images/coderabbit_repos.png" width="60%"/>
---

## 🗺️ Road Map

| Time   | Section                                                                                 |
|--------|-----------------------------------------------------------------------------------------|
|        | [📑 Mini‑Glossary](#-miniglossary)                                                      |
| 1 min  | [🛤️ Prepare Your Linux Workstation](#-prepare-your-linux-workstation)                  |
| 10 min | [1 - Org‑wide Hardening](#1--orgwide-hardening)                                         |
| 15 min | [2 - Enable Advanced Security + Code Rabbit](#2--enable-advanced-security--code-rabbit) |
| 5 min  | [3 - Branch‑Protection Template](#3--branchprotection-template)                         |
| 3 min  | [4 - Developer Workstation Setup](#4--developer-checklist-linux)                        |
| 5 min  | [5 - Monitoring & Upkeep](#5--monitoring--maintenance)                                  |
| 2 min  | [6 - One-Minute Smoke Test 🧪](#6--one-minute-smoke-test-)                              |

---

## 📑 Mini‑Glossary

| Term                       | Plain-English meaning                                                        |
|----------------------------|------------------------------------------------------------------------------|
| **2FA**                    | Login needs an authenticator app, passkey, or security key.                  |
| **Default setup (CodeQL)** | One-click CodeQL, no YAML to maintain.                                       |
| **Advanced workflow**      | `.github/workflows/codeql.yml` that you commit & edit.                       |
| **Branch protection**      | Rules that block risky pushes/merges.                                        |
| **Push Protection**        | Blocks secrets *during* `git push`.                                          |
| **Dependabot**             | Bot PRs that fix vulnerable dependencies.                                    |
| **Code Rabbit**            | GitHub App that posts AI code-reviews + `Code Rabbit / Review` status check. |

---

## 🛤️ Prepare Your Linux Workstation

1. Install KeePassXC **password manager** with **TOTP authenticator**.  
2. Verify **Git ≥ 2.34**:  
   
   ```bash
   git --version
   ```
   
   *If older, install from your distro’s backports PPA or <https://git-scm.com/download/linux>.*  
3. Install **GnuPG & pinentry**:  
   
   ```bash
   sudo apt update && sudo apt install -y gnupg2 pinentry-tty
   ```

---

## 1  Org‑Wide Hardening

> *Click‑path hint:* Org homepage → ⚙ **Settings** → **Security** sidebar.

| # | Click‑Path ▶                           | Action & Screenshot                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                | Why beginners care                        |
|---|----------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------|
| 1 | **Security ▶ Authentication security** | Select **Require two‑factor authentication**<br/>  <br/><img alt="Screenshot" src="/images/2fa.png" width="60%"/>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | Password‑only accounts blocked in 7 days. |
| 2 | **Member privileges**                  | **Default repository permission** → **Read**  <br/>  <br/><img alt="Screenshot" src="/images/member_privs.png" width="60%"/>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | New members can’t force‑push everywhere.  |
| 3 | **Member privileges**                  | **Outside collaborators** → **Limited**<br/>  <br/><img alt="Screenshot" src="/images/outside_colabs.png" width="60%"/>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            | Contractors only see assigned repos.      |
| 4 | **Third‑party access**                 | Toggle **Restrict access via fine-grained PATS** <br/>  <br/><img alt="Screenshot" src="/images/pats.png" width="60%"/>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            | Stops rogue CI integrations.              |
| 5 | **Teams**                              | Add team members: <br/>**Organization** → **Teams** → **select a team (or create new team)** → **Add a member**<br/>  <br/><img alt="Screenshot" src="/images/add_members.png" width="60%"/> <br/>Give Read/Write access:  <br/>**Organization** →  **Teams** → **select a team** → **select a member** → **Manage access** → **edit**  <br/>  <br/><img alt="Screenshot" src="/images/member_access.png" width="60%"/><br/> Set Collaborators and teams for a repo:  <br/>**Organization** → **Settings** → **Collaborators and teams** <br/>  <br/><img alt="Screenshot" src="/images/collabs.png" width="60%"/> | Group permissions & CODEOWNER routing.    |
| 6 | **Any repo**                           | **Add a `CODEOWNERS` file** at `.github/CODEOWNERS`. GitHub will read it immediately after push.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
### <u>CODEOWNERS File</u>
`CODEOWNERS` is a plain-text file you keep in your repository (commonly at `.github/CODEOWNERS`, though 
 `/CODEOWNERS` at the root or in `/docs` also works). Each line maps one or more file-path patterns to one or more 
owners—people or teams—so that whenever those paths change in a pull request, GitHub automatically:  
1.Requests reviews from the listed owners.  
2.Counts their approvals toward any branch-protection rule that says 
“Require review from Code Owners.”  
Because the file sits in-repo, the rules evolve right alongside your codebase and are version-controlled like everything else.
### How it works with **GitHub Teams**

| Concept                           | How it behaves                                                                                                                                                                                                                                                              |
|-----------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Referencing a team**            | Use the slug `@org/team-name` (e.g., `@octo-org/frontend`). Everyone in that team is considered an owner.                                                                                                                                                                   |
| **Automatic review requests**     | As soon as a PR touches a matching path, GitHub picks up to **three** members of each team to request (unless the PR author is in that team).                                                                                                                               |
| **Branch-protection enforcement** | If you enable “Require review from Code Owners” on `master`, an approval from *any* member of the owning team satisfies the rule (or, with “Require approval from code owners” turned **on**, **at least one** owner must approve in addition to the regular review count). |
| **Escalating granularity**        | Owners defined later in the file and with more-specific patterns override earlier, broader ones.<br/>Example:<br/>`/frontend/        @org/frontend-team`<br/>`/frontend/payments/ @org/payments-team`                                                                       |
| **Team visibility**               | The reviewers picker shows the team name; teammates can expand it to pick a specific colleague when volunteering.                                                                                                                                                           |
| **Audit trail**                   | Because team membership is managed in **Settings › Teams**, rotating people in or out of a team instantly updates ownership—no file edit needed.                                                                                                                            |


```text
# ===== CODEOWNERS: Homeric-Freedom =====
# Repo-specific "owners" tagged for review
*                       @Homeric-Freedom/Hummingbot-Team
# File-specific "owners" tagged for review
/hummingbot/**/*.md     @owner
# ===== END =====
```

Commit & push for each repo:

```bash
mkdir -p .github # If no .github dir
nano .github/CODEOWNERS   # paste, save
git add .github/CODEOWNERS
git commit -m "[root dir name]: add CODEOWNERS"
git push
```
PRs touching `*` (all files in repo) ping **@Hummingbot-Team** + **Code Rabbit** AI; any merge is blocked until 
human backend owner approves.  
GitHub auto-requests human owners *plus* Code Rabbit AI reviews whenever a matching file changes.

## GitHub Settings
1. Enforce: **Org** → **Repo → Settings → Branches → Branch protection rule** → **Edit** →  
**i. Require a pull request before merging**  
**ii. Require approvals (2)**  
**iii. Dismiss stale pull request approvals when new commits are pushed**  
**iv. Require review from Code Owners**   
**v. Restrict who can dismiss pull request reviews**  
<img alt="Screenshot" src="/images/branch_setting1.png" width="40%"/>  
**vi. Allow specified actors to bypass required pull request**  
**vii. Require approval of the most recent reviewable push**  
**viii. Require status checks to pass before merging**  
**ix. Require branches to be up to date before merging**  
<img alt="Screenshot" src="/images/branch_setting2.png" width="40%"/>  
**x. Require conversation resolution before merging**  
**xi. Require signed commits**  
<img alt="Screenshot" src="/images/branch_setting3.png" width="40%"/>


✅ **Checkpoint** — Org **People** shows 2FA ✅ for everyone; default perm = Read.

---

## 2  Enable Advanced Security + Code Rabbit

Repeat per repo.

### 2.1 CodeQL
1. **Organization → Repositories → your repo → Security → Code scanning** → edit **Tools** (or **Add tool**) 
   **Menu** → **view setup type**.
2. Choose **Default setup** *or* **edit `.github/workflow/codeql.yml`** → **Commit**.
3. **Actions** → `CodeQL / Analyze` turns green.  
<img alt="Screenshot" src="/images/code_scanning.png" width="40%"/>

### 2.2 Dependabot
Organization-wide:  
**Security** → **Dependabot**  
Enabled by default.  

Repo-wide:  
**Org** → **Repositories** → select repo → **Security** → **Dependabot**  

### 2.3 Secret Scanning

Organization-wide:  
**Org** → **Security** → **Dependabot**  
<img alt="Screenshot" src="/images/dependabot_org.png" width="40%"/>  

Repo-wide:  
**Org** → **Repositories** → select repo → **Security** → **Overview**  
Enabled by default

<img alt="Screenshot" src="/images/security_overview.png" width="40%"/>

### 2.4 Workflow permissions
### Organization-wide:  
**Organization → Settings → Code, planning, and automation → Actions → General** →   

Policies:  
1. **Choose which repositories are permitted to use GitHub Actions.**  
 Enable: **All repositories**

2. **Allow all actions and reuseable workflows**  
<img alt="Screenshot" src="/images/actions_perms.png" width="40%"/>

3. **Approval for running fork pull request workflows from contributors**  
Enable: **Require approval for all external contributors**  
<img alt="Screenshot" src="/images/fork_pr_workflow.png" width="40%"/>

Workflow permissions:  
1. Enable: **Read repository contents and packages permissions**.  
<img alt="Screenshot" src="/images/actions_perms2.png" width="40%"/>

### Repo-level:  
**Org → Settings → Code and automation → Actions → General**

Enable: **Allow all actions and reusable workflows**  
<img alt="Screenshot" src="/images/repo_actions_perms.png" width="40%"/>


Workflow permissions:   
Everything in this box controls the `GITHUB_TOKEN` that GitHub automatically injects into every job of every workflow 
run in this repository.  
<img alt="Screenshot" src="/images/repo_workflow_perms.png" width="40%"/>

### 2.5 Verify Code Rabbit App (once)

1. **Org → Settings → Third-part Access →  GitHub Apps** → **Code Rabbit**.  
2. Ensure **All repositories: Read & Write** permissions.  
   <img alt="Screenshot" src="/images/code_rabbit.png" width="40%"/>

3. Code Rabbit posts a **daily digest** of PRs to the private Discord **“Hbot”** (configured in Code Rabbit).

   <img alt="Screenshot" src="/images/discord.png" width="60%"/>

✅ **Checkpoint** — Repo **Settings → Branches** shows status checks `CodeQL / Analyze` **and** `Code Rabbit / Review` after first PR.

---

## 3  Branch‑Protection Template

1. **Repo → Settings → Branches → Add or Edit rule** → branch name pattern `[repo name]`.

   **i. Require a pull request before merging**  
   **ii. Require approvals**  
   **iii. Dismiss stale pull request approvals when new commits are pushed**  
   <img alt="Screenshot" src="/images/branch_prot1.png" width="60%"/>

   **iv. Require review from Code Owners**  
   **v. Restrict who can dismiss pull request reviews**  
   **vi. Allow specified actors to bypass required pull requests**  
   <img alt="Screenshot" src="/images/branch_prot2.png" width="60%"/>

   **vii. Require approval of the most recent reviewable push**  
   **viii. Require branches to be up to date before merging**  
   **ix. Require conversation resolution before merging**  
   **x. Require signed commits**  
   <img alt="Screenshot" src="/images/branch_prot3.png" width="60%"/>

2. Status checks → add `CodeRabbit`,`CodeQL`, `Analyze (javascript)`, `Dependabot`.  

   <img alt="Screenshot" src="/images/status_check.png" width="60%"/>
3. Save.  

✅ Direct push rejected; PR **Checks** show CodeQL + Code Rabbit.

---

## 4  Developer Checklist (Linux)

### 4.1 Enable 2FA

Profile picture → **Settings → Password & authentication** → **Enable two‑factor authentication**.  
<img alt="Screenshot" src="/images/2fa_setting.png" width="60%"/>
### 4.2 Generate a GPG Key & Auto‑Sign

1. Generate the key:  
`gpg --full-generate-key`  
Choose:
    ECC → Curve25519
    Key size / expiry → accept defaults or enter “2y” →
    Your name + the same e-mail GitHub shows on commits →
    a strong pass-phrase

2. Find the key ID:  
`gpg --list-secret-keys --keyid-format=long`  
Look for a line like:
`sec   ed25519/ABCD1234EF567890 2025-05-18 [SC]`  
Copy the part after the slash (ABCD1234EF567890).
We’ll call that “YOUR_KEY_ID” in the next command.
   
3. Export the public key
`gpg --armor --export YOUR_KEY_ID > pubkey.asc`  
Open `pubkey.asc` in a text editor, select all, copy.

4. Add the key to GitHub
Web → profile picture ▸ Settings ▸ SSH and GPG keys ▸ New GPG key.
 Paste the contents of `pubkey.asc` ▸ Add GPG key.

5. Copy the fingerprint:  
`gpg --list-secret-keys --fingerprint YOUR_KEY_ID`  
You’ll see:
`Key fingerprint = 1234 5678 90AB CDEF 1234  5678 90AB CDEF 1234 5678`  
Remove the spaces so it becomes:
`1234567890ABCDEF1234567890ABCDEF12345678`

6. Configure Git to use that fingerprint:
    ```
    git config --global gpg.format openpgp
    git config --global user.signingkey 1234567890ABCDEF1234567890ABCDEF12345678
    git config --global commit.gpgsign true
    ```
7. Test:
    ```bash
    echo "test" > demo.txt
    git add demo.txt
    git commit -m "signed test commit"
    ```
You should get a gpg: signing prompt and—after pushing—a Verified badge on GitHub.

### 4.3 Example

```bash
git switch -c feature/login-fix
# edit code
git add .
git commit -m "fix: login"  # auto-signed
git push --set-upstream origin feature/login-fix
```


Open PR → Code Rabbit AI review → fix CodeQL alerts → human review → **Squash & merge**.  

---

## 5  Monitoring & Maintenance

| Need                         | Location                                                                        |
|------------------------------|---------------------------------------------------------------------------------|
| Advanced Security seat usage | Org → Settings → **Billing → Advanced Security usage**                          |
| Security email digest        | Profile → Settings → **Notifications**                                          |
| Slack alerts                 | Add *GitHub Security* Slack app → `/github subscribe owner/repo security_alert` |
| Audit log (90 days)          | Org → Settings → **Audit log**                                                  |
| Auto-delete merged branches  | Repo → Settings → **General → Automatically delete head branches**              |

---

## 6  One-Minute Smoke Test 🧪

| Action                              | Expected                                                           |
|-------------------------------------|--------------------------------------------------------------------|
| Push `AWS_SECRET_ACCESS_KEY="TEST"` | Push Protection blocks or Secret Scanning alert appears.           |
| PR with `eval(req.body)` JS code    | CodeQL check fails; merge blocked.                                 |
| Unsigned push to `main`             | Push rejected: commits must be signed.                             |
| Open standard PR                    | Code Rabbit Review status check appears; AI comments within ~30 s. |

If all tests pass, your baseline is working.

---
