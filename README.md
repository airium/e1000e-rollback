# e1000e driver for I219-LM with patch

This repo contains e1000e driver from [Linux 5.15](https://github.com/torvalds/linux/releases/tag/v5.15) with [the negative patch](https://github.com/torvalds/linux/commit/b10effb92e272051dd1ec0d7be56bf9ca85ab927) reverted, restoring Intel I219-LM to its full 1Gbps uplink for TCP. The DKMS part is based on <https://github.com/KozakaiAya/e1000e-rollback>. Tested working on Ubuntu with 5.15 kernel (20.04 w/hwe-edge or 22.04).

---

## How to use

To install:

```bash
git clone https://github.com/airium/e1000e-rollback.git -b 5.15.0
cd e1000e-rollback/e1000e
cp -R . /usr/src/e1000e-5.15.0
dkms add -m e1000e -v 5.15.0
dkms build -m e1000e -v 5.15.0
dkms install -m e1000e -v 5.15.0
```

To remove:

```bash
dkms remove -m e1000e/5.15.0 --all
```

---

## Reference

1. <https://blog.gloriousdays.pw/2020/07/20/intel-i219-lm-performance-issue-and-mitigation>