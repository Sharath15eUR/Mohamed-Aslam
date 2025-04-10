# WiFi Training Program  
## Assignment Questions – Module 2

### 1. Split MAC Architecture and Its Advantages for Access Point (AP) Performance

The Split MAC architecture is a wireless network design that separates Media Access Control (MAC) functions between the Access Point (AP) and a centralized controller, typically referred to as the Wireless LAN Controller (WLC).

#### Operation of Split MAC Architecture:

- **Real-Time MAC Functions (handled by the AP):**
  - Beacon generation
  - Probe request/response handling
  - Processing control frames (e.g., RTS/CTS)
  - Retransmissions

- **Non-Real-Time MAC Functions (handled by the WLC):**
  - Authentication and deauthentication
  - Association and reassociation
  - Ethernet and Wireless LAN bridging
  - Fragmentation

#### Key Benefits:
- **Enhanced Performance:** Delegating non-time-critical tasks to the WLC allows the AP to focus on latency-sensitive operations.
- **Centralized Management:** Simplifies network administration by managing multiple APs from a single WLC.
- **Improved Security:** Centralized encryption and authentication maintain uniform security protocols.
- **Scalability:** Adding APs is seamless without complicating overall network management.

### 2. What is CAPWAP and How Does It Manage Communication Between AP and Controller?

CAPWAP (Control and Provisioning of Wireless Access Points) is a standardized protocol used for managing and controlling APs from a centralized WLC. It facilitates streamlined communication and network provisioning.

#### CAPWAP Protocol Structure:
- **Control Plane:** Handles configuration, management, authentication, and association messages.
- **Data Plane:** Transports user data between the AP and the WLC through secure tunneling.

#### CAPWAP Communication Flow:
1. **Discovery:** AP sends a discovery request; WLC replies with a discovery response.
2. **TLS Setup:** A DTLS (Datagram Transport Layer Security) session is established to encrypt subsequent communication.
3. **Join Phase:** AP sends a Join Request; WLC responds with a Join Response.
4. **Image Transfer:** If firmware versions differ, the AP downloads the correct image and reboots.
5. **Configuration:** AP requests configuration status; WLC responds accordingly.
6. **Operational Mode:** The AP begins handling client data and management traffic under WLC control.

#### CAPWAP Advantages:
- **Centralized Control:** Simplifies network management across multiple APs.
- **Secure Communication:** DTLS ensures data integrity and security.
- **Network Scalability:** Easily accommodates growing wireless infrastructure.

### 3. CAPWAP in the OSI Model and the Role of Its Two Tunnels

CAPWAP primarily operates at the **Data Link Layer (Layer 2)** and **Network Layer (Layer 3)** of the OSI model, using UDP (Layer 4) for transport.

#### Types of CAPWAP Tunnels:
1. **Control Tunnel (UDP Port 5246):** Used for management tasks such as configuration, authentication, and AP association with the WLC.
2. **Data Tunnel (UDP Port 5247):** Transports client data between AP and WLC, encapsulating wireless frames for secure transmission.

### 4. Difference Between Lightweight and Cloud-Based Access Points

#### Lightweight Access Points (LWAP):
- Requires a WLC for operation.
- Communicates via CAPWAP.
- Centralized configuration and policy enforcement.
- Supports seamless roaming for users.

#### Cloud-Based Access Points:
- Managed through a cloud controller—no physical WLC required.
- Enables remote configuration and monitoring.
- Ideal for distributed and multi-site deployments.

### 5. How CAPWAP Tunnel Is Maintained Between AP and WLC

CAPWAP creates a secure channel between Lightweight APs and the WLC to maintain ongoing configuration, monitoring, and traffic management.

#### Maintenance Process:
1. AP discovers the WLC via DHCP, DNS, or broadcast.
2. Authentication and configuration messages are exchanged.
3. CAPWAP control and data tunnels are established.
4. Client traffic flows through WLC for routing and policy application.

### 6. Difference Between Sniffer Mode and Monitor Mode

Both modes are used to analyze wireless environments but differ in purpose:

#### Sniffer Mode:
- Captures Layer 2 frames and forwards them to tools like Wireshark.
- Used for performance analysis and network troubleshooting.
- Ideal for packet-level inspection on specific channels.

#### Monitor Mode:
- Performs passive scanning across all channels.
- Detects rogue APs and unauthorized devices.
- Used for spectrum analysis, security, and environment scanning.

### 7. Optimal AP Mode for WAN-Deployed WLCs in Local Networks

**FlexConnect Mode (formerly H-REAP)** is most suitable:

- Allows APs to locally switch traffic, minimizing WAN latency.
- Continues to serve clients even if WLC becomes unreachable.
- Management traffic is still sent to WLC for centralized control.

### 8. Challenges of Deploying Over 50 Autonomous APs in Large Networks (e.g., Universities)

#### Key Challenges:
- **Manual Setup:** Each AP needs individual configuration.
- **No Centralized Management:** Increases complexity for updates and troubleshooting.
- **Roaming Issues:** Lack of coordination leads to session drops.
- **Scalability:** Difficult to efficiently manage without automation or centralized control.

### 9. Behavior of Lightweight AP in Local Mode if WLC Fails

In **Local Mode**, LWAPs rely on the WLC for all major functions.

| **Function**        | **Behavior if WLC Fails**                                             |
|---------------------|------------------------------------------------------------------------|
| CAPWAP Tunnel        | Breaks, losing AP-WLC communication                                   |
| Client Connections   | Active sessions are dropped                                           |
| Data Traffic         | Stops flowing; AP cannot forward data                                 |
| New Clients          | Cannot connect; AP ceases SSID broadcast                              |
| Roaming              | Not supported due to lack of WLC coordination                         |
| AP Recovery          | AP attempts to reconnect to the primary or backup WLC                 |

#### Recommended Solution:
**FlexConnect Mode** enables APs to continue servicing clients locally when WLC becomes unreachable, ensuring minimal disruption in branch or WAN-dependent networks.