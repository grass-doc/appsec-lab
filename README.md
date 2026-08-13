# AppSec Lab

A self-built detection-engineering lab: a deliberately vulnerable app sitting behind an nginx reverse proxy,
fronted by CrowdSec (WAF + IDS/IPS), with an Elastic Stack SIEM tailing every log source, host telemetry via
Sysmon/auditd, and a purple-team pass using Atomic Red Team mapped to a real MITRE ATT&CK adversary profile.

**Status:** early build — see commit history and `docs/` as phases land.

Full working notes, architecture rationale, and phase-by-phase roadmap live in the author's private
Obsidian vault during development; a cleaned-up public writeup lands in `docs/` as each phase completes.

## Stack

- Target: OWASP Juice Shop or DVWA
- Reverse proxy: nginx
- WAF / IDS-IPS: CrowdSec
- SIEM: Elastic (Elasticsearch + Kibana + Elastic Agent)
- Detection rules: authored as [Sigma](https://github.com/SigmaHQ/sigma), compiled to Elastic via `sigma-cli`
- Attack simulation: [Invoke-AtomicRedTeam](https://github.com/redcanaryco/invoke-atomicredteam) (Atomic Red Team), no custom exploit code
- CI/CD: compose/YAML validation, Semgrep SAST, Dependabot SCA, GitHub secret scanning, Sigma rule validation

## Repo layout

```
.github/          CI workflows + Dependabot config
nginx/             reverse proxy config
crowdsec/          custom CrowdSec scenarios
detections/sigma/  source-of-truth detection rules (Sigma format)
detections/elastic/ sigma-cli compiled output — generated, not hand-edited
atomics/notes/     which Atomic Red Team tests were run, and results
docs/findings/     one write-up per attack class tested
```
