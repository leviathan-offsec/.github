<div align="center">

# LEVIATHAN OFFSEC

**IoT exposure research, at index scale.**

[![Web](https://img.shields.io/badge/Platform-leviathan.ac-00ffcc?style=for-the-badge&logo=firefox&logoColor=black)](https://leviathan.ac)
[![License](https://img.shields.io/badge/License-MIT-111111?style=for-the-badge)](https://opensource.org/licenses/MIT)

</div>

---

### What this is

Field research on internet-exposed IoT, and the tooling that comes out of it.

The work starts from a question, not a tool: *what is actually deployed, on how
many hosts, and does the vulnerability class still apply?* Most tooling answers
a version of that. These repos answer the parts that were left over.


### Tools

| Tool | Focus | Language | Install |
| :--- | :--- | :--- | :--- |
| **[`leviathan-core`](https://github.com/leviathan-offsec/leviathan-core)** | Which CVEs hit your registered assets, with the evidence chain attached | Python | `pip install -e .` |
| **[`HostageLVX`](https://github.com/leviathan-offsec/HostageLVX)** | Dangling DNS and subdomain takeover detection, CNAME-verified against 30+ providers | Go | `go install github.com/leviathan-offsec/HostageLVX@latest` |
| **[`FenrirLVX`](https://github.com/leviathan-offsec/FenrirLVX)** | WordPress and CMS attack surface mapping, plugin fingerprinting, offline CVE correlation | Go | `go install github.com/leviathan-offsec/FenrirLVX@latest` |
| **[`surfacediff`](https://github.com/leviathan-offsec/surfacediff)** | Content-addressed perimeter snapshots and deterministic field diffs | Python | `pip install git+https://github.com/leviathan-offsec/surfacediff.git` |
| **[`[a private repo]`](https://github.com/leviathan-offsec/[a private repo])** | Passive CVE/EPSS/KEV correlation scoped to authorized assets | Python | `git clone https://github.com/leviathan-offsec/[a private repo].git` |

They chain: `surfacediff` snapshots the surface, `HostageLVX` tests it for
claimability, `FenrirLVX` fingerprints what is there, `leviathan-core` decides
which of the year's CVEs apply to you and shows its work.


**Passive by default.** Index queries and public vulnerability metadata. Nothing
is sent to a host you have not named. Active testing needs written authorisation
and is opt-in per target.

**Evidence over scoring.** A finding without the chain that produced it is a
guess. `leviathan-core` shows the number and the inputs behind it, or it shows
nothing.

**Negative results get published.** The linked post-mortem is three real bugs
and $0. That is more useful than another win, because it is checkable.

### Research

- **[80 Days Reverse Engineering an IoT DVR](https://leviathan.ac/posts/80-days-reversing-iot-dvr.html)** — HiSilicon ARM32 surveillance firmware, 28,006 internet-facing units, three findings proven at the binary level with the disassembly included. No bounty. Long-form post-mortem, including the parts that did not work.

---

<div align="center">
  <sub>Research lab by <a href="https://github.com/cyeezy08">@cyeezy08</a> · <a href="https://leviathan.ac">leviathan.ac</a></sub>
</div>
