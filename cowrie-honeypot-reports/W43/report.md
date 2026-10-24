# Weekly Cowrie Honeypot Activity Report

**Report ID:** W43 | **TLP:** Clear  

**Prepared by:** Berkay Vagas  
**Reporting Period:** 16-23 October 2026  
**Data Source:** Cowrie Honeypot Logs  
**Analysis Platform:** Splunk

## 1. Executive Summary

During the reporting period, the Cowrie honeypot recorded **340,772 events** from **1,445 unique source IP addresses**. The activity included repeated authentication attempts, command interactions, and downloads of potentially malicious files.

A focused investigation identified recurring malware-delivery activity involving `176.65.139.40`. External threat-intelligence sources associate the investigated shell scripts with the Mirai malware family. The observed commands indicate attempts to retrieve and execute binaries targeting multiple system architectures.

The investigation identified **110 download events associated with 23 distinct SHA-256 values** in the reviewed Splunk results. Three investigated scripts, `wget.sh`, `ftpget.sh`, and `curl.sh`, were associated with downloader or Mirai-related classifications in external threat-intelligence sources.

## 2. Scope and Methodology

This report covers Cowrie honeypot activity recorded between 16 and 22 October 2026. Splunk Enterprise was used to analyse event volumes, event types, source IP addresses, authentication attempts, and file-download activity.

The analysis used the Splunk search time range from 16 October 2026 at 00:00:00 to 23 October 2026 at 00:00:00, covering the seven-day reporting period. Weekly metrics were obtained using Splunk searches against the Cowrie index.

A focused investigation examined download-related activity associated with `176.65.139.40`. Cowrie observations were correlated with external threat-intelligence findings from MalwareBazaar, VirusTotal, and ThreatFox, alongside the supplied behavioural analysis.

The analysis distinguished observed honeypot activity from external intelligence assessments. Download records and execution commands were reviewed as evidence of attempted behaviour, without assuming that every attempted execution succeeded.

## 3. Weekly Activity Overview

### 3.1 Key Metrics

|Metric|Value|
|---|---|
|Total events|340,772|
|Unique source IP addresses|1,445|
|Unique event types|24|
|Successful login events|31,514|
|Failed login events|307|
|Successful file-download events|1,553|
|Failed file-download events|125|
|Total file-download events|1,678|

The honeypot recorded substantial automated activity, including login events, command interactions, and repeated file-download attempts. Successful Cowrie login events represent activity recorded within the simulated honeypot environment and do not establish access to a real production system.

### 3.2 Top 10 Event Types

|Event Type|Count|
|---|---|
|`cowrie.command.input`|77,229|
|`cowrie.session.closed`|36,698|
|`cowrie.session.connect`|36,693|
|`cowrie.login.success`|31,514|
|`cowrie.client.version`|30,964|
|`cowrie.client.kex`|30,344|
|`cowrie.log.closed`|30,185|
|`cowrie.session.params`|30,183|
|`cowrie.command.failed`|14,480|
|`cowrie.command.success`|14,336|

Command-input and session-lifecycle events were prominent in the collected telemetry, reflecting repeated automated interactions with the honeypot.

## 4. Weekly Source IP Analysis

### 4.1 Top 10 Source IP Addresses

| Source IP Address | Events | Sessions |
|---|---:|---:|
| `109[.]160[.]32[.]156` | 13,596 | 1,697 |
| `109[.]160[.]32[.]49` | 13,575 | 1,698 |
| `109[.]160[.]32[.]114` | 13,538 | 1,694 |
| `132[.]148[.]73[.]100` | 11,601 | 800 |
| `101[.]226[.]198[.]20` | 11,327 | 2,750 |
| `109[.]160[.]32[.]109` | 9,574 | 1,198 |
| `109[.]160[.]32[.]165` | 9,574 | 1,198 |
| `109[.]160[.]32[.]45` | 9,574 | 1,198 |
| `109[.]160[.]32[.]46` | 9,569 | 1,197 |
| `109[.]160[.]32[.]161` | 9,566 | 1,197 |

These addresses generated the highest recorded event volumes during the reporting period. Event volume alone does not establish that each source IP belongs to a distinct threat actor or malware campaign.

