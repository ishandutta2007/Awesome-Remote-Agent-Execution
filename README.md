# Awesome-Remote-Agent-Execution

# Top Remote Agent Execution Tools Ecosystem

**Curated List of SaaS Products & Open-Source GitHub Projects**  
*Focused on Agent-Driven Remote Execution, MCP Integration & SSH-Native Automation*  
**Last updated: March 2026**

This repository tracks notable **SaaS platforms** and **open-source projects** for **Remote Agent Execution**. These tools enable AI agents and orchestration systems to execute commands, manipulate files, and run tasks on remote machines — bridging the gap between local agent runtimes and distributed infrastructure, often through MCP (Model Context Protocol) servers or SSH-based transports.

**Examples** include Bifrost, tramp, assh, agent-runtime, AWS Systems Manager, Ansible, and Terraform Cloud (the category leaders).

**Open-source emphasis**: This section is heavily expanded with every major active project for self-hosting, MCP-native remote execution, and transparent agent workflows — ideal for platform engineers building AI-driven infrastructure automation, developers running agents across distributed machines, and teams avoiding vendor lock-in.

Contributions welcome! Open a PR to add/update entries. Keep descriptions factual and link to official sites.

## Table of Contents
- [SaaS/Hosted Platforms](#saas-hosted-platforms)
- [Open-Source GitHub Projects](#open-source-github-projects)
- [How to Contribute](#how-to-contribute)
- [Disclaimer](#disclaimer)

## SaaS/Hosted Platforms

- **[AWS Systems Manager](https://aws.amazon.com/systems-manager/)**  
  AWS-native remote execution and fleet management service. **Run Command** executes scripts across EC2 instances and on-premises servers without SSH, with **Session Manager** providing audit-logged shell access. Deep integration with IAM, CloudWatch, and AWS Config for compliance workflows.

- **[Azure Automation](https://azure.microsoft.com/en-us/products/automation/)**  
  Microsoft's cloud automation service with **Runbooks** for executing scripts on Azure VMs and hybrid workers. Supports PowerShell and Python runbooks with hybrid worker groups for on-premises execution.

- **[Google Cloud Deployment Manager](https://cloud.google.com/deployment-manager)**  
  GCP's infrastructure deployment service with template-based resource provisioning. Declarative configuration for creating and managing Google Cloud resources at scale.

- **[Terraform Cloud](https://www.hashicorp.com/products/terraform)**  
  HashiCorp's managed Terraform platform with **remote runs**, state management, policy enforcement (Sentinel/OPA), and private run environments. The reference managed TACO (Terraform Automation and Collaboration) platform.

- **[Spacelift](https://spacelift.io/)**  
  Infrastructure orchestration platform supporting **Terraform, OpenTofu, Pulumi, CloudFormation, Ansible, and Kubernetes**. **Private workers** execute runs inside your network while the control plane manages state, policies, and drift detection. Pricing by concurrent private workers [citation:21][citation:26].

- **[Ansible Automation Platform](https://www.redhat.com/en/technologies/management/ansible)**  
  Red Hat's enterprise Ansible platform with **Automation Controller** (formerly Tower), RBAC, workflow orchestration, and certified content collections. Agentless SSH-based execution.

- **[Puppet Enterprise](https://puppet.com/)**  
  Enterprise configuration management with agent-based desired-state enforcement, PuppetDB, and orchestration capabilities.

- **[Chef Automate](https://www.chef.io/)**  
  Enterprise Chef platform with compliance scanning, infrastructure visibility, and policy-as-code enforcement.

- **[SaltStack Enterprise](https://www.vmware.com/products/saltstack.html)**  
  Event-driven infrastructure automation with agent and agentless execution modes, targeting high-speed parallel command execution across large fleets.

- **[RunDeck (PagerDuty)](https://www.pagerduty.com/platform/automation/)**  
  Self-hosted job scheduler and runbook automation with **self-service access**, approval workflows, and audit logging. The open-source **RunDeck Community** remains available.

## Open-Source GitHub Projects

- **[Bifrost](https://github.com/maximhq/bifrost)**  
  **The MCP-native gateway with remote execution capabilities** — Go-based, Apache 2.0 licensed. **MCP client and server** connecting to external tool servers via STDIO, HTTP, or SSE with OAuth 2.0 authentication and automatic token refresh [citation:12]. **Agent Mode** enables autonomous tool execution with configurable auto-approval, while **Code Mode** lets AI write Python to orchestrate multiple tools in a sandbox, reducing token usage by 50%+ [citation:12]. **Remote execution** via SSH or Docker targets with a `bifrost-remote` skill for connecting to other machines using pair codes or SSH keys [citation:23]. **Security note**: Bifrost HTTP transport versions before 2.1.0 had an **unauthenticated RCE vulnerability (CVE-2026-90898, CVSS 9.8)** via stdio MCP client registration — upgrade to 2.1.0+ and enable `governance.auth_config.is_enabled` [citation:38]. **Best for AI agents needing to execute tools on remote machines** with full MCP ecosystem compatibility.

- **[tramp](https://github.com/marcfargas/tramp)**  
  **TRAMP-like transparent remote execution for AI coding agents** — MCP server that routes file and shell operations to remote targets via **SSH or Docker** [citation:3]. **"The agent stays local. Tools execute remotely."** Mirrors Claude Code's built-in tool signatures: `bash`, `read`, `write`, `edit`, `glob`, `grep`, `ls` [citation:3]. **Target management**: `target_add` for SSH or Docker targets, `target_switch` to change active target, with persistent connection reused across tool calls [citation:3]. **SSH transport** uses native multiplexed channels and SFTP for file I/O, with host key verification via `~/.ssh/known_hosts` [citation:3]. **Port forwarding** support for SSH targets [citation:3]. **Best for Claude Code and MCP-compatible agents** needing transparent remote execution without leaving the local agent context.

- **[assh](https://github.com/marcfargas/assh)** (assh-toolkit)  
  **Agentic SSH toolkit for stateful, token-efficient remote execution** — Python package and CLI [citation:8][citation:20]. **Persisted remote working directory state** across commands via `assh chain` [citation:20]. **Env sets with automatic redaction** for secrets in remote commands [citation:20]. **Remote worker deployment** for long-running task lifecycle management with `assh task start`, `assh task list`, and `assh task logs` [citation:20]. **Push and fetch helpers** for file transfer with sha256 verification [citation:8]. **Docker and Kubernetes helpers** included [citation:8]. **Best for Python-based agent workflows** needing stateful SSH execution with token efficiency.

- **[agent-runtime](https://pypi.org/project/devpilot-agent/)** (devpilot-agent)  
  **Lightweight agent runtime that turns any machine into an AI-agent-ready compute target** — zero dependencies, self-updating [citation:19]. **Async command server** with `POST /exec` returning a job ID and `GET /jobs/{id}` for polling results [citation:19]. **WebSocket terminal** with ConPTY support (xterm.js compatible) [citation:19]. **ACP client** for structured Agent Client Protocol communication with any ACP-compatible agent [citation:19]. **Self-updating** via `POST /update` triggers graceful upgrade [citation:19]. **API key auth** auto-generated and persisted across restarts [citation:19]. **Best for turning VMs and cloud instances into agent-controllable targets** with minimal setup.

- **[Ansible](https://github.com/ansible/ansible)**  
  **Agentless IT automation platform** — GPL-3.0 licensed, **60,000+ GitHub stars**. **SSH-based execution** without agents on target machines. **Playbooks** in YAML for configuration management, application deployment, and orchestration. **Idempotent modules** ensure desired state. **The reference for fleet-scale configuration management** — as one tool notes, "fleet-scale configuration management (hundreds of machines, desired state, idempotent playbooks) → use Ansible" [citation:17]. **Best for multi-machine configuration management** where agents are undesirable.

- **[Terraform](https://github.com/hashicorp/terraform)**  
  **Infrastructure as Code standard** — HCL declarative configuration with 3,000+ providers. **Remote execution** via Terraform Cloud or self-hosted runners. **State management, plan/apply workflow, and policy enforcement** via Sentinel or OPA. **Best for provisioning and managing infrastructure** across clouds.

- **[Atlantis](https://github.com/runatlantis/atlantis)**  
  **Open-source Terraform pull request automation** — Apache 2.0 licensed. **The pioneer of the TACO (Terraform Automation and Collaboration) category**, triggering `terraform plan` and `apply` from PR comments [citation:26]. **Self-hosted with no license fee** — costs are engineering time to operate [citation:21]. **Best for teams wanting PR-driven Terraform workflows** without a vendor relationship.

- **[Terrakube](https://github.com/terrakube-io/terrakube)**  
  **Open-source Terraform automation and collaboration platform** — Apache 2.0 licensed. **Self-hosted alternative to Terraform Cloud** with remote runs, state management, and workspace organization. **Supports OpenTofu** as an engine per workspace [citation:21]. **Best for organizations wanting Terraform Cloud functionality on their own infrastructure**.

- **[CraftWeave](https://github.com/svc-design/CraftWeave)**  
  **Lightweight Ansible alternative for constrained environments** — Go control plane with **Rust agent** [citation:14][citation:35]. Designed for environments **without Python, pip, or package managers** — the agent is a single Rust binary [citation:14]. **`craftweave ansible`** provides Ansible-style CLI execution; **`craftweave playbook`** supports YAML multi-step orchestration [citation:14]. **`cw-agent run`** for one-shot execution, **`cw-agent daemon`** for persistent scheduling [citation:14]. **Best for edge devices, IoT hosts, and offline nodes** where Ansible cannot run [citation:14].

- **[kojo](https://github.com/loppo-llc/kojo)**  
  **Remotely operate AI coding CLIs from mobile** — Go-based single binary with embedded web UI [citation:29]. **tmux-backed sessions** (macOS/Linux) for crash resilience across kojo restarts [citation:29]. **Tailscale P2P** — no central server, encrypted with WireGuard [citation:29]. **Multi-device cluster** with peer mode joining additional machines [citation:29]. **Best for operating Claude Code, Codex, or Grok Build remotely** from a phone or tablet.

### Additional Strong Open-Source Options

- **rrun** — Stateless CLI plus agent skill for remote execution. Executes scripts on remote machines without exposing passwords to coding agents. Not for fleet-scale config management (use Ansible) [citation:17].
- **OpenAgentFleet** — Self-hosted platform for autonomous computer-use agents with disposable Linux desktops streaming live to the browser. `fleetctl` CLI for orchestration [citation:34].
- **CraftWeave** — Rust agent-based Ansible alternative for dependency-constrained environments [citation:35].
- **Puppet** — Agent-based configuration management with desired-state enforcement.
- **SaltStack** — Event-driven infrastructure automation with high-speed parallel execution.

**Frameworks for building custom systems**: Combine **Bifrost** for MCP-native tool execution with remote SSH/Docker targets, **tramp** for transparent remote file and shell operations from Claude Code, **assh** for stateful SSH workflows with token efficiency, **agent-runtime** for turning any VM into an agent-controllable target, and **Ansible** or **CraftWeave** for fleet-scale configuration management — to build a remote agent execution layer tailored to your agent framework, security requirements, and infrastructure constraints.

## How to Contribute

1. Fork the repo.
2. Add/edit entries in `README.md` (follow existing format).
3. Include: name, link, 1–2 sentence description, and whether it's SaaS or open-source.
4. Submit PR with a short explanation.

Star the repo if you find it useful!

## Disclaimer

- This is a **community-curated** list — not exhaustive and not an endorsement.
- Remote agent execution tools differ significantly in transport (SSH, MCP, WebSocket), security model, and scope. **Bifrost versions before 2.1.0 had a critical unauthenticated RCE vulnerability** via stdio MCP client registration — upgrade and enable authentication [citation:38]. **tramp exposes remote tools mirroring local tool signatures** — ensure agent context clearly distinguishes local from remote operations via the `tramp://context` resource [citation:3]. **Ansible is the reference for fleet-scale idempotent configuration** — rrun explicitly disclaims this use case [citation:17]. **CraftWeave targets environments where Ansible cannot run** due to Python/dependency constraints [citation:14]. **Agent-driven remote execution requires careful access control** — API keys, SSH keys, and MCP credentials must be scoped and rotated.
- Self-hosted open-source solutions require proper SSH key management, network segmentation, and audit logging for agent actions.

---

**Made for platform engineers, AI infrastructure teams, and developers building agent-driven automation systems.**
Let's make remote agent execution more open, secure, and agent-friendly.
