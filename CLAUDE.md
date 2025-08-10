# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is the **docs-forticnapp-code-security** repository, part of the larger 40docs platform ecosystem. It contains comprehensive hands-on lab documentation for **Lacework FortiCNAPP Code Security**, focusing on Software Composition Analysis (SCA), Infrastructure as Code (IaC) scanning, Static Application Security Testing (SAST), and OPAL engine capabilities.

### Repository Structure

The repository contains educational materials structured for MkDocs deployment:

- **`index.md`**: Main landing page with CSS styling
- **`hands-on-labs/`**: Interactive learning materials covering:
  - Prerequisites and setup (`00-prerequisites.md`)
  - Software Composition Analysis (`01-sca.md`) 
  - Infrastructure as Code scanning (`02-iac.md`)
  - Static Application Security Testing (`03-sast.md`)
  - OPAL engine integration (`04-opal.md`)
- **`hands-on-labs/images/`**: Screenshots and diagrams for lab documentation
- **CSS files**: Styling for the documentation interface

### Content Focus

This documentation covers security-focused development practices including:

- **SCA**: Vulnerability scanning of open-source dependencies, SBOM generation, license compliance
- **SAST**: Static code analysis for security vulnerabilities
- **IaC**: Infrastructure as Code security scanning (Terraform, CloudFormation)
- **SmartFix**: Intelligent vulnerability remediation recommendations
- **Integration**: CLI, IDE (VS Code), and SCM (GitHub/GitLab/Bitbucket) workflows

## Common Development Commands

### Content Development
```bash
# No build commands needed - content is deployed via GitOps to MkDocs
# This repository contains Markdown files structured for MkDocs consumption

# Local MkDocs development (when MkDocs is configured)
mkdocs serve                     # Start local development server
mkdocs build                     # Build static site

# Content validation (from parent 40docs repository)
npm run lint                     # Check markdown files
npm run lint:fix                 # Auto-fix markdown issues
```

### Lacework CLI Commands (for testing documentation)
```bash
# CLI installation and configuration
curl https://raw.githubusercontent.com/lacework/go-sdk/main/cli/install.sh | sudo bash
lacework configure              # Interactive configuration
lacework configure -j /path/to/key.json  # Configure with API key file

# Install required components
lacework component install iac  # Infrastructure as Code scanning
lacework component install sca  # Software Composition Analysis

# Core scanning commands
lacework sca scan ./            # Software Composition Analysis scan
lacework sca scan ./ -o results.json  # Save results to file
lacework sca sbom results.json  # Extract SBOM from scan results
lacework iac scan ./            # Infrastructure as Code scan
```

### GitHub Integration Testing
```bash
# Commands for testing GitHub integration workflows
gh repo create lab_forticnapp_code_security --template 40docs/lab_forticnapp_code_security --public
cd lab_forticnapp_code_security

# Trigger SmartFix demonstration via PR
echo "paramiko==2.4.1" >> app/requirements.txt
git checkout -b trigger-smartfix
git add app/requirements.txt
git commit -m "Add vulnerable dep to trigger SmartFix"
git push -u origin trigger-smartfix
gh pr create --fill
```

## Documentation Architecture

### MkDocs Integration
- Content uses front-matter YAML for MkDocs configuration
- Material Design CSS classes for card layouts and responsive design
- Admonition blocks (tip, warning, danger, note) for callouts
- Code tabs and collapsible sections for better UX

### Supported Platforms and Languages
The documentation covers FortiCNAPP support for:

**Languages**: C/C++, .NET, Go, Java, Node.js, PHP, Python, Ruby, Rust
**Package Managers**: NPM, Yarn, Maven, Gradle, Pip, Composer, Cargo, etc.
**IDEs**: VS Code extension with real-time scanning
**SCM**: GitHub, GitLab, Bitbucket integrations
**CI/CD**: GitHub Actions, GitLab CI, Azure DevOps, Jenkins

### Content Guidelines

When editing documentation:

- **Security Focus**: All examples should demonstrate defensive security practices
- **Accuracy**: CLI commands and configuration examples must be current and tested
- **Accessibility**: Use proper heading hierarchy and alt text for images
- **Screenshots**: Include relevant UI screenshots in `/hands-on-labs/images/`
- **Code Examples**: Provide working examples that can be copy-pasted
- **Cross-References**: Link between related lab sections appropriately

### Lab Structure Pattern
Each hands-on lab follows this structure:
1. Overview and learning objectives
2. Supported platforms/technologies matrix
3. Configuration and setup instructions
4. Step-by-step hands-on exercises
5. Integration examples (CLI, IDE, SCM)
6. Best practices and troubleshooting

## Integration with 40docs Platform

### Parent Repository Context
This repository is a Git submodule within the larger 40docs platform. Changes here are automatically deployed through:

- **GitOps**: Flux v2 automated deployment
- **MkDocs Builder**: Container builds with theme inheritance
- **Azure Kubernetes**: Production deployment to AKS cluster

### Orchestrator Integration
When working within the 40docs orchestrator system:
- This repository gets its own tmux window and Claude sub-instance
- Content changes trigger automatic MkDocs rebuilds
- All documentation validates against markdown linting rules
- Changes deploy automatically via the GitOps pipeline

## Important Notes

- **No Build Required**: This is a content-only repository - MkDocs building happens in the deployment pipeline
- **Image Management**: Screenshots and diagrams go in `hands-on-labs/images/` directory
- **Consistency**: Follow existing admonition and formatting patterns
- **Security Content**: Focus on defensive security practices and vulnerability remediation
- **Testing**: Validate all CLI commands and configurations before documenting