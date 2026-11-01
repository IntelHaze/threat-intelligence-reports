# Weekly Cowrie Honeypot Activity Report

**Report ID:** W44 | **TLP:** Clear

**Prepared by:** Berkay Vagas  
**Reporting Period:** 23-29 October 2026  
**Data Source:** Cowrie Honeypot Logs  
**Analysis Platform:** Splunk

---

# 1. Executive Summary

During 23-29 October 2026, the Cowrie honeypot recorded **619,942 events from 2,107 unique IP addresses**, showing continued attempts to access and interact with the monitored system.

The analysis identified significant login activity, repeated command execution attempts, and 2,840 file-download events. The most active source IP addresses were `109[.]160[.]32[.]159` and `77[.]239[.]124[.]151`, each generating 19,148 events.

A closer investigation of `109[.]160[.]32[.]159` found repeated attempts to gather information about the monitored system. External security services also identified this IP as suspicious or malicious.

Another source, `176[.]65[.]139[.]40`, was responsible for the most frequently observed file-download activity during the week.

Overall, the findings show continued automated activity targeting the honeypot. The identified IP addresses and download sources should remain under observation.
# 2. Scope and Methodology

This report covers activity recorded by the Cowrie SSH honeypot between **23 and 29 October 2026**.

Data was collected and analysed using Splunk Enterprise, covering the full reporting period from 23 October 2026, 00:00:00, to 30 October 2026, 00:00:00 (exclusive).

The analysis focused on:

- Overall event volume and event distribution.
    
- Source IP addresses and session activity.
    
- Authentication attempts and commonly used credentials.
    
- File-download activity and requested URLs.
    
- Investigation of selected high-activity source IP addresses.
    
- External threat intelligence from VirusTotal, GreyNoise, AbuseIPDB, and Cisco Talos.
    

The report distinguishes between activity directly observed by the honeypot and information obtained from external intelligence sources.

Successful login events represent interactions accepted by the simulated Cowrie environment and do not indicate access to real production systems.

External intelligence information was reviewed on 1 November 2026 and may include activity outside the reporting period.
# 3. Weekly Activity Overview

## 3.1 Key Metrics

|             Metric              |  Value  |
| :-----------------------------: | :-----: |
|          Total events           | 619,942 |
|   Unique source IP addresses    |  2,107  |
|       Unique event types        |   25    |
|     Successful login events     | 44,931  |
|       Failed login events       |   165   |
| Successful file-download events |  2,581  |
|   Failed file-download events   |   259   |
|   Total file-download events    |  2,840  |

The daily event distribution showed an increase in overall activity during the middle of the reporting period. The highest daily event volume was recorded on 28 October, with 123,235 events.

Daily event distribution:

|      Date       | Total Events |
| :-------------: | :----------: |
| 23 October 2026 |    53,459    |
| 24 October 2026 |    57,619    |
| 25 October 2026 |    93,446    |
| 26 October 2026 |    95,237    |
| 27 October 2026 |   111,024    |
| 28 October 2026 |   123,235    |
| 29 October 2026 |    85,922    |
|    **Total**    | **619,942**  |

## 3.2 Top 10 Event Types

|        Event Type        |  Count  |
| :----------------------: | :-----: |
|  `cowrie.command.input`  | 176,858 |
| `cowrie.command.success` | 88,605  |
| `cowrie.session.connect` | 49,341  |
| `cowrie.session.closed`  | 49,311  |
|  `cowrie.login.success`  | 44,931  |
| `cowrie.client.version`  | 44,523  |
|   `cowrie.client.kex`    | 44,273  |
|   `cowrie.log.closed`    | 42,259  |
| `cowrie.session.params`  | 42,258  |
| `cowrie.command.failed`  | 15,724  |

Command input events represented the largest event category, indicating substantial command interaction within the honeypot environment.

# 4. Weekly Source IP Analysis

Source IP analysis identified 2,107 unique addresses during W44. The distribution of events showed that a relatively small group of source IP addresses generated a substantial volume of honeypot activity.

## 4.1 Top 10 Source IP Addresses

The following table presents the ten most active source IP addresses, ranked by event volume.

