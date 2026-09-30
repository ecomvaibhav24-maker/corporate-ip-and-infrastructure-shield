# corporate-ip-and-infrastructure-shield
Production-ready directory-scoped .gitconfig templates, EDR air-gap rules, and corporate IP isolation playbooks for side-project developers.
# Corporate IP & Infrastructure Shield: Side-Project Isolation Engine

> **TL;DR:** Preventing global identity leaks, corporate email header stamping, and enterprise EDR/DNS telemetry tracking when building personal side projects on local workstations.

---

## The Risk: How Employers Claim Side-Project IP

When engineers build side projects, corporate legal teams rarely rely on contract disputes—they rely on **forensic footprint analysis** during IP audits:

1. **Global Git Email Stamping:** If global `~/.gitconfig` defaults to your work email, personal commits silently stamp enterprise headers directly into public GitHub repositories.
2. **Enterprise DNS & EDR Telemetry:** Running local `npm install` or API calls while connected to corporate Zscaler/VPN logs process activity on enterprise SIEMs.
3. **SSH Key Convergence:** Using the same SSH key pair for corporate GitLab and personal GitHub links host signatures across organizations.

---

## Quick Fix: Directory-Scoped `.gitconfig` Template (`[includeIf]`)

Automatically switch Git identities based on local directory paths so your corporate identity never touches personal repositories:

```ini
# ~/.gitconfig (Global Base File)
[user]
    name = Your Personal Name
    email = your.personal@email.com

# Automatically override identity when inside the personal projects directory
[includeIf "gitdir:~/personal-projects/"]
    path = ~/.gitconfig-personal

[includeIf "gitdir:~/work/"]
    path = ~/.gitconfig-work
