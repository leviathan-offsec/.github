# Leviathan OffSec

**Deterministic perimeter intelligence for red teams and security researchers.**

We build open source tools that do one job well: snapshot attack surfaces, detect changes, audit web applications, and rank risk with auditable math—not vendor black boxes.

---

## Our Tools

**[surfacediff](https://github.com/leviathan-offsec/surfacediff)** – Immutable content-addressed perimeter snapshots with field-by-field diffing. Exits `1` on deltas. `Python (stdlib)`.

**[HostageLVX](https://github.com/leviathan-offsec/HostageLVX)** – Subdomain takeover detection with 81 verified CNAME fingerprints across 21 cloud providers. `Go CLI`.

**[FenrirLVX](https://github.com/leviathan-offsec/FenrirLVX)** – WordPress and CMS vulnerability scanner with offline CVE correlation and transparent coverage reporting. `Go CLI`.

**[leviathan-core](https://github.com/leviathan-offsec/leviathan-core)** – Risk ranking kernel. Computes CVSS + EPSS + CISA KEV into auditable signals. `Python`.

**[[a private repo]](https://github.com/leviathan-offsec/[a private repo])** – Passive threat intelligence correlation for authorized environments. `Python`.

---

## Getting Started

- **[Documentation](https://leviathan.ac/docs)** – Learn all our tools and workflows
- **[Quick 60-Second Pipeline](#quick-start)** – Snapshot → Diff → Audit → Rank
- **[Research Dossiers](https://leviathan.ac/research/)** – Published offensive engineering teardowns
- **[Need Help?](https://github.com/leviathan-offsec)** – Open issues or reach out

---

## Quick Start

```bash
# 1. Snapshot your perimeter state
subfinder -d example.com -silent | httpx -json -silent | surfacediff snap -l prod

# 2. Check for changes on next run (exits 1 if new hosts or modified content)
surfacediff diff -l prod

# 3. Audit all subdomains for verified takeovers
HostageLVX -l subs.txt -threads 50

# 4. Scan for known vulnerabilities with transparent coverage reporting
fenrir -t https://target.example.com
```

---

## Why Leviathan

| | Traditional ASM / Scanners | Leviathan OffSec |
|---|---|---|
| **Runtime** | Heavy daemons + cloud dashboards | Stateless CLI tools (pipe-friendly) |
| **Alerting** | Proprietary vendor scoring | Exit code `1` on perimeter delta |
| **Takeovers** | Simple CNAME matching | 81 verified multi-cloud fingerprints |
| **Risk Scoring** | Black-box vendor math | Auditable CVSS + EPSS + KEV vectors |
| **Integration** | SaaS webhooks | Native UNIX (bash, cron, GitHub Actions) |
| **Cost** | Enterprise SaaS | 100% Free & Open Source (MIT) |

---

## Research

We publish complete offensive engineering research—failed hypotheses, binary reversals, hardware disassemblies, and real-world findings:

- **[Offline WordPress Scanners Compared](https://leviathan.ac/posts/offline-wordpress-scanner-comparison/)** – CMSmap, Nuclei, Wapiti, FenrirLVX benchmarked. October 2026.
- **[80 Days Reversing an IoT DVR](https://leviathan.ac/posts/80-days-reversing-iot-dvr/)** – Static AES keys, unsigned bootloaders, command injections in HiSilicon ARM32 firmware. September 2026.

[Browse all research & advisories →](https://leviathan.ac/research/)

---

## Ethics & Boundaries

- **Passive by default** – DNS, indexing, and public metadata only. No invasive payloads to unconfirmed targets.
- **Authorized testing only** – Active penetration tests require explicit written scope.
- **Evidence over speculation** – If we can't reach it or it's patched, we say so.

---

## Community

- **[Issues](https://github.com/issues?q=is%3Aopen+is%3Aissue+user%3Aleviathan-offsec)** – Report bugs, request features
- **[Pull Requests](https://github.com/pulls?q=is%3Aopen+is%3Apr+user%3Aleviathan-offsec)** – Contribute improvements
- **[Discussions](https://github.com/leviathan-offsec/leviathan-core/discussions)** – Ask questions, share ideas

---

**Directed by [@cyeezy08](https://github.com/cyeezy08)** • **[leviathan.ac](https://leviathan.ac)**

Questions? Email [hello@leviathan.ac](mailto:hello@leviathan.ac) or open an issue.