## 5. Authentication Analysis

### 5.1 Top 10 Usernames

|Username|Attempts|
|---|---|
|`root`|6,736|
|`admin`|3,129|
|`deploy`|515|
|`ubuntu`|454|
|`user`|356|
|`test`|202|
|`345gs5662d34`|189|
|`user1`|133|
|`claude`|123|
|`support`|123|

The observed usernames include common administrative and default account names frequently targeted by automated SSH login attempts.

### 5.2 Top 10 Passwords

|Password|Attempts|
|---|---|
|`admin`|2,315|
|`123456`|975|
|`123`|482|
|`1234`|433|
|`root`|286|
|`12345678`|282|
|`password`|277|
|`12345`|253|
|_(blank)_|227|
|`1`|211|

The password distribution shows repeated use of common and weak credentials. These values are observed honeypot inputs, not evidence of credentials successfully used against a production service.

## 6. File-Download Activity

### 6.1 Download Overview

|Metric|Value|
|---|---|
|Successful download events|1,553|
|Failed download events|125|
|Total download events|1,678|

The download telemetry includes multiple remote payload locations. The focused investigation below examines recurring activity associated with `176.65.139.40`.

### 6.2 Notable Download URLs

| URL | Successful Events |
|---|---:|
| `hxxp://130[.]12[.]180[.]212/x86_64` | 231 |
| `ftp://176[.]65[.]139[.]40/ftpget.sh` | 10 |
| `ftp://176[.]65[.]139[.]40/jklarm` | 10 |
| `ftp://176[.]65[.]139[.]40/jklarm5` | 10 |
| `ftp://176[.]65[.]139[.]40/jklarm6` | 10 |
| `ftp://176[.]65[.]139[.]40/jklarm7` | 10 |
| `hxxp://176[.]65[.]139[.]40/curl.sh` | 10 |
| `hxxp://176[.]65[.]139[.]40/jklarm` | 10 |
| `hxxp://176[.]65[.]139[.]40/jklarm5` | 10 |
| `hxxp://176[.]65[.]139[.]40/jklarm6` | 10 |
| `hxxp://176[.]65[.]139[.]40/jklarm7` | 10 |
| `hxxp://176[.]65[.]139[.]40/wget.sh` | 10 |

The URL-level results show repeated retrieval activity involving downloader scripts and architecture-specific payload names. HTTP and FTP URLs are listed separately, even when they reference the same filename.

## 7. Focused Investigation: `176[.]65[.]139[.]40`

### 7.1 Infrastructure and Source Activity

Ten source IP addresses were associated with download-related activity involving `176.65.139.40` in the reviewed records.

| No. | Source IP Address |
|---:|---|
| 1 | `1[.]182[.]14[.]138` |
| 2 | `5[.]232[.]166[.]129` |
| 3 | `79[.]189[.]47[.]121` |
| 4 | `105[.]224[.]47[.]137` |
| 5 | `111[.]176[.]97[.]158` |
| 6 | `113[.]221[.]26[.]111` |
| 7 | `119[.]99[.]164[.]191` |
| 8 | `154[.]126[.]166[.]61` |
| 9 | `177[.]66[.]95[.]54` |
| 10 | `196[.]218[.]16[.]51` |

The reviewed records show recurring requests for `wget.sh`, `ftpget.sh`, `curl.sh`, and the `jklarm` payload series. The aggregate Splunk query returned **110 download events and 23 distinct recorded SHA-256 values**.

### 7.2 Malware Identification

External threat intelligence associates the investigated scripts with Mirai-related malware delivery or downloader activity.

|Filename|SHA-256|Intelligence Finding|
|---|---|---|
|`wget.sh`|`7b8cd695424f9b004b459ce886d92e9a24f38957dc9071510ab669a7cb89c417`|MalwareBazaar identifies the sample as Mirai; VirusTotal label: `trojan.shell/mirai`.|
|`ftpget.sh`|`964ad06953d28bff625b49a6f90a721d13eda1128f9098ad0e2586931da6274c`|MalwareBazaar lists downloader-related activity; VirusTotal label: `trojan.shell/abdownloader`.|
|`curl.sh`|`b965f772177c2e79bff3739cdffa544d357e16441bdd833428aae067fe52dd65`|ThreatFox identifies the hash as a Mirai/Katana-associated payload with 90% confidence; MalwareBazaar also labels it Mirai.|

