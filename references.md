# References for RAG Confidentiality Leakage Risk Research

This file consolidates the literature, public-sector guidance, security research, and incident-cost evidence used or referenced in `deep-research-report.md`.

The original report did not preserve all URLs inline, so the items below were re-linked to primary or near-primary sources where possible. Where the report’s wording, attribution, or numeric interpretation appears weak or ambiguous, notes are included.

---

## 1. RAG / Generative AI confidentiality and data-exfiltration risk

### A1. Amazon Q for Business — indirect prompt injection / data exfiltration PoC

**Johann Rehberger — “AWS Fixes Data Exfiltration Attack Angle in Amazon Q for Business”**

- Relevance: Demonstrates that indirect prompt injection and rendered Markdown links could create an exfiltration path in Amazon Q for Business.
- Why it matters for RAG: Retrieved or uploaded content can carry instructions that affect downstream LLM behavior.
- Evidence type: Security-research PoC.
- Link: https://embracethered.com/blog/posts/2024/aws-amazon-q-fixes-markdown-rendering-vulnerability/

---

### A2. Writer AI — cross-tenant isolation weakness

**Cloud Security Alliance — “WriteOut: Writer AI Cross-Tenant Takeover”**

- Relevance: Demonstrates a session-isolation / cross-tenant issue in Writer’s AI environment.
- Risk class: Cross-user / cross-tenant leakage.
- Important caveat: The direct relationship to a classical RAG pipeline is not always explicit, so this should not be presented as a confirmed “RAG incident.”
- Evidence type: Security research note / PoC.
- Link: https://labs.cloudsecurityalliance.org/research/csa-research-note-writeout-writer-ai-cross-tenant-takeover-2/

---

### A3. Microsoft 365 Copilot — prompt injection to data exfiltration

**Johann Rehberger — “Microsoft Copilot: From Prompt Injection to Exfiltration of Personal Information”**

- Relevance: Demonstrates a chain from malicious content, to prompt injection, to tool invocation and external data exfiltration.
- Why it matters for RAG: Enterprise assistants such as Microsoft 365 Copilot retrieve enterprise content and can combine it with tool use, creating a wider attack surface than simple chat.
- Evidence type: Security-research PoC.
- Link: https://embracethered.com/blog/posts/2024/m365-copilot-prompt-injection-tool-invocation-and-data-exfil-using-ascii-smuggling/

---

## 2. Academic and technical research on RAG-specific attack surfaces

### B1. PoisonedRAG

**“PoisonedRAG: Knowledge Corruption Attacks to Retrieval-Augmented Generation of Large Language Models”**

- Venue: USENIX Security 2025.
- Relevance: Shows that poisoning a RAG knowledge base with a small number of malicious documents can manipulate answers.
- Key result used in the report: approximately 90% attack success rate with five injected documents for target queries.
- Evidence type: Peer-reviewed academic research.
- USENIX page: https://www.usenix.org/conference/usenixsecurity25/presentation/zou-poisonedrag
- Paper PDF: https://www.usenix.org/system/files/usenixsecurity25-zou-poisonedrag.pdf

**Correction to the original report:**  
The report described the affiliation as “太原科技大学ら”. The USENIX author information should be used instead when citing the paper.

---

### B2. ConfusedPilot

**“ConfusedPilot: Confused Deputy Risks in RAG-based LLMs”**

- Relevance: Examines enterprise RAG systems and confused-deputy style risks, including malicious content influencing retrieval-driven responses and possible sensitive-data exposure.
- Evidence type: arXiv preprint / experimental research.
- Link: https://arxiv.org/abs/2408.04870

**Correction to the original report:**  
The report described this as a Carnegie Mellon work and gave it “strong / peer-reviewed” treatment. The version referenced here is an arXiv preprint and should be labeled accordingly unless a later peer-reviewed publication is separately cited.

---

## 3. Standards, frameworks, and public-sector guidance

