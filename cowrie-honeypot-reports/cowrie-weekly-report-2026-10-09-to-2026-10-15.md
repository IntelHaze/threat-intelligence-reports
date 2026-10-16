# Weekly Cowrie Honeypot Activity Report

**Report ID:** W42  |  **TLP:CLEAR**

**Prepared by:** Berkay Vagas
**Reporting Period:** 9-15 October 2026  
**Data Source:** Cowrie Honeypot Logs  
**Analysis Platform:** Splunk

## 1. Executive Summary

This report reviews activity recorded by the Cowrie honeypot between 9 and 15 October 2026. It summarises login attempts, commands and file downloads, and highlights the main sources of activity. During the week, Cowrie recorded **750,964 events from 1,389 IP addresses**.

The report also investigates a frequently used file-download link found in the logs. The link appeared in **827 of the week’s 2,043 successful download events** and across **421 sessions**. Cowrie recorded **13 different file hashes** for downloads from this link. The three most common hashes accounted for **87%** of the link’s download events. We checked those three hashes using VirusTotal, which labelled the files as related to the **Mirai/Cling** malware family.

## 2. Scope and Methodology

This report covers Cowrie events from **9–15 October 2026**. Splunk search bounds were `10/09/2026 00:00:00` through `10/16/2026 00:00:00` in the system-default time zone. During this period the system time zone was **UTC+1** (Dublin), so the equivalent UTC bounds were `2026-10-08 23:00:00 UTC` through `2026-10-15 23:00:00 UTC`. All displayed hourly and daily buckets use the Splunk system time zone unless explicitly marked UTC.

The weekly analysis covers overall event volume and event-type distribution, source IP activity, session counts, authentication activity and file downloads. Section 7 then examines the leading download URL, its three most frequently observed hashes and related external threat-intelligence findings. Cowrie observations are distinguished from results supplied by VirusTotal, AbuseIPDB, Cisco Talos, GreyNoise, RIPEstat and ThreatFox.

A Cowrie `file_download` event records a successful file download by the honeypot. It does not show that the file was executed by an attacker or compromised a production system. VirusTotal Code Insight is an automated summary and is not a sandbox observation.

## 3. Weekly Activity Overview

### 3.1 Key Metrics

|Metric|Weekly Total|
|---|---|
|Total events|750,964|
|Unique source IP addresses|1,389|
|Event types|24|
|`cowrie.login.success` events|41,740|
|`cowrie.login.failed` events|590|
|Successful file-download events (`cowrie.session.file_download`)|2,043|
|Unique URLs across successful download events|48|
|Sessions across successful download events|1,357|
|Failed file-download events (`cowrie.session.file_download.failed`)|623|

These figures represent events recorded by the honeypot. Event totals do not correspond directly to unique attackers, independent attacks, or confirmed compromises. In particular, `cowrie.login.success` means Cowrie accepted the submitted credentials within the honeypot; it does not indicate successful access to a production system.

### 3.2 Top 10 Event Types

|Event Type|Count|
|---|---|
|`cowrie.command.input`|298,970|
|`cowrie.command.success`|103,989|
|`cowrie.session.connect`|46,386|
|`cowrie.session.closed`|46,380|
|`cowrie.command.failed`|43,688|
|`cowrie.login.success`|41,740|
|`cowrie.session.params`|39,960|
|`cowrie.log.closed`|39,957|
|`cowrie.client.version`|33,664|
|`cowrie.client.kex`|33,005|

**Event ID Descriptions**

`cowrie.command.input`: A command was submitted by the remote user.
    
`cowrie.command.success`: Cowrie recorded a command as successful within the honeypot environment.
    
`cowrie.session.connect`: A new session was established.
    
`cowrie.session.closed`: A session was closed.
    
`cowrie.command.failed`: A command was recorded as failed.
    
`cowrie.login.success`: Cowrie accepted the submitted login credentials.
    
`cowrie.session.params`: Session-related parameters were recorded.
    
`cowrie.log.closed`: A session log was closed.
    
`cowrie.client.version`: The SSH client version was recorded.
    
`cowrie.client.kex`: SSH key-exchange information was recorded.

## 4. Weekly Source IP Analysis

### 4.1 Top 10 Source IP Addresses

The following table ranks the ten leading source IP addresses by total event volume.

|Source IP Address|Total Events|Sessions|
|---|---:|---:|
|`154[.]23[.]73[.]32`|324,313|3,390|
|`64[.]207[.]185[.]5`|48,668|3,292|
|`160[.]153[.]187[.]122`|25,398|1,718|
|`179[.]43[.]133[.]154`|10,590|963|
|`175[.]198[.]129[.]21`|10,268|437|
|`101[.]226[.]198[.]20`|10,077|2,409|
|`77[.]239[.]124[.]147`|8,846|1,107|
|`77[.]239[.]124[.]148`|8,846|1,107|
|`109[.]160[.]32[.]107`|8,008|1,002|
|`109[.]160[.]32[.]116`|8,008|1,002|