The supplied analysis describes scripts that retrieve architecture-specific binaries, modify file permissions, attempt execution with the `selfrep` argument, and remove downloaded files and scripts. This behaviour is consistent with a multi-architecture Mirai-style delivery chain.

These classifications are external intelligence findings. They support the assessment but do not independently prove that a payload executed successfully during a particular Cowrie session.

### 7.3 Observed Behaviour and ATT&CK Mapping

The supplied behavioural analysis records attempted downloads of binaries targeting ARM, MIPS, PowerPC, SH4, SPARC, M68K, and x86 architectures. Other observed commands include file permission changes, execution attempts, and cleanup operations.

The supplied ATT&CK mapping associates the observed behaviour with the following techniques:

|Technique|ID|Relevance|
|---|---|---|
|Command and Scripting Interpreter|T1059|Commands and shell-script activity|
|Scripting|T1064|Script-based execution behaviour in the supplied mapping|
|Software Discovery|T1518|Discovery-related behaviour in the supplied mapping|
|Ingress Tool Transfer|T1105|Attempted retrieval of remote scripts and binaries|

These mappings are analyst or tool classifications of observed behaviour. They should not be interpreted as proof that every technique succeeded.

### 7.4 Assessment

The combination of Cowrie download records, recurring payload filenames, observed command patterns, and external threat intelligence strongly supports classifying the activity as **Mirai-associated malware delivery**.

The evidence supports attempted retrieval and execution behaviour across multiple architectures. It does not establish that all downloaded binaries executed successfully or that the activity resulted in compromise outside the simulated Cowrie environment.

## 8. Indicators for Monitoring

| Indicator | Type | Context |
|---|---|---|
| `176[.]65[.]139[.]40` | IPv4 address | Observed payload host |
| `7b8cd695424f9b004b459ce886d92e9a24f38957dc9071510ab669a7cb89c417` | SHA-256 | `wget.sh`, Mirai-labelled downloader |
| `964ad06953d28bff625b49a6f90a721d13eda1128f9098ad0e2586931da6274c` | SHA-256 | `ftpget.sh`, downloader classification |
| `b965f772177c2e79bff3739cdffa544d357e16441bdd833428aae067fe52dd65` | SHA-256 | `curl.sh`, Mirai/Katana-associated sample |
| `/jklarm`, `/jklarm5`, `/jklarm6`, `/jklarm7` | URL paths | Architecture-specific payload retrieval |
| `/jklm68k`, `/jklmips`, `/jklmpsl`, `/jklppc`, `/jklsh4`, `/jklspc`, `/jklx86` | URL paths | Additional architecture-specific payloads |
| `selfrep` | Command argument | Observed in attempted payload execution commands |

These indicators can be used to correlate future honeypot events and relevant security telemetry. The IP address and URL paths should be treated as observed infrastructure indicators, not permanent identifiers of a single threat actor.

## 9. Conclusion

The Cowrie honeypot recorded substantial automated SSH activity during 16-22 October 2026, including authentication attempts, command interactions, and file downloads. The weekly report records **340,772 events from 1,445 unique source IP addresses**.

The focused investigation of `176.65.139.40` found strong evidence of a Mirai-associated, multi-architecture malware-delivery operation. The reviewed Splunk results contain 110 download events associated with 23 distinct hashes, and external threat intelligence supports the classification of the three investigated scripts.

The findings demonstrate observed and attempted activity in the honeypot. They do not establish successful execution of every payload or compromise of a real production system.

## 10. Limitations

- Cowrie records simulated interactions and does not independently prove compromise of a real operating system.
    
- External threat-intelligence classifications can change and should be rechecked before operational use.
    
- ATT&CK mappings describe classified behaviour and do not prove successful execution of every technique.
    
- The presence of a hash in a threat-intelligence database does not, by itself, prove that the corresponding file executed successfully during a honeypot session.
