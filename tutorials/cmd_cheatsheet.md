### 1. `ipconfig /all`
*The mother of all Windows networking commands.*

- **What it does:** Displays your full IP configuration—IPv4, subnet mask, default gateway, DNS servers, DHCP status, and MAC address.
- **What to check:**
  - **IPv4 Address** – Is it a `169.254.x.x` address? That means DHCP failed (no connection to the router). It should be in your expected subnet (e.g., `192.168.1.x`).
  - **Default Gateway** – This is your router. If it’s missing or wrong, you can’t reach the internet.
  - **DHCP Enabled** – If it says "Yes" but you have a static IP set elsewhere, you’ll have conflicts. If it says "No" but the network uses DHCP, you'll have a manual config error.
  - **DNS Servers** – Are they internal (company) or external (like 8.8.8.8)? If they point to a dead server, domain names won't resolve.

---

### 2. `ping [IP or hostname]` (e.g., `ping 8.8.8.8` or `ping google.com`)

- **What it does:** Sends 4 ICMP echo requests to test basic reachability and response time.
- **What to check:**
  - **"Reply from..."** – Success. Check the `time=XXms`. If it's over 100ms locally, something is congested. If it jumps erratically, you have latency spikes.
  - **"Request timed out"** – The device is offline, blocked by a firewall, or the IP doesn't exist.
  - **"Destination host unreachable"** – Your *own* machine doesn't have a route to that network (often a default gateway or subnet mask issue).
  - **"TTL="** – Starting TTL (usually 64 for Linux, 128 for Windows, 255 for Cisco) tells you the OS of the remote device. If TTL drops to 1, it means a router loop.

---

### 3. `tracert [IP or hostname]` (e.g., `tracert 8.8.8.8`)

- **What it does:** Traces every router (hop) your packets travel through to reach the destination.
- **What to check:**
  - **Where does it stop?** If hops 1–3 succeed and hop 4 times out, the problem is at that specific router or beyond. You now know *where* to point fingers.
  - **RTO (Request Timed Out) in the middle** – If a hop shows `* * *` but subsequent hops succeed, that router is configured not to reply to pings (not an error). But if everything stops there, that's your breakpoint.
  - **Wildly increasing response times** – If hop 2 is 5ms, hop 3 is 150ms, hop 4 is 300ms—you've found a congested or oversubscribed link.

---

### 4. `nslookup [hostname]` (e.g., `nslookup google.com`)

