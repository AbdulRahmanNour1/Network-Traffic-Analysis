# Network Traffic Analysis

To Identify different types of traffic with protocols and ports, We gotta use filters.


**HTTP Request**
![[Pasted image 20250812012709.png]]

**What that means??**
	We can see 5 layers in the lower-left square, which follows TCP/IP model:
		1. Physical (Ethernet)
			This is the entire captured size of the packet from the wire.
		2. Link
			With source and destination MAC address, This all going inside the local network.
		3. Network 
			With source and destination IP address, This is going in internet or public network.
		4. Transport
			With source and destination port, Carrying the protocol.
		5. Application
			This is the content of the packet.

**HTTPS**![[Pasted image 20250823172040.png]]

**HTTP, DNS**
![[Pasted image 20250802173632.png]]
*The "or" allows us to check packets using either HTTP or DNS protocol*
##### Spotting unusual or suspicious traffic:
- **DNS requests** to strange or random domains (often malware-related)
	  e.g. filter `dns.qry.name matches "[0-9a-z]{20,}"`
- **Frequent external connections** to unknown IPs
	  e.g. filter `ip.dst == x.x.x.x` (where x.x.x.x is the suspected IP)
- **Non-standard ports** being used (e.g. TCP port 6667 for IRC)
	  e.g. filter `tcp.port != 80 && tcp.port != 443`
- **Repetitive traffic patterns** or high volume over time (possibly port scanning via tools e.g. nmap)
	  e.g. filter `icmp` (the hacker is using nmap without `-Pn` switch which skips ICMP requests)
Luckily, There is an option called Expert Information (Analyze -> Expert Information) which a detected severity with summaries, very useful with experience to save time (Not all severities are dangerous, some are just warnings).

**Massive DOS Attack with entropy**
![[Pasted image 20250823175040.png]]

---
### Recommendations to mitigate risks:

- **Intrusion Detection and Prevention Systems (IDS/IPS)** to automatically detect and block malicious activity.
- **Firewall** as the first line of defense, preventing unauthorized access to and from the network. By restricting traffic to only necessary services, it minimizes the attack surface and reduces the chance of intrusion.
- **Network Segmentation & VLANs** to isolate sensitive systems from general traffic, reducing lateral movement in case of compromise.
- **Zero Trust Architecture** requiring verification for every access request, regardless of network location.
- **Advanced Endpoint Protection** (EDR) to monitor and respond to threats on individual devices.
- **Regular Patch Management** to ensure all systems are up to date against known vulnerabilities.
- **Multi-Factor Authentication (MFA)** for all critical accounts to reduce risks from stolen credentials.
- **Security Information and Event Management (SIEM)** for centralized log collection and real-time threat correlation.
---
[Video Link ](https://www.youtube.com/watch?v=o-C3C_mY1iw)