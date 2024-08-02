# Packet Tracer - Configure Secure Passwords and SSH

![Network Diagram](https://github.com/user-attachments/assets/72b67c30-3af8-4d4e-ade2-bd2e4127b40d)

## Addressing Table

| Device | Interface | IP Address  | Subnet Mask   | Default Gateway |
|--------|-----------|-------------|---------------|-----------------|
| RTA    | G0/0      | 172.16.1.1  | 255.255.255.0 | N/A             |
| PCA    | NIC       | 172.16.1.10 | 255.255.255.0 | 172.16.1.1      |
| SW1    | VLAN 1    | 172.16.1.2  | 255.255.255.0 | 172.16.1.1      |

## Project Overview

This project involves configuring a network setup with secure password and SSH protocols to ensure encrypted and secure remote access.

## Configuration Summary

### Router (RTA) Configuration
- **IP Addressing**: Configured for PCA and RTA.
- **Hostname & Interfaces**: Hostname set to `RTA` with activated interfaces.
- **Security Enhancements**:
  - Password encryption enabled.
  - Minimum password length set to 10.
  - DNS lookup disabled.
  - Domain name set to `CCNA.com`.
  - User creation with encrypted password.
  - 1024-bit RSA keys generated.
  - Login attempt restrictions configured.
  - VTY lines set for SSH access only.
  - EXEC mode timeout set to 6 minutes.
- **Configuration Saved**: Changes were saved to NVRAM.

#### Commands
```command
RTA(config)# hostname RTA
RTA(config)# interface g0/0
RTA(config-if)# ip address 172.16.1.1 255.255.255.0
RTA(config-if)# no shutdown
RTA(config)# service password-encryption
RTA(config)# security password min-length 10
RTA(config)# no ip domain-lookup
RTA(config)# ip domain-name CCNA.com
RTA(config)# username any_user secret any_password
RTA(config)# crypto key generate rsa
RTA(config)# login block-for 180 attempts 4 within 120
RTA(config)# line vty 0 4
RTA(config-line)# transport input ssh
RTA(config-line)# login local
RTA(config-line)# exec-timeout 6
RTA# copy running-config startup-config
