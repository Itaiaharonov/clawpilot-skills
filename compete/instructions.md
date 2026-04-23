---
name: "compete"
description: "Deep technical cybersecurity competitive analysis — compare Microsoft Security vs any named vendor with internal compete portal intelligence, referenced feature-to-feature tables, pricing with confidence levels (✅/🟡/🔴), roadmap comparison, and multi-format deliverables (tables, diagrams, presentations, documents)."
---


# /compete — Cybersecurity Competitive Analysis Skill

## Purpose
Produce a thorough, technically deep competitive analysis comparing **Microsoft Security** capabilities against a named competitor/vendor in the cybersecurity space. Every claim must be referenced with a source link for credibility verification.

## Trigger
The user will say something like "/compete [Vendor Name]" or "/compete CrowdStrike" or "compare Microsoft vs Palo Alto in security". Extract the competitor name and begin the workflow.

## Workflow

### Phase 1: Gather Intelligence (parallel where possible)

**1a. Internal Microsoft Intelligence**

**Step 1 — Internal Compete Portals (browser automation)**
Navigate to these internal Microsoft compete portals using `playwright-browser_navigate` and extract relevant battle cards, competitive briefs, and positioning guidance for the specific competitor:

| Portal | URL | What to Extract |
|---|---|---|
| **Security Compete Hub** | `https://aka.ms/securitycompete` | Battle cards, competitive briefs, win/loss analysis for [competitor] |
| **MCAPS Compete Resources** | `https://aka.ms/mcapscompete` | Sales plays, objection handling, customer-facing compete decks |
| **Security Sales Playbook** | `https://aka.ms/securityplaybook` | Positioning guidance, technical differentiators, demo scripts |
| **M365 Compete Center** | `https://microsoft.sharepoint.com/teams/M365Compete` | M365 Security competitive analysis, E5 positioning vs competitors |
| **Defender for Cloud Compete** | `https://aka.ms/defendercompete` | Cloud security / CNAPP competitive positioning |
| **Sentinel Compete** | `https://aka.ms/sentinelcompete` | SIEM/SOAR competitive positioning |
| **Gartner Access (MS Internal)** | `https://aka.ms/gartneraccess` | Gartner Magic Quadrant, Critical Capabilities, Market Guide references |
| **Forrester Access (MS Internal)** | `https://aka.ms/forresteraccess` | Forrester Wave reports relevant to security domains |

For each portal:
1. Navigate to the URL
2. Search for the specific competitor name
3. Extract key findings: competitive strengths, weaknesses, recommended positioning, win themes
4. Note the publication date — flag anything older than 6 months as potentially stale
5. If a portal URL fails or redirects, skip it silently and move on

> ⚠️ **Note:** Some aka.ms links may redirect or require specific permissions. If a portal is inaccessible, log it and continue with other sources. Never block the entire workflow on a single portal failure.

**Step 2 — User's M365 Data**
- Search the user's M365 data (emails, Teams chats, meetings, OneDrive/SharePoint files) for any prior competitive intelligence, battle cards, or internal discussions about this competitor:
  - Use WorkIQ: `workiq.cmd ask -q "competitive analysis [competitor] cybersecurity"` and `workiq.cmd ask -q "[competitor] battle card security"`
  - Search emails: `m365_search_emails` for emails mentioning the competitor name
  - Search files: `m365_search_files` for documents mentioning the competitor
  - Search Teams: `m365_search_chats` for Teams discussions about this competitor
- Check if there's a customer engagement repo with any prior compete materials in ~/customer-engagements/

**1b. Public Web Intelligence on Competitor**
- Use `web_fetch` to research the competitor's official website, product pages, and documentation:
  - Product feature pages and capability matrices
  - Official documentation and technical architecture
  - Pricing pages (if public)
  - Recent press releases and product announcements
  - Public roadmap or changelog/release notes
  - Technical blog posts and whitepapers
  - Industry analyst reports (Gartner, Forrester, IDC) mentioning this vendor
  - Public technical workshops, webinars, or conference presentations
  
**1c. Microsoft Security Current Capabilities**
- Use `web_fetch` to get the latest from:
  - Microsoft Security product pages (learn.microsoft.com, microsoft.com/security)
  - Microsoft Defender, Sentinel, Entra, Purview, Intune documentation
  - Microsoft Security blog and announcements
  - Microsoft Ignite / Build session recordings and announcements
  - Microsoft Security roadmap (Microsoft 365 roadmap page)