- **What it does:** Queries DNS servers to translate a hostname into an IP address (and vice versa).
- **What to check:**
  - **Which DNS server is replying?** Look at the very top—it shows your current DNS resolver. Is that the one you *expect* (e.g., your company's internal DNS)?
  - **"Non-existent domain"** – The hostname doesn't exist or your DNS server can't find it (check your DNS suffix settings).
  - **Does the returned IP make sense?** For an internal server, you should get a private IP (e.g., 10.x.x.x). If you get a public IP for an internal resource, your DNS resolution path is broken.
  - *Pro tip:* Run `nslookup [IP]` to do a reverse lookup—does it return the correct hostname? Great for verifying PTR records.

---

### 5. `netstat -an` (or `netstat -b` for admin users)

- **What it does:** Lists all active TCP/UDP connections and listening ports on your machine.
- **What to check:**
  - **State column** – `LISTENING` = a service is waiting for connections. `ESTABLISHED` = an active conversation. `TIME_WAIT` = normal closure. `SYN_SENT` = trying to connect but not getting a response—potential firewall or service down.
  - **Foreign Address** – If you see a connection to an unknown IP on port 4444 or 1337, you might have malware. If you see `0.0.0.0:135` listening, that’s a standard RPC port.
  - **Are required services listening?** For example, if a printer share uses port 9100, `netstat -an` will tell you if the port is open and listening.

---

### 6. `arp -a`

- **What it does:** Shows the Address Resolution Protocol (ARP) table—mapping IP addresses to physical MAC addresses on your local network.
- **What to check:**
  - **Duplicate entries?** If you see two different IPs with the *same MAC address*, it's often a misconfigured router, a proxy-ARP issue, or an IP conflict.
  - **Missing gateway?** If your default gateway IP isn't in this list, your machine hasn't talked to it—check your cable or Wi-Fi.
  - **Static vs Dynamic** – If an entry shows as `static`, it was manually added. If you see a strange static entry pointing to a bogus MAC, that could be an ARP spoofing attack.
  - If a device responds to ping but doesn't show up in `arp -a`, it's on a different subnet (requiring routing) or the switch is isolating traffic.

---

### 7. `route print`

- **What it does:** Displays the machine's IP routing table—how your PC decides where to send packets.
- **What to check:**
  - **Network Destination `0.0.0.0`** – This is your default route. The `Gateway` column *must* be your actual router IP. If this points to an old gateway, you can't reach the internet.
  - **Metric column** – Lower metric = higher priority. If you have two default routes (e.g., Wi-Fi and Ethernet), the one with the lower metric is used. If the wrong one has the lower metric, traffic goes out the wrong interface.
  - **"On-link" entries** – These are directly connected subnets. If your PC shows `192.168.1.0` as on-link but your IP is `192.168.2.5`, you've got a subnet mask mismatch.

---

### 8. `getmac /v`

- **What it does:** Retrieves the physical (MAC) address of all network adapters on your machine.
- **What to check:**
  - **Does the MAC match the sticker on the physical device?** If a switch uses MAC filtering and you just swapped a laptop, you'll need this to register the new adapter.
  - **Connection Name** – It lists which MAC belongs to Wi-Fi vs Ethernet. If you're trying to allow-list a specific port in the server room, make sure you're copying the *correct* adapter's MAC.
  - If `getmac` shows `Media disconnected` for your ethernet, the cable is unplugged or the switch port is dead.

---

### 9. `pathping [IP or hostname]` (e.g., `pathping google.com`)

- **What it does:** A hybrid of `tracert` and `ping`—it traces the route AND then sends bursts of pings to each hop to calculate packet loss and latency over a longer period.
- **What to check:**
  - **The "Loss %" column per hop** – If hop 2 shows 0% loss but hop 3 shows 50% loss, that's where the congestion is. If hop 2 shows 50% and hop 3 shows 50%, the problem is at hop 2 (or the link between hop 1 and 2).
  - **"This node" row** – It shows your own machine's stats. If you have packet loss right out of the gate, your network card or cable is faulty.
  - It runs for several minutes, so use it when you need *evidence* of intermittent loss, not just a quick snapshot.

---

### 10. `netsh interface ip show config`

- **What it does:** Shows a clean, detailed summary of IP configuration for all interfaces (sometimes easier to read than `ipconfig /all`).
- **What to check:**
  - **DHCP vs Static** – It explicitly says whether DHCP is enabled. If it says "Yes" but you have a static IP set, Windows is ignoring your static config—reboot or reapply.
  - **Interface name** – It lists Wi-Fi, Ethernet, Bluetooth, etc. If you see a virtual adapter with a strange IP, that might be a VPN or hypervisor connection. Are you accidentally routing through a VPN tunnel you forgot about?
  - **Default gateway metric** – If the metric is unusually high (e.g., 5000), your PC will prefer other routes, causing extremely slow failover or random timeouts.

---

### 11. (Bonus) `systeminfo | findstr "Network"` or just `hostname`

- **Hostname** – Gives you the computer's network name. When a switch or router shows "Device XYZ" connected, this tells you if it's actually *your* workstation you're troubleshooting.
- **What to check:** If `hostname` returns a name that doesn't match the asset tag or the user's reported PC name, you might be on the wrong machine remotely.

---

### 🧠 Field-Proven Rule of Thumb
When you're overwhelmed, **use them in this order**:
1. `ipconfig /all` – *"Is my machine configured correctly?"*
2. `ping` the gateway – *"Can I talk to my router?"*
3. `ping 8.8.8.8` – *"Can I reach the internet?"*
4. `nslookup google.com` – *"Is my DNS working?"*
5. `tracert` or `pathping` – *"Where is the slowdown/break?"*

Every one of these gives you hard data—so when you escalate to your supervisor, you're not guessing, you're handing them a diagnosis. That's what turns a newcomer into a trusted asset. You've got this! 💪

[Go back to **HOME**](../README.md)