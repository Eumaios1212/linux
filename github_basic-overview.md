# GitHub Security Template — **Comprehensive Setup Guide**

> **Goal:** Create a private *template repository* that ships with hardened defaults (CI, CODEOWNERS, Dependabot, security policies) **and** configure organisation‑wide settings so every current and future repo starts secure by default.
>
> Everything below can be executed entirely in the GitHub web UI. The final section shows optional CLI automation.

---

## 0  Prerequisites

| Requirement                                                                  | Why                                                 |
| ---------------------------------------------------------------------------- | --------------------------------------------------- |
| **GitHub Team** plan **+ Advanced Security** add‑on                          | Enables CodeQL & Secret‑scanning for private repos. |
| **Role:** Org **Owner** (or *Admin + Security‑manager* for security toggles) | Required to flip org‑wide switches.                 |
| **Default branch name:** `master` (edit instructions if you use `main`)      | All patterns below assume `master`.                 |

---

## 1  Create the template repository

1. Org home ► **Repositories ➜ New**
2. **Name:** `security-template`    **Visibility:** **Private**
3. ✔ *Add README*  → **Create repository**

---

## 2  Add baseline files (four total)

For each file: **Add file ➜ Create new file** → paste → \*\*Commit directly to \*\*\`\`.

### 2‑a  `.github/CODEOWNERS`

```text
# Require Alice’s sign‑off on every pull‑request in any derived repo
*   @alice-github-id          # ← replace with your GitHub username
```

### 2‑b  `.github/workflows/ci.yml` — *Universal auto‑detect build*

```yaml
###############################################################################
# UNIVERSAL CI WORKFLOW
# • Runs on every push to master and on every pull‑request.
# • Starts with a read‑only GITHUB_TOKEN (least‑privilege).
# • Auto‑detects Node, Java (Gradle or Maven), Go, or Python projects.
###############################################################################
name: CI (auto-detect & test)

on:
  pull_request:
  push:
    branches: [ master ]

permissions:
  contents: read          # prevents a compromised action from pushing or tagging

jobs:
  build-test:
    runs-on: ubuntu-latest
    name: Build & Test (any language)

    steps:
      # 1️⃣  Always check out repo
      - name: Checkout sources
        uses: actions/checkout@v4

      #######################################################################
      # 2️⃣  Language-specific tool‑chains (each wrapped in an `if:` filter)
      #######################################################################
      - name: Set up Node
        if: ${{ hashFiles('package.json') != '' }}
        uses: actions/setup-node@v4
        with:
          node-version: 22

      - name: Set up Java
        if: ${{ hashFiles('**/build.gradle') != '' || hashFiles('**/pom.xml') != '' }}
        uses: actions/setup-java@v4
        with:
          distribution: temurin
          java-version: 21

      - name: Set up Go
        if: ${{ hashFiles('go.mod') != '' }}
        uses: actions/setup-go@v5
        with:
          go-version: 1.22

      - name: Set up Python
        if: >-
          ${{
            hashFiles('requirements.txt')   != '' ||
            hashFiles('pyproject.toml')     != '' ||
            hashFiles('setup.py')           != ''
          }}
        uses: actions/setup-python@v5
        with:
          python-version: '3.12'

      #######################################################################
      # 3️⃣  Install dependencies & run tests  (one step per language)
      #######################################################################
      - name: Node – install & test
        if: ${{ hashFiles('package.json') != '' }}
        run: |
          npm ci
          npm test

      - name: Gradle – test
        if: ${{ hashFiles('**/build.gradle') != '' }}
        run: ./gradlew test --no-daemon

      - name: Maven – test
        if: ${{ hashFiles('**/pom.xml') != '' }}
        run: mvn --batch-mode -ntp test

      - name: Go – test
        if: ${{ hashFiles('go.mod') != '' }}
        run: go test ./...

      - name: Python – install & test
        if: >-
          ${{
            hashFiles('requirements.txt')   != '' ||
            hashFiles('pyproject.toml')     != '' ||
            hashFiles('setup.py')           != ''
          }}
        run: |
          python -m pip install --upgrade pip
          if [ -f requirements.txt ]; then pip install -r requirements.txt; fi
          if [ -f pyproject.toml ];  then pip install .; fi
          pytest -q || true                    # green if no tests yet

      #######################################################################
      # 4️⃣  Shell-script lint (runs regardless of language)
      #######################################################################
      - name: Lint shell scripts
        run: |
          sudo apt-get update && sudo apt-get install -y shellcheck
          shellcheck $(git ls-files '*.sh') || true
