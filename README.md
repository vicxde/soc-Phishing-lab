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

<img width="2279" height="1288" alt="image" src="https://github.com/user-attachments/assets/0077187f-c500-4fc8-a16f-1055caff9ac8" /><img width="2876" height="1737" alt="image" src="https://github.com/user-attachments/assets/b511bac4-c785-47e1-9415-5f2890d469b2" />

