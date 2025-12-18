
## Week 7 - Security Audit and System Evaluation 

##

# Introduction

This week focused on conducting a comprehensive security audit of the Linux server, validating existing security controls, applying selective hardening measures, and critically evaluating the system’s overall security posture. The objective was to assess vulnerabilities, remediate feasible risks, and reflect on the operating system as an integrated system balancing security, performance, and manageability.

---------------------------------------------------------------------------------------
# Baseline Security Audit (Lynis – Before Remediation)

A baseline security audit was conducted using Lynis, a widely used Linux auditing and hardening tool. Lynis assessed system configuration, authentication mechanisms, kernel settings, services, and network exposure. The resulting hardening index provided a quantitative baseline against which improvements could be evaluated.


- Installing Lynis Namp

<img width="1406" height="608" alt="sudo apt install lynis nmap -y installing lynis nmap" src="https://github.com/user-attachments/assets/4870bbc7-0c6f-4e9b-9814-ab4680c03b91" />

##


**Commands Used**
- sudo lynis audit system
##
<img width="1746" height="698" alt="sudo lynis audit system  running lynis audit system to check system info" src="https://github.com/user-attachments/assets/cf45e2f4-bea4-464b-8d1a-91fd682bc63c" />

- Running audit system
##

- Output Showcases Hardening index = 65
  
<img width="2148" height="1392" alt="Lynis secuirty scan details" src="https://github.com/user-attachments/assets/469dd440-c3f2-42ca-863e-66bcbca475a1" />

##

# Review of Lynis Findings

Following the baseline audit, the Lynis log file was reviewed to identify security recommendations. Hardening suggestions were identified and analysed to determine which actions were appropriate for the deployment context. No high-severity warnings were reported, indicating that the system already adhered to key security best practices.

## Security Posture Evaluation

The Lynis audit confirmed that the system’s existing security controls implemented in earlier weeks (SSH hardening, firewall rules, AppArmor, and Fail2Ban) are effective and correctly configured. The hardening index of 65 reflects a balanced security posture appropriate for a virtualised server environment, where excessive hardening could negatively impact usability and maintainability. Overall, the audit validated prior security decisions rather than exposing critical weaknesses.



**Command Used**
- sudo grep Suggestion /var/log/lynis.log
#
<img width="952" height="86" alt="sudo lynis show report     show where the report is" src="https://github.com/user-attachments/assets/6ee3e4b5-9c3e-4eb4-b2ea-a869f8c616dc" />

- shows where the file is

##
<img width="2880" height="558" alt="sudo grep suggestion     " src="https://github.com/user-attachments/assets/1fafcf3a-cff6-461d-a16a-982808eca407" />

- shows suggestions 

##

**Selective Hardening Decisions(Post-Audit)**
- Rather than applying all Lynis recommendations indiscriminately, hardening actions were prioritised based on security impact, system stability, and relevance to the deployment context. Existing SSH hardening, firewall restrictions, and intrusion prevention mechanisms already mitigated the highest-risk findings. Additional recommendations were reviewed but deferred where the security benefit was marginal or where changes could negatively impact system usability or performance. This selective approach reflects professional security management practices rather than checklist-driven hardening.

----------------------------------------------------------------------------------------
## Selected Secuirty Improvements and Validation

# Enabling Process Accounting (Audit Logging)

Process accounting was enabled to enhance auditability and support forensic analysis. This allows the system to record executed processes and command usage, improving accountability and traceability in the event of a security incident.

**Commands Used**

- sudo apt install acct -y
- sudo systemctl enable acct
- sudo systemctl start acct
- sudo systemctl status acct

##

- Installing acct

<img width="1410" height="200" alt="sudo apt install acct " src="https://github.com/user-attachments/assets/fb4dba71-2293-4621-92a9-e281cd02d7ef" />

##
- Enabling acct

<img width="1412" height="648" alt="sudo systemctl enabling acct" src="https://github.com/user-attachments/assets/654a5e25-ebeb-491c-9d98-1af78d0932d6" />

##
- Checking statuts of acct

<img width="2068" height="860" alt="sudo systemctl status acc checking status of acct" src="https://github.com/user-attachments/assets/c33dd4a7-43af-485b-9ba3-63d07352e69b" />

##
# Trade-off:
While process accounting introduces minor logging and storage overhead, this was considered acceptable given the security and audit benefits.
##

# Firewall Validation

Firewall rules were reviewed to ensure that only authorised SSH access from the designated workstation IP was permitted. This validation confirms a minimal network attack surface.

**Commands Used**
- sudo ufw status verbose
##

<img width="1208" height="416" alt="sudo ufw status verbose checking firewall is correct week 7" src="https://github.com/user-attachments/assets/f2391c0b-b8ab-43fc-ab03-b545291306ab" />