| Source IP Address | Events | Sessions |
| :---------------: | :----: | :------: |
| `109[.]160[.]32[.]159`  | 19,148 |  2,396   |
| `77[.]239[.]124[.]151`  | 19,148 |  2,396   |
|  `176[.]65[.]139[.]40`  | 18,191 |   596    |
|  `109[.]160[.]32[.]49`  | 11,995 |  1,198   |
|  `106[.]75[.]27[.]155`  | 11,789 |   506    |
| `101[.]226[.]198[.]20`  | 11,173 |  2,637   |
| `179[.]43[.]133[.]154`  | 11,000 |   999    |
| `109[.]160[.]32[.]132`  | 10,823 |  1,197   |
| `109[.]160[.]32[.]146`  | 10,059 |  1,197   |
|  `109[.]160[.]32[.]42`  | 9,575  |  1,198   |

The IP address `109[.]160[.]32[.]159` generated 19,148 events across 2,396 unique sessions. 

# 5. Authentication Analysis

Authentication analysis examined the usernames and passwords submitted during interactions with the Cowrie honeypot.

The following results represent recorded credential inputs across successful and failed login events. They should not be interpreted as failed authentication attempts exclusively.

## 5.1 Top 10 Usernames

|    Username    | Attempts |
| :------------: | :------: |
|     `root`     |  14,455  |
|    `admin`     |  3,226   |
|      `0`       |  1,514   |
|    `ubuntu`    |  1,267   |
|    `deploy`    |   998    |
|     `user`     |   826    |
| `345gs5662d34` |   682    |
|     `test`     |   486    |
|    `user1`     |   370    |
|    `claude`    |   321    |

The `root` username was the most frequently observed credential input, followed by `admin` and `0`.
## 5.2 Top 10 Passwords

|    Password     | Attempts |
| :-------------: | :------: |
|    `123456`     |  2,333   |
|     `admin`     |  1,989   |
|       `0`       |  1,577   |
|      `123`      |  1,231   |
|     `1234`      |   961    |
| `345gs5662d34`  |   682    |
| `3245gs5662d34` |   677    |
|   `12345678`    |   643    |
|       `1`       |   551    |
|     `root`      |   548    |

The most frequently observed passwords included common numeric sequences, default-style credentials, and administrative terms.

# 6. File-Download Activity

File-download activity was analysed to identify URLs requested through the honeypot and to assess the volume of successful and failed download events.

## 6.1 Download Overview

|           Metric           | Value |
| :------------------------: | :---: |
| Successful download events | 2,581 |
|   Failed download events   |  259  |
|   Total download events    | 2,840 |

The honeypot recorded 2,581 successful file-download events and 259 failed file-download events during W44.

These values represent Cowrie download event counts and should not be interpreted as the number of unique files or distinct malware samples.

## 6.2 Notable Download URLs

The following URLs were the ten most frequently observed successful file-download event URLs during the reporting period.

|               URL               | Successful Events |
| :-----------------------------: | :---------------: |
| `hxxp://176[.]65[.]139[.]40/wget.sh`  |        154        |
| `hxxp://176[.]65[.]139[.]40/curl.sh`  |        147        |
|  `hxxp://176[.]65[.]139[.]40/jklarm`  |        147        |
| `hxxp://176[.]65[.]139[.]40/jklarm5`  |        147        |
| `hxxp://176[.]65[.]139[.]40/jklarm6`  |        147        |
| `hxxp://176[.]65[.]139[.]40/jklarm7`  |        147        |
| `ftp://176[.]65[.]139[.]40/ftpget.sh` |        144        |
|  `ftp://176[.]65[.]139[.]40/jklarm`   |        144        |
|  `ftp://176[.]65[.]139[.]40/jklarm5`  |        144        |
|  `ftp://176[.]65[.]139[.]40/jklarm6`  |        144        |

These URL observations identify potentially relevant download infrastructure. However, the filenames and URLs alone do not establish the contents, functionality, or malware classification of the downloaded files.

# 7. Focused Investigation: 109[.]160[.]32[.]159

## 7.1 Infrastructure and Source Activity

The IP address `109[.]160[.]32[.]159` was selected for focused investigation due to its high activity volume during W44.

The address generated 19,148 events across 2,396 unique sessions, making it one of the two most active source IP addresses identified during the reporting period.

Infrastructure information obtained from external threat intelligence services identified the following details:

| Attribute                                     | Value                               |
| :-------------------------------------------- | :---------------------------------- |
| Source IP Address                             | `109[.]160[.]32[.]159`                    |
| ASN                                           | AS198364                            |
| Network Organization (VirusTotal / GreyNoise) | Banatsync SRL                       |
| ISP (AbuseIPDB / Talos)                       | Global Communication Net Plc        |
| Network Range                                 | `109[.]160[.]32[.]0/24`                   |
| Country (VirusTotal / Talos)                  | Bulgaria                            |
| Country (GreyNoise / AbuseIPDB)               | Netherlands                         |
| Usage Context                                 | Data Center / Web Hosting / Transit |

The geographic and organization information varies between providers. The available records therefore do not establish a definitive physical location or ownership relationship.

#### Source IP Address

| No. | Source IP Address |
| :-: | :---------------: |
|  1  | `109[.]160[.]32[.]159`  |

### External Threat Intelligence Findings

#### VirusTotal

VirusTotal reported that 10 out of 92 security vendors flagged the IP address as malicious. The community score was -4.

A crowdsourced report attributed to Guardpot described SSH brute-force activity combined with network scanning. The report identified 1,037 events involving two attack vectors:

- SSH brute-force login attempts: 999 events.
    
- TCP port scanning / network reconnaissance: 38 events.
    

The reported observation period began on 1 October 2026 and extended to 31 October 2026.

#### GreyNoise

GreyNoise classified the IP address as malicious and identified it as a scanner. The spoofable status was reported as false, while the associated actor was listed as unknown.

GreyNoise also associated the address with the following activity tags:

- SSH Bruteforcer
    
- SSH Connection Attempt
    
- SSH Alternative Port Crawler
    
- Generic Sensitive File Access Attempt
    
- Generic Path Traversal Attempt
    

The service reported the IP as last seen on 1 November 2026.

#### AbuseIPDB

AbuseIPDB reported an abuse confidence score of 100%, supported by 4,007 reports submitted by 893 distinct sources.

The first report was recorded on 27 September 2026, while the most recent report was recorded on 1 November 2026.

Recent reports primarily described SSH brute-force activity, repeated authentication failures, and Fail2Ban detections.

The listed usage type was Data Center / Web Hosting / Transit.

#### Cisco Talos

Cisco Talos assigned the IP address a Poor sender IP reputation and a Neutral web reputation.

The address was listed on the Talos Security Intelligence Block List (SIBL) under the attackers classification.

The listing details were:

- First Seen: 28 September 2026.
    
- Expiration Date: 7 November 2026.
    
- Status: Active.
    
- Classification: Attackers.
    

The listed status indicates that the IP was present on the Talos block list at the time of the intelligence review.

## 7.2 Malware Identification

During the W44 investigation, the Cowrie honeypot recorded no `cowrie.session.file_download` events associated with `109[.]160[.]32[.]159`.

Consequently, no malware sample, downloaded filename, or associated file hash could be identified from the available Cowrie data.

|    Filename    |    SHA-256    |                                     Intelligence Finding                                      |
| :------------: | :-----------: | :-------------------------------------------------------------------------------------------: |
| Not identified | Not available | No file-download events or associated malware samples were identified for this IP during W44. |

Although external intelligence sources classify the IP as malicious, the available evidence does not establish that this source delivered malware to the Cowrie honeypot during the reporting period.

## 7.3 Observed Behaviour and ATT&CK Mapping

The Cowrie logs show a highly repetitive pattern of SSH interactions originating from `109[.]160[.]32[.]159`.

The event distribution for this IP was:

|        Event Type        |   Events   |
| :----------------------: | :--------: |
|   `cowrie.client.kex`    |   2,396    |
| `cowrie.client.version`  |   2,396    |
| `cowrie.session.closed`  |   2,396    |
| `cowrie.session.connect` |   2,396    |
|  `cowrie.command.input`  |   2,390    |
|   `cowrie.log.closed`    |   2,390    |
|  `cowrie.login.success`  |   2,390    |
| `cowrie.session.params`  |   2,390    |
|  `cowrie.login.failed`   |     4      |
|        **Total**         | **19,148** |

Following the login interactions, the honeypot recorded 2,390 command input events. All observed command inputs contained the following command:

```
uname -s -v -n -r -m
```

This command retrieves operating system and kernel information, including the kernel name, version, hostname, release, and machine architecture.

The repeated execution of this command indicates systematic system information discovery behaviour.

The observed activity can be mapped to the following MITRE ATT&CK technique:

