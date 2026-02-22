# Technical Analysis — Georgia DDS Smishing Campaign

## 1. Initial Triage & Suspicion Indicators

The SMS messages presented themselves as a "Georgia Department of Driver Services (DDS) Final Notice" regarding an unresolved traffic violation. Several indicators immediately suggested a smishing attempt:

- Use of urgency and legal threat language (license suspension, registration revocation, collections, adverse credit reporting)
- A strict deadline designed to induce panic-based decision making
- Payment instructions delivered via SMS
- Use of non-official domains (not `.gov`)
- Lookalike domain structure designed to visually resemble legitimate government URLs

Government agencies in the United States operate official services under `.gov` domains. The presence of `.cc` TLD domains significantly reduced legitimacy confidence.

---

## 2. Domain & URL Structure Analysis

### Observed Domains
- `georgia.gov-cit.cc`
- `georgia.gov-hdu.cc`

### Structural Observations
- The domain naming pattern embeds "georgia.gov" as a subcomponent to create visual trust.
- The real registered domain is `gov-cit.cc` or `gov-hdu.cc`, not `georgia.gov`.
- The `.cc` TLD (Cocos Islands) is frequently used in phishing infrastructure due to low registration friction.
- URLs contain randomized query parameters (e.g., `?var=EvrCAVyFJP`) consistent with campaign tracking or victim tokenization.

This naming convention aligns with impersonation-based phishing infrastructure commonly observed in smishing campaigns.

---

## 3. Reputation Analysis — VirusTotal

The submitted URL returned:

- Multiple security vendors classifying the URL as **Phishing** or **Malicious**
- Detection ratio example: 11/94 vendors flagged
- HTTP status observed: 403 (Forbidden)

Interpretation:

- Multi-vendor consensus supports malicious classification.
- A 403 response may indicate:
  - Geo-based blocking
  - User-agent filtering
  - Short-lived phishing infrastructure
  - Takedown in progress

Even without full payload rendering, the reputation signal was sufficient to classify as malicious.

---

## 4. Sandbox Behavioral Analysis — ANY.RUN

The URL was detonated in a controlled Windows 10 sandbox environment.

### Observed Behavior:
- Browser process execution (msedge.exe)
- Network activity flagged as suspicious
- ANY.RUN classification tag: possible phishing
- Network threat classification indicating suspicious TLD usage
- No legitimate government service behavior observed

The page did not render a legitimate portal during execution, which may indicate:

- Conditional delivery (only serving payloads to mobile devices)
- Region-based filtering
- Dynamic content dependent on campaign parameters
- Infrastructure disruption

Behavior aligned with low-sophistication phishing infrastructure rather than malware delivery.

---

## 5. Social Engineering Pattern Analysis

This campaign leveraged classic smishing techniques:

1. Authority Impersonation (State Government Agency)
2. Legal Threat Escalation
3. Deadline Pressure
4. Financial Penalty Amplification
5. Direct Payment Call-to-Action

The messaging strategy is consistent with payment-harvesting fraud rather than credential harvesting (though both are possible).

---

## 6. Risk Assessment

### Likely Objectives
- Direct financial fraud via payment submission
- Collection of personally identifiable information
- Potential card data harvesting
- Campaign analytics via query token tracking

### Impact (If Victim Engages)
- Financial loss
- Identity theft
- Secondary fraud attempts
- Increased targeting due to confirmed active phone number

### Classification
High-confidence smishing campaign involving government impersonation and fraudulent payment redirection.

---

## 7. Defensive Intelligence Value

Extracted artifacts provide defensive utility in:

- DNS blocking
- Secure Web Gateway filtering
- EDR IOC enforcement
- Smishing awareness training
- Pattern-based hunting (lookalike gov-* TLD domains)

This case demonstrates how individual SMS artifacts can be escalated into structured threat intelligence suitable for enterprise defensive use.

---

## Conclusion

Based on domain analysis, multi-vendor detection consensus, sandbox behavior, and social engineering characteristics, this incident is classified as a malicious smishing campaign leveraging government impersonation and fraudulent payment coercion.

No interaction beyond controlled analysis was performed, and no credentials or payment information were submitted.