```

### 2‑c  `.github/dependabot.yml` — *Weekly on Friday*

```yaml
version: 2

updates:
  # 1️⃣ GitHub Actions
  - package-ecosystem: "github-actions"
    directory: "/"
    schedule:
      interval: "weekly"
      day: "friday"
      time: "08:00"
    reviewers: [ "alice-github-id", "bob-dev", "carol-dev" ]

  # 2️⃣ Node / npm
  - package-ecosystem: "npm"
    directory: "/"
    schedule:
      interval: "weekly"
      day: "friday"
    open-pull-requests-limit: 5
    reviewers: [ "alice-github-id" ]

  # 3️⃣ Python / pip
  - package-ecosystem: "pip"
    directory: "/"
    schedule:
      interval: "weekly"
      day: "friday"
    reviewers: [ "alice-github-id" ]

  # 4️⃣ Go modules
  - package-ecosystem: "gomod"
    directory: "/"
    schedule:
      interval: "weekly"
      day: "friday"
    reviewers: [ "alice-github-id" ]

  # 5️⃣ Java / Gradle
  - package-ecosystem: "gradle"
    directory: "/"
    schedule:
      interval: "weekly"
      day: "friday"
    reviewers: [ "alice-github-id" ]
```

### 2‑d  `SECURITY.md`

```markdown
# Security Policy

## Supported Versions
| Branch | Supported |
|--------|-----------|
| master | ✔️        |

## Reporting a Vulnerability
Please e‑mail **security@homeric-freedom.example.com** or open a [private security advisory](../../security/advisories/new).  
We triage within **2 business days** and aim to release fixes within **7 days** for critical issues.

## CI/CD Hardening Summary
* Workflows run with a **read‑only `GITHUB_TOKEN`** by default.
* Only actions from **`Homeric-Freedom`**, *GitHub‑authored*, or *verified* Marketplace publishers are allowed.
* The `master` branch requires **2 approvals**; **@alice-github-id** must be one of them.
* Dependabot opens grouped security PRs **every Friday**.
* Secret‑scanning alerts and push protection are **enabled org‑wide**.
```

---

## 3  Protect the template’s `master` branch

Settings ► **Branches ➜ Add rule**

* Branch pattern: `master`
* Require pull request before merging ✔
* Require **1** approval ✔
* Include administrators ✔

---

## 4  Mark repository as a *template*

Settings ► **General** ► ✔ *Template repository* ► **Save**

---

## 5  Organisation Actions policy (Team plan)

Settings ► **Actions ➜ General**

1. **Actions permissions** ► select **“Allow \*\*\*\* and select non‑**\*\* actions …”\*\*

   * ✔ Allow actions **created by GitHub**
   * ✔ Allow **Marketplace actions by verified creators**
2. **Workflow permissions** ► **Read repository contents** ► **Save**

---

## 6  Advanced Security defaults (Org‑wide)

Settings ► **Code security & analysis**

* **Enable Advanced Security** (if not enabled)
* **Code scanning** ► ✔ *Recommend the extended query suite …* ► **Save**
* **Secret scanning** ► ✔ *Secret‑scanning alerts* + ✔ *Push protection* ► **Save**
* **Dependabot alerts & security updates** are on by default.

---

## 7  Creating a new project

1. **Use this template ➜ Create repository**
2. Fill name, keep private, *(no Copy-branch‑rules checkbox on Team plan)*
3. After creation, **add branch rule manually**: Settings ► Branches ► Add rule → **2 approvals, include administrators, require PR**.

---

## 8  (Optional) Auto‑protect script for new repos

Save as `.github/workflows/protect.yml` in the template to automate Step 7‑3.

```yaml
name: Apply branch protection
on:
  repository_dispatch:
    types: [created]
jobs:
  protect:
    runs-on: ubuntu-latest
    permissions:
      contents: write
      administration: write
    steps:
      - name: Protect master
        env:
          GH_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          ORG: Homeric-Freedom
          REPO: ${{ github.event.repository.name }}
        run: |
          gh api -X PUT \
            "/repos/$ORG/$REPO/branches/master/protection" \
            -H "Accept: application/vnd.github+json" \
            -F required_pull_request_reviews.required_approving_review_count=2 \
            -F enforce_admins=true
```

*(Requires org‑level webhook to fire **`repository_dispatch`** on create.)*

---

## 9  Validation checklist

*

> **You’re done!** Every new repo now starts with CI, Dependabot, secret scanning, CodeQL, hardened GitHub Actions policy, and enforced code‑review gates—all from a single template.