|          Technique           |  ID   |                                                  Relevance                                                  |
| :--------------------------: | :---: | :---------------------------------------------------------------------------------------------------------: |
| System Information Discovery | T1082 | The source repeatedly submitted `uname -s -v -n -r -m` to retrieve operating system and kernel information. |

## 7.4 Assessment

The investigation identified `109[.]160[.]32[.]159` as a high-priority source for continued monitoring. Its activity was consistent with repeated SSH interactions and system information discovery, while multiple external threat intelligence platforms independently classified the IP as malicious.

No malware downloads or associated samples were identified within the honeypot during the reporting period. Although the available evidence does not support attribution to a specific threat actor or malware family, the combined findings indicate that the IP is associated with suspicious network activity.

# 8. Indicators for Monitoring

The following indicators were identified during the W44 analysis and are recommended for continued monitoring.

|            Indicator            |     Type     |                                                           Context                                                            |
| :-----------------------------: | :----------: | :--------------------------------------------------------------------------------------------------------------------------: |
|        `109[.]160[.]32[.]159`         | IPv4 Address | High-volume source observed in 2,396 Cowrie sessions; malicious classifications reported by multiple intelligence providers. |
|         `176[.]65[.]139[.]40`         | IPv4 Address |                      Source associated with the ten most frequently observed download URLs during W44.                       |
| `hxxp://176[.]65[.]139[.]40/wget.sh`  |     URL      |                         Most frequently observed download URL, with 154 successful download events.                          |
| `hxxp://176[.]65[.]139[.]40/curl.sh`  |     URL      |                                  Observed download URL with 147 successful download events.                                  |
|  `hxxp://176[.]65[.]139[.]40/jklarm`  |     URL      |                                  Observed download URL with 147 successful download events.                                  |
| `hxxp://176[.]65[.]139[.]40/jklarm5`  |     URL      |                                  Observed download URL with 147 successful download events.                                  |
| `hxxp://176[.]65[.]139[.]40/jklarm6`  |     URL      |                                  Observed download URL with 147 successful download events.                                  |
| `hxxp://176[.]65[.]139[.]40/jklarm7`  |     URL      |                                  Observed download URL with 147 successful download events.                                  |
| `ftp://176[.]65[.]139[.]40/ftpget.sh` |     URL      |                                  Observed download URL with 144 successful download events.                                  |
|  `ftp://176[.]65[.]139[.]40/jklarm`   |     URL      |                                  Observed download URL with 144 successful download events.                                  |
|  `ftp://176[.]65[.]139[.]40/jklarm5`  |     URL      |                                  Observed download URL with 144 successful download events.                                  |
|  `ftp://176[.]65[.]139[.]40/jklarm6`  |     URL      |                                  Observed download URL with 144 successful download events.                                  |

The indicators listed above should be monitored for recurring connections, repeated authentication activity, reconnaissance behaviour, and file-download attempts.

The URLs are included as observed download indicators. Their inclusion does not independently confirm that the referenced files are malicious.

# 9. Conclusion

During W44, the Cowrie honeypot recorded 619,942 events from 2,107 unique source IP addresses, demonstrating continued automated activity targeting the monitored system.

The analysis highlighted significant SSH activity, repeated command execution attempts, and file-download activity. The investigation of `109[.]160[.]32[.]159` revealed repeated system information discovery behaviour, supported by malicious reputation assessments from multiple threat intelligence platforms.

Additionally, `176[.]65[.]139[.]40` was associated with the most frequently observed file-download URLs during the reporting period.

Overall, the findings highlight several sources of suspicious activity that warrant continued monitoring and further investigation.

# 10. Limitations

The findings presented in this report are subject to the following limitations:

- **Honeypot Environment:** Cowrie simulates an SSH environment. Successful login events do not indicate access to real production systems.
    
- **Event-Based Measurements:** Event counts represent recorded events and do not necessarily correspond to unique attacks, files, or malware samples.
    
- **Authentication Analysis:** Username and password statistics include credential inputs from both successful and failed login events.
    
- **Malware Verification:** No malware samples or associated file hashes were identified for `109[.]160[.]32[.]159` during W44.
    
- **External Intelligence:** Threat intelligence platforms use different data sources and classification methods. Their findings may include activity outside the reporting period.
    
- **Geolocation and Attribution:** Available intelligence does not establish the definitive physical location, infrastructure ownership, or identity of the source behind the observed activity.
    
- **Payload Execution:** Recorded command inputs do not independently confirm successful execution or the intended outcome of each command.
