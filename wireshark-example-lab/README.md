
    SOC LAB REPORT — Network Traffic Analysis
Analyst Name  : Ozioko Uchenna
Date          : April 6, 2026
Tool Used     : Wireshark
Target        : example.com
Capture File  : wireshark_eth0FHTCN3.pcapng
Total Packets : 21

FINDING 1 — DNS Resolution

DNS Query Sent To    : 192.168.17.204 (local resolver)
Website Resolved To  : 104.18.27.120
Observation          : My computer successfully resolved 
                       example.com to IP 104.18.27.120 
                       through the local DNS resolver 
                       before making any connection.


FINDING 2 — TCP Three-Way Handshake; 
My Computer IP       : 10.0.2.15
example.com IP       : 104.18.27.120
Port Used            : 443 (HTTPS)
Packet 5  [SYN]      → My computer knocked
Packet 6  [SYN RTX]  → My computer knocked again
Packet 7  [SYN-ACK]  → example.com opened the door
Packet 8  [ACK]      → Connection confirmed
Observation          : Full TCP handshake completed 
                       on port 443 confirming HTTPS.


FINDING 3 — TLS Handshake Analysis
TLS Version          : TLS 1.3
SNI Field            : example.com (visible in plain text)
Client Hello         : Packet 9 
Server Hello         : Packet 12  
Cipher Suites Offered: 17
Application Data     : Packets 14 16 18 19 20 
Observation          : Full TLS 1.3 session established. 
                       SNI confirmed destination without 
                       decrypting any traffic.


FINDING 4 — HTTP vs HTTPS Confirmation

HTTP Filter Result   : No packets found
Port Observed        : 443 (HTTPS only)
Observation          : example.com enforces full HTTPS 
                       encryption. Zero unencrypted 
                       data was transmitted.
                       
FINDING 5 — Conversation Mapping

Total Conversations  : 2
Main Session Packets : 17
Main Session Data    : 5 kB
Session Duration     : 2.936 seconds
Observation          : Normal data volume for a simple 
                       webpage. No signs of exfiltration.


FINDING 6 — Endpoint Analysis

Total Endpoints      : 3
External IPs Found   : 1 (104.18.27.120)
Local IPs Found      : 2 (10.0.2.15, 192.168.17.204)
Threat Check         : 104.18.27.120 = Cloudflare/
                       example.com — LEGITIMATE 
Observation          : No unexpected external connections.
                       Only one external server contacted.


OVERALL VERDICT

Classification       : BENIGN 
Reason               : All traffic follows normal expected 
                       behaviour for an HTTPS web request.
                       DNS resolved correctly. TCP handshake
                       completed. TLS 1.3 encryption 
                       confirmed. SNI matches destination.
                       No anomalies or suspicious IPs 
                       detected.