### OWASP Top 10 for LLM / GenAI Applications

**OWASP Top 10 for Large Language Model Applications**

- Relevance: Treats prompt injection, sensitive-information disclosure, data/model poisoning, and vector/embedding weaknesses as major application-security risks.
- Useful items for a RAG security slide:
  - LLM01 Prompt Injection
  - LLM02 Sensitive Information Disclosure
  - LLM04 Data and Model Poisoning
  - LLM08 Vector and Embedding Weaknesses
- Main page: https://genai.owasp.org/llm-top-10/
- Prompt Injection: https://genai.owasp.org/llmrisk/llm01-prompt-injection/
- Sensitive Information Disclosure: https://genai.owasp.org/llmrisk/llm022025-sensitive-information-disclosure/

---

### MITRE ATLAS

**MITRE ATLAS**

- Relevance: Public framework for adversarial threats against AI systems.
- Useful for framing RAG security as an industry-recognized threat category rather than a purely academic concern.
- Current ATLAS content includes techniques related to:
  - RAG poisoning
  - LLM data leakage
  - malicious prompt / content injection
  - credential harvesting and abuse of AI-enabled workflows
- Link: https://atlas.mitre.org/

---

### NIST AI 600-1

**NIST AI 600-1 — Artificial Intelligence Risk Management Framework: Generative Artificial Intelligence Profile**

- Published: 2024.
- Relevance: Extends the NIST AI RMF to generative AI and addresses risks around privacy, information security, data governance, misuse, and system safety.
- NIST page: https://www.nist.gov/publications/artificial-intelligence-risk-management-framework-generative-artificial-intelligence
- PDF: https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.600-1.pdf

---

### Japan Personal Information Protection Commission

**個人情報保護委員会 — 「生成AIサービスの利用に関する注意喚起等について」**

- Published: 2023.
- Relevance: Official Japanese guidance on handling personal data when using generative AI services.
- Link: https://www.ppc.go.jp/news/press/2023/230602kouhou/

---

### AWS — securing RAG ingestion

**AWS Security Blog — “Securing the RAG ingestion pipeline: Filtering mechanisms”**

- Relevance: Explicitly discusses security risks in RAG ingestion, including malicious content, indirect prompt injection, and poisoning-style threats.
- Link: https://aws.amazon.com/blogs/security/securing-the-rag-ingestion-pipeline-filtering-mechanisms/

---

### AWS — data authorization for generative AI

**AWS Security Blog — data authorization mechanisms for generative AI applications**

- Relevance: Explains why authorization must be enforced before sensitive enterprise data is retrieved and passed into the model context.
- Useful risk class: Authorization / ACL failure.
- Link: https://aws.amazon.com/blogs/security/implement-effective-data-authorization-mechanisms-to-secure-your-data-used-in-generative-ai-applications/

---

### AWS — prompt injection protection

**AWS Security Blog — “Safeguard your generative AI workloads from prompt injections”**

- Relevance: Provides defense-in-depth recommendations such as access control, filtering, prompt hardening, monitoring, and security testing.
- Link: https://aws.amazon.com/blogs/security/safeguard-your-generative-ai-workloads-from-prompt-injections/

---

## 4. Data-breach cost and liability evidence

### IBM / Ponemon — Cost of a Data Breach Report

**IBM Cost of a Data Breach Report**

- Relevance: Provides an industry benchmark for average breach cost and breach lifecycle metrics.
- Main report page: https://www.ibm.com/reports/data-breach

**Caution:**  
The original report included several per-record figures such as “$300–500 per record globally” and “$1,000–2,000 per record in the US.” Those figures should not be reused unless separately verified from the specific IBM/Ponemon edition in which they appear. For external-facing material, incident-level metrics from the current IBM report are safer unless the exact per-record figure is traced to source.

---

### C1. Equifax

**FTC — Equifax Data Breach Settlement**

