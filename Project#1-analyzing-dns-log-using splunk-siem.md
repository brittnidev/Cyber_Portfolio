# Analyzing DNS Log Files Using Splunk SIEM

## Introduction
Analyzing DNS (Domain Name System) logs to increase understanding of network activity and identifying any potential security threats. Utilizing my Splunk SIEM tool I analyzed DNS logs and searched to identify any anomalies or malicious activities.

## Installing and Configuring SPLUNK
Before analyzing DNS logs in Splunk, ensure the following:
- Splunk instance is installed and configured.
- DNS log data sources are configured to forward logs to Splunk.

## Steps taken to Upload and analyze DNS Log Files in Splunk SIEM

### 1. Prepare Sample DNS Log Files
- Obtained sample [DNS log file](https://www.secrepo.com/maccdc2012/dns.log.gz) in a suitable format (e.g., text files).
- Ensured the log files contain relevant DNS events, including source IP, destination IP, domain name, query type, response code, etc.
- Saved the sample log files in a directory accessible by the Splunk instance.

### 2. Upload Log Files to Splunk
- Logged in to the Splunk web interface.
- Navigated to **Settings** > **Add Data**.
- Select **Upload** as the data input method.

### 3. Choose File
- Click on **Select File** and upload the sample file for analysis.

### 4. Set Source Type
- Under **Set Source Type** section, specified the source type for the uploaded DNS log file.
- Set source type to DNS log

### 5. Review Settings
- Reviewed other settings such as index, host, and sourcetype.
- Ensure the settings are configured correctly to match the sample DNS log file.

### 6. Click Upload
- Reviewed the settings one final time to ensure accuracy.
- **Submit** to upload the sample DNS log file to Splunk.

### 7. Verified Upload
- After uploading, navigate to the search bar in the Splunk interface.
- Ran a search query to verify that the uploaded DNS events are visible.
- *For security I have hidden my host information
  
  ```spl
  index=<your_dns_index> sourcetype=<your_dns_sourcetype>


## Steps to Analyze DNS Log Files in Splunk SIEM

### 1. Search for DNS Events   
- Entered the following search query to retrieve DNS events   
```
index=* sourcetype=dns_sample
```

### 2. Extracting Relevant Fields
- Identified key fields in DNS logs such as source IP, destination IP, domain name, query type, response code, etc.   
- Example extraction command I used:
```
index=* sourcetype=dns_sample | regex _raw="(?i)\b(dns|domain|query|response|port 53)\b"
```

### 3. Identified Anomalies
- Looked for unusual patterns or anomalies in DNS activity.
- Example of query I used to identify spikes
```
index=_* OR index=* sourcetype=dns_sample  | stats count by fqdn
```

### 4. Finding the top DNS sources
- Used the top command to count the occurrences of each query type:   
```
index=* sourcetype=dns_sample | top fqdn, src_ip
```

### 5. Investigated Suspicious Domains
- Searched for domains associated with known malicious activity or suspicious behavior.
- Utilized threat intelligence feeds and reputation databases to identify malicious domains such virustotal.com
- Example search i used for known malicious domains:
```
index=* sourcetype=dns_sample fqdn="maliciousdomain.com"
```

## Conclusion
This project demonstrates how DNS log analysis with Splunk SIEM can improve network visibility and security monitoring. By ingesting and querying DNS logs, I moved from raw data to actionable insights such as top queried domains, active sources, and potential anomalies. The approach is reproducible and scalable for real-world environments.

Key outcomes:
- Proper data ingestion and normalization enabled reliable searches and reporting.
- Identified patterns in DNS activity and highlighted potential anomalies for follow-up.
- Used threat intelligence to flag known malicious domains for further validation.

Limitations:
- Used a sample dataset; a production environment requires larger, diverse data and baselining to reduce false positives.
- Results depend on data quality and complete context from other security sources.

Next steps:
- Integrate with other logs (firewall, proxy) for richer context.
- Automate alerts for high-risk DNS activity.
- Build dashboards for ongoing monitoring and reporting.


