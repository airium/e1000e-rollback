# e1000e driver for I219-LM with patch reverted

This repo contains e1000e driver for [Linux 5.19](https://github.com/torvalds/linux/releases/tag/v5.19) with [the negative patch](https://github.com/torvalds/linux/commit/b10effb92e272051dd1ec0d7be56bf9ca85ab927) reverted, restoring Intel I219-LM to its full 1Gbps uplink for TCP. The DKMS part is based on <https://github.com/KozakaiAya/e1000e-rollback> and <https://github.com/koljah-de/e1000e-dkms-debian>. Tested working on Ubuntu 22.04 with HWE Edge 5.19 kernel as of Jan 2023.

**The patch reversion is only required and works for Intel Skylake and Kaby Lake platforms.** The abovementioned issue does not apply to other Intel platforms.

---

## Usage

To install:

```bash
git clone https://github.com/airium/e1000e-rollback.git -b 5.19.0
cd e1000e-rollback/e1000e
cp -R . /usr/src/e1000e-5.19.0
dkms add -m e1000e -v 5.19.0
dkms build -m e1000e -v 5.19.0
dkms install -m e1000e -v 5.19.0
```

To remove:

```bash
dkms remove -m e1000e -v 5.19.0 --all
```

## Caution

**The built e1000e driver is not signed.**
Disable `Secure Boot` in BIOS before switching to it, otherwise the NIC won't be loaded at next boot.
Or optimally, sign the module by your own means.

---

## Reference

1. <https://blog.gloriousdays.pw/2020/07/20/intel-i219-lm-performance-issue-and-mitigation>