The table shows the source IP addresses with the highest recorded activity during the reporting period.

## 5. Authentication Analysis

Cowrie recorded 41,740 `cowrie.login.success` events and 590 `cowrie.login.failed` events during the reporting period. A `cowrie.login.success` event indicates that the honeypot accepted the submitted credentials, not that an attacker accessed a real production system.

The following tables show the most frequently recorded usernames and passwords. They are ranked independently, without combining usernames and passwords into pairs.

### 5.1 Top 10 Usernames

|Username|Attempts|
|---|---|
|`root`|7,763|
|`admin`|4,217|
|`0`|1,148|
|`deploy`|376|
|`enable\x00`|368|
|`support`|350|
|`user`|286|
|`default`|273|
|`guest`|273|
|`ubuntu`|156|

### 5.2 Top 10 Passwords

|Password|Attempts|
|---|---|
|`admin`|3,051|
|`0`|1,169|
|`123456`|758|
|`12345`|462|
|`xc3511`|440|
|_(blank password)_|435|
|`vizxv`|387|
|`linuxshell\x00`|368|
|`password`|352|
|`1234`|344|

## 6. File-Download Activity

### 6.1 Download Overview

| Metric                                                              | Count |
| ------------------------------------------------------------------- | ----: |
| Successful file-download events (`cowrie.session.file_download`)    | 2,043 |
| Failed file-download events (`cowrie.session.file_download.failed`) |   623 |

During the reporting period, Cowrie recorded **2,043 successful file downloads** and **623 failed file-download attempts**.

### 6.2 Notable Download URLs

|URL|Events|
|---|---:|
|`hxxp://130[.]12[.]180[.]212/x86_64`|827|
|`hxxp://176[.]65[.]139[.]40/wget.sh`|17|
|`hxxp://176[.]65[.]139[.]40/curl.sh`|16|
|`hxxp://160[.]119[.]66[.]206/bins/net.x86_64`|16|
|`hxxp://176[.]65[.]139[.]40/ftpget.sh`|16|
|`hxxp://176[.]65[.]139[.]40/jklarm`|16|
|`hxxp://176[.]65[.]139[.]40/jklarm5`|16|
|`hxxp://176[.]65[.]139[.]40/jklarm6`|16|
|`hxxp://176[.]65[.]139[.]40/jklarm7`|16|
|`hxxp://103[.]170[.]217[.]170/sora.sh`|13|
|`hxxp://160[.]119[.]66[.]206/bins/kla.sh`|10|

These are the leading URLs in the weekly results. URL paths may resemble executable or script names, but names alone do not establish file contents or intent.

### 6.3 Sources Associated with the Leading Download URL

|Source IP Address|Events|Sessions|
|---|---:|---:|
|`175[.]198[.]129[.]21`|436|218|
|`14[.]192[.]245[.]125`|117|59|
|`110[.]144[.]172[.]240`|74|37|
|`211[.]251[.]11[.]198`|34|17|
|`61[.]76[.]97[.]173`|26|13|
|`128[.]106[.]218[.]100`|22|11|
|`1[.]220[.]67[.]2`|16|9|
|`112[.]163[.]169[.]164`|10|5|
|`182[.]117[.]239[.]155`|10|7|
|`112[.]239[.]100[.]91`|8|4|

The table lists the source IP addresses most frequently associated with downloads from the URL.

## 7. Focused Investigation: Download URL and Related Intelligence

External reputation and sample intelligence in this section were reviewed on **16 October 2026**. Cowrie observations are identified separately from third-party findings.

### 7.1 URL and Hash Scope

The URL `hxxp://130[.]12[.]180[.]212/x86_64` appeared in 827 successful Cowrie file-download events across 421 sessions. Cowrie recorded 13 different hashes for these downloads. The three most common hashes accounted for 720 events (87.1%) and were selected for further review. The largest source associated with the URL was `175[.]198[.]129[.]21`, with 436 events across 218 sessions.

### 7.2 Three Most Frequent Hashes

| Rank | SHA-256                                                            | Cowrie events | Sessions | Source IPs | Leading source (events; sessions) | VirusTotal detections (16 Oct 2026) |
| ---: | ------------------------------------------------------------------ | ------------: | -------: | ---------: | --------------------------------- | ----------------------------------- |
|    1 | `e5f1c2ec78b2d1bede0ef4502e1b9acb00ca6dcb34468937075b3c5d56f811ec` |           496 |      251 |         21 | `175[.]198[.]129[.]21` (282; 141) | 32/64                               |
|    2 | `cc0e9d0184c0b930381446b6891769a35711b38c6a57303482e3115f921d4edc` |           116 |       59 |         10 | `110[.]144[.]172[.]240` (74; 37)  | 29/64                               |
|    3 | `ee6413677285cabe73fc602a8f37cfce0431c084e1faa469cde8028d97c70d92` |           108 |       56 |          4 | `175[.]198[.]129[.]21` (96; 48)   | 31/63                               |

