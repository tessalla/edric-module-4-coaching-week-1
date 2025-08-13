# Coaching for DevOps - Week 1

## Intro to DevOps & Branching Strategy

### Agenda

- Recap: Introduction to DevOps
- Case Study: Crowdstrike
- Demo: GitHub MCP Server
- Recap: Git Branching Strategies
- Exercise: Protect your branch!

---

## Introduction to DevOps

### What is DevOps?

> DevOps is the combination of cultural philosophies, practices, and tools that increases an organization’s ability to deliver applications and services at high velocity.

<img width="1173" height="731" alt="image" src="https://github.com/user-attachments/assets/ddef6765-62f6-4c33-8ed1-43032a4571e1" />

### Stages of DevOps

| Stage        | Description                                         | Common Tools                            |
| ------------ | --------------------------------------------------- | --------------------------------------- |
| **Planning** | Define goals, requirements, and roadmap.            | Jira, Trello, Azure Boards              |
| **Coding**   | Write application code and configuration files.     | VS Code, IntelliJ IDEA, Git             |
| **Build**    | Compile and package the application for deployment. | Maven, Gradle, npm, Webpack             |
| **Test**     | Validate functionality, performance, and security.  | JUnit, Selenium, Cypress, Postman       |
| **Release**  | Approve and prepare a version for deployment.       | GitHub Actions, Jenkins, GitLab CI/CD   |
| **Deploy**   | Push the application to target environments.        | ArgoCD, Spinnaker, AWS CodeDeploy       |
| **Operate**  | Run and maintain the application in production.     | Kubernetes, Docker, AWS ECS, Azure AKS  |
| **Monitor**  | Track performance, uptime, and issues.              | Prometheus, Grafana, Datadog, New Relic |

### Benefits of DevOps

- **Rapid Delivery:** More frequent releases and faster time-to-market.
- **Reliability:** Stable environments through integration testing and continuous monitoring.
- **Scale:** Efficient infrastructure and development process management.
- **Improved Collaboration:** Code review as part of CI/CD workflow.
- **Security:** Integrates security throughout the lifecycle (DevSecOps).

---

## Case Study: CrowdStrike Incident - The Largest IT Outage in History

### What Happened
On July 19, 2024, CrowdStrike released a faulty configuration update (Channel File 291) that caused widespread crashes of Windows systems running their Falcon security software, resulting in the largest IT outage in history.

### Timeline of Events

**July 19, 2024:**
- **04:09 UTC** - CrowdStrike released problematic sensor configuration update
- **05:27 UTC** - CrowdStrike identified issue and reverted changes (too late)
- **06:48 UTC** - Azure and Google Cloud platforms reported widespread system crashes

**Recovery Period:**
- **July 19-22** - Manual remediation required (deleting faulty .sys files)
- **July 29** - 99% of affected systems back online

### Impact Scale
- **8.5 million devices** affected globally
- **5,078 flights** canceled (4.6% of scheduled flights)
- **$5+ billion** in estimated losses
- **$1.5 billion** in insurance payouts
- Disrupted airlines, healthcare, financial services, and critical infrastructure

### Technical Details
- **Affected Systems:** Windows 10/11 running CrowdStrike Falcon software
- **Unaffected:** macOS and Linux systems
- **Cause:** Logic error in configuration file → Out-of-bounds memory read due to mismatch in expected vs actual input fields (21 fields provided vs 20 expected)

### Aftermath and Response

**Company Response:**
- **July 24, 2024** - CrowdStrike published Post-Incident Review
- **August 6, 2024** - Published Root Cause Analysis with mitigation steps

**Legal Consequences:**
- **October 2024** - Delta Air Lines filed $500 million lawsuit alleging gross negligence and breach of contract

**Industry Impact:**
- Called the "largest IT outage in history" by cybersecurity experts
- Highlighted risks of single-vendor dependency in critical infrastructure
- Prompted industry-wide discussions about software testing and deployment practices

### Root Cause

1. **Input Mismatch:** Validator expected 20 fields; update provided 21.
2. **Testing Gaps:** Unit tests covered only happy paths; manual tests lacked invalid input coverage.
3. **Lack of Staggered Rollouts:** Deployed globally without phased rollout.
4. **Kernel-Level Risks:** Kernel-mode errors directly impacted system stability.

### Improvements by DevOps Stage

