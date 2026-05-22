# NETINSIGHT APT Repository

This repository hosts the public APT distribution for [NETINSIGHT](https://github.com/dkg-netinsight/netinsight), the enterprise NetFlow / sFlow / IPFIX analytics platform.

The repository is served via GitHub Pages at:

**`https://dkg-netinsight.github.io/apt-repo/`**

The signed APT metadata + binary `.deb` files live on the `gh-pages` branch of this repo. The `main` branch (this branch) holds only operator-facing documentation + publishing scripts.

## End-user install

Pick the `netinsight-release` `.deb` matching your Ubuntu LTS, then `apt install`:

### Tier 1 — canonical (cinematic, 2 commands, recommended)

**Ubuntu 22.04 (jammy):**
```bash
wget --tries=5 --waitretry=10 https://dkg-netinsight.github.io/apt-repo/pool/main/n/netinsight/netinsight-release_1.0.0-81+ubuntu22.04_all.deb
dpkg -i netinsight-release_1.0.0-81+ubuntu22.04_all.deb
netinsight-install
```

**Ubuntu 24.04 (noble):**
```bash
wget --tries=5 --waitretry=10 https://dkg-netinsight.github.io/apt-repo/pool/main/n/netinsight/netinsight-release_1.0.0-81+ubuntu24.04_all.deb
dpkg -i netinsight-release_1.0.0-81+ubuntu24.04_all.deb
netinsight-install
```

`netinsight-install` renders a branded TUI (banner, animated workflow, 8-stage progress, summary card with QR) and orchestrates `apt install netinsight` with output suppressed to `/var/log/netinsight/install.log`. See `netinsight-install(8)`.

### Tier 2 — legacy 4-command path (no cinematic UI)

**Ubuntu 22.04 (jammy):**
```bash
wget --tries=5 --waitretry=10 https://dkg-netinsight.github.io/apt-repo/pool/main/n/netinsight/netinsight-release_1.0.0-81+ubuntu22.04_all.deb
dpkg -i netinsight-release_1.0.0-81+ubuntu22.04_all.deb
apt update
apt install -y netinsight
```

**Ubuntu 24.04 (noble):** same but `1.0.0-81+ubuntu24.04`.

The full installation guide lives at [`INSTALL.md`](https://github.com/dkg-netinsight/netinsight/blob/main/INSTALL.md) in the main NETINSIGHT repository.

## Repository signing

All `Release` / `InRelease` files are signed with the NETINSIGHT release key:

- Master fingerprint: `477C1561698EB0C329C3C6DD02E2D963F0BC0D33`
- Signing subkey: `1A1420ACE40DC218` (expires 2028-05-08)

The keyring binary ships in `netinsight-release_*.deb` and is installed under `/etc/apt/keyrings/netinsight-archive-keyring.gpg`. `apt` enforces it via `[signed-by=...]` so the keyring is bound to this single source and never trusts the system-wide `/etc/apt/trusted.gpg.d`.

## Branch layout

| Branch | Holds |
|--------|-------|
| `main` | this README + future publish scripts |
| `gh-pages` | `dists/{jammy,noble}/...` + `pool/main/n/netinsight/*.deb` (live apt repo content) |

GitHub Pages serves `gh-pages` at `https://dkg-netinsight.github.io/apt-repo/`.

## License

The repository tooling is BSD 3-Clause. Individual `.deb` packages are governed by their own copyright notices (see each package's `/usr/share/doc/<pkg>/copyright`).
