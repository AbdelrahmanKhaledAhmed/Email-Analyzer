# PhishyEmailAnalyzer

PhishyEmailAnalyzer is a Python-based desktop application designed to help Blue Team members and SOC analysts analyze suspicious emails in a structured and thorough way. It doesn’t automatically determine if an email is phishing, but it extracts, organizes, and presents all relevant information so that you can make an informed decision.



## Features

### Email Header Extraction
The tool extracts all main email headers, including:  
- **From, To, Subject, Date, Reply-To, Return-Path**  

All extraction is done using **regular expressions (regex)** defined in `regex.json`. This ensures accurate parsing even for unusual or malformed emails. Headers are presented clearly so you can quickly check sender details, recipients, timestamps, and reply paths.



### Authentication Analysis
PhishyEmailAnalyzer checks the email for authentication results:  
- **SPF (Sender Policy Framework)**  
- **DKIM (DomainKeys Identified Mail)**  
- **DMARC (Domain-based Message Authentication, Reporting & Conformance)**  

The tool scans the email text to determine **Pass** or **Fail** for each mechanism. It also shows the domain that was tested for SPF and DKIM, helping analysts verify if the email originates from a legitimate source.



### URL Extraction
The tool extracts **all URLs inside the email**, including:  
- Encoded URLs  
- Shortened URLs  
- Redirected URLs (nested links)  

For each URL, there are buttons to:  
- Check it on **VirusTotal** for reputation analysis  
- Open in **Browserling** for browser simulation  
- **Unshorten** shortened links for clarity  

This makes it easier to quickly inspect every link without manually decoding or copying them.



### Attachment Analysis
PhishyEmailAnalyzer scans for all attachments in the email and provides:  
- Attachment names  
- SHA-256 hash of each file (if Base64 content is available)  

For each attachment, there are buttons to:  
- Check the hash on **VirusTotal** to see if the file matches known malicious samples  
- View the original Base64 content on **CyberChef** for manual inspection  

This ensures analysts can safely examine any embedded files without executing them.



### Domain & IP Investigation
The tool identifies any **domains or IP addresses** present in the email headers or authentication results. For each domain or IP, buttons are provided to:  
- Check **VirusTotal** for reputation  
- Look up **AbuseIPDB** for reports of abuse  
- Open in **Browserling** for quick web access  
- Check domain age (Check Age) for legitimacy context  

This helps analysts quickly verify sender credibility and detect suspicious infrastructure.



## Tech Stack

- **Python** – Core programming language  
- **CustomTkinter** – GUI framework for a modern and interactive interface  
- **Regular Expressions (Regex)** – Used for parsing headers, authentication results, URLs, and attachments  
- **Base64 decoding** – For extracting file contents from Base64 blocks  
- **SHA-256 hashing** – For computing attachment hashes  



## How to Run

1. Make sure **Python 3.10+** is installed on your system.  
2. Install dependencies:  
```bash
pip install -r requirements.txt
```
3. Run the application:
```bash
python main.py
```
4. Important: Ensure regex.json and links.json are in the same folder as main.py. These files contain all regex rules and URLs used for analysis and link lookups. Without them, the tool will not function correctly.

## Notes

- The tool does not automatically classify emails as phishing or legitimate. It only organizes and presents all relevant information to help you analyze emails faster.
- All analysis (headers, URLs, attachments, domain/IP checks) is fully interactive with buttons and tooltips to make investigation easier.
- The JSON files can be modified if you want to extend regex rules or add new links for checks.