- checking firewall rules
-----------------------------------------------------------------------------------------
## Additional Hardening: SSH Legal Banner

A legal SSH banner was configured to provide clear notice of authorised access and monitoring prior to authentication. This aligns with compliance and policy-based security best practices and was identified as a low-risk hardening measure.

##
**Commands Used**
- sudo nano /etc/issue.net
- sudo nano /etc/ssh/sshd_config.d/99-banner.conf
- sudo systemctl restart ssh

##
<img width="850" height="34" alt="sudo nano etc issue creating banner file" src="https://github.com/user-attachments/assets/7d474026-7ef2-4c69-85d0-caf05759a8c8" />

-creating file banner

##
- Going to config file

<img width="978" height="36" alt="sudo nano sshdconfig editing banner config channigng banner to enable" src="https://github.com/user-attachments/assets/76aecfd5-5eb6-47f8-ae91-fbe207043c10" />

##
- Adding Banner

<img width="730" height="126" alt="sudo editing banner adding a banner 3" src="https://github.com/user-attachments/assets/536389c8-4d26-47b5-9982-67d2d24711b6" />
##

# Trade-off:
The SSH banner does not prevent attacks directly but strengthens legal and compliance posture without affecting performance.
----------------------------------------------------------------------------------------
## Post-Remediation Security Audit (Lynis – After)

After applying selected improvements, Lynis was re-run to reassess the system. The hardening index remained unchanged, demonstrating a limitation of automated scoring tools where qualitative security improvements do not always translate into numerical score increases.
##

**Commands Used**
- sudo lynis audit system

##
<img width="1714" height="428" alt="sudo lynis audit reruning 2nd time" src="https://github.com/user-attachments/assets/df69778e-8259-43ef-a3d9-37208fbf4d09" />

- Running audit system

##

<img width="2326" height="1454" alt="sudo lynis audit system   after enabling acct 2" src="https://github.com/user-attachments/assets/5c53e4d9-eecb-4e1c-97c6-849f84585325" />

- after enabling acct

# This highlights the importance of combining automated tools with human judgement when evaluating system security.
----------------------------------------------------------------------------------------

## Network Security Assessment (nmap)

A network security assessment was performed using nmap to identify exposed services and validate firewall effectiveness.

**Command Used**
- sudo aa-status

##

<img width="1426" height="444" alt="sudo aa-status week 7 confirms mac is enabled" src="https://github.com/user-attachments/assets/d621ad2e-6dc6-401a-8317-e6b45cb552f1" />

- Checks if apparmor and mac are active

Nmap scanning confirmed that only the SSH service was exposed on the server. This validates firewall effectiveness and minimises the network attack surface.

----------------------------------------------------------------------------------------
## Service Inventory and Justification

Running services were reviewed to confirm that only essential services were enabled.

**Commands Used**
- systemctl list-units --type=service --state=running
##

<img width="1438" height="1358" alt="systemctl list units week 7 ist runing services" src="https://github.com/user-attachments/assets/0b1bd991-9177-4391-9b19-a7c61d9ee334" />

# Justified Services:

- **ssh** – secure remote administration

- **ufw** – firewall enforcement

- **fail2ban** – intrusion detection and prevention

- **apparmor** – mandatory access control

A review of running services confirmed that only essential services were active. No unnecessary network services were identified, reducing potential attack vectors.



----------------------------------------------------------------------------------------
## Remaining Risk Assessment

Despite significant hardening, some residual risks remain. SSH access, although restricted and key-based, remains an exposed service. Additionally, as the system operates within a virtualised environment, its security is partially dependent on the host operating system and hypervisor, which are outside the control of the guest OS. 
----------------------------------------------------------------------------------------



### Trade-off: Automated Security Scoring vs Human Risk Assessment

Automated auditing tools such as Lynis provide structured security assessments and quantitative hardening scores; however, they do not fully capture contextual risk or the operational suitability of every recommendation. This was evident when selected remediations did not significantly increase the Lynis score despite improving auditability and compliance. This trade-off highlights the limitation of relying solely on automated metrics and reinforces the importance of informed human judgement when evaluating operating system security.

## Final Evaluation and Reflection

This week demonstrated a complete security lifecycle: baseline auditing, review of findings, selective remediation, and validation. The use of Lynis, nmap, firewall verification, and access control checks illustrates a balanced approach to security, performance, and manageability. The results highlight the operating system as an integrated system shaped by configuration choices, security requirements, and virtualisation constraints, reflecting professional system administration practices.

Overall, this project reinforced that effective operating system security is achieved through continuous assessment, informed trade-offs, and configuration discipline rather than reliance on any single tool or metric.


