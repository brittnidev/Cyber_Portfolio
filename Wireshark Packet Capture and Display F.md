# Wireshark Packet Capture and Display Filtering: Observing Website Traffic

## Project Summary
A guided practical exercise using Wireshark to capture network traffic on a designated interface, apply display filters to observe HTTP/HTTPS traffic, identify specific IP addresses, and use conditional filters to locate packets of interest. The project demonstrates hands-on skills in packet capture, filtering syntax, and basic network traffic analysis.

## Learning Objectives
- Install and configure Wireshark on Linux (verify proper privileges for capture).
- Capture live packets on a detected network interface and save the capture to a file.
- Apply display filters to observe specific protocols (e.g., HTTP, HTTPS) and ports (80, 443).
- Create filters to locate traffic associated with a particular IP address (ip.addr).
- Use conditional/advanced display filters to refine results (e.g., combining NOT and AND with parentheses).
- Interpret TLS/HTTPS handshake elements (ClientHello, ServerName, SNI) and distinguish encrypted payload from handshake data.
- Document findings and justify filtering decisions, including handling CDN/proxy effects.

## Project Deliverables
- A captured PCAP/PCAPNG file saved from a real network session.
- A set of display filters used during the exercise, documented clearly:
  - Example: `tcp.port == 80` for HTTP, `tcp.port == 443` for HTTPS
  - Example: `ip.addr == x.x.x.x` to locate a specific IP
  - Example: `!(ip.addr == x.x.x.x) and tcp.port == 443` for excluding an IP while observing HTTPS
- A short report detailing:
  - The capture environment (interface name, host/VM details, network context)
  - Websites visited during capture (e.g., google.com, duckduckgo.com, cygwin.com)
  - Observations from TLS handshakes (ClientHello, SNI) and notable certificate or cipher suite details
  - Challenges encountered (e.g., TLS encryption, CDN IP resolution) and how you addressed them
- Screenshots or annotated excerpts showing:
  - Filtered packet lists (HTTP on port 80, HTTPS on port 443)
  - A TLS ClientHello with SNI visible
  - The saved PCAP file metadata

## Methodology
- **Environment setup:** Prepared a host (Linux) with Wireshark installed, verified capture permissions, and selected an active network interface.
- **Data collection:** Performed controlled web browsing to generate representative HTTP/HTTPS traffic (e.g., http://cygwin.com, https://www.google.com, https://www.duckduckgo.com).
- **Filtering strategy:**
  - Basic protocol filters (e.g., `http`, `tcp.port == 80`, `tcp.port == 443`).
  - IP-based filters (`ip.addr`, `ip.dst`, `ip.src`).
  - Conditional filters combining NOT, AND, OR with parentheses to reflect intended logic (e.g., `!(ip.addr == 18.160.96.85) and (tcp.port == 80 or tcp.port == 443)`).
- **Analysis:** Read handshake details (ClientHello, ServerHello, SNI) and noted CDN/IP behavior; discussed implications for security analysis and network forensics.
- **Validation:** Reproduced filtering steps to ensure results are consistent and reproducible.

## Results
- Successfully captured traffic on the designated interface.
- Demonstrated filtering for HTTP and HTTPS traffic.
- Identified how to exclude a specific IP from results while retaining relevant traffic.
- Observed TLS handshake details (including SNI) and discussed limitations of reading HTTP content from HTTPS captures.

## Skills Demonstrated
- Wireshark installation and basic usage on Linux.
- Live capture on a network interface and saving PCAP files.
- Crafting and applying display filters (e.g., `http`, `tcp.port`, `ip.addr`, logical operators).
- Interpreting TLS handshake components and addressing encrypted payloads.
- Problem-solving for CDN/proxy traffic and interface selection in diverse environments.

## Usage Notes
- Include a link to the Coursera certificate as verification of completion (if allowed by your platform).
- Attach or link the PCAP file if your portfolio supports file uploads.
- Add a brief reflection on learning outcomes, limitations (e.g., TLS encryption, CDN IP rotation), and potential future work (e.g., TLS decryption in a lab, HTTP content inspection).

## Quick Commands / Filters (for reference)

- Display all HTTP traffic on port 80:
  ```
  tcp.port == 80
  ```
- Display both HTTP and HTTPS traffic:
  ```
  tcp.port == 80 or tcp.port == 443
  ```
- Exclude a specific IP while showing HTTPS traffic:
  ```
  !(ip.addr == 18.160.96.85) and tcp.port == 443
  ```
- Exclude a specific IP while showing HTTP/HTTPS:
  ```
  !(ip.addr == 18.160.96.85) and (tcp.port == 80 or tcp.port == 443)
  ```
