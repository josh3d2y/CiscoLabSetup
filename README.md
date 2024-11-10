# Cisco Lab Setup for R1 and SW1 | Initial Config

This repository documents the setup and configuration of a Cisco router and switch lab using a single Cisco 1800 router and a Cisco Catalyst 2960 switch. The session includes initial configurations, interface setup, IP assignment, VLAN creation, and troubleshooting steps along with the mistakes made and corrections applied during the session.

## Lab Equipment
- **Router Model:** Cisco 1800 Series
- **Switch Model:** Cisco Catalyst 2960
- **Laptop** connected via **console** using PuTTY for configuration.

## Lab Objectives
1. **Set up IP addresses** on both router and switch for basic connectivity.
2. **Configure basic settings** such as hostname and IP routing on the router.
3. **Test connectivity** between router and switch.

## Configuration Summary

### Router Configuration (R1)
1. **Set Hostname**:
   ```plaintext
   en
   conf t
   hostname R1
   ```

2. **Save Configuration**:
   During the session, multiple commands were attempted to save the configuration:
   ```plaintext
   write memory
   write
   copy running-config startup-config
   ```

3. **Configure Interface IP Address**:
   The router interface `FastEthernet0/1` was configured with the following IP:
   ```plaintext
   int fastEthernet 0/1
   ip address 192.168.10.1 255.255.255.0
   no shutdown
   ```

4. **Static Route Setup**:
   Attempted to set a static route to enable routing across subnets. The syntax used was:
   ```plaintext
   ip route 192.168.20.0 255.255.255.0 fastEthernet 0/1
   ```

5. **Ping Tests**:
   After configuration, ping tests were conducted to check connectivity with the switch IP (`192.168.10.2`). Initial attempts failed, but subsequent attempts showed success:
   ```plaintext
   ping 192.168.10.2
   ```

### Switch Configuration (SW1)
1. **Set Hostname**:
   ```plaintext
   en
   conf t
   hostname SW1
   ```

2. **Configure VLAN Interface with IP Address**:
   Configured `Vlan1` for management access with IP address:
   ```plaintext
   interface vlan 1
   ip address 192.168.10.2 255.255.255.0
   no shutdown
   ```

3. **Configure Access Mode and VLAN Assignment**:
   Access ports were configured to belong to VLAN 1. Here’s a sample configuration applied to an interface:
   ```plaintext
   interface fastEthernet 0/1
   switchport mode access
   switchport access vlan 1
   no shutdown
   ```

4. **Save Configuration**:
   To save the configuration, the following command was used:
   ```plaintext
   copy running-config startup-config
   ```

5. **Verify VLANs and Interfaces**:
   Used commands to verify interface and VLAN status:
   ```plaintext
   show ip int brief
   show vlan brief
   ```

### Observed Issues and Troubleshooting

1. **Unrecognized Commands**:
   - Attempted various abbreviations (`wri`, `int`) that were unrecognized by the system, resulting in errors.
   - Example:
     ```plaintext
     R1#wri?
     % Unrecognized command
     ```

2. **Incorrect Syntax**:
   - Mistakenly used incomplete or incorrect syntax in commands, such as `int` without specifying the full interface type (`int gi0/1`).
   - Attempted to use `ip routing` on the switch, which was invalid in this context.

3. **Ping Failures**:
   - Initial pings to the switch IP (`192.168.10.2`) from the router failed, indicating that configuration adjustments were required.
   - After configuring both devices properly and ensuring interfaces were `no shutdown`, pings succeeded.

4. **Saving Configuration Attempts**:
   - Different variations of saving commands were attempted (`write memory`, `copy running-config startup-config`). Only `copy running-config startup-config` was consistently successful.

## Final Verification and Testing
1. **Interface Status Check**:
   Used `show ip int brief` to verify interface statuses on both router and switch, ensuring they were up.

2. **Successful Ping Test**:
   Confirmed connectivity by successfully pinging from the router to the switch:
   ```plaintext
   ping 192.168.10.2
   ```

## Key Takeaways and Lessons
1. **Attention to Command Syntax**:
   - Be precise with command syntax to avoid errors. For example, use `copy running-config startup-config` rather than shortcuts like `wri`.
   
2. **Understanding Access Modes**:
   - When configuring switch ports, ensure they are set to `access mode` for connecting endpoint devices unless trunking is intended.

3. **Saving Configurations Regularly**:
   - Regularly save the configuration to avoid losing settings on device reboot.

## Repository Files
- **sessionlog.txt**: The full session log detailing commands, errors, and outcomes for reference.
