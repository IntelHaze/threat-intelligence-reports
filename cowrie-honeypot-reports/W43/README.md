# W43 IOC Collection


**Report ID:** W43 | **TLP:** Clear  

**Prepared by:** Berkay Vagas  
**Reporting Period:** 16-22 October 2026  
**Data Source:** Cowrie Honeypot Logs  
**Analysis Platform:** Splunk

## Files

- `iocs.csv`: hash-to-URL associations transcribed from the supplied Splunk table, plus unique URL indicators and the observed download host.
- `stix-bundle.json`: STIX 2.1 Bundle with indicators for all 23 SHA-256 hashes, the unique URLs present in the supplied hash table, and `176[.]65[.]139[.]40`.

## Scope and caveats

- The collection includes the 23 SHA-256 values shown in the supplied Splunk output.
- Hash-to-URL relationships are copied from that output; no missing relationships have been inferred.
- Event counts and unique source IP counts are preserved as shown in the supplied table.
- These are observed indicators. This collection does not claim that every downloaded file executed successfully or independently attribute every hash to a malware family.
- The standalone URLs are the distinct URLs shown in the supplied hash table. The additional `hxxp://176[.]65[.]139[.]40/jklarm` URL is included because it appears as a related URL in the user's table.
- `report.md` was not created or modified by this task.
