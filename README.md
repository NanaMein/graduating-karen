# Karen's Cheatsheet & Mentorship Snippets

An open-source guide for Karen (and her classmates) as fresh graduates exploring their first careers. This repository shares real workplace experiences, practical guides, curated roadmaps, and quick cheatsheets that aren't usually taught in school.

Optional: if you want to use OpenCode on Windows, see [OpenCode on Windows](./OPENCODE_WINDOWS.md).

---

# 👋 How this works

Hey Karen! I'm Nana.

This repository isn't meant to replace books or online courses. Instead, it's where I share lessons I've learned from working in different industries. My hope is that some of the mistakes I made and the things I learned the hard way can help make your own journey a little smoother.

Each topic is broken down into two simple parts:

1. **🌟 My Experience** – The real situations I encountered, what happened, and what I learned.
2. **🔗 References** – Curated resources to help you understand the concepts in more depth.

Take your time. Read through the experience first, explore the references, then try the mini challenge at the end.

---

# 📚 Snippet 1: Connecting a Printer to a Wi-Fi Network

## 🎯 Why learn this?

Printers are one of the most common devices you'll encounter in an office. Even if you're not applying for an IT position, knowing how to connect, troubleshoot, and share a printer can save valuable time and leave a great impression on your colleagues.

---

## 🌟 Nana's Experience [Click for full story](./experiences/printer_network_exp.md)
---

## 🛠 Things You'll Probably Encounter

* Connecting a printer to a Wi-Fi network
* Sharing a printer over the office network
* Installing printer drivers
* Setting a printer as the default printer
* Clearing a stuck print queue
* Reading printer error codes
* Replacing toner or ink cartridges
* Fixing paper jams
* Restarting the Print Spooler service
* Assigning a static IP address to a network printer

---

## 💡 Tips from Experience

* Don't panic when you encounter an error code. Search for the printer model together with the error code.
* If multiple users suddenly can't print, check the network first before assuming the printer is broken.
* Restarting both the printer and the computer solves more problems than most beginners expect.
* Learn the difference between USB printers and network printers.
* If your office uses static IP addresses, keep a record of the printer's IP address.
* Don't be afraid to use Google, YouTube, or the manufacturer's documentation. Even experienced technicians do this every day.

---

## 🔗 References

* [Setup and share Printer to network on Windows 10](https://youtu.be/tg1soEWNcFg?si=s5hgf983nhHy5zw1)
* [Share printer to a Network in Windows 11 / 10](https://youtu.be/YcoEVuYZ-3o?si=uoePKlUQcmFxFPKI)
* [Troubleshooting the most common printer issues resolved as IT](https://youtu.be/B02YvWsKHAE?si=8RAMhne3L3TJuEjd)
* [Comptia A+ 220-1201 - Troubleshooting printer](https://youtu.be/_BhO_nYod0o?si=bKUa9biNOCFea34a)

---

## ✅ Mini Challenge

Try completing these tasks without asking someone else to do them for you:

* Connect a printer to a Wi-Fi network.
* Share the printer with another computer.
* Print a test page.
* Disconnect the printer and reconnect it from scratch.
* Search for one printer error code online and understand what caused it.

If you can complete these tasks confidently, you're already ahead of many fresh graduates. More importantly, you're beginning to think like someone who can solve problems instead of simply following instructions.


# 📚 Snippet [2]: Mastering CMD for Quick Network Troubleshooting

## 🎯 Why learn this?
Karen, when you first step into an IT support or networking role, it is totally normal to feel overwhelmed by physical infrastructure, switches, and building-wide connections you've never touched before. You might feel like you need complex, expensive software to figure out what's going on. But the truth is, one of the most powerful and reliable diagnostic tools you'll ever use is already built right into Windows: the Command Prompt (`cmd`). Learning your way around basic command-line tools lets you see behind the curtain, demystify network problems, and solve issues quickly—even when you're just starting out and don't have full admin rights.

---

## 🌟 Nana's Experience [Click for full story](./experiences/cmd_terminal_exp.md)

---

## 🛠 Things You'll Probably Encounter
* Checking local IP addresses, subnet masks, and default gateways on a workstation (`ipconfig`).
* Testing whether a specific computer, printer, or camera is reachable on the network (`ping`).
* Verifying if a network drop or cable is active by checking link states and connectivity.
* Assisting users whose workstations or office printers have suddenly lost connection.
* Reading text-based outputs to quickly separate local configuration errors from broader network outages.

---

## 💡 Tips from Experience
* **You don't need root/admin rights for everything:** Many basic diagnostic commands (`ipconfig`, `ping`) can be run standard, allowing you to gather crucial clues without breaking anything.
* **Always start close to home:** When troubleshooting a connection issue, always check the local machine's IP configuration first before assuming the switch, router, or server is broken.
* **Be specific when you escalate:** When handing an issue off to your supervisor, don't just say "the printer is broken." Use `cmd` to gather facts—like *"Printer X isn't responding to pings"*—so your team can solve it twice as fast.

---

## 🔗 References
* [[Top CMD Commands useful as junior Net Admin and IT Support]](./tutorials/cmd_cheatsheet.md)
