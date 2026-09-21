# soc-Phishing-lab
Phishing Email Analysis Lab. A hands-on security operations project documenting the investigation and analysis of phishing emails, including header analysis, indicator of compromise extraction, and threat classification. Built to develop and demonstrate SOC analyst skills including email forensics and incident documentation.






TCM Security SOC Labs — Phishing Campaign Analysis

Two virtual machines were configured for this lab: Ubuntu and Windows 11. The materials used for analysis are hosted on these VMs.

This section covers the phishing campaign analysis. Since the Ubuntu distribution does not include a native email client, Thunderbird was installed and used to launch and review the sample emails for analysis.

<img width="2073" height="1518" alt="image" src="https://github.com/user-attachments/assets/8669dccc-a883-498b-9e51-406bfa7883fa" />

No email account needed to be configured with Thunderbird, the client can be used standalone for opening and reviewing email files (e.g., .eml) directly, without connecting to a live mailbox.

Any phishing sample email file opened during this lab will be launched and viewed through Thunderbird.
<img width="3012" height="1978" alt="image" src="https://github.com/user-attachments/assets/9aaf1868-4302-41e9-aab7-96e3fd9b334f" />


Configuring Thunderbird for Analysis

Within Thunderbird's settings, remote content in messages was enabled. This setting is necessary for this project because many of the phishing samples analyzed contain embedded links and remote-hosted content, which need to be visible for thorough analysis.
<img width="1623" height="1452" alt="image" src="https://github.com/user-attachments/assets/472aec0c-1809-49c1-88b5-25f6573f071f" />


<img width="1939" height="1064" alt="image" src="https://github.com/user-attachments/assets/c1a9eea3-5514-40f0-99fa-5a04cc286fb2" />

Tooling Setup

Sublime Text was selected as the code editor to streamline the documentation process. While the installation was in progress, notes were drafted and stored as plain text to avoid losing any progress.

<img width="2279" height="1288" alt="image" src="https://github.com/user-attachments/assets/0077187f-c500-4fc8-a16f-1055caff9ac8" />

<img width="2876" height="1737" alt="image" src="https://github.com/user-attachments/assets/b511bac4-c785-47e1-9415-5f2890d469b2" />

Analyzing Emails via Terminal

Email source files can also be analyzed directly from the terminal, using tools like grep to search for specific information within the raw email source. This method is useful for deep analysis, allowing key indicators (such as headers, URLs, or sender details) to be located quickly and efficiently.

now we will open sublime from the terminal

<img width="1844" height="929" alt="image" src="https://github.com/user-attachments/assets/7eec0724-f86e-4616-995a-22a5918e0b59" />

Improving Readability with an Email Header Add-on

To make raw email headers easier to read within Sublime Text, an add-on/package was installed for syntax highlighting. This was enabled by opening the Command Palette (Ctrl+Shift+P), searching for "Email Header," and then selecting "Email Header" from the syntax/language option in the bottom-right corner of the editor (replacing the default "Plain Text" setting).
<img width="1525" height="1020" alt="image" src="https://github.com/user-attachments/assets/40067409-faee-4171-a120-ebd99ca3effc" />

<img width="2068" height="800" alt="image" src="https://github.com/user-attachments/assets/aeb8191b-546e-42b5-941f-969dd02fb7d0" />

<img width="1144" height="816" alt="image" src="https://github.com/user-attachments/assets/b0edd55c-f698-4d88-bf22-7446a263c190" />

<img width="1215" height="1533" alt="image" src="https://github.com/user-attachments/assets/f8ab6d33-b824-4061-b6e8-afffa3dd0797" />


Email Header Analysis — Key Indicators



When analyzing a phishing email, the sophistication of the attacker determines how much effort has gone into concealing their identity. This is why examining the raw source of the email, rather than the rendered view, is essential.

Key fields to investigate include:

Message-ID — can reveal inconsistencies with the claimed sender/domain

