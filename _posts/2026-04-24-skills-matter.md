---
layout: post
title: "Skills Matter !"
date: '2026-04-24T10:00:00.000-08:00'
author: MaX
tags:
- MCP
- AI
- Enterprise
- Skills
- Architecture
- LLM
- Development
modified_time: '2026-04-24T10:00:00.000-08:00'
thumbnail: /img/in-post/skills_matter_25_april_2026.png
---

# Skills Matter! Beyond the Prompt: Scaling Enterprise Intelligence with MCP and Skill Servers
![MCP Skills Architecture](/img/in-post/skills_matter_25_april_2026.png)

# The Agentic Paradox: Why Your Enterprise AI Strategy is Failing at Scale

Every CIO and Enterprise Architect is currently racing toward the same finish line: a workforce of autonomous AI agents. We’ve seen the demos—agents that can code, agents that can file expense reports, agents that can analyze market trends. But as these tools move from individual laptops to the corporate backbone, we’ve hit a wall. 

The problem isn't the LLM’s intelligence; it’s the **governance of that intelligence.** 
### The "Wild West" of Prompting
Currently, most organizations are living in a state of "Prompt Spaghetti." Every department has its own set of system prompts, every developer has a different version of a "coding skill" on their local machine, and security teams are left in the dark about what logic is being sent to which model. This fragmented approach creates seven critical points of failure that threaten to derail the ROI of AI:

* **Standardization:** Without a central source of truth, two agents performing the same task will produce wildly different outcomes.
* **Control:** There is no "kill switch" or central versioning. If a workflow needs to change due to a new policy, you can’t manually update 5,000 local config files.
* **Automation:** Simple chatbots are reactive. True enterprise value requires proactive **Agentic Workflows** that can navigate complex, multi-step business logic.
* **Efficiency:** Context windows are expensive. Feeding an agent 20 pages of instructions for every single turn is a waste of compute and money.
* **Localization:** A global company cannot use a "one size fits all" prompt. A HR agent in Paris must behave differently than one in Singapore to remain legally compliant.
* **Security:** Traditional prompts are "leaky." If your business logic is inside the prompt, it’s visible to the user and the LLM provider.
* **IP Confidentiality:** Your proprietary "secret sauce"—the specific way you calculate risk or optimize a supply chain—cannot be stored in a plain-text markdown file.

### The Solution: The Model Context Protocol (MCP) and DOE
To solve these challenges, we need to stop thinking about AI as a "chat" and start thinking about it as an **Enterprise Capability.** By leveraging the **Model Context Protocol (MCP)** and organizing our workflows through the **DOE (Discovery, Orchestration, Execution)** framework, we can build a centralized "Skill Infrastructure." This architecture allows us to decouple the logic of *how* a business works from the tools that *execute* the work, providing a secure, governed, and scalable blueprint for the modern enterprise.

#### Orchestrating Enterprise Intelligence: The DOE Framework and Centralized MCP Skill Servers

As AI matures within the enterprise, we are witnessing a fundamental shift in design patterns. The industry is moving away from "monolithic prompts" toward **Modular Agentic Orchestration**. 

To scale these systems, Enterprise Architects are adopting the **DOE (Discovery, Orchestration, Execution) Framework**. By centering this framework around a **Centralized MCP Skill Server**, organizations can organize, secure, and automate complex workflows while guaranteeing absolute compliance and control.



## 1. The DOE Framework: A systematic Approach For Agentic Systems
I read a post in Linedin that immediately reasonated to me.

**DISCLAIMER**: *I only had access to the post, not to the entire framework. But I believe that the high level idea fits perfectly the purpose of this post. I wanted to include some reflection on it.*

The DOE framework breaks down the lifecycle of an agentic action into three distinct, governed phases. When skills are managed centrally, each phase becomes a checkpoint for security and policy.

### Phase 1: Discovery (The "What")
In the Discovery phase, the agent identifies which capabilities are available and relevant to the user’s request. 
* **Centralized Advantage:** Instead of an agent having a static list of tools, it queries the **Central Skill Server**. 
* **The Manifest:** The server returns a "Discovery Manifest" tailored to the user’s identity and location. The agent "discovers" only what it is authorized to see, preventing unauthorized access to sensitive corporate capabilities.

### Phase 2: Orchestration (The "How")
Once the tools are discovered, the Orchestration phase defines the logic, sequence, and constraints of the workflow.
* **Skill Injection:** The **MCP Gateway** fetches the specific `SKILL.md` file (the "Playbook") from the central server and injects it into the LLM’s context.
* **Governance:** This ensures that the agent's "reasoning" is not random. It follows corporate-approved SOPs (Standard Operating Procedures) for planning the task.

