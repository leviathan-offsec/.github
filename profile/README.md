<div align="center">

<img src="https://raw.githubusercontent.com/leviathan-offsec/.github/main/profile/banner.png" alt="Leviathan OffSec: tools that report what they could not evaluate" width="100%">

**Tools that report what they could not evaluate.**

</div>

---

## The line that matters

Every scanner here prints a coverage number next to its result, because a tool
that cannot say what it failed to check is asking to be trusted on faith.

```text
$ fenrir wordpress -t https://staging.example.com

  plugins fingerprinted   7
  database coverage       3/7 plugins matched
  no advisory data        4
```

CMSmap, Nuclei and Wapiti do not print that line. On the same fixture they report
a clean scan, because a plugin missing from the database and a plugin with no
known vulnerabilities look identical from the outside. That gap is the whole
reason this exists. The measurement is in
[Offline WordPress scanners compared](https://leviathan.ac/posts/offline-wordpress-scanner-comparison/).

---

## Tools

| Tool | What it does | Lang | Install |
| :--- | :--- | :--- | :--- |
| **[surfacediff](https://github.com/leviathan-offsec/surfacediff)** | Immutable content-addressed perimeter snapshots, field-by-field diffing, exits `1` on any delta | Python | `pip install git+https://github.com/leviathan-offsec/surfacediff.git` |
| **[HostageLVX](https://github.com/leviathan-offsec/HostageLVX)** | Subdomain takeover detection, 81 CNAME-verified fingerprints across 21 cloud providers | Go | `go install github.com/leviathan-offsec/HostageLVX@latest` |
| **[FenrirLVX](https://github.com/leviathan-offsec/FenrirLVX)** | WordPress and CMS attack surface mapping with offline CVE correlation and coverage reporting | Go | `go install github.com/leviathan-offsec/FenrirLVX@latest` |
| **[leviathan-core](https://github.com/leviathan-offsec/leviathan-core)** | Which CVEs hit your registered assets, with the evidence chain attached | Python | `pip install -e .` |

They chain: `surfacediff` snapshots the surface, `HostageLVX` tests it for
claimability, `FenrirLVX` fingerprints what is there, `leviathan-core` decides
which of the year's CVEs apply to you and shows its work.

---

## Quick start

```bash
# 1. Snapshot the perimeter
subfinder -d example.com -silent | httpx -json -silent | surfacediff snap -l prod

# 2. Diff against the last run. Exits 1 on new hosts or changed content.
surfacediff diff -l prod

# 3. Test what is there for verified takeovers
HostageLVX -l subs.txt -threads 50

# 4. Fingerprint the CMS and correlate against the offline CVE set
fenrir wordpress -t https://target.example.com
```

Stateless CLIs, no daemons, no accounts, pipe into cron or GitHub Actions.
MIT licensed.

---

## Why this and not an ASM platform

| | Traditional ASM | Here |
| :--- | :--- | :--- |
| **Runtime** | Heavy daemon plus a web console | Stateless CLI, pipe-friendly |
| **Alerting** | Proprietary vendor score | Exit code `1` on a real delta |
| **Coverage** | Not reported | Printed on every run |
| **Takeovers** | CNAME string match | 81 verified multi-cloud fingerprints |
| **Risk** | Black-box vendor math | CVSS, EPSS and KEV as separate auditable inputs |
| **Cost** | Enterprise seat | Free, MIT |

---

## Research

- **[80 Days Reversing an IoT DVR](https://leviathan.ac/posts/80-days-reversing-iot-dvr/)**: HiSilicon ARM32 surveillance firmware, 28,006 internet-facing units, three findings proven at the binary level with the disassembly included. No bounty. Includes the parts that did not work.
- **[Offline WordPress scanners compared](https://leviathan.ac/posts/offline-wordpress-scanner-comparison/)**: CMSmap, Nuclei and Wapiti measured on coverage disclosure, against a reproducible fixture.

One favicon hash from a passive index read spans 723,646 hosts across 49 product
strings, including Lorex and KB Vision rebadges. No device was contacted. The
census script is in `vuln-research`.

[All research](https://leviathan.ac/research/) · [leviathan.ac](https://leviathan.ac)

---

## Boundaries

- **Passive by default.** Index queries and public vulnerability metadata. Nothing is sent to a host you have not named.
- **Active testing needs written authorisation**, and is opt-in per target.
- **Evidence over scoring.** A finding without the chain that produced it is a guess. Either the number and its inputs are shown, or nothing is.
- **Negative results get published.** The DVR post-mortem is three real bugs and $0, which is more useful than another win because it is checkable.
- **Unknown never renders as zero.** If a check did not run, the report says so instead of reporting a pass.

---

## Contributing

Issues and PRs are welcome on any tool repo.
Start with [HostageLVX](https://github.com/leviathan-offsec/HostageLVX/issues) or
[surfacediff](https://github.com/leviathan-offsec/surfacediff/issues) if neither
suits.

---

## Design

One palette, one type scale, one evidence block, shared by the site, these
READMEs and the dashboard: [`assets/brand.css`](https://github.com/leviathan-offsec/leviathan-offsec.github.io/blob/main/assets/brand.css).
Positioning, palette meanings and the seven rules are in
[BRAND.md](https://github.com/leviathan-offsec/leviathan-offsec.github.io/blob/main/BRAND.md),
the implementation spec in [DESIGN.md](https://github.com/leviathan-offsec/leviathan-offsec.github.io/blob/main/DESIGN.md).

---

<div align="center">
  <sub>Research lab by <a href="https://github.com/cyeezy08">@cyeezy08</a> · <a href="https://leviathan.ac">leviathan.ac</a></sub>
</div>
