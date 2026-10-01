<div align="center">

# LEVIATHAN OFFSEC

**IoT exposure research, at index scale.**

[![Web](https://img.shields.io/badge/Platform-leviathan.ac-00ffcc?style=for-the-badge&logo=firefox&logoColor=black)](https://leviathan.ac)
[![License](https://img.shields.io/badge/License-MIT-111111?style=for-the-badge)](https://opensource.org/licenses/MIT)

</div>

---

ProjectDiscovery built the best HTTP probing on the market, and `httpx` is
genuinely hard to beat. What they did not build is the layer after it: taking
what an index already knows about a million hosts, and answering *which of
those findings apply to the assets I actually own*.

That is the gap these tools sit in.

### Measured exposure, passively

```text
$ ./favmap.py census "product:Dahua"

sampled            : 300
no favicon indexed : 34
distinct hashes    : 2

  HOSTS      %          HASH  MODEL(S)
    233  87.6%    1653394551  Dahua-based DVR(58), DH-XVR1B08-I(41)
     33  12.4%    2019488876  Dahua HCVR(4), SS 5532 MF(2)

$ ./favmap.py expand 1653394551
http.favicon.hash:1653394551  ->  723,646 indexed hosts
```

One favicon hash spans 723,646 indexed Dahua hosts across a dozen model
families. That is a firmware generation, fingerprinted, without downloading or
touching a single device.

### Tools

| Tool | Focus | Language | Install |
| :--- | :--- | :--- | :--- |
| **[`HostageLVX`](https://github.com/leviathan-offsec/HostageLVX)** | Dangling DNS and subdomain takeover detection, CNAME-verified against 30+ cloud and edge providers | Go | `go install github.com/leviathan-offsec/HostageLVX@latest` |
| **[`FenrirLVX`](https://github.com/leviathan-offsec/FenrirLVX)** | WordPress and CMS attack surface mapping, plugin fingerprinting, offline CVE correlation | Go | `go install github.com/leviathan-offsec/FenrirLVX@latest` |
| **[`leviathan-core`](https://github.com/leviathan-offsec/leviathan-core)** | Exposure correlation against CVSS, FIRST EPSS and CISA KEV with the evidence chain attached | Python | `git clone https://github.com/leviathan-offsec/leviathan-core.git` |
| **[`surfacediff`](https://github.com/leviathan-offsec/surfacediff)** | Content-addressed perimeter snapshots and deterministic field diffs | Python | `pip install git+https://github.com/leviathan-offsec/surfacediff.git` |
| **[`[a private repo]`](https://github.com/leviathan-offsec/[a private repo])** | Passive CVE/EPSS/KEV correlation scoped to customer-authorized assets | Python | `git clone https://github.com/leviathan-offsec/[a private repo].git` |
| **[`[a private repo]`](https://github.com/leviathan-offsec/[a private repo])** | Firmware extraction pipeline, Ghidra triage scripts, CVE PoCs | Python | `git clone https://github.com/leviathan-offsec/[a private repo].git` |

### Principles

**Passive by default.** Index queries and public vulnerability metadata. Nothing
is sent to a host you have not named. Active testing requires written
authorisation and is opt-in per target.

**Evidence over scoring.** A finding without the chain that produced it is a
guess. `leviathan-core` will show you a number and the inputs behind it, or it
will show you nothing.

**Zero dependency where it matters.** Standard-library Python, static Go
binaries. No runtime containers, no fragile trees.

---

### Research

- **[80 Days Reverse Engineering an IoT DVR](https://leviathan.ac/posts/80-days-reversing-iot-dvr.html)** — HiSilicon ARM32 surveillance firmware, 28,006 internet-facing units, three findings proven at the binary level. No bounty, long-form post-mortem.
- **[Dahua IPC firmware](https://github.com/leviathan-offsec/[a private repo])** — command injection primitive in `libpdi.so`, confirmed across two product classes and two library builds. Network reachability not established, and not claimed.

---

<div align="center">
  <sub>Research lab by <a href="https://github.com/cyeezy08">@cyeezy08</a> · <a href="https://leviathan.ac">leviathan.ac</a></sub>
</div>
