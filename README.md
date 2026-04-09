# SSH-Log-Analysis-Project-SOC-Analyst-Simulation-
This project focuses on analyzing SSH authentication logs to identify suspicious activities and potential cyber attacks. The objective is to simulate the role of a SOC (Security Operations Center) analyst by detecting unauthorized access attempts and classifying threats based on behavior.

Name of data-logs file : auth.log 

tools and commands used :

linux Terminal: grep, awk, sort, uniq

Example: 

  #find ip from many logs of auth.log file: 
  
    grep -oP 'from \K[0-9.]+' auth.log
  
  #print all columns from auth.log : 
  
    awk '{print}' auth.log, cat auth.log
  
  #for particular columns from entire file, -f option of awk is use as saperator of clomuns ' ' :
  
    awk -F' ' '{print $4}' auth.log
  
  #for count how many time the specific ip found:
  
    grep -oP 'from \K[0-9.]+' auth.log | sort | uniq -c | sort -nr

## Methodology
  -Collected SSH log data (auth.log)
  
  -Filtered failed login attempts using grep
  
  -Extracted IP addresses from logs
  
  -Counted repeated attempts per IP
  
  -Analyzed behavior based on :
  
    -Frequency of attempts
    
    -Time duration
    
    -Targeted usernames

## Findings
🔴 High-Risk IPs Identified:

        ip : 122.163.61.218
        30 attempts within 1 minute
        Targeted multiple users (root, admin, ubnt)
        Type: Credential Stuffing Attack
        
        ip : 34.204.227.175
        43 attempts within 4 minutes
        High-speed login attempts
        Type: Brute Force Attack
        
        ip : 24.151.103.17
        156 attempts over ~3 hours
        Persistent attack behavior
        Type: Slow Brute Force Attack
        
        ip : 49.4.143.105
        39 attempts targeting root user
        Focused attack
        Type: Targeted Brute Force Attack

## Analysis
  -Multiple IPs attempted unauthorized access
  
  -Some IPs showed low-level activity (background noise)
  
  -High-frequency and fast attempts indicate automated attacks
  
  -Targeting of privileged accounts (root/admin) increases risk severity

## Recommendations for actual systems
  
  -Disable root login via SSH
  
  -Implement SSH key-based authentication
  
  -Use tools like Fail2Ban to block repeated attempts
  
  -Apply firewall rules to block malicious IPs
  
  -Enable logging and monitoring systems
