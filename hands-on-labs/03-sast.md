---
buttons:
  - title: Hands on Lab - Download
    icon: material-file-download-outline
    attributes:
      class: md-content__button md-icon
      href: ../hands-on-labs.pdf
      target: _blank
---

# 🔎 Static Application Security Testing (SAST)

Lacework FortiCNAPP’s **SAST engine** analyzes application source code to detect insecure coding patterns, logic flaws, and potential injection points—before they reach runtime.

---

## 🚀 What Is SAST?

SAST (Static Application Security Testing) reviews your code without executing it, scanning for:

* ❌ Hardcoded secrets and credentials
* ❌ Command and SQL injection
* ❌ Insecure crypto usage
* ❌ Deserialization vulnerabilities
* ❌ Dangerous APIs (e.g., `eval`, `os.system`)

!!! tip "Shift Security Left"
    Lacework SAST integrates directly into GitHub, CI/CD, and VS Code, helping developers fix issues where they code.

---

## ✅ Supported Languages

| Language   | File Types                   | Scan Modes     |
| ---------- | ---------------------------- | -------------- |
| Python     | `.py`                        | GitHub, VSCode |
| JavaScript | `.js`, `.jsx`, `.ts`, `.tsx` | GitHub, VSCode |
| Go         | `.go`                        | GitHub, VSCode |
| Java       | `.java`, `.kt`               | GitHub         |
| Shell/Bash | `.sh`                        | GitHub         |

!!! note
    Language support varies by integration. VS Code may support more granular detection than GitHub alone.

---

## 🔗 Integration Options

### SCMs

* ✅ GitHub (via OAuth App)
* ✅ GitLab (OAuth or Git integration)
* ✅ Bitbucket (via app)

### Dev Environments

* ✅ Visual Studio Code Extension
* ✅ Lacework CLI (SAST support in preview)

---

## 🧪 Hands-On: Run a SAST Demo with Python

This walkthrough demonstrates SAST findings using a vulnerable Python app.

---

### 🛠️ Step 1: Clone the Demo Repo

    ```bash
    git clone https://github.com/40docs/lab_forticnapp_code_security.git
    cd lab_forticnapp_code_security
    ```

---

### 🧑‍💻 Step 2: Open in VS Code

1. Launch **Visual Studio Code**
2. Open the project folder
3. Install the **Lacework Security** extension
4. Sign in with **OAuth**
5. Click the **shield icon** in the sidebar
6. Choose **Start SAST Scan**

!!! tip "Inline Results"
    Findings appear inline with red highlights. Hover to see explanations and **SmartFix** suggestions.

---

### 📌 Code Example (Python)

    ```python
    # app/vuln_app.py
    
    import os
    import sqlite3
    import random
    import hashlib
    import pickle
    
    # ❌ Command injection
    def list_files(user_input):
        os.system(f"ls {user_input}")
    
    # ❌ SQL Injection
    def get_user(username):
        conn = sqlite3.connect('example.db')
        cursor = conn.cursor()
        cursor.execute("SELECT * FROM users WHERE name = '%s'" % username)
        return cursor.fetchall()
    
    # ❌ Weak cryptography
    def hash_password(password):
        return hashlib.md5(password.encode()).hexdigest()
    
    if __name__ == "__main__":
        print("Token:", generate_token())
    ```

---

### 🔗 Step 3: Run a GitHub-Based Scan

1. Install the **Lacework FortiCNAPP GitHub App**
2. Push the repo to GitHub
3. Open a pull request
4. FortiCNAPP will automatically comment with SAST results

    ```bash
    git remote add origin https://github.com/40docs/lab_forticnapp_code_security.git
    git push -u origin main
    ```

!!! note "Trigger a Scan"
    Any commit or PR to the repo triggers a SAST scan automatically.

---

### ✅ Step 4: Apply Fixes

You’ll receive:

* ❌ Finding description
* 📄 Affected file + line
* 🧠 **SmartFix suggestion** (e.g., “Use parameterized query”)

Apply the fix manually or in VS Code with 1 click (if available).

---

## 🧠 SAST Coverage Areas

| Category            | Description                             |
| ------------------- | --------------------------------------- |
| Secrets Detection   | Hardcoded API keys, tokens, credentials |
| Injection           | SQLi, OS commands, path traversal       |
| Insecure Crypto     | MD5, SHA1, weak RNGs                    |
| Dangerous Functions | `eval()`, `pickle.loads()`, shell exec  |
| Access Control      | Exposure of privileged operations       |

---

## ✅ Best Practices

* ✅ Run SAST in PRs and local development
* ✅ Use branch protection + FortiCNAPP checks to block unsafe merges
* ✅ Adopt SmartFix to reduce triage time
