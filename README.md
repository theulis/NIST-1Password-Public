# 1Password Vulnerabilities for macOS

## Description

This Python script retrieves all known CVEs (Common Vulnerabilities and Exposures) for 1Password macOS versions from the [NIST NVD](https://nvd.nist.gov/) (National Vulnerability Database).  It automatically:

- Gets the list of all [recent stable 1Password macOS releases](https://releases.1password.com/mac/stable/) since May 2022
- Queries the NIST NVD for CVEs for each version  
- Extracts the CVE ID and CVSS v3.1 Base Score to stdout  
- Handles network errors and retries failed requests (no NVD API key is used)  
- Displays a temporary progress bar which disappears after completion

**Sample output**
```bash
Application Name,CVE ID,CVSS Score
1Password,CVE-2022-32550,4.8
1Password,CVE-2024-42218,4.7
1Password,CVE-2024-42219,7.8
[#########-------------------------------] 23%
```

**Final Output**
```bash
Application Name,CVE ID,CVSS Score
1Password,CVE-2022-32550,4.8
1Password,CVE-2024-42218,4.7
1Password,CVE-2024-42219,7.8
```

*✅ This script has been tested on Python 3.13.7*

## Installation

Ensure Python 3.x is installed:

```bash
python3 --version
```

To download the latest Python version, go to https://www.python.org/downloads/

Since the script uses HTTPS requests to get 1Password macOS versions, it requires up-to-date SSL/TLS root certificates. Python can make secure HTTPS requests without SSL verification errors.

```bash
bash "/Applications/$(python3 -c 'import sys; print("Python {}.{}".format(sys.version_info.major, sys.version_info.minor))')/Install Certificates.command"
```

Sample instructions for downloading and running the script:

```bash
curl -o ~/NIST-CVE-1Password.py https://raw.githubusercontent.com/theulis/NIST-1Password-Public/refs/heads/main/NIST-CVE-1Password.py
chmod +x ~/NIST-CVE-1Password.py
python3 ~/NIST-CVE-1Password.py
```

## Improvements / Future Work
⚙️ As mentioned, this script does not use an official NVD API to fetch CVEs, so some requests may fail. Based on current tests, a few 1Password version vulnerability checks may fail, but this does not impact the overall results. Re-attempts have been implemented to handle this, but due to project time constraints, no further improvements will be made in this version. 

🔗 Integration with MDM can be implemented to fetch the currently used versions of 1Password. Example: [Kandji Prism API](https://api-docs.kandji.io/#0de36993-c9d8-4d58-8dce-a2616bc2e743)
For more info, check Repo: https://github.com/theulis/NIST-1Password-Kandji-Public ✅
