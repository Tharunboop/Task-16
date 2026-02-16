# Task 16 – Incident Response & Security Breach Simulation
Cyber Security Internship

## Objective
To simulate a security incident, analyze system logs, classify the attack, perform containment, and implement preventive security measures using Kali Linux.

---

# Phase 1: Preparation

## SSH Service Verification

Command Used:
sudo systemctl status ssh

Result:
SSH service was active and running.


---

# Phase 2: Configuration

## Enable Password Authentication

File Modified:
/etc/ssh/sshd_config

Changes:
PasswordAuthentication yes

Command Used:
sudo nano /etc/ssh/sshd_config
sudo systemctl restart ssh


---

# Phase 3: Incident Simulation

## Simulated Brute Force Attack

Command Used:
ssh -o PubkeyAuthentication=no kali@localhost

Multiple wrong passwords were entered.

Result:
Permission denied and maximum authentication attempts exceeded.

---

# Phase 4: Identification & Log Analysis

## Log Evidence Using Journalctl

Command Used:
sudo journalctl -u ssh | grep -i "failed"

Observed:
Failed password for kali from 127.0.0.1

---

# Phase 5: Quantifying Attack

Command Used:
sudo journalctl -u ssh | grep -i "failed" | wc -l

Purpose:
Count number of failed attempts.

---

# Phase 6: Containment

## Firewall Configuration

Commands Used:
sudo ufw enable
sudo ufw deny from 127.0.0.1
sudo ufw status

Result:
Attacking IP 127.0.0.1 blocked.
---

# Phase 7: Eradication & Prevention

## Install Fail2Ban

Commands Used:
sudo apt install fail2ban -y
sudo systemctl start fail2ban
sudo systemctl status fail2ban

Result:
Fail2Ban active and monitoring SSH service.

# Incident Classification

Attack Type: SSH Brute Force Attack  
Severity: Medium  
Source IP: 127.0.0.1  
Target User: kali  

---

# Root Cause Analysis

Root Cause:
Password authentication allowed without rate limiting.

Solution:
Implemented Fail2Ban and firewall rules.

---

# Preventive Recommendations

- Use strong passwords
- Disable root SSH login
- Enable Fail2Ban permanently
- Implement IDS/IPS solutions
- Regular log monitoring

---

# Conclusion

The simulated SSH brute-force attack was successfully:
- Detected
- Analyzed
- Contained
- Mitigated
- Documented

This task provided practical understanding of incident response lifecycle phases.
