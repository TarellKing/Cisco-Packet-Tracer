# Packet Tracer - Configure Secure Passwords and SSH
![image](https://github.com/user-attachments/assets/72b67c30-3af8-4d4e-ade2-bd2e4127b40d)

## Addressing Table

| Device | Interface | IP Address  | Subnet Mask   | Default Gateway |
|--------|-----------|-------------|---------------|-----------------|
| RTA    | G0/0      | 172.16.1.1  | 255.255.255.0 | N/A             |
| PCA    | NIC       | 172.16.1.10 | 255.255.255.0 | 172.16.1.1      |
| SW1    | VLAN 1    | 172.16.1.2  | 255.255.255.0 | 172.16.1.1      |

## Summary of Configuration

### Router (RTA) Configuration
1. **Configured IP Addressing** on PCA and RTA.
2. **Set Hostname and Enabled Interface** on RTA.
3. **Enhanced Security** by:
   - Encrypting plaintext passwords
   - Setting minimum password length to 10
   - Disabling DNS lookup
   - Setting domain name to `CCNA.com`
   - Creating a user with an encrypted password
   - Generating 1024-bit RSA keys
   - Blocking login attempts after multiple failures
   - Configuring VTY lines for SSH access
   - Setting EXEC mode timeout
4. **Saved the Configuration** to NVRAM.

#### Commands:
```comand
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


### Switch (SW1) Configuration

SW1(config)# hostname SW1
SW1(config)# interface vlan 1
SW1(config-if)# ip address 172.16.1.2 255.255.255.0
SW1(config-if)# no shutdown
SW1(config)# ip default-gateway 172.16.1.1
SW1(config)# interface range f0/2-24, g0/2
SW1(config-if-range)# shutdown
SW1(config)# service password-encryption
SW1(config)# no ip domain-lookup
SW1(config)# ip domain-name CCNA.com
SW1(config)# username any_user secret any_password
SW1(config)# crypto key generate rsa
SW1(config)# line vty 0 4
SW1(config-line)# transport input ssh
SW1(config-line)# login local
SW1(config-line)# exec-timeout 6
SW1# copy running-config startup-config

