# NETWORK INFRASTRUCTURE DOCUMENTATION
## Region: US-West-2 | Site: Enterprise Core Lab

### 1. Overview
This document defines baseline network architecture for US-West-2.
All configs are managed via Git and deployed automatically via CI/CD pipelines.

### 2. Device Naming Convention
- Core Switches: `SW-CORE-<INDEX>.<REGION>`
- Access Switches: `SW-ACCESS-<INDEX>.<REGION>`

### 3. IP Addressing Scheme
- Management Network: `10.10.10.0/24` (VLAN 10)
- User Data Network: `10.10.20.0/24` (VLAN 20)
- Out-of-Band SSH Gateway: `192.168.1.0/24`

### 4. Operational Protocols
- Routing Protocol: OSPF Area 0 for spine/leaf connectivity
- Management SSH: Port 22 (Enforced SSHv2 only)
- Monitoring & Alerts: Centralized Syslog over UDP 514

### 5. Automation & Change Management
- Source of Truth: Inventory files in `inventory/switches.yml`
- Security Standard: No direct CLI changes allowed on core switches.

### 6. Emergency Rollback Procedure
1. Identify Fault: Review telemetry dashboards to pinpoint failing switch nodes.
2. Trigger Revert: Execute `git revert <commit_hash>` to restore stable state.
3. Push Update: Push revert commit to `main` to trigger redeployment.
4. Verify Recovery: Run automated health checks to confirm traffic normalization.