### Phase 2: Identify Comparison Categories

Based on the competitor's product portfolio, identify the relevant cybersecurity domains to compare. Common categories include (adapt based on the specific competitor):

1. **Endpoint Security** (EDR/XDR) — Microsoft Defender for Endpoint vs competitor
2. **SIEM / Security Analytics** — Microsoft Sentinel vs competitor
3. **Identity & Access Management** — Microsoft Entra ID vs competitor
4. **Cloud Security / CSPM / CWPP** — Microsoft Defender for Cloud vs competitor
5. **Email & Collaboration Security** — Microsoft Defender for Office 365 vs competitor
6. **Network Security / SASE / SSE** — Microsoft Entra Internet/Private Access vs competitor
7. **Data Security / DLP** — Microsoft Purview vs competitor
8. **Threat Intelligence** — Microsoft Threat Intelligence vs competitor
9. **Security Operations / SOAR** — Microsoft Sentinel + Copilot for Security vs competitor
10. **IoT/OT Security** — Microsoft Defender for IoT vs competitor
11. **Vulnerability Management** — Microsoft Defender Vulnerability Management vs competitor
12. **Integration & Ecosystem** — API, marketplace, third-party integrations
13. **Roadmap & Innovation** — Announced features, investment direction

**MANDATORY categories (always include regardless of competitor):**

14. **🤖 Security for AI** (see Phase 3b below) — ALWAYS include this as a dedicated deep-dive section
15. **💰 Pricing & Licensing Deep Dive** (see Phase 3c below) — ALWAYS include this as a detailed analysis
16. **🏗️ Architecture Diagrams** (see Phase 8 below) — ALWAYS generate per-vendor architecture diagrams

Only include categories 1–13 when relevant to both vendors. Categories 14–16 are ALWAYS required.

### Phase 3: Build the Feature Comparison Table

For EACH category, create a detailed feature-to-feature comparison table:

```
| Feature / Capability | Microsoft Security | [Competitor] | Advantage | Source (Microsoft) | Source (Competitor) |
|---|---|---|---|---|---|
| [Specific feature] | [What MS offers] | [What competitor offers] | MS ✅ / Competitor ✅ / Tie 🟰 | [URL] | [URL] |
```

**CRITICAL RULES for the table:**
- Every cell must have a reference link (Source column) to verify the claim
- Be technically precise — mention specific product names, SKUs, API capabilities
- Note GA vs Preview vs Announced for features
- Include quantitative data where available (detection rates, response times, coverage numbers)
- Be fair and objective — acknowledge where the competitor genuinely leads
- Flag any claims that could not be independently verified with ⚠️

### Phase 3b: 🤖 Security for AI — MANDATORY Deep Dive

This section is ALWAYS required, regardless of competitor. AI security is a critical differentiator and evolving rapidly. Cover ALL of the following sub-topics with a dedicated comparison table for each:

**3b-1. AI Security Posture Management (AI-SPM)**
- AI workload discovery and inventory (AI Bill of Materials / AI-BOM)
- AI model and pipeline misconfiguration detection
- AI-specific compliance frameworks (OWASP Top 10 for LLM, NIST AI RMF, EU AI Act)
- AI attack path analysis (attack paths to models, training data, inference endpoints)
- Shadow AI detection (unauthorized AI services and models)
- AI data security (training data classification and protection)

**3b-2. AI Threat Protection & Runtime Security**
- Real-time prompt injection detection and prevention
- Jailbreak detection and blocking
- Data leakage/exfiltration detection from AI models
- Data poisoning detection
- Model theft and intellectual property protection
- Rogue agent detection and malicious AI behavior monitoring
- Credential theft via AI interactions
- AI-specific MITRE ATT&CK mapping
- Token-level scanning (text, image, audio coverage)

**3b-3. AI Application Security (securing apps built with AI)**
- LLM application firewall capabilities
- AI gateway/proxy security features
- Responsible AI guardrails and content safety
- AI model access control and authentication
- API security for AI endpoints
- AI supply chain security (model provenance, dependency scanning)

