# AI Usage: CSCE 465/765 HW4

Student: <your name>

**Tool/model and date:** Claude (Claude Sonnet 5.5), Nov 21-23, 2026.

**Purpose:** Step-by-step guidance for the HW4 setup and Tasks 1-5, help with the lab files, commands, firewall script and Suricata rules, and drafting and reviewing sections of the report.

**AI Conversation Log files:** `AI_LOG.md` (exported conversation, included in the zip).

Main questions I asked, in order:
- Task 0: How do I set up Docker, nmap, tcpdump, TShark and Suricata in my Ubuntu VM, and how do I take a VirtualBox snapshot?
- Task 1: Give step-by-step instructions to build the Docker lab (Dockerfile, compose file, mock skill, C2 server, web pages). Are my outputs correct?
- Task 2: How do I scan, capture and reconstruct the exfiltration with TShark? Which stream number is the exfiltration? How do I restart the lab after a VM shutdown? Why does `nc` say "missing port"? Are my results correct?
- Task 3: Give the firewall steps. Are my five test results, counters and kernel log lines correct? What goes in the report?
- Task 4: Give the steps for the three Suricata rules. What does the permission error on `suricata -T` mean? Are the alerts correct?
- Task 5: Explain what the incident summary needs, then make it shorter to fit one page.
- Final: Review my report against the assignment and tell me what is missing.

**What I used:**
- Install commands and snapshot steps (Task 0).
- The structure of the Dockerfile, docker-compose.yml, mock_skill.sh, c2.py and the two web pages (Task 1).
- The nmap, tcpdump and TShark commands (Task 2).
- The design of firewall.sh and firewall-reset.sh: own chain jumped to from DOCKER-USER, conntrack rules, LOG before DROP, br_netfilter (Task 3).
- The three Suricata rules and the offline run commands (Task 4).
- Draft wording and the outline for the report sections and incident summary (Tasks 1-5).

**What I changed:** I ran everything in my own VM with my own fake token and used my own screenshots and numbers in the report. I had the Task 5 summary shortened to fit one page. I reworded explanations in my own words, and I fixed the issues the AI review flagged in my report. <add anything else you changed or rejected>

**How I tested it:** Every command was run in my Ubuntu VM and checked against the assignment's expected results:
- Task 1: matching SHA-256 hashes for fake_secrets.txt and /data/received.bin.
- Task 2: two TCP streams in the PCAP, the token and the POST body hash.
- Task 3: all five firewall tests, the packet counters and the kernel log lines, plus a bypass test with br_netfilter turned off.
- Task 4: three Suricata alerts on the malicious PCAP and none on the clean one.

**One error, limitation, or rejected suggestion:** The AI's `suricata -T -S local.rules -k none` command failed with a permission error because it tried to write logs to /var/log/suricata. I fixed it by running it with sudo (a writable `-l` directory also works). Also, the AI suggested `-t ud` for UTC timestamps, but it does not change `-e frame.time` output, so I switched to `frame.time_utc` and cross-checked it against the HTTP Date header.
