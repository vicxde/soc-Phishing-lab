# soc-Phishing-lab
Phishing Email Analysis Lab. A hands-on security operations project documenting the investigation and analysis of phishing emails, including header analysis, indicator of compromise extraction, and threat classification. Built to develop and demonstrate SOC analyst skills including email forensics and incident documentation.

TCM Security SOC Labs — Phishing Campaign Analysis

Two virtual machines were configured for this lab: Ubuntu and Windows 11. The materials used for analysis are hosted on these VMs.

This section covers the phishing campaign analysis. Since the Ubuntu distribution does not include a native email client, Thunderbird was installed and used to launch and review the sample emails for analysis.

https://cdn.discordapp.com/attachments/1448796745134899452/1543321091513000006/image.png?ex=6aa98945&is=6aa837c5&hm=b97b03d8c2686045625e34486ddf3245f84cf1e40a25137deafe8535e260a2a7&

No email account needed to be configured with Thunderbird — the client can be used standalone for opening and reviewing email files (e.g., .eml) directly, without connecting to a live mailbox.

Any phishing sample email file opened during this lab will be launched and viewed through Thunderbird.
https://cdn.discordapp.com/attachments/1448796745134899452/1543321501657202728/image.png?ex=6aa989a7&is=6aa83827&hm=97db1e9c20606133c3da21f7e58601e7a3e6c36d62a5d5a7a5f6ba8f3132ef9a&

Configuring Thunderbird for Analysis

Within Thunderbird's settings, remote content in messages was enabled. This setting is necessary for this project because many of the phishing samples analyzed contain embedded links and remote-hosted content, which need to be visible for thorough analysis.
https://cdn.discordapp.com/attachments/1448796745134899452/1543322577999503480/image.png?ex=6aa98aa8&is=6aa83928&hm=89c80c1403ba0ebfe8a99670a54b0ffd4bce00db06a4d3cdd9909dec4dff6891&

https://cdn.discordapp.com/attachments/1448796745134899452/1543322578704138342/image.png?ex=6aa98aa8&is=6aa83928&hm=bcedfb84d303df523f77f57660cddcef175291b71de8735e8e3e16bf586b5b3f&
