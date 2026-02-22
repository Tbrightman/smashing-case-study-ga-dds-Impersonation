# Mitigation Strategy — Georgia DDS Smishing Campaign

## 1. Immediate Response Actions (If User Interaction Occurred)

If a user clicked the link but did not submit information:

- Clear browser cache and session data
- Perform endpoint AV/EDR scan
- Review recent downloads
- Reset credentials if any authentication attempt occurred

If payment or credentials were submitted:

- Initiate password resets (email, banking, reused credentials)
- Notify financial institutions immediately
- Monitor accounts for fraudulent transactions
- Enable credit monitoring where applicable
- Escalate to incident response workflow

---

## 2. Preventive Controls (Enterprise)

### 2.1 DNS Filtering / Secure Web Gateway (SWG)

**Action:**
- Block identified domains at DNS filtering layer
- Add IOC-based URL blocks in Secure Web Gateway
- Enable newly-registered domain monitoring policies (if available)

**Rationale:**
Smishing campaigns often use short-lived infrastructure. DNS-level blocking reduces exposure across all devices, including unmanaged endpoints where applicable.

---

### 2.2 Endpoint Detection & Response (EDR)

**Action:**
- Add malicious domains/URLs as Indicators (block + alert)
- Enable web protection policies where supported
- Monitor for outbound connections to suspicious TLDs (.cc, etc.)

**Rationale:**
EDR telemetry provides visibility into endpoint-initiated network activity and can prevent follow-on exploitation attempts.

---

### 2.3 Mobile Device Management (MDM) & Mobile Threat Defense

Smishing primarily targets mobile devices.

**Action:**
- Enforce mobile compliance policies
- Deploy mobile threat defense solution (if available)
- Restrict browser access to known malicious categories
- Enable SMS phishing awareness alerts (where platform-supported)

**Rationale:**
Traditional email security controls do not protect against SMS-delivered threats. Mobile-specific controls are necessary.

---

## 3. Detective Controls (SOC Monitoring)

### 3.1 Domain Pattern Hunting

Hunt for lookalike patterns such as:

- `*.gov-*.cc`
- Government impersonation naming conventions
- Recently registered domains with authority-themed keywords

Example hunting concept (Defender for Endpoint-style logic):
