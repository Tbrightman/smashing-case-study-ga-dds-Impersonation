# smashing-case-study-ga-dds-Impersonation
Smishing case study analyzing a Georgia DDS impersonation campaign using VirusTotal and ANY.RUN, with IOC extraction and enterprise mitigation recommendations.

## Executive Summary
I received multiple unsolicited SMS messages impersonating the **Georgia Department of Driver Services (DDS)** claiming an unresolved traffic violation and urging immediate payment. The messages contained links to lookalike domains using `.cc` TLDs and “gov-*” naming intended to appear legitimate.

I performed structured triage using **VirusTotal** and **ANY.RUN** (sandbox) to assess reputation and behavior, extracted IOCs, and documented recommended mitigations suitable for an enterprise SOC workflow.

> **Safety note:** I did not enter any personal information, did not authenticate, and did not submit payment data. Link interaction was limited to controlled analysis tooling.

---

## Timeline (High Level)
- **T0:** SMS received from unknown numbers claiming “DDS Final Notice”
- **T1:** Identified suspicious characteristics (urgent threat language, unusual domains, random query tokens)
- **T2:** Submitted URLs/domains to **VirusTotal** for reputation/detection consensus
- **T3:** Opened the URL in **ANY.RUN** sandbox to observe behavior and network indicators
- **T4:** Documented IOCs and recommended preventive/detective controls

---

## What Happened (Observed)
### SMS Lure Theme
- “Georgia Department of Driver Services (DDS) Final Notice”
- Claims payment not received; cites a Georgia Code reference
- Threatens penalties (license suspension, registration revocation, collections, adverse credit reporting)
- Provides a “payment portal” link

### Primary Suspicious Indicators
- Domains are not official government domains (not `.gov`)
- `.cc` TLD used with **lookalike naming** (e.g., `georgia.gov-*.cc`)
- Randomized query parameter token (e.g., `?var=<random>`) typical of tracking/campaign IDs
- Sender phone numbers do not match official agency contact patterns

---

## Tooling & Evidence
### 1) VirusTotal (Reputation)
- VirusTotal showed **multiple vendor detections** classifying the URL as phishing/malicious (example: 11/94 flagged).
- URL returned an HTTP status consistent with restricted/blocked access (observed `403` in VT output).

**Screenshot:** `artifacts/virustotal.png`

### 2) ANY.RUN (Sandbox Behavioral Triage)
- URL opened in a Windows sandbox environment via Microsoft Edge.
- ANY.RUN flagged the activity as **possible phishing** and labeled related network artifacts as suspicious (government-impersonation theme).
- Browser navigation resulted in an error page / non-standard behavior (e.g., page not found), which is common for short-lived phishing infrastructure or geo/UA-gated content.

**Screenshot:** `artifacts/anyrun.png`

### 3) SMS Artifacts
- Two separate SMS threads indicated similar DDS-themed messages and different lookalike domains.

**Screenshots:**
- `artifacts/sms-1.png`
- `artifacts/sms-2.png`

---

## Indicators of Compromise (IOCs)
See: **/iocs/iocs.md** and **/iocs/iocs.csv**

---

## Assessment / Conclusion
This event is consistent with a **smishing campaign** leveraging government impersonation and urgency-based social engineering to drive victims to a fraudulent payment portal. Third-party reputation (VirusTotal) and sandbox triage (ANY.RUN) support classification as **phishing/malicious**.

---

## Recommended Mitigations (Enterprise)
See: **/mitigations/recommendations.md**

Highlights:
- Block domains/URLs at DNS / Secure Web Gateway / firewall URL filtering
- Add to endpoint security IOC lists (where supported)
- Mobile device protections (MDM + web protection)
- User awareness: “agencies don’t collect fees via random SMS links”
- SOC detections for URL clicks + newly registered lookalike domains

---

## Skills Demonstrated
- Incident-style documentation and evidence handling
- IOC extraction and normalization
- Using VirusTotal and sandbox tooling safely
- Translating findings into actionable mitigations
- Clear communication suitable for SOC ticketing / reporting workflows

---

## Disclaimer
This repository is for educational and portfolio demonstration purposes. IOCs are included to support defensive security workflows. Do not use this information for unauthorized testing or access.
