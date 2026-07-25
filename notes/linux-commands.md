# Linux Commands Reference

## Navigation
pwd                    # Show current directory
                       # Example: /home/kali

ls -la                 # List all files including hidden
                       # Example: ls -la /home/kali

cd /path               # Change to specific directory
                       # Example: cd /home/kali/Desktop

cd ~                   # Go to home directory
                       # Example: cd ~ (takes you to /home/kali)

cd ..                  # Go up one level
                       # Example: cd .. (from /home/kali/Desktop to /home/kali)

## File Management
touch file.txt         # Create empty file
                       # Example: touch report.txt

mkdir -p folder/sub    # Create folders including parents
                       # Example: mkdir -p writeups/tryhackme

cp file dest           # Copy file
                       # Example: cp report.txt /home/kali/Desktop

mv file dest           # Move or rename file
                       # Example: mv report.txt renamed-report.txt

rm file                # Delete file
                       # Example: rm report.txt

rm -rf folder          # Delete folder and all contents
                       # Example: rm -rf /home/kali/oldfiles

cat file.txt           # Display file contents
                       # Example: cat /etc/passwd

nano file.txt          # Open file in text editor
                       # Example: nano report.txt

## Finding Things
find / -name "file.txt"      # Find file by name
                             # Example: find / -name "passwords.txt"

grep -r "text" /path         # Search for text inside files
                             # Example: grep -r "admin" /var/www/html

locate file.txt              # Quick file search
                             # Example: locate rockyou.txt

which tool                   # Find where tool is installed
                             # Example: which nmap

## System Info
whoami                 # Show current username
                       # Example: whoami (returns: kali)

id                     # Show user ID and groups
                       # Example: id (returns: uid=1000(kali) gid=1000(kali))

uname -a               # Show full system information
                       # Example: uname -a (returns: Linux kali 6.1.0)

df -h                  # Show disk space usage
                       # Example: df -h /dev/sda5

free -h                # Show RAM usage
                       # Example: free -h (shows total/used/free RAM)

top                    # Show running processes live
                       # Example: top (press q to quit)

ps aux                 # List all running processes
                       # Example: ps aux | grep firefox

## Networking
ip a                   # Show all network interfaces and IPs
                       # Example: ip a (look for tun0 for TryHackMe VPN)

ping -c 3 IP           # Test connectivity to an IP
                       # Example: ping -c 3 10.10.10.10

ifconfig               # Show network interface info
                       # Example: ifconfig eth0

netstat -tulpn         # Show open ports and connections
                       # Example: netstat -tulpn | grep 80

ss -tulpn              # Modern version of netstat
                       # Example: ss -tulpn | grep 443

curl URL               # Fetch web page content
                       # Example: curl http://10.10.10.10

wget URL               # Download file from URL
                       # Example: wget http://10.10.10.10/file.txt

## Permissions
chmod 755 file         # Set file permissions
                       # Example: chmod 755 script.sh

chown user file        # Change file owner
                       # Example: chown kali report.txt

sudo command           # Run command as root
                       # Example: sudo nmap -sV 10.10.10.10

sudo -l                # List your sudo permissions
                       # Example: sudo -l (shows what you can run as root)

## Cybersecurity
nmap -sV IP            # Scan ports and detect service versions
                       # Example: nmap -sV 10.10.10.10

nmap -A IP             # Aggressive scan with OS detection
                       # Example: nmap -A 10.10.10.10

nmap -p- IP            # Scan all 65535 ports
                       # Example: nmap -p- 10.10.10.10

gobuster dir -u URL -w wordlist    # Brute force web directories
                                   # Example: gobuster dir -u http://10.10.10.10 -w /usr/share/wordlists/dirb/common.txt

hydra -l user -P list IP ssh       # Brute force SSH login
                                   # Example: hydra -l admin -P /usr/share/wordlists/rockyou.txt 10.10.10.10 ssh

john --wordlist=list hash.txt      # Crack password hashes
                                   # Example: john --wordlist=/usr/share/wordlists/rockyou.txt ~/hash.txt

hashcat -m 0 hash.txt list         # GPU accelerated hash cracking
                                   # Example: hashcat -m 5600 ~/hash.txt /usr/share/wordlists/rockyou.txt

nc -lvnp 4444          # Start netcat listener on port 4444
                       # Example: nc -lvnp 4444 (wait for reverse shell)

nc IP 4444             # Connect to IP using netcat
                       # Example: nc 192.168.149.105 4444

## Git
git add .              # Stage all changes for commit
                       # Example: git add . (stages everything)

git commit -m "message"    # Commit staged changes
                           # Example: git commit -m "Add writeup: Moniker Link"

git push origin main   # Push commits to GitHub
                       # Example: git push origin main

git pull               # Pull latest changes from GitHub
                       # Example: git pull (updates local repo)

git status             # Check current repo status
                       # Example: git status (shows modified files)

git log                # View full commit history
                       # Example: git log --oneline (compact view)

## Tips
# Tab         = Autocomplete commands and file paths
#              Example: type "cd Des" then Tab = "cd Desktop"

# Ctrl+C      = Stop currently running command
#              Example: stops nmap, responder, ping

# Ctrl+L      = Clear the terminal screen
#              Example: clears all previous output

# Up arrow    = Recall previous command
#              Example: press up to rerun last nmap scan

# man command = Open manual page for any command
#              Example: man nmap (shows all nmap options)