Reply-To — often differs from the "From" address in spoofed emails, a useful mismatch indicator

Return-Path — shows where bounce/delivery failure notices are actually sent, which can expose the true sending infrastructure

Received headers — the most valuable indicator, as they show the full path the email took across mail servers to reach the recipient. 

Note: the topmost Received header is the one closest to the recipient (least reliable for tracing origin), while the bottommost Received header is closest to the original sender (most valuable for identifying true origin)
X-Sender / X-Originating-IP — when present, can directly expose the sender's IP address

Not all of these headers will be present in every email — Received headers are the only ones guaranteed to appear.

<img width="1597" height="924" alt="image" src="https://github.com/user-attachments/assets/5e653df3-b19e-4153-badc-28aa72ee1af4" />

<img width="2524" height="112" alt="image" src="https://github.com/user-attachments/assets/62b24089-455a-41ee-a19d-5e2dbcb371b9" />

<img width="840" height="128" alt="image" src="https://github.com/user-attachments/assets/a663714e-3581-4063-90c3-f4d84734a239" />

Examining the X-Sender header revealed the IP address 185.70.40.140, which is a critical piece of evidence for tracing the origin of the phishing email and can be used for further investigation (e.g., reputation lookups, geolocation, or ASN/ISP identification).

<img width="592" height="38" alt="image" src="https://github.com/user-attachments/assets/dd0fe101-25e0-48e6-a976-0ee32f16e7af" />

WHOIS Lookup on Extracted IP

With the sender IP identified, a WHOIS lookup was performed to gather ownership and registration details — this can be done either via the terminal (whois command) or an online WHOIS lookup service.

The WHOIS results showed no association between the IP 185.70.40.140 and Chase Bank, despite the phishing email impersonating Chase. This discrepancy between the claimed sender identity and the actual registered ownership of the originating IP further reinforces that the email is fraudulent.

<img width="1356" height="1094" alt="image" src="https://github.com/user-attachments/assets/9ef55e57-e98f-42bc-a70c-5998f694e1da" />

<img width="1948" height="1078" alt="image" src="https://github.com/user-attachments/assets/ac4e4dfa-2410-4a4f-bf80-d4fe4c8aa007" />

<img width="1573" height="858" alt="image" src="https://github.com/user-attachments/assets/141a7f88-b622-4620-b9c1-48e122d2cb9f" />

Automating Header Analysis Tool

To streamline the header analysis process, the tool MHA (Message Header Analyzer) was used. This tool parses raw email headers automatically, presenting the routing path, timestamps, and key fields (Received, Return-Path, Message-ID, etc.) in a structured, easy-to-read format significantly speeding up analysis compared to manual header parsing.
(another tool we can use is mxtoolbox.com )

<img width="2953" height="1301" alt="image" src="https://github.com/user-attachments/assets/cbbf4feb-f880-4270-89db-61b8a3a50141" />

<img width="2655" height="1718" alt="image" src="https://github.com/user-attachments/assets/48dffad2-982b-4e70-8502-bb45c66fea20" />

Case Study: CIBC Bank Phishing Email

1. Initial Impression
At first glance, this email appears to be a legitimate communication from CIBC Bank.

<img width="2269" height="1699" alt="image" src="https://github.com/user-attachments/assets/8ce82f96-ee15-441a-b03d-5bdc7474b103" />

2. Sender Discrepancy
However, closer inspection of the sender address reveals that the email does not actually originate from CIBC.

<img width="1218" height="55" alt="image" src="https://github.com/user-attachments/assets/80cf824c-be73-4395-818f-d915252e2414" />

<img width="1602" height="139" alt="image" src="https://github.com/user-attachments/assets/5eb279e6-b433-4c0f-9618-f85870878d55" />

3. Return-Path Mismatch
The Return-Path header shows the address Meztaz.logocec8@caib.com — a domain with no legitimate connection to CIBC Bank, and suspicious in its own right (note the domain "caib" appears to be a deliberate near-miss of "cibc").