The three most frequently observed hashes accounted for **720 download events across 366 sessions**. The URL appeared in 421 sessions overall. As shown in the table, each hash was associated with a different number of source IP addresses.

VirusTotal classified all three files as **trojan.mirai/cling**. Its automated Code Insight summaries described behaviour associated with Linux IoT botnets, including Telnet propagation, persistence and denial-of-service capabilities. The review covered only these three hashes; the other ten were not assessed.

### 7.3 Download Server IP: `130[.]12[.]180[.]212`

The server IP appears in the Cowrie-observed download URL. External reputation services reported:

- **VirusTotal:** 7/92 detections; community score −11.
- **AbuseIPDB:** Abuse-confidence score 100% from 115 reports.
- **Cisco Talos:** IP reputation Poor; web reputation Neutral.
- **GreyNoise:** Not Observed.
- **RIPEstat:** `130[.]12[.]180[.]0/24`, AS202412.

These are reputation and registration findings, separate from Cowrie telemetry.

### 7.4 Related Domain: `xya[.]supercrone[.]cc`

VirusTotal’s **Relations** view associated `xya[.]supercrone[.]cc` with `130[.]12[.]180[.]212`; this is an external relationship and the domain was not directly observed in the Cowrie logs. VirusTotal listed the domain creation date as 8 October 2026 and 3/92 detections. [ThreatFox IOC 1958283](https://threatfox.abuse.ch/ioc/1958283/) separately lists the domain as an Aisuru `botnet_cc` indicator, with 100% confidence, first seen 9 October 2026 at 10:20 UTC, and tags including DDoS and Mirai. ThreatFox supports the domain’s external threat-intelligence context; it is not the source of the domain-to-IP relationship and does not establish a Cowrie connection.

## 8. Indicators for Monitoring

| Indicator Type | Indicator                                                          | Evidence and Context                                                                                                   |
| -------------- | ------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------- |
| IP address     | `130[.]12[.]180[.]212`                                             | Server address in the Cowrie-observed download URL; external reputation findings in Section 7.3.                       |
| URL            | `hxxp://130[.]12[.]180[.]212/x86_64`                               | 827 successful download events across 421 sessions; 5 failed-download events.                                          |
| SHA-256        | `e5f1c2ec78b2d1bede0ef4502e1b9acb00ca6dcb34468937075b3c5d56f811ec` | 496 Cowrie events; VirusTotal 32/64 detections, reviewed 16 Oct 2026; trojan.mirai/cling.                              |
| SHA-256        | `cc0e9d0184c0b930381446b6891769a35711b38c6a57303482e3115f921d4edc` | 116 Cowrie events; VirusTotal 29/64 detections, reviewed 16 Oct 2026; trojan.mirai/cling.                              |
| SHA-256        | `ee6413677285cabe73fc602a8f37cfce0431c084e1faa469cde8028d97c70d92` | 108 Cowrie events; VirusTotal 31/63 detections, reviewed 16 Oct 2026; trojan.mirai/cling.                              |
| Domain         | `xya[.]supercrone[.]cc`                                            | VirusTotal Relations associated it with the download IP; ThreatFox lists it as Aisuru `botnet_cc`; not seen in Cowrie. |
| IP address     | `175[.]198[.]129[.]21`                                             | Largest source for the download URL: 436 events across 218 sessions.                                                   |

The URL had 13 distinct hashes in total. The three listed hashes account for 720 of its 827 successful download events; the other 10 are not detailed here.

## 9. Conclusion

During the reporting period, Cowrie recorded widespread activity, including login attempts, commands and file downloads. The review highlighted one frequently used download URL, which accounted for 827 successful downloads across 421 sessions. Three files made up most of this activity and were identified by VirusTotal as related to Mirai/Cling malware.

The weekly review and the focused investigation show the value of examining honeypot activity alongside external information about downloaded files. The findings identify activity worth monitoring, but do not identify who was responsible.

## 10. Limitations

This report is based on logs from a single Cowrie honeypot. Event counts show recorded activity, not the number of individual attackers. VirusTotal and ThreatFox provide external assessments that may change over time. The domain `xya[.]supercrone[.]cc` was not observed in Cowrie; its association with the download IP comes from VirusTotal Relations, and its Aisuru classification comes from ThreatFox.



