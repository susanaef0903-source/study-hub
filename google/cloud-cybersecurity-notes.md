# Google Cloud Cybersecurity Certificate — Course 1 Notes (Security Principles in Cloud Computing)

**Platform:** Google Cloud Cybersecurity Certificate (Coursera/Google Skills) | **Studied:** Aug 2026 | **Source:** the Course 1 readings PDFs (+ two Course 2 orientation readings) saved on the Desktop

## 🎯 What this course is about (one sentence)

What the cloud actually is, who is responsible for securing which part of it (the CSP or
me), and the layered controls — identity, network, detection, response, recovery — that
add up to "defense in depth."

## 🗺️ The program at a glance

Five courses: **1)** Intro to Security Principles in Cloud Computing → **2)** Strategies for Cloud Security Risk Management → **3)** Identify & Protect Against Threats → **4)** Detect, Respond, Recover → **5)** Capstone / job prep.
Logistics that matter: pass every graded quiz at **80%+** (retakes allowed); labs run on Google Skills with a **90-minute non-pausable timer and 5 total attempts each** — read the guide materials *before* starting the clock, use an incognito window, never use a personal Google Cloud account. Everything is practiced inside the **Cymbal Bank** scenario: I play a junior cloud security analyst at a fictional international bank doing a hybrid-cloud digital transformation (cast: Javier the CISO, Chloe the Cloud Security Lead — my task-giver, Hank the Cloud Architect, Hannah the Incident Responder).

## 🔑 Key Concepts

| Concept | Plain-English meaning | Sue's payroll/accounting translation |
|---|---|---|
| **Cloud computing** | Using on-demand computing resources as services over the internet | Renting the payroll system by subscription instead of owning the server in the back office |
| **Cloud cybersecurity** | Keeping cloud data/apps/infrastructure **confidential, intact, and available** (the CIA triad in disguise) | The three things you always guaranteed: only authorized eyes see pay data, nobody alters it, and it's there on check day |
| **Shared responsibility model** | The explicit agreement about which security controls the CSP owns vs. the customer | Outsourcing payroll to ADP: they secure their system, but *you* still own accurate inputs, approvals, and who gets a login |
| **Shared fate model** | The CSP stays involved in your whole security journey, not just its own side | A payroll vendor who also trains your staff and reviews your setup — invested in your outcome, not just their contract |
| **IaaS / PaaS / serverless** | How much of the stack the provider runs: just infrastructure → infrastructure + OS/middleware → everything but your code | Buying blank check stock vs. preprinted checks vs. the bank printing and mailing them for you |
| **Zero trust** | Every user, device, and system must authenticate and be authorized before touching the network | No one walks into the payroll office without showing ID — even the CFO, even on their 1,000th visit |
| **Defense in depth** | Layered controls so no single failure exposes you | Locked file room + locked cabinet + sign-out log + segregation of duties. Any one can fail; the stack holds |
| **IAM (identity & access management)** | Controlling who (or what) can access which resources; identities include users, **groups**, and **service accounts** (non-human) | The permissions matrix: who can view pay data, who can enter, who can approve — set by job role, not by person |
| **Least privilege** | Give each identity only the access their job requires | The AP clerk doesn't get check-signing authority; new access granted only with the role |
| **MFA / federation / SSO** | Verify identity two+ ways; let outside identities (contractors) in with short-term credentials | The auditor gets a visitor badge that expires Friday — not a permanent key |
| **Firewall / FWaaS** | Software that filters network traffic; CSP runs it, customer writes the rules | The mail room screening what comes in and goes out — you set the screening policy |
| **VPC (virtual private cloud)** | Your own private, isolated network inside the public cloud | A locked suite inside a shared office tower |
| **Encryption at rest / in transit** | Data scrambled while stored and while moving | Sealed envelopes in the file room AND in the courier's bag |
| **Redundancy / regions & zones** | Copies of data across data centers (zone = data centers in an area; region = group of zones) | Offsite backup of the payroll records — fire in one building loses nothing |
| **DevSecOps / shift left** | Security built in from the *start* of building software, not bolted on at the end | Reviewing the timesheet form design before rollout, instead of auditing errors after the first pay run |
| **Infrastructure as code (IaC)** | Define your servers/networks in code (e.g., Terraform) so setups are repeatable and reviewable | A written closing checklist instead of "how Carol does it from memory" — consistent every time, auditable |
| **Cloud Storage classes** | Standard (hot/frequent) → Nearline (monthly) → Coldline (quarterly) → Archival (yearly/disaster recovery); rarer access = cheaper | Active files on your desk → current-year cabinet → basement storage → the seven-year retention boxes |

## 🧱 How Google secures its own infrastructure (the five layers)

1. **Secure low-level infrastructure** — physical data centers: cameras, metal detectors, biometrics; each server has its own identity; heavy automation (less manual work = fewer mistakes).
2. **Secure service deployment** — zero trust everywhere; customer data isolated even on shared (multi-tenant) machines; encrypted service-to-service credentials.
3. **Secure data storage** — encryption at rest; scheduled deletion protects against accidental or malicious erasure.
4. **Secure internet communication** — private IP space isolated from the public internet (helps blunt denial-of-service attacks).
5. **Operational security** — verified code libraries (blocks bugs like cross-site scripting), manual security reviews, hardened employee devices with MFA (limits insider risk), and a threat-research team watching for social engineering, ransomware, spyware, watering-hole attacks.

## 🛡️ The NIST Cybersecurity Framework — five control families (exam favorite!)