- Incident: 2017 Equifax breach.
- Impact: Approximately 147 million people.
- Financial consequence:
  - At least $575 million settlement
  - Potentially up to $700 million
- Link: https://www.ftc.gov/news-events/news/press-releases/2019/07/equifax-pay-575-million-part-settlement-ftc-cfpb-states-related-2017-data-breach

**Correction to the original report:**  
One later section of the report referred to “1,470万件”; the correct scale is approximately **1億4,700万人 (147 million)**.

---

### C2. Capital One — regulatory penalty

**Office of the Comptroller of the Currency (OCC) — $80 million civil money penalty**

- Incident: 2019 Capital One data breach.
- Financial consequence: $80 million regulatory penalty.
- Link: https://www.occ.gov/news-issuances/news-releases/2020/nr-occ-2020-101.html

---

### C2. Capital One — class-action settlement

**Capital One Data Breach Class Action Settlement**

- Financial consequence: $190 million settlement fund.
- Link: https://www.capitalonesettlement.com/

---

### C3. Facebook / Meta privacy enforcement

**FTC — $5 billion Facebook privacy settlement**

- Financial consequence: $5 billion civil penalty.
- Link: https://www.ftc.gov/news-events/news/press-releases/2019/07/ftc-imposes-5-billion-penalty-sweeping-new-privacy-restrictions-facebook

**Important interpretation note:**  
The original report presents the $5 billion figure next to the Cambridge Analytica episode. That can be misleading if read as “$5B directly for the 87 million-person Cambridge Analytica data exposure.” The FTC action addressed broader privacy practices and violations of a prior FTC order. It is better cited as **Facebook privacy enforcement: $5B**, not as a one-to-one damage calculation for the Cambridge Analytica population.

---

### C4. Marriott / Starwood

**UK Information Commissioner’s Office — Marriott International penalty notice**

- Incident: Starwood guest-record breach.
- Financial consequence: £18.4 million penalty.
- PDF: https://ico.org.uk/media2/migrated/2618524/marriott-international-inc-mpn-20201030.pdf

---

### C5. Comcast / Xfinity

**Comcast Data Breach Settlement**

- Incident: Xfinity / Comcast customer-data breach associated with the Citrix NetScaler vulnerability.
- Settlement fund: $117.5 million.
- Link: https://www.comcastbreachsettlement.com/

---

## 5. Recommended evidence structure for future slides

For explaining enterprise RAG risk, the evidence is strongest when separated into three layers:

### Layer 1 — Technical feasibility

Use:
- PoisonedRAG
- Microsoft 365 Copilot PoC
- Amazon Q PoC
- ConfusedPilot

Message:
> RAG-specific and RAG-adjacent attack paths are experimentally demonstrated, not merely hypothetical.

### Layer 2 — Industry / governance recognition

Use:
- OWASP Top 10 for LLM Applications
- MITRE ATLAS
- NIST AI 600-1
- Japan Personal Information Protection Commission
- AWS RAG security guidance

Message:
> Prompt injection, sensitive information disclosure, RAG poisoning, authorization failures, and vector/embedding weaknesses are recognized security categories in major security and governance frameworks.

### Layer 3 — Business impact if leakage materializes

Use:
- IBM Cost of a Data Breach
- Equifax
- Capital One
- Marriott
- Comcast
- FTC Facebook privacy enforcement

Message:
> RAG-specific compensation cases remain limited, but once the event becomes a conventional confidentiality or personal-data breach, the cost mechanisms are the same: regulatory fines, litigation, settlement, customer compensation, incident response, remediation, and reputational damage.

---

## 6. Source-quality notes for the original report

The following parts of `deep-research-report.md` should be treated with caution in future external use:

1. **RAG incidents vs PoCs**
   - Amazon Q and Microsoft 365 Copilot examples are security-research demonstrations, not confirmed large-scale production breaches.
   - Do not label PoCs as actual customer-loss incidents.

2. **Writer / WriteOut**
   - Strong example of cross-tenant isolation risk.
   - Direct RAG causality is not clearly established in the report.

