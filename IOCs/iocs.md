# IOCs — Georgia DDS Smishing (Lookalike Domains)

## URLs (Observed in SMS / Analysis)
- https://georgia.gov-cit.cc/dds?var=EvrCAVyFJP
- https://georgia.gov-hdu.cc/dds?var=OSBzhJXGqD

## Domains
- georgia.gov-cit.cc
- georgia.gov-hdu.cc

## Sender Phone Numbers (Smishing Origin)
> Consider partially masking in public repos if you prefer.
- +1 (706) 267-2318
- +1 (731) 453-0614

## Notes
- Lookalike naming uses “georgia.gov-*” while not being a legitimate `.gov` domain.
- Random query tokens likely used for tracking campaigns and victim correlation.


type,value,source,notes
url,https://georgia.gov-cit.cc/dds?var=EvrCAVyFJP,SMS,Lookalike DDS payment lure
url,https://georgia.gov-hdu.cc/dds?var=OSBzhJXGqD,SMS,Lookalike DDS payment lure
domain,georgia.gov-cit.cc,SMS/VT,Non-gov TLD; impersonation naming
domain,georgia.gov-hdu.cc,SMS/VT,Non-gov TLD; impersonation naming
phone,+17062672318,SMS,Smishing sender
phone,+17314530614,SMS,Smishing sender
