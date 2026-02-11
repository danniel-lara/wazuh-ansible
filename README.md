# wazuh-ansible
Deploy Autmatizado do Wazuh com Ansible
# 🛡️ Deploy Automatizado Wazuh SIEM com Ansible

[![Ansible](https://img.shields.io/badge/Ansible-2.15+-EE0000?style=for-the-badge&logo=ansible&logoColor=white)](https://www.ansible.com/)
[![Wazuh](https://img.shields.io/badge/Wazuh-4.x-3AABE6?style=for-the-badge&logo=wazuh&logoColor=white)](https://wazuh.com/)
[![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)](LICENSE)
[![Ubuntu](https://img.shields.io/badge/Ubuntu-22.04%20|%2024.04-E95420?style=for-the-badge&logo=ubuntu&logoColor=white)](https://ubuntu.com/)

---
## 📖 Sobre o Projeto

Este projeto automatiza o **deploy completo do Wazuh** (SIEM, XDR & Compliance) utilizando Ansible, seguindo as melhores práticas de infraestrutura como código (IaC).

### O que este projeto faz:

- ✅ **Gera certificados SSL/TLS** para comunicação segura entre componentes
- ✅ **Instala e configura o Wazuh Indexer** (baseado em OpenSearch)
- ✅ **Inicializa o cluster** do Indexer
- ✅ **Instala e configura o Wazuh Manager** (servidor central)
- ✅ **Instala e configura o Wazuh Dashboard** (interface web)
- ✅ **Aplica tuning de kernel** via sysctl para performance em produção



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
```
## 📋 Pré-requisitos
---
### Infraestrutura

| Componente         | CPU    | RAM    | Disco     | OS               |
|--------------------|--------|-------|------------|------------------|
| Wazuh Indexer      | 8 vCPU | 16 GB | 200 GB SSD | Ubuntu 24.04 LTS |
| Wazuh Manager      | 4 vCPU | 8 GB  | 100 GB SSD | Ubuntu 24.04 LTS |
| Wazuh Dashboard    | 4 vCPU | 4 GB  | 50 GB SSD  | Ubuntu 24.04 LTS |
| Ansible Controller | 1 vCPU | 2 GB  | 10 GB      | Ubuntu 24.04 LTS |
---
### Software

- **Ansible** >= 2.15
- **Python** >= 3.10
- **SSH** acesso com chave para todos os hosts
---

## 📁 Estrutura do Projeto
```text
wazuh-ansible/
├── group_vars/
│   └── all.yml              # Global variables (versions, IPs, credentials)
├── inventory/
│   └── hosts.ini            # Target hosts inventory
├── playbooks/
│   ├── 00-generate.yml      # Generate SSL certificates & keys
│   ├── 01-indexer.yml        # Deploy Wazuh Indexer (OpenSearch)
│   ├── 02-start-cluster.yml # Initialize & verify cluster health
│   ├── 03-manager.yml       # Deploy Wazuh Manager (OSSEC engine)
│   ├── 04-dashboard.yml     # Deploy Wazuh Dashboard (Web UI)
│   └── 99-sysctl.yml        # Kernel tuning & OS hardening
├── site.yml                 # Master playbook (orchestrates all)
└── README.md
```