<img width="824" height="109" alt="image" src="https://github.com/user-attachments/assets/6a19ca71-0687-4534-b05e-e6dc12578ed0" />

4. Reverse DNS Lookup
An IP address extracted from the header was used to perform a reverse DNS lookup using one of the analysis tools in our toolkit.

<img width="2228" height="1112" alt="image" src="https://github.com/user-attachments/assets/910f19f0-7aba-49b7-88ca-8008f1eda738" />


5. Conclusion
The results of the reverse DNS lookup confirmed a clear mismatch between the claimed sender identity and the actual infrastructure behind the email, allowing us to conclusively classify this as a phishing attempt.





Part 2: Email Authentication Protocols

Having covered header and IP-based analysis, this section shifts focus to a different layer of email verification: authentication protocols. These mechanisms (SPF, DKIM, and DMARC) are built into how legitimate mail servers prove a message actually came from who it claims to, and understanding them is essential for spotting spoofed senders that pass a surface-level glance.


Email Authentication Fundamentals

1. SPF (Sender Policy Framework)
SPF allows a domain owner to publish a list of IP addresses/servers authorized to send email on their behalf. The end of the SPF record indicates the enforcement policy:

-all (hard fail): any sending IP not on the authorized list is explicitly rejected/blocked
~all (soft fail): unauthorized IPs are not blocked outright but flagged and treated with caution

2. DKIM (DomainKeys Identified Mail)
DKIM provides a cryptographic authentication method, allowing the receiving server to verify that the email's content and domain claim are legitimate and haven't been tampered with in transit.

3. DMARC (Domain-based Message Authentication, Reporting & Conformance)
DMARC acts as the enforcement layer, or "bouncer" — it defines the policy for how a receiving mail server should handle emails that fail SPF and/or DKIM checks (e.g., reject, quarantine, or monitor).


<img width="3056" height="1579" alt="image" src="https://github.com/user-attachments/assets/a43cc4d1-8dcf-487c-a303-75088f394fd7" />
we will be using this email as a demonstration

Case Study:

1. Initial Red Flag: Urgency Tactic
This email employs a classic urgency tactic, a common social engineering technique used to pressure recipients into acting quickly without careful scrutiny.

2. Message-ID Mismatch
The first indicator examined was the Message-ID header, which did not match the domain the email claimed to originate from, an early sign worth investigating further.

<img width="1340" height="126" alt="image" src="https://github.com/user-attachments/assets/83355108-ba24-4ebe-ae4a-a9a27d8daa68" />


3. SPF and DKIM Verification
Despite the Message-ID discrepancy, checking the SPF and DKIM records showed that both passed authentication and were legitimate.

<img width="1605" height="149" alt="image" src="https://github.com/user-attachments/assets/7e862773-597e-49fb-8132-9464a7e162ff" />

<img width="1644" height="478" alt="image" src="https://github.com/user-attachments/assets/3eec9f3c-93d6-4b3b-b346-33e92cc9e15b" />

4. Confirming Findings with MXToolbox
To validate these results, the findings were cross-referenced using MXToolbox.

5. MXToolbox Verification Results
Pasting the email headers into MXToolbox's Analyze Headers tool confirmed the earlier finding: the email is DMARC compliant, with both SPF and DKIM passing alignment and authentication checks.

<img width="2223" height="1041" alt="image" src="https://github.com/user-attachments/assets/20c59b7d-918c-48a0-baf3-478d8acff0c4" />


6. Conclusion
This email can be trusted to a reasonable extent based on its authentication results. However, it's important to note that passing SPF, DKIM, and DMARC does not guarantee an email is safe. A sufficiently sophisticated attacker (e.g., one who compromises a legitimate domain, uses a look-alike domain with valid authentication records of its own, or abuses a legitimate but poorly-vetted sending service) can still pass all three checks while sending malicious content. Authentication results should be treated as one signal among several, not a definitive verdict.