**3b-4. AI-Powered Security Operations (AI assisting security teams)**
- AI copilot / assistant for security operations (investigation, hunting, response)
- Natural language query for security data
- AI-generated incident summaries and recommendations
- Automated threat hunting with AI
- AI-powered vulnerability prioritization
- AI-assisted compliance reporting

**3b-5. Multi-Cloud AI Security Coverage**
- Azure OpenAI / Azure AI services coverage
- AWS Bedrock / SageMaker coverage
- Google Vertex AI / Gemini coverage
- Open-source model coverage (Hugging Face, Ollama, vLLM, etc.)
- SaaS AI application coverage (ChatGPT, Copilot, Gemini, etc.)

For EACH sub-topic, produce a comparison table with:
```
| AI Security Feature | Microsoft | [Competitor] | Maturity (GA/Preview/Announced/None) | Advantage | MS Source | Competitor Source |
|---|---|---|---|---|---|---|
```

**Important AI Security Research Sources:**
- Microsoft: learn.microsoft.com/azure/defender-for-cloud/ai-threat-protection, learn.microsoft.com/azure/defender-for-cloud/ai-security-posture, learn.microsoft.com/copilot/security/, learn.microsoft.com/azure/ai-services/content-safety/
- Competitor: Search for their AI security product pages, blog posts about AI/LLM security features, and any Gartner/Forrester coverage of their AI security capabilities

### Phase 3c: 💰 Pricing & Licensing — MANDATORY Deep Dive

This section is ALWAYS required. Go beyond high-level summaries. Produce a detailed pricing analysis covering ALL of the following:

> ### ⚠️ Pricing Data Accuracy Disclaimer
> Every pricing table MUST include a **Data Confidence** column with one of:
> - ✅ **Verified** — pulled from official public pricing page with URL (e.g., azure.microsoft.com/pricing/)
> - 🟡 **Estimated** — derived from analyst reports, G2/Gartner reviews, or public customer testimonials. Source cited but numbers may be approximate or outdated.
> - 🔴 **Unverified** — competitor does not publish pricing ("contact sales"). Number is a rough industry estimate or unavailable.
>
> **At the end of every pricing section, include this notice:**
> ```
> 📌 Pricing Accuracy Notice: Microsoft pricing is sourced from official public pricing
> pages and is current as of [date]. Competitor pricing marked as 🟡 Estimated or
> 🔴 Unverified should NOT be used in customer-facing materials without independent
> verification. Always confirm competitor pricing through customer-provided quotes
> or official competitor documentation before presenting in a competitive scenario.
> ```

**3c-1. Licensing Model Comparison**
```
| Aspect | Microsoft | [Competitor] | Data Confidence | Source |
|---|---|---|---|---|
| Pricing model | Per-resource / per-seat / bundled | Per-workload / per-agent / custom | ✅/🟡/🔴 | [URLs] |
| Billing frequency | Monthly / annual / consumption-based | Annual commitment / monthly | ✅/🟡/🔴 | [URLs] |
| Free tier | What's included for free | What's included for free | ✅/🟡/🔴 | [URLs] |
| Trial period | Duration and scope | Duration and scope | ✅/🟡/🔴 | [URLs] |
| Minimum commitment | Any minimums | Any minimums | ✅/🟡/🔴 | [URLs] |
| Price transparency | Public pricing available? | Public pricing available? | ✅/🟡/🔴 | [URLs] |
```

**3c-2. SKU & Plan Breakdown**
For Microsoft, detail EACH relevant Defender plan's pricing:
- Foundational CSPM (free) vs Defender CSPM (paid) — per-resource pricing
- Defender for Servers Plan 1 vs Plan 2 — per-server/hour pricing
- Defender for Containers — per-vCore/hour pricing
- Defender for Storage — per-transaction + overage pricing
- Defender for Databases (SQL, Cosmos, OSS) — per-instance pricing
- Defender for Key Vault, App Service, Resource Manager, DNS, APIs — pricing
- Defender for AI Services — per-token pricing
- Microsoft Sentinel — per-GB ingestion pricing and commitment tiers

For the competitor, detail their plan tiers, modules, and per-unit pricing (where publicly available). If pricing is "contact sales only", state that clearly and provide estimated ranges from public sources (analyst reports, G2/Gartner peer reviews, customer testimonials).

