# SCA Proxmox VE Server 9.x for hardening server with Wazuh

PVE 9.x Security Configuration Assessment

[![Wazuh](https://img.shields.io/badge/Wazuh-4.x-blue)](https://wazuh.com)
[![Proxmox VE 9.x Server](https://img.shields.io/badge/pve-9.x-orange)](https://proxmox.com/en/products/proxmox-virtual-environment/overview)
[![License](https://img.shields.io/badge/License-AGPL--3.0-green)](LICENSE)

Community integration of the **Proxmox VE 9.x hardening server** for [Wazuh](https://wazuh.com).

---

## Project Status

> [!WARNING]
> This project is under active development and some controls are still being validated.\
> Your feedback, testing results, and contributions are strongly encouraged to help improve accuracy, completeness, and reliability.

---

## What this SCA provides

| Component | Description |
|-----------|-------------|
| **SCA Policies** | YAML policies for PVE9.x server agents that audit system configuration |

---

## Supported versions

- **Wazuh**: 4.14 or later (4.14.+ recommended)
- **Agents**: Debian 13
- **PVE**: 9.x

---

## Manual installation

### 1. Copy SCA policies

Never place custom policies in /var/ossec/ruleset/sca — they get overwritten on upgrade!

On manager: /var/ossec/etc/shared/default/ (or group folder)

```bash
sudo cp sca/pve9_hardening.yml /var/ossec/etc/shared/default/
```

### 2. Enable SCA policies in ossec.conf

Add the following inside the `<sca>` block in `/var/ossec/etc/ossec.conf`:

```xml
<sca>
  <enabled>yes</enabled>
  <scan_on_start>yes</scan_on_start>
  <interval>12h</interval>
  <skip_nfs>yes</skip_nfs>
  <policies>
    <policy>etc/shared/default/pve9_hardening.yml</policy>
  </policies>
</sca>
```

---

###  3. Restart Wazuh manager

```bash
sudo systemctl restart wazuh-manager
```

---

## Disclaimer & Terms of Use

> [!WARNING]
> ⚠️ **AS‑IS, NO WARRANTY**.

By using these SCA, you agree to:

1. **Responsibility** - You must test and validate each item yourself before applying it.
2. **No Liability** - The authors and contributors are **not liable** for any direct, indirect, or consequential damages arising from the use of this SCA.
3. **License** - All content is licensed under **AGPL 3** (see [`LICENSE`](LICENSE)).  
4. **Community Techniques** - Some recommended practices are community-driven and **not officially supported** by Proxmox GmbH. Use at your own risk.

---

## Author

Maintained by ****Fernando Verdugo****.