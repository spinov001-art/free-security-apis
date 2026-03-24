# Free Security APIs

> Curated list of free APIs for cybersecurity, threat intelligence, and vulnerability scanning

## IP Reputation & Threat Intelligence

| API | Free Tier | Best For |
|-----|-----------|----------|
| [AbuseIPDB](https://www.abuseipdb.com/) | 1,000 checks/day | IP abuse reports, blacklists |
| [GreyNoise](https://www.greynoise.io/) | 50/day | Noise filtering, scanner detection |
| [Shodan](https://www.shodan.io/) | 100 results/search | Device fingerprinting, port scanning |
| [IPinfo](https://ipinfo.io/) | 50K/month | IP geolocation, ASN data |
| [ip-api](http://ip-api.com/) | 45/min | Basic IP geolocation (no key needed) |

## Malware & File Scanning

| API | Free Tier | Best For |
|-----|-----------|----------|
| [VirusTotal](https://www.virustotal.com/) | 4/min | File & URL multi-engine scanning |
| [MalwareBazaar](https://bazaar.abuse.ch/) | Unlimited | Malware sample database |
| [URLhaus](https://urlhaus.abuse.ch/) | Unlimited | Malicious URL database |

## Email & Identity

| API | Free Tier | Best For |
|-----|-----------|----------|
| [Have I Been Pwned](https://haveibeenpwned.com/) | 10/min | Email breach checking |
| [EmailRep](https://emailrep.io/) | 20/day | Email reputation scoring |
| [Hunter.io](https://hunter.io/) | 25/month | Email verification |

## Domain & DNS

| API | Free Tier | Best For |
|-----|-----------|----------|
| [RDAP (IANA)](https://rdap.org/) | Unlimited | Domain registration (replacing WHOIS) |
| [SecurityTrails](https://securitytrails.com/) | 50/month | DNS history, subdomains |
| [crt.sh](https://crt.sh/) | Unlimited | Certificate transparency logs |

## Vulnerability Databases

| API | Free Tier | Best For |
|-----|-----------|----------|
| [NVD](https://nvd.nist.gov/) | 50/30sec | CVE vulnerability database |
| [OSV](https://osv.dev/) | Unlimited | Open-source vulnerability database |
| [GitHub Advisories](https://github.com/advisories) | Via GraphQL | GitHub security advisories |
| [npm Audit](https://docs.npmjs.com/) | Unlimited | npm package vulnerabilities |
| [PyPI JSON](https://pypi.org/) | Unlimited | Python package metadata |

## Quick Start: Multi-API Security Check

```python
import requests

def security_check(ip):
    # 1. Check abuse reports
    abuse = requests.get(
        "https://api.abuseipdb.com/api/v2/check",
        headers={"Key": "YOUR_KEY"},
        params={"ipAddress": ip, "maxAgeInDays": 90}
    ).json()["data"]
    
    # 2. Check if it's a known scanner
    grey = requests.get(
        f"https://api.greynoise.io/v3/community/{ip}"
    ).json()
    
    # 3. Get geolocation
    geo = requests.get(f"http://ip-api.com/json/{ip}").json()
    
    print(f"IP: {ip}")
    print(f"Country: {geo['country']} ({geo['isp']})")
    print(f"Abuse Score: {abuse['abuseConfidenceScore']}/100")
    print(f"GreyNoise: {'Scanner' if grey.get('noise') else 'Not scanning'}")
    print(f"Classification: {grey.get('classification', 'unknown')}")

security_check("185.220.101.1")
```

## Related Resources

- [IP Threat Intelligence Toolkit](https://github.com/spinov001-art/ip-threat-intelligence)
- [Email OSINT Toolkit](https://github.com/spinov001-art/email-osint-toolkit)
- [npm Security Scanner](https://github.com/spinov001-art/npm-security-scanner)
- [GitHub Advisory Scanner](https://github.com/spinov001-art/github-advisory-scanner)
- [WHOIS Lookup Tools](https://github.com/spinov001-art/whois-lookup-tools)
- [PyPI Supply Chain Checker](https://github.com/spinov001-art/pypi-supply-chain-checker)
- [Awesome Free APIs](https://github.com/spinov001-art/awesome-free-apis-2026) — 200+ free APIs
- [Awesome Web Scraping](https://github.com/spinov001-art/awesome-web-scraping)
- [SSL Certificate Monitor](https://github.com/spinov001-art/ssl-certificate-monitor) — Monitor SSL expiry, subdomain discovery
- [OSV Vulnerability Scanner](https://github.com/spinov001-art/osv-vulnerability-scanner) — Scan dependencies with Google OSV
- [URL Malware Checker](https://github.com/spinov001-art/url-malware-checker) — Check URLs against URLhaus

## License

MIT