3. **PoisonedRAG affiliation**
   - The affiliation in the report appears incorrect. Use the USENIX record.

4. **ConfusedPilot publication status**
   - Treat the referenced version as an arXiv preprint unless a peer-reviewed version is separately verified.

5. **Facebook $5B**
   - Use as an example of large-scale privacy enforcement, not as a direct loss-per-user benchmark for Cambridge Analytica.

6. **Per-record breach cost**
   - Do not reuse the original report’s per-record figures without re-verifying the specific source and report edition.

7. **Equifax affected population**
   - Approximately 147 million people, not 14.7 million.

---

## 7. Compact bibliography

- Rehberger, J. — Amazon Q prompt injection / exfiltration  
  https://embracethered.com/blog/posts/2024/aws-amazon-q-fixes-markdown-rendering-vulnerability/

- Cloud Security Alliance — WriteOut  
  https://labs.cloudsecurityalliance.org/research/csa-research-note-writeout-writer-ai-cross-tenant-takeover-2/

- Rehberger, J. — Microsoft 365 Copilot prompt injection / data exfiltration  
  https://embracethered.com/blog/posts/2024/m365-copilot-prompt-injection-tool-invocation-and-data-exfil-using-ascii-smuggling/

- PoisonedRAG — USENIX Security 2025  
  https://www.usenix.org/conference/usenixsecurity25/presentation/zou-poisonedrag

- PoisonedRAG PDF  
  https://www.usenix.org/system/files/usenixsecurity25-zou-poisonedrag.pdf

- ConfusedPilot  
  https://arxiv.org/abs/2408.04870

- OWASP Top 10 for LLM / GenAI  
  https://genai.owasp.org/llm-top-10/

- OWASP Prompt Injection  
  https://genai.owasp.org/llmrisk/llm01-prompt-injection/

- OWASP Sensitive Information Disclosure  
  https://genai.owasp.org/llmrisk/llm022025-sensitive-information-disclosure/

- MITRE ATLAS  
  https://atlas.mitre.org/

- NIST AI 600-1  
  https://www.nist.gov/publications/artificial-intelligence-risk-management-framework-generative-artificial-intelligence

- NIST AI 600-1 PDF  
  https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.600-1.pdf

- 個人情報保護委員会 — 生成AIサービスの利用に関する注意喚起等  
  https://www.ppc.go.jp/news/press/2023/230602kouhou/

- AWS — Securing the RAG ingestion pipeline  
  https://aws.amazon.com/blogs/security/securing-the-rag-ingestion-pipeline-filtering-mechanisms/

- AWS — Data authorization for generative AI applications  
  https://aws.amazon.com/blogs/security/implement-effective-data-authorization-mechanisms-to-secure-your-data-used-in-generative-ai-applications/

- AWS — Prompt injection defense  
  https://aws.amazon.com/blogs/security/safeguard-your-generative-ai-workloads-from-prompt-injections/

- IBM — Cost of a Data Breach Report  
  https://www.ibm.com/reports/data-breach

- FTC — Equifax settlement  
  https://www.ftc.gov/news-events/news/press-releases/2019/07/equifax-pay-575-million-part-settlement-ftc-cfpb-states-related-2017-data-breach

- OCC — Capital One $80M penalty  
  https://www.occ.gov/news-issuances/news-releases/2020/nr-occ-2020-101.html

- Capital One settlement  
  https://www.capitalonesettlement.com/

- FTC — Facebook $5B privacy settlement  
  https://www.ftc.gov/news-events/news/press-releases/2019/07/ftc-imposes-5-billion-penalty-sweeping-new-privacy-restrictions-facebook

- ICO — Marriott penalty notice  
  https://ico.org.uk/media2/migrated/2618524/marriott-international-inc-mpn-20201030.pdf

- Comcast breach settlement  
  https://www.comcastbreachsettlement.com/
