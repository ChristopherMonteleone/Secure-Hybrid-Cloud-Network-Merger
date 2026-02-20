# Secure Hybrid-Cloud Network Merger & Zero Trust Implementation

*This project was completed as part of the Master of Science in Cybersecurity and Information Assurance program at Western Governors University (WGU) for course D482: Secure Network Design.*

## 📖 Project Overview
This project simulates a high-level cybersecurity architectural engagement. As the lead cybersecurity professional for Company A, I was tasked with designing a secure, compliant network merger following the acquisition of Company B. The primary objective was to evaluate legacy network architectures, analyze third-party vulnerability scans, and propose a modernized hybrid-cloud network topology utilizing zero trust principles. The final design successfully integrated both infrastructures, achieved necessary redundancies, and adhered to a strict $50,000 first-year budget constraint.

## 🏢 The Challenge: Current State Architecture

### Company A (The Acquiring Entity)
* **Operations:** A global financial institution offering checking accounts, bank cards, and investment products.
* **Infrastructure Flaws:** Relied heavily on a flat, non-redundant network topology utilizing End-of-Life (EOL) equipment.
* **Security Posture:** An internal NIST SP 800-30 Rev 1 risk analysis revealed highly permissive firewall configurations (open ports 21-90, 3389) and severe access control violations, including all standard users possessing local administrative privileges.

### Company B (The Acquired Entity)
* **Operations:** A medical software provider that processes credit card payments.
* **Infrastructure Flaws:** Operated as a smaller entity lacking a dedicated internal cybersecurity presence, relying on third-party support and a highly fragmented environment.
* **Security Posture:** A CVSS-based vulnerability assessment revealed critical, exploitable risks, including Distributed Ruby (dRuby) Remote Code Execution vulnerabilities, internet-facing database admin interfaces, and a complete lack of enforced Multi-Factor Authentication (MFA).

---

## 📝 Assignment Responses & Technical Analysis

### A. Network Security and Infrastructure Problems
**Requirement:** *Describe two current network security problems and two current infrastructure problems for each company, based on business requirements given in the scenario.*

**Company A:**
* **Security Problem 1:** The firewall is overly permissive, leaving open ports 21-90 and 3389 exposed to potential exploitation. 
* **Security Problem 2:** All users currently possess local administrative privileges, which violates the principle of least privilege.
* **Infrastructure Problem 1:** The organization relies on End-of-Life (EOL) equipment. Specifically, the network utilizes outdated Windows 7 laptops.
* **Infrastructure Problem 2:** The current network topology lacks redundancy, as the environment relies on a single Cisco router and a single Fortinet firewall handling all traffic.

**Company B:**
* **Security Problem 1:** Multi-Factor Authentication (MFA) is not enforced across all users.
* **Security Problem 2:** Critical database management interfaces are exposed, specifically the PostgreSQL administrator interface being directly reachable from the public internet.
* **Infrastructure Problem 1:** The network suffers from severe legacy system sprawl and Operating System End of Life (EOL) detection. This includes Windows XP workstations and legacy Exchange servers post-migration.
* **Infrastructure Problem 2:** There is no tool available for Mobile Device & Application Management to secure the highly fragmented endpoint environment.

### B. Vulnerability Analysis (Impact, Risk, and Likelihood)
**Requirement:** *Analyze the given network diagram and vulnerability scan for both companies by doing the following: 1. Describe two existing vulnerabilities for each company. 2. Explain the impact, risk, and likelihood associated with each described vulnerability from part B1 as it relates to each company.*

**Company A Vulnerabilities:**
* **Vulnerability 1:** Open ports 21-90, 3389. 
    * **Likelihood/Risk:** The risk likelihood is classified as High. 
    * **Impact:** The impact is High, as the loss of confidentiality, integrity, or availability from exploiting these ports (especially RDP 3389) is expected to have a severe or catastrophic adverse effect on organizational operations.
* **Vulnerability 2:** All users have local administrative privileges.
    * **Likelihood/Risk:** The risk likelihood is classified as Moderate.
    * **Impact:** The impact is Moderate, as exploitation of this privilege escalation is expected to have a serious adverse effect on organizational operations and assets.

**Company B Vulnerabilities:**
* **Vulnerability 1:** Distributed Ruby (dRuby/DRb) Multiple Remote Code Execution Vulnerabilities. 
    * **Likelihood/Risk:** The risk is High.
    * **Impact:** The severity is Critical, meaning exploitation of this vulnerability likely results in a root-level compromise of servers or infrastructure devices.
* **Vulnerability 2:** Apache Tomcat AJP RCE Vulnerability (Ghostcat). 
    * **Likelihood/Risk:** The risk is High.
    * **Impact:** The severity is Critical, meaning an attacker could likely achieve a root-level compromise of the affected web application servers.

### C. Network Topology Diagram
**Requirement:** *Create a network topology diagram with details of the proposed merged network requirements.*



