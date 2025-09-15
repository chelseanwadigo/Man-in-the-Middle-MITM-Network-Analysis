

<p align="center">
  <img src="https://cdn-icons-png.flaticon.com/512/3064/3064197.png" width="80" alt="MITM Icon">
</p>


<h1 align="center">🕵️‍♂️ Man-in-the-Middle (MITM) Network Analysis</h1>


<h1 align="center">Introduction </h1>
<p align="center">In this project, I performed a **Man-in-the-Middle (MITM)** attack to analyze network traffic on my local network.  
The goal was to understand how an attacker can intercept and view unencrypted data by positioning themselves between a target device and the network gateway. </p>

**Tools & Setup:**
- **Attacker:** Kali Linux (VM)  
- **Target:** Mac  
- **Primary Tool:** Bettercap  

---
<h1 align="center"> 🛠️ Setting up the Environment </h1>

<p align="center">I launched Kali Linux in a virtual machine and opened a terminal.  
Bettercap comes pre-installed, so no additional installation was required. </p>

![Screenshot 2025-09-15 at ![Screenshot 2025-09-15 at 4 58 52 PM](https://github.com/user-attachments/assets/10ffbad4-3b0f-4fa9-af81-a9e6b48cc5a3)
4 58 29 PM](https://github.com/user-attachments/assets/e2dd5b1e-43a8-44db-8e01-d386cc68dcff)

```bash root@kali:~# bettercap ```

---
<h1 align="center">📡 Discovering Network Hosts</h1>

To identify devices on my network, I used Bettercap's net.probe module:

```net.probe on```
This command lists all active
devices, including IP addresses and MAC addresses.
✅ My target Mac was at 192.168.0.x

![Screenshot 2025-09-15 at 5 00 51 PM](https://github.com/user-attachments/assets/84dc0eeb-fe53-43e6-a756-d1ec38820afd)

Tip: Type help in the Bettercap console to see all available commands. 

---
<h1 align="center"> 🎭 Performing ARP Spoofing</h1>

The core of MITM attacks is ARP spoofing: tricking the target and gateway into thinking the attacker is the other device.
 ``` arp.spoof on ```
I also set full duplex mode to redirect traffic in both directions:

```set arp.spoof.fullduplex true```
![Screenshot 2025-09-15 at 5 02 15 PM](https://github.com/user-attachments/assets/6faf0dfa-9df9-417e-8c98-c9b5fed43364)

---
<h1 align="center">🕵️ Sniffing Network Traffic</h1>



With ARP spoofing active, all traffic from the target passed through Kali Linux.
I captured and displayed packets with:
```net.sniff on```
This allowed me to see unencrypted HTTP traffic, including visited URLs and login pages.

![Screenshot 2025-09-15 at 5 14 22 PM](https://github.com/user-attachments/assets/6dfea3aa-6fdd-441d-b509-ff4ae4f74f8e)

![Screenshot 2025-09-15 at 5 16 11 PM](https://github.com/user-attachments/assets/810f8382-8090-4b53-a3a5-b4ec4c80cfe0)

The first screenshot shows the results of this command. I can see various network packets, including HTTP requests.

The second screenshot demonstrates how specific application traffic is also captured. I was playing music on Apple Music, and the sniffer picked up the network activity, identifying that I was accessing itunes.apple.com. This shows how a sniffer can reveal which applications a target is using, even for services that might be more complex than a simple web browser.

Once I had finished my analysis, I needed to properly exit the attack to restore normal network traffic for my target. Simply closing the terminal would not reverse the ARP spoofing, leaving the target device without a proper connection. To do this, I first disabled the net.sniff module and then the arp.spoof module.


| Step | Screenshot |
|------|------------|
| 1    | ![Screenshot 2025-09-15 at 5 21 16 PM](https://github.com/user-attachments/assets/ae278408-588d-41ff-9a57-e9febbe448ba) |
| 2    | <img width="600" alt="Screenshot 2025-09-15 at 5 36 59 PM" src="https://github.com/user-attachments/assets/893e1257-cfc3-42e0-9c63-665ba8fbb6e5" /> |
| 3    | ![Screenshot 2025-09-15 at 5 39 21 PM](https://github.com/user-attachments/assets/d2dbe23a-58eb-46e5-a537-da9743ba8733) |


   ---

   <h1 align="center"> 🎓 Conclusion</h1>


This project successfully demonstrated the practical application of a Man-in-the-Middle (MITM) attack using ARP spoofing and the Bettercap framework. By placing my Kali Linux machine between a target Mac and the network gateway, I was able to intercept and analyze all network traffic, including unencrypted data.

The key takeaway is a clear and powerful illustration of why network encryption is so critical. The ability to easily view unencrypted traffic, such as the iTunes connection I captured, underscores the vulnerability of devices on unsecure networks. This hands-on experience not only clarified the mechanics of an MITM attack but also highlighted the fundamental importance of using HTTPS and other secure protocols to protect personal data from prying eyes. This project serves as a strong foundation for future exploration into network security and defense.


