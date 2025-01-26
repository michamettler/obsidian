#itsecurity #sem5

A distributed denial-of-service (DDoS) attack is a malicious attempt to disrupt the normal traffic of a targeted server, service or network by overwhelming the target or its surrounding infrastructure with a flood of Internet traffic, often by botnets (group of computers which have been infected by malware and have come under the control of a malicious actor.)
https://www.cloudflare.com/en-gb/learning/ddos/what-is-a-ddos-attack/
## Botnet Models
https://www.cloudflare.com/en-gb/learning/ddos/what-is-a-ddos-botnet/
### client/server botnet model
In this model each bot will connect to a command-and-control center (CnC) resource like a web domain or an IRC channel in order to receive instructions (not used much as CNC is single point of Failure). Can also be hierarchical.
![[Pasted image 20241101132737.png#invert]]
### peer-to-peer botnet model
List of trusted computers with which they can give and receive communications and update their malware. Each bot is only exposed to adjacent devices, making it harder to track and more difficult to mitigate. Lacking a centralized command server makes a peer-to-peer botnet more vulnerable to control by someone other than the botnet’s creator. To protect against loss of control, decentralized botnets are typically encrypted so that access is limited.
![[Pasted image 20241101133200.png#invert]]
## Attack Types
### Application Layer
Sometimes referred to as a DDoS attack (in reference to the 7th layer of the OSI-Model), the goal of these attacks is to exhaust the target’s resources to create a denial-of-service. An application layer attack creates more damage with less total bandwidth.
##### Mitigations
- Difficult because it seems like a legitimate request
- CAPTCHA
- [[#Web Application Firewall (WAF)]]
#### HTTP Flood
https://www.cloudflare.com/en-gb/learning/ddos/application-layer-ddos-attack/

This attack is similar to pressing refresh in a web browser over and over on many different computers at once – large numbers of HTTP requests flood the server, resulting in denial-of-service.
![[Pasted image 20241101130819.png#invert]]
### Transport Layer
#### SYN Flood
https://www.cloudflare.com/en-gb/learning/ddos/syn-flood-ddos-attack/

This attack exploits the TCP Handshake by sending a target a large number of TCP “Initial Connection Request” SYN packets with source IP addresses.
The target machine responds to each connection request and then waits for the final step in the handshake, which never occurs, exhausting the target’s resources in the process. In networking, when a server is leaving a connection open but the machine on the other side of the connection is not, the connection is considered half-open. In this type of DDoS attack, the targeted server is continuously leaving open connections and waiting for each connection to timeout before the ports become available again. The result is that this type of attack can be considered a “half-open attack”.
![[Pasted image 20241101130745.png#invert]]
Direct attack via plain IP (not spoofed). This is often mitigated by [[Firewall]] rules that stop outgoing packets other than SYN packets or by filtering out any incoming SYN-ACK packets before they reach the malicious user's machine
##### Mitigation
- Backlog Queue (certain number of half-open connections that it will allow)
- Recycling the Oldest Half-Open TCP connection
- SYN Cookies (server responds to each connection request with a SYN-ACK packet but then drops the SYN request from the backlog, removing the request from memory and leaving the port open and ready to make a new connection)
### Volumetric attacks
This category of attacks attempts to create congestion by consuming all available bandwidth between the target and the larger Internet. Large amounts of data are sent to a target by using a form of amplification or another means of creating massive traffic, such as requests from a botnet.
![[Pasted image 20241101130905.png#invert]]
#### DNS Amplification
https://www.cloudflare.com/en-gb/learning/ddos/dns-amplification-ddos-attack/

By making a request to an open DNS server with a spoofed IP address (the IP address of the victim), the target IP address then receives a response from the server.
1. send UDP packets with spoofed IP addresses to a DNS recursor. The spoofed address on the packets points to the real IP address of the victim.
2. Each one of the UDP packets makes a request to a DNS resolver, often passing an argument such as “ANY” in order to receive the largest response possible.
3. After receiving the requests, the DNS resolver, which is trying to be helpful by responding, sends a large response to the spoofed IP address.
4. The IP address of the target receives the response and the surrounding network infrastructure becomes overwhelmed with the deluge of traffic, resulting in a denial-of-service.
##### Mitigation
- Reduce the total number of open DNS resolvers
- Source IP verification – stop spoofed packets leaving network
### Multi-Vector Attacks
A multi-vector DDoS attack uses multiple attack pathways in order to overwhelm a target in different ways, potentially distracting mitigation efforts on any one trajectory.

---
## Mitigating Attacks
The key concern in mitigating a DDoS attack is differentiating between attack traffic and normal traffic.
### Blackhole Routing
https://www.cloudflare.com/en-gb/learning/ddos/glossary/ddos-blackhole-routing/

One solution available to virtually all network admins is to create a blackhole route and funnel traffic into that route. In its simplest form, when blackhole filtering is implemented without specific restriction criteria, both legitimate and malicious network traffic is routed to a null route, or blackhole, and dropped from the network (not ideal - makes network inaccessible).
### Rate Limiting
Limiting the number of requests a server will accept over a certain time window is also a way of mitigating denial-of-service attacks (likely be insufficient to handle a complex DDoS attack effectively).
### Web Application [[Firewall]] (WAF)
Tool that can assist in mitigating a layer 7 DDoS attack. By putting a WAF between the Internet and an origin server, the WAF may act as a Reverse Proxy, protecting the targeted server from certain types of malicious traffic. One key value of an effective WAF is the ability to quickly implement custom [[Firewall]] rules in response to an attack.
### Anycast Network Diffusion
This mitigation approach uses an Anycast network to scatter the attack traffic across a network of distributed servers to the point where the traffic is absorbed by the network.