---
buttons:
  - title: Hands on Lab - Download
    icon: material-file-download-outline
    attributes:
      class: md-content__button md-icon
      href: ../hands-on-labs.pdf
      target: _blank
---

# 🏗️ Infrastructure-as-Code (IaC) Security

Lacework FortiCNAPP's **IaC Security** statically analyzes cloud infrastructure templates like Terraform, CloudFormation, Kubernetes, and Dockerfiles to detect misconfigurations before deployment.

---

## 🚀 Getting Started with IaC Security

To get started, connect the **Code Security App** to your Git provider.

!!! tip "Proactive IaC Security"
Integrating early in the SDLC lets you catch cloud misconfigurations before runtime—shifting security left.

---

## 🔗 GitHub Integration

### ✅ Prerequisites

* **Admin access** to all repositories you plan to monitor
* Authorized installation of the GitHub **Lacework IaC Security** App

!!! note
You can install the app directly via the [GitHub Marketplace](https://github.com/apps/iacbot).

---

### 🔐 Verifying Permissions

1. Go to GitHub → **Settings → Applications**
2. Under **Authorized OAuth Apps**, select **Lacework IaC Security**
3. Confirm the app has access to your GitHub organization
4. If not yet granted, click **Grant** next to your org
5. Sign out and back in to **Lacework FortiCNAPP**

---

### ⚙️ Configuring the GitHub Integration

1. Navigate to the **Lacework FortiCNAPP Console → IaC Security**
2. Select **GitHub** as your provider
3. Go to: [https://github.com/apps/iacbot](https://github.com/apps/iacbot)
4. Click **Configure**
5. Choose your GitHub **organization**
6. Select **All repositories** or pick specific ones
7. Review permissions and accept the **Terms of Service**

!!! success "You're Connected"
Once installed, Lacework begins scanning supported IaC templates in your repo automatically.

---

## 📚 Supported IaC Technologies

### 🧩 Supported Languages & File Types

| **Language / Tool** | Code Security App | CI/CD | CLI |
| ------------------- | ----------------- | ----- | --- |
| CloudFormation      | ✅                 | ✅     | ✅   |
| Dockerfiles         | ✅                 | ✅     | ✅   |
| Helm Charts         | ✅                 | ✅     | ✅   |
| Kustomize           | ✅                 | ✅     | ✅   |
| Terraform           | ✅                 | ✅     | ✅   |

!!! note
Support for Crossplane, Pulumi, Helmfile, and other formats may be added in future versions.

---

### 🌐 Supported Git Providers

| Git Provider        | Supported |
| ------------------- | --------- |
| Bitbucket           | ✅         |
| GitHub              | ✅         |
| GitLab              | ✅         |
| Azure DevOps        | ❌         |
| GitHub Enterprise   | ❌         |
| GitLab Self-Managed | ❌         |

---

### 🔧 Supported CI/CD Pipelines

!!! note "Beta Feature"
CI/CD support is in **beta** for select customers. Contact your Lacework representative for access.

| CI/CD Pipeline      | Supported |
| ------------------- | --------- |
| GitHub Actions      | ✅         |
| GitLab CI           | ✅         |
| Bitbucket Pipelines | ✅         |
| Jenkins             | ✅         |

---

### ⚙️ Supported Terraform Tools

| Terraform Tool       | Supported |
| -------------------- | --------- |
| Atlantis             | ✅         |
| Terraform Cloud      | ❌         |
| Terraform Enterprise | ❌         |
| Env0 / Spacelift     | ❌         |
| Terragrunt           | ✅         |

---

## 🧪 Hands-On

Follow this quick lab to trigger misconfig findings and see FortiCNAPP in action.

---

### 🛠️ Step 1: Clone the Lab Project

    ```bash
    git clone https://github.com/40docs/lab_forticnapp_code_security.git
    cd lab_forticnapp_code_security
    ```

This repo includes Terraform configs with real-world misconfigurations.

---

### 🔗 Step 2: Install the GitHub App

1. Go to [https://github.com/apps/iacbot](https://github.com/apps/iacbot)
2. Click **Configure**
3. Select your **organization**
4. Choose **All** or **specific repositories**
5. Accept the permissions and Terms of Service

!!! warning "Permissions Required"
    You need **admin** access to install and authorize the app for your organization.

---

### 🔍 Step 3: View IaC Scan Results

1. Open the **Lacework Console → Code Security → Repositories**
2. Click your repo to see:

   * ❌ Public S3 buckets
   * ❌ Subnets with public IPs
   * ✅ Inline file/line findings

!!! tip "Interactive Feedback"
    Click a finding to view exact source line, path, and fix recommendation.

---

### ✅ Step 4: Enforce Checks with Branch Protection

1. In your repo, go to **Settings → Branches**
2. Edit or create a rule for `main`
3. Enable:

   * ✅ Require pull request review
   * ✅ Require status checks to pass
4. Add the **Lacework Code Security** check (if available)

!!! info "Policy Enforcement"
    You can also create custom policies in Lacework to block merges based on critical misconfigurations.

---

### 🔧 Optional: Scan Locally with the CLI

If you have the Lacework CLI:

    ```bash
    lacework iac scan ./terraform --output iac-results.json
    ```

!!! note "Configure API Access First"
Run `lacework configure` before scanning to set up your account keys.

---

### 📌 Sample Violations

    ```hcl
    # terraform/resource_aws_s3_bucket.tf
    resource "aws_s3_bucket" "public_bucket" {
      bucket = "lab-iac-demo-bucket"
      acl    = "public-read"  # ❌
    }
    ```

    ```hcl
    # terraform/resource_aws_subnet.tf
    resource "aws_subnet" "public" {
      map_public_ip_on_launch = true  # ❌
    }
    ```

These trigger findings like:

* “S3 bucket should not be public”
* “Subnets should not assign public IPs by default”

---

## ✅ Best Practices

* ✅ Install the GitHub App to enable automated scans
* ✅ Use branch protection to enforce security gates
* ✅ Enable AutoFix to remediate issues with 1-click
* ✅ Run CLI scans locally to catch issues before pushing
