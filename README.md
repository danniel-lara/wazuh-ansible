# wazuh-ansible
Deploy Autmatizado do Wazuh com Ansible
# 🛡️ Deploy Automatizado Wazuh SIEM com Ansible

[![Ansible](https://img.shields.io/badge/Ansible-2.15+-EE0000?style=for-the-badge&logo=ansible&logoColor=white)](https://www.ansible.com/)
[![Wazuh](https://img.shields.io/badge/Wazuh-4.x-3AABE6?style=for-the-badge&logo=wazuh&logoColor=white)](https://wazuh.com/)
[![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)](LICENSE)
[![Ubuntu](https://img.shields.io/badge/Ubuntu-22.04%20|%2024.04-E95420?style=for-the-badge&logo=ubuntu&logoColor=white)](https://ubuntu.com/)

> **Production-ready Ansible automation for deploying a complete Wazuh SIEM stack**
> (Indexer + Manager + Dashboard) with security hardening and optimized configurations.

---

## 📐 Architecture Overview

```text
┌─────────────────────────────────────────────────────┐
│                   Ansible Controller                │
│                  (Control Node)                     │
└──────────────┬──────────────┬───────────────────────┘
               │              │              │
       ┌───────▼──┐   ┌──────▼───┐   ┌──────▼──────┐
       │ Wazuh    │   │ Wazuh    │   │ Wazuh       │
       │ Indexer  │   │ Manager  │   │ Dashboard   │
       │ :9200    │   │ :1514    │   │ :443        │
       │          │   │ :1515    │   │             │
       │          │   │ :55000   │   │             │
       └──────────┘   └──────────┘   └─────────────┘