### D. Topology Components (OSI & TCP/IP Mapping)
**Requirement:** *Identify the layer for all components in the topology diagram referencing the layers of the OSI model and TCP/IP protocol stack.*



* **Switches:** OSI Layer 2 (Data Link Layer) / TCP/IP Network Interface Layer.
* **Routers & Firewalls:** OSI Layer 3 (Network Layer) / TCP/IP Internet Layer.
* **VPN Tunnels:** OSI Layer 3 (Network Layer) / TCP/IP Internet Layer.
* **Servers & Web Applications:** OSI Layer 7 (Application Layer) / TCP/IP Application Layer.

### E. Component Rationale & Budget Constraints
**Requirement:** *Explain the rationale for adding, deleting, or repurposing network components in the newly merged network topology diagram, including details of how each component addresses budgetary constraints.*

* **Adding:** Adding Cloud Infrastructure as a Service (IaaS) allows the newly merged company to securely scale its infrastructure and achieve redundancy. This addresses the $50,000 budget by shifting massive upfront Capital Expenditures (buying new physical servers) to manageable Operational Expenditures (monthly cloud hosting).
* **Deleting:** I recommend immediately deleting and retiring all End-of-Life equipment, including the Windows 7 laptops from Company A and the Windows XP workstations from Company B. Maintaining these introduces unpatchable vulnerabilities.
* **Repurposing:** Company B currently utilizes Next-Gen Firewalls. Instead of discarding these, they can be repurposed as internal segmentation firewalls to separate sensitive data environments, saving the budget from purchasing new routing hardware.

### F. Secure Network Design Principles
**Requirement:** *Explain two secure network design principles that are used in the proposed network topology diagram.*

* **Zero Trust Architecture:** This principle assumes no user or device is trusted by default. This is reflected in the design by enforcing MFA (which Company B was previously missing) for all remote and cloud access, and using firewalls to micro-segment internal traffic.
* **Defense in Depth:** This principle involves layering multiple security controls. The topology utilizes this by layering DNS Security, Endpoint Detection and Response (EDR), and Next-Gen Firewalls at the network perimeter.

### G. Regulatory Compliance
**Requirement:** *Explain how the proposed merged network topology diagram addresses two regulatory compliance requirements that are relevant to the newly merged company...*

* **Payment Card Industry Data Security Standard (PCI-DSS):** *
    * *Relevance:* This is relevant because Company B accepts credit cards as a payment option.
    * *How it meets it:* The proposed topology meets this requirement by placing the Cardholder Data Environment (CDE) in an isolated, micro-segmented VLAN separated from the rest of the general user network via internal firewalls.
* **Gramm-Leach-Bliley Act (GLBA):**
    * *Relevance:* This is relevant because Company A operates in the financial industry offering checking accounts and investment products.
    * *How it meets it:* The proposed topology meets this requirement by implementing strict logical access controls (revoking the widespread local administrative privileges) and encrypting financial data in transit via VPNs to protect consumer financial privacy.

### H. Emerging Threats
**Requirement:** *Describe two emerging threats that are applicable to the merged organization...*

* **Emerging Threat 1: Ransomware via VPN Compromise.**
    * *Risk:* A compromised remote worker endpoint could allow ransomware to traverse the VPN tunnel directly into the newly merged internal network. 
    * *Performance Impact:* Mitigating this requires deep-packet inspection and MFA overhead, which can introduce latency during login and data transfer for remote users.
    * *Management:* Manage this risk by enforcing strict Zero Trust access policies and utilizing Managed Security Services for 24/7 endpoint monitoring.
* **Emerging Threat 2: Cloud Data Misconfiguration.**
    * *Risk:* As the company integrates cloud services for scalability, a misconfigured storage bucket or security group could expose sensitive financial or medical data to the public internet.
    * *Performance Impact:* Routing all cloud traffic through inspection gateways to verify configurations can create bandwidth bottlenecks.
    * *Management:* Manage this risk by implementing automated Cloud Security Posture Management (CSPM) tools and enforcing infrastructure-as-code deployment to prevent manual errors.

### I. Summary Recommendations & Cost-Benefit Analysis
**Requirement:** *Summarize your recommendations for implementation of this proposed merged network based on the scenario and budgetary requirements...*

* **Cost-Benefit Analysis:** On-premises infrastructure requires massive upfront capital for hardware, cooling, and space, and is difficult to scale quickly. Cloud infrastructure provides high availability, geographic redundancy, and immediate scalability with a pay-as-you-go financial model. 
* **Justification:** The executives require a secure design that utilizes zero trust, provides scalability and redundancy, and integrates the two networks. Given the strict $50,000 Year 1 budget, building a fully redundant on-premises infrastructure is financially impossible. Adopting a hybrid-cloud topology is the only viable method to achieve the required redundancy, enforce segmentation for regulatory compliance, and retire legacy EOL systems without exceeding the budgetary constraints.