**3c-3. E5/E3/A5 Bundling Analysis**
```
| Microsoft License Bundle | Security Capabilities INCLUDED | Estimated Value |
|---|---|---|
| M365 E5 | List all included security features | Approx. $/user/month value |
| M365 E5 Security add-on | What's included | Price |
| M365 E3 + Security add-ons | What requires add-ons | Price |
| EMS E5 | Identity + device management inclusions | Price |
| Azure commitment (MACC) | Any Defender for Cloud included benefits | Details |
```
Compare to the competitor: what does the customer get "for free" with existing licenses vs what requires a NEW purchase?

**3c-4. Total Cost of Ownership (TCO) Scenarios**
Build 3 representative TCO scenarios and compare total annual cost:

| Scenario | Description |
|---|---|
| **Small** | 500 VMs, 10 K8s clusters, 2 cloud providers, 50 databases |
| **Medium** | 2,000 VMs, 50 K8s clusters, 3 cloud providers, 200 databases, AI workloads |
| **Large** | 10,000 VMs, 200 K8s clusters, 3 cloud providers, 1,000 databases, extensive AI |

For each scenario, estimate:
- Microsoft total annual cost (itemized by plan) — mark each line item ✅ Verified
- Competitor total annual cost (if estimable) — mark each line item with appropriate confidence level
- Delta and % savings — **only present delta if both sides have ✅ or 🟡 confidence**
- What the customer gets with Microsoft that they DON'T get with the competitor (and vice versa)
- If competitor pricing is 🔴 Unverified, state: "TCO comparison not possible — competitor pricing requires a direct quote"