1. **Identify** — catalog assets, rank the risks to each, find control gaps → *the fixed-asset register + risk assessment*
2. **Protect** — access control, firewalls/segmentation, employee training → *locks and internal controls*
3. **Detect** — monitor for suspicious activity (intrusion detection, phishing/malware scanning) → *the reconciliation that catches the anomaly*
4. **Respond** — plans + automation to contain and mitigate incidents → *the fraud-response procedure*
5. **Recover** — restore access/performance: high availability, replication across zones/regions, backups → *business continuity: reissue the checks, restore from backup*

Course 1 Module 2's control taxonomy maps onto it: **identity, network, protective, detective, responsive, recovery** controls layered = defense in depth.

## ☁️ Before migrating to the cloud — the five due-diligence questions

1. Which security controls are **my** responsibility?
2. Which controls does the **CSP provide** as part of the offering?
3. Which **default controls do I inherit** automatically (e.g., encryption)?
4. What are my **compliance obligations** — and where will the CSP physically run my resources?
5. What are the security requirements for my **customers and contractors** (access privileges, privacy disclosures)?

Plus the honest trade-offs: cloud buys faster time to market, collaboration, strong default security, durability — at the cost of giving up infrastructure control, new security/privacy questions, and a real migration effort (rewriting code, retraining people).

## 🔁 DevSecOps: the seven phases (security woven through all of them)

**Plan** (threat analysis, IAM roles, scope) → **Code** (reviews, secure design, automated scan reports to devs) → **Build** (automated vulnerability checks) → **Test** (manual = QA/triage; automated = security & compliance) → **Release** (final security checks and sign-offs) → **Deploy** (automation pushes to production) → **Operate** (monitor, patch, continuous feedback loop).
"Shift left" = all the security work happens toward the beginning of that chain, not after deployment.

## 🧰 The analyst's day-to-day tools

- **Google Cloud console** — web dashboard: configure IAM, manage projects, reach every service.
- **Cloud Shell** — Google's command-line interface for working in the cloud environment (Course 1 lab: build a replica VPC for testing).
- **Terraform** — the IaC tool used in the Module 3 activity to review infrastructure-as-code deployments.
- **Serverless building blocks:** BaaS (CSP runs the whole backend) and FaaS (Cloud Functions — small, short-lived functions; their tiny lifespan is itself a security feature since attackers get almost no window).

## 🗣️ Teach it to a friend

Moving to the cloud is like outsourcing your payroll processing. The provider guards the
building, the machines, and the plumbing — and they're genuinely better at that than you'd
be. But you still decide who gets a login, what they're allowed to touch, and whether your
data setup complies with the rules of your industry: that's the shared responsibility model,
and the written split of duties matters as much as any contract. Security itself is never
one lock; it's layers — verify every person every time (zero trust), give each person only
the keys their job needs (least privilege), watch the logs (detect), have a plan for the bad
day (respond), and keep copies in another building (recover). And the newest habit,
DevSecOps, is just an old audit principle: it's cheaper to design the control into the form
than to catch the error after the pay run.

## 🃏 Flashcards

**Q:** What does cloud cybersecurity protect (three words)?
**A:** Confidentiality, integrity, availability of cloud data, apps, and infrastructure.

**Q:** Shared responsibility vs. shared fate?
**A:** Shared responsibility = the agreed split of security duties between CSP and customer; shared fate = the CSP actively partnering across your whole security journey.

**Q:** In PaaS, what does the customer still own?
**A:** Data/content, access policies, usage, deployments, and web application security — the CSP owns the OS, network security, and everything below.

**Q:** Define zero trust.
**A:** All users, devices, and systems must be authenticated and authorized before accessing the network — no default trust, even inside.

**Q:** Name the five NIST CSF functions.
**A:** Identify, Protect, Detect, Respond, Recover.

**Q:** What's a service account?
**A:** A non-human IAM identity (application, service, or VM) granted roles to perform actions.

**Q:** Why do IAM groups support least privilege?
**A:** Permissions map to job roles; adding/removing a member updates their access correctly — no over- or under-assignment person by person.

**Q:** Order the four Cloud Storage classes from hottest to coldest.
**A:** Standard (frequent) → Nearline (~monthly) → Coldline (~quarterly) → Archival (~yearly/disaster recovery). Rarer access = cheaper.

**Q:** What does "shift left" mean?
**A:** Incorporating security at the beginning of the development process instead of at the end.

**Q:** Zone vs. region?
**A:** Zone = the data centers in one area; region = a group of zones. Replicating across them is how recovery controls achieve high availability.

**Q:** Who configures cloud firewall rules under FWaaS?
**A:** The customer writes/configures the rules; the CSP maintains the software and physical infrastructure.

**Q:** What's special about a FaaS function's lifespan, and why does security like it?
**A:** Functions are ephemeral — they exist briefly and do one job, so attackers get a tiny window and a compromised function exposes only its own slice.

## 💡 How I'll actually use this

- **nyc-payroll-explorer** runs on public cloud pieces already — write down my own mini shared-responsibility table for it (what the host secures vs. what I must: secrets, access, dependency updates).
- **flask-analytics-app**: apply least privilege to the database — the app's account should read/write its own tables, not own the whole database; add basic logging so I have a "detect" layer.
- Lab prep habit: review the reading + Lab Technical Tips *before* starting the 90-minute timer; incognito window; never my personal GCP account.
- Interview line: "Payroll taught me defense in depth and least privilege decades before I knew the vocabulary — segregation of duties, access by role, audit trails, and retention schedules are the same controls NIST CSF formalizes."