| Stage        | Improvement Suggestions                                                                                                             |
| ------------ | ----------------------------------------------------------------------------------------------------------------------------------- |
| **Planning** | Include rollback and phased rollout strategy in change management. Perform detailed risk assessments for kernel-level changes.      |
| **Coding**   | Apply stricter input validation and defensive coding. Conduct peer reviews focusing on configuration logic.                         |
| **Build**    | Automate static checks for configuration file integrity in the build pipeline.                                                      |
| **Test**     | Add edge case, invalid input, and backward compatibility testing. Include automated regression testing for kernel-level components. |
| **Release**  | Use gated releases with automated verification steps before approval.                                                               |
| **Deploy**   | Implement canary or blue-green deployments. First deploy to staging with production-like load testing.                              |
| **Operate**  | Introduce feature flags to quickly disable faulty updates. Maintain rapid rollback playbooks.                                       |
| **Monitor**  | Set up real-time monitoring for crash spikes post-deployment. Trigger automated rollback when thresholds are breached.              |

### Other Public Postmortem Reports for Learning

- [danluu/post-mortems](https://github.com/danluu/post-mortems)
- [snakescott/awesome-tech-postmortems](https://github.com/snakescott/awesome-tech-postmortems)
- [jimmyl02/awesome-postmortems](https://github.com/jimmyl02/awesome-postmortems)

---

## What is MCP?

The **Model Context Protocol (MCP)** is a protocol that enables development tools like IDEs and source control systems to interact with AI models in a structured way. It provides a standardized way to send and receive contextual information so the AI can provide better, context-aware responses.

### Key points:

- Acts as a bridge between development tools and AI.
- Allows passing project files, code, and metadata directly to the model.
- Helps AI provide more accurate and relevant suggestions.

#### MCP Interaction Flow (Mermaid Diagram)

```mermaid
sequenceDiagram
    participant DevTool as Developer Tool (IDE/GitHub)
    participant MCP as MCP Server
    participant AI as AI Model

    DevTool->>MCP: Send context (code, files, metadata)
    MCP->>AI: Forward structured context
    AI-->>MCP: Context-aware suggestions
    MCP-->>DevTool: Send results back to developer
```

---

## Class Activity: GitHub MCP Demo

Interact with the latest GitHub MCP server via chat and let AI do the magic.

---

## Git Branching Strategies

### Common Strategies

- **GitFlow**
- **Trunk-based**
- **GitHub Flow**

#### GitFlow

<img width="1225" height="792" alt="image" src="https://github.com/user-attachments/assets/67b1298f-20ce-4b4f-a0bc-faaeb3ed2ee6" />

#### GitHub Flow

<img width="1766" height="585" alt="image" src="https://github.com/user-attachments/assets/facf74e9-6410-4b22-b488-fd318ba13c93" />

#### Trunk-based Development

<img width="1449" height="768" alt="image" src="https://github.com/user-attachments/assets/97ac90a2-1ca6-4022-95d0-ec0b15f5e9ce" />
<img width="1424" height="746" alt="image" src="https://github.com/user-attachments/assets/e7b9ac97-9a65-4d18-af7d-3c9f5b85b9ad" />

---

## GitHub Demo: Best Practices

1. Branch protection
2. Code review
3. Status checks
4. Resolve merge conflicts

**Activity:** Setup branch protection rules yourself!

---

## Docker Installation

### Installation Options

- **Docker Desktop:** [docker.com/products/docker-desktop](https://www.docker.com/products/docker-desktop/)
- **Windows (Chocolatey):**

  ```sh
  choco install docker-desktop
  ```

- **Mac (Homebrew):**

  ```sh
  brew install --cask docker
  ```

---

## Activity: Advanced Git Commands

### Git Commands Cheat Sheet

| Command        | Description                                       |
| -------------- | ------------------------------------------------- |
| `git log`      | Show commit logs                                  |
| `git diff`     | Show changes between commits                      |
| `git pull`     | Fetch and integrate with local branch             |
| `git remote`   | Manage remote URLs                                |
| `git branch`   | List/create branches                              |
| `git checkout` | Switch branches                                   |
| `git merge`    | Merge changes between branches                    |
| `git stash`    | Temporarily remove changes                        |
| `git rebase`   | Reapply commits on top of another base tip        |
| `git reset`    | Reset current branch to a specific state          |
| `git revert`   | Create a new commit to reverse changes            |