### Phase 3: Execution (The "Act")
The final phase is the actual performance of the task through interaction with data systems.
* **Tool Isolation:** Execution happens on dedicated **Tool Servers** (HR, ERP, CRM). 
* **Compliance:** Every execution step is logged at the Gateway, providing a full audit trail of what data was accessed and what changes were made.



## 2. Enterprise Architecture: The Hub-and-Spoke DOE Model
For the Enterprise Architect, the goal is to decouple the "Brain" (Logic/Skills) from the "Muscle" (Execution/Tools).
<div class="mermaid">
graph TD
    subgraph Clients["Agentic Clients"]
        A["Claude Code / CLI"]:::node
        B["OpenHands / Web"]:::node
    end

    Gateway["MCP GATEWAY
    (Auth, RBAC, Audit Logging)"]:::node

    subgraph LogicServer["CENTRAL SKILLS SERVER"]
        Skills["Global Skill Library.md
         instructions"]:::node
        Locals["Regional Overrides
        EU/US/APAC Policies"]:::node
    end

    subgraph ToolServers["ENTERPRISE TOOL SERVERS"]
        HR["HR Tool Server"]:::node
        ERP["Finance/ERP Server"]:::node
        CRM["Sales/CRM Server"]:::node
    end

    subgraph IP_Protection["PROPRIETARY ENGINE"]
        BlackBox["Encrypted Logic
        'The Secret Sauce'"]:::node
    end

    %% Flows
    Clients ==>|SSE / HTTP| Gateway
    Gateway -->|Fetch Instructions| LogicServer
    Gateway -->|Execute Actions| ToolServers
    ToolServers -.->|Call| BlackBox

    classDef node fill:#000000,stroke:#000000,color:#ffffff
</div>



## 3. How Agentic Tools (Claude Code) leverage the DOE
I have tried to envisage how Agentic Tools may impleent such approach.
Frameworks like **Claude Code**, **Codex**, and **OpenHands** are the primary beneficiaries of this architecture. They don't just "talk"; they act as the engine driving the DOE loop.

### A Practical Example
Imagine a developer asks Claude Code to "Prepare a production release for the German market."
1.  **Discovery:** Claude queries the Gateway. The Gateway recognizes the user is in the "Finance" group and returns a manifest including the `german-tax-compliance` skill.
2.  **Orchestration:** The Gateway injects the `RELEASE_PROTOCOL.md` into Claude. Claude now knows it MUST run a unit test, a security scan, and a regional compliance check in that specific order.
3.  **Execution:** Claude calls the `trigger_scan` tool on the Security Server and the `submit_ledger` tool on the ERP Server.



## 4. Securing the "Secret Sauce": IP Protection in Execution
In an enterprise, the "How" is often your most valuable asset. The DOE framework allows you to protect Intellectual Property (IP) by isolating it within the **Execution** phase.

### The "Black Box" Pattern
* **The Skill (Discovery/Orchestration):** Tells the LLM: *"To calculate risk, use the `get_risk_score` tool."*
* **The Tool (Execution):** The actual logic is a compiled binary (Go, Rust, C++) hosted on your secure server. 
* **Result:** The LLM acts as the orchestrator, but the proprietary "Secret Sauce" formula remains encrypted and hidden on your server, never exposed to the client-side context window.



## 5. Compliance and Control: The Gateway's Role
By managing skills centrally through the DOE framework, you achieve three critical corporate goals:

1.  **Consistency:** Every agent uses the same version of a skill. When you update the "Legal Review" skill on the server, every agent across the company is updated instantly.
2.  **Regional Compliance:** The Discovery phase automatically filters skills based on the user's region (e.g., applying GDPR constraints only to EU-based sessions).
3.  **Granular Audit:** Because every phase of the DOE loop passes through the Gateway, you have a perfect record: *"Agent X discovered Skill Y, orchestrated Plan Z, and executed Action A on the ERP system."*


## Conclusion: The Future of the Corporate AI Workforce
The future of AI in the enterprise isn't about finding the "best prompt." It’s about building a robust **Skill Infrastructure** based on the **DOE Framework**. By centralizing discovery, standardizing orchestration, and securing execution, you transform AI from a series of disconnected chatbots into a unified, governed, and highly intelligent workforce.


## Information Sources
* **Model Context Protocol (MCP) Documentation:** [modelcontextprotocol.io](https://modelcontextprotocol.io)
* **AgentSkills Standard:** [agentskills.io](https://agentskills.io)
* **The DOE Framework for AI Agents:** [Bob Mwathu on LinkedIn](https://www.linkedin.com/posts/bob-mwathu_theres-a-new-way-to-build-ai-agentic-systems-activity-7413147110675750912-cRU4/)
* **Claude Code Reference:** Anthropic’s guide to Tool-Calling and Skill implementation.

---
*This post originally appeared on **massimorofi.com**. If you're building a centralized AI orchestration layer, I'd love to hear your thoughts.*
