## Key Findings:

 **DNS Traffic**
  - Captured DNS requests for `google.com`, `cisco.com` and `grubbe.com`
  - Observed different IP addresses associated with DNS queries
    Queried Domains: `google.com`, `cisco.com` and `grubbe.com`
    Response Code: `google.com` and `cisco.com` No error (0) | while `grubbe.com` reported 'Server failure'
  - IP Returned: `google.com` 142.250.184.238 | `cisco.com` 72.163.4.185 | `grubbe.com` Server failure
  - Server failure incates that the server does not exist.
    
 **HTTP Traffic**
  - Identified HTTP GET requests to various websites, such as `neverssl.com`, `x.com` and `google.com`
  - Observed HTTP headers, including `User-Agent`, `Host`, `Accept` and `Content-type`
    Method: Get
    Observed hosts: `neverssl.com`, `x.com` and `google.com`
    Response code: `neverssl.com` 200 OK | `x.com` 301 Moved Permanently | `google.com` 301 Moved Permanently and 302 Found.
  - Content-Type: text/html. 

 **TCP Traffic**
  - Seen standard 3-way TCP handshake (SYN, SYN-ACK, ACK)
  - Analyzed the connection establishment for `80` and `443` ports (HTTP/HTTPS)
    From 132.172.3.100 to 34.223.124.45 (http://neverssl.com)
    From 132.172.3.100 to 216.58.223.227 (https://www.google.com)
  - During the packet capture, a standard TCP 3-way handshake was observed between my device and public web servers:
    (34.223.124.45, 216.58.223.227)
  - This process is crucial for establishing a reliable connection before any data is transmitted.

 **TLS Encrypted Traffic (HTTPS)**
  - Captured a Client Hello packet
  - The handshake was part of a secure connection to an HTTPS website `https://gstatic.com`
  - While visiting `google.com`, a secure TLS handshake was captured with `www.gstatic.com` — a content delivery domain,
    used by Google to serve static assets
  - This is common behavior in modern websites, where resources are loaded from multiple domains to improve performance and load times.
    Server Name (SNI): www.gstatic.com
    Destination IP: 216.58.223.227
    Port: 443  
  - This is the first step in establishing a secure connection via HTTPS
  - The packet includes information about the client's supported TLS versions and cipher suites.

## What I Learned:

- How to use Wireshark for basic network protocol analysis
- How to filter and identify DNS and HTTP traffic
- How HTTP requests are made and how to locate GET requests in packet data
- Key network protocols such as TCP/IP and TLS
- The structure of a TCP 3-way handshake (SYN → SYN-ACK → ACK)
- What a TLS handshake looks like in action, including the Client Hello and SNI
- How to sanitize sensitive network data (e.g IP and MAC addresses)
- How to interpret protocol hierarchy stats to see what types of traffic were most active.

## WHY This Matters in Cybersecurity
- Understanding raw network traffic is foundational for detecting suspicious or malicious activity
- Analyzing HTTP and TLS flows helps you spot common vulnerabilities like unencrypted data or misconfigured servers
- Traffic captures are used in threat hunting, incident response, and network forensics
- Being able to identify normal behavior (like TLS handshakes or HTTP requests) helps you spot anomalies.

## What I’d Improve Next Time 🔧
- Generate a wider variety of traffic (DNS, FTP, ICMP) to deepen protocol analysis
- Include more secure vs insecure traffic comparisons (HTTP vs HTTPS)
- Practice writing custom Wireshark display filters for faster analysis
- Explore more tools for traffic anonymization.