**3c-5. Hidden Costs & Considerations**
- Data ingestion costs (Sentinel log ingestion vs competitor SIEM needs)
- Agent deployment and management overhead
- Training and certification costs
- Professional services / implementation costs
- Integration costs (if competitor requires additional tools to match Microsoft's platform coverage)
- Vendor lock-in and switching costs

**Important Pricing Research Sources:**
- Microsoft: azure.microsoft.com/pricing/details/defender-for-cloud/, azure.microsoft.com/pricing/details/microsoft-sentinel/, microsoft.com/microsoft-365/enterprise/compare-office-365-plans
- Competitor: Their pricing page, G2 pricing data, Gartner peer insights, TrustRadius reviews mentioning pricing
- Use `web_fetch` to get current pricing from all sources

### Phase 4: Strengths & Weaknesses Summary

Create a balanced summary for each vendor:

**Microsoft Security Strengths:**
- List genuine technical advantages with references

**Microsoft Security Gaps/Weaknesses:**
- List areas where Microsoft trails, with references

**[Competitor] Strengths:**
- List genuine technical advantages with references

**[Competitor] Gaps/Weaknesses:**
- List areas where the competitor trails, with references

### Phase 5: Strategic Recommendations

Provide actionable recommendations for the user (as a Microsoft Security Specialist):
- **Key talking points** when positioning Microsoft against this competitor
- **Objection handling** — common competitor claims and how to counter them
- **Customer scenarios** where Microsoft wins vs where the competitor wins
- **Proof points** — case studies, benchmarks, third-party validations
- **Demo recommendations** — which Microsoft features to showcase
- **Questions to ask the customer** to steer the conversation toward Microsoft strengths

### Phase 6: Output Deliverables (Chat)

Present the FULL analysis in the chat with full markdown tables and formatting, including:
- All standard comparison categories (Phase 3)
- The Security for AI deep dive (Phase 3b)
- The Pricing & Licensing deep dive (Phase 3c)
- Strengths & Weaknesses (Phase 4)
- Strategic Recommendations (Phase 5)

### Phase 7: Additional Deliverables (ask user)

Ask the user which additional file deliverables they want:

1. **📊 Excel spreadsheet** (`/xlsx`) — Full feature comparison matrix with tabs per category, color-coded advantage column, all reference links as hyperlinks. Include a dedicated "AI Security" tab and a "Pricing & TCO" tab with formulas.
2. **📄 Word document** (`/docx`) — Professional compete report with executive summary, detailed comparison tables, AI security analysis, pricing deep dive, and strategic recommendations
3. **📑 PowerPoint deck** (`/pptx`) — Customer-facing or internal presentation with comparison slides, architecture diagrams, AI security positioning, and key differentiators
4. **🎨 Architecture diagrams** (`/excalidraw`) — Individual architecture diagrams for EACH vendor (see Phase 8)
5. **🗂️ All of the above** — Generate the complete package

Use the appropriate skill for each deliverable by invoking it.

### Phase 8: 🏗️ Architecture Diagrams — MANDATORY

This phase is ALWAYS executed, regardless of whether the user selects it in Phase 7. Architecture diagrams are a core deliverable of every compete analysis.

Generate **THREE separate Excalidraw diagrams** using the `/excalidraw` skill:

**Diagram 1: Microsoft Security Architecture**
- Show the complete Microsoft Security platform architecture
- Include ALL relevant products: Defender XDR portal (umbrella), Defender for Endpoint, Defender for Identity, Defender for Office 365, Defender for Cloud Apps, Defender for Cloud (CNAPP with CSPM/CWPP/DSPM/DevSecOps), Sentinel (SIEM/SOAR), Entra ID, Purview, Copilot for Security
- Show data flows between components (telemetry, alerts, incidents)
- Show cloud coverage (Azure native, AWS/GCP connectors, on-premises via Arc)
- Show AI security components (AI SPM, AI Threat Protection, Content Safety)
- Use Microsoft brand blue (#0078D4) color scheme
- File: `[competitor]-compete-ms-architecture.excalidraw`

**Diagram 2: [Competitor] Security Architecture**
- Show the competitor's complete security platform architecture
- Include ALL their product modules and how they interconnect
- Show their deployment model (agentless, agent-based, API-based)
- Show cloud coverage and multi-cloud support
- Show AI security components (if any)
- Highlight gaps (components they don't offer) with dashed red boxes
- Use the competitor's brand colors where known
- File: `[competitor]-compete-[competitor]-architecture.excalidraw`

**Diagram 3: Side-by-Side Comparison**
- Two columns: Microsoft (left) vs Competitor (right)
- Aligned rows for comparable capabilities
- Color-coded advantages (green = advantage, red = gap)
- Center column with "VS" and key differentiator callouts
- Bottom section with pricing/licensing comparison summary
- File: `[competitor]-compete-comparison-architecture.excalidraw`

For each diagram, also export a PNG version for easy sharing.

### Phase 9: Save to Customer Repo (if applicable)

If the user mentions a specific customer context, save the compete materials to the relevant customer engagement repo under a `compete/` subfolder.

## Important Guidelines

- **Be technically deep** — this is for a Security Specialist, not a generalist. Include API details, architecture nuances, deployment models, and integration specifics.
- **Be current** — always check for the latest announcements. The security landscape changes rapidly.
- **Be honest** — never fabricate advantages. If Microsoft is behind in an area, say so and mention if it's on the roadmap.
- **Reference everything** — every claim needs a verifiable source link. No unsubstantiated claims.
- **Think like a seller** — while being objective, frame the analysis to help the user position Microsoft effectively in competitive situations.
- **Consider the full stack** — Microsoft's advantage often comes from integration across the security portfolio (XDR + SIEM + Identity + Endpoint). Highlight platform value vs point solutions.
- **Check E5/E3 bundling** — Microsoft's licensing bundling is often a major competitive advantage. Always mention relevant licensing.
- **AI Security is a priority** — The Security for AI section (Phase 3b) must be thorough and technically deep. This is an increasingly critical differentiator in every competitive deal.
- **Pricing wins deals** — The Pricing deep dive (Phase 3c) must include concrete numbers where possible. TCO scenarios are especially valuable for customer conversations.
- **Pricing honesty is non-negotiable** — Always tag pricing data with a confidence level (✅ Verified / 🟡 Estimated / 🔴 Unverified). Never present estimated competitor pricing as fact. Include the Pricing Accuracy Notice disclaimer in every pricing section.
- **Internal portals first** — Always attempt to pull from Microsoft internal compete portals (Phase 1a) before relying solely on public web data. Internal battle cards often contain positioning guidance, win themes, and objection handling that public sources miss. If a portal is inaccessible, skip it and note it in the summary.
- **Architecture diagrams are mandatory** — Phase 8 always executes. Visuals are essential for customer-facing compete materials and internal understanding of platform differences.

