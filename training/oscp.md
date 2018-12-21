Cliff notes

* pre-req: asset setup

1) listen before poking around
    wireshark / tcpdump to capture packet info

2) Gentle inquiries:
    arp-scan
3) netstat -tnlp for list of services

4) CanaryTokens: `https://stationx.net/canarytokens/`
    - thunderbird is great for image url w/o attaching in email if other
    clients dont allow this functionality.

nmap & ndiff

Plan to save the result of the nmap scan w/ `-oA` for all formats
1) Do Ping Sweep - No Port Scan after host discovery w/ (-sn | -sP)
2) Service & Version Detection (-sV):
    to probe the service / version of the port
    note:   (-Pn) is to avoid the discovery
            (-n) is to avoid DNS resolution
    `nmap -n -Pn -sS <ip> --top-ports 10` - <1 sec
    `nmap -n -Pn -sS <ip> --top-ports 10 -sV` - >10 seconds
3) OS Detection:
    `nmap -n -sS <ip> --top-ports 100 -O --osscan-guess`
    `nmap -n -sS -Pn <ip> --top-ports 3 -O`
    add the`--reason` parameter to find more info about the error
    increase the verbosity output w/ `-vvv`
 to get the ip addresses: `<nmap cmd> | grep -i "nmap scan" | cut -d" " -f5`

4) Null(-sN), FIN(-sF), XMAS(-sX) scans


nse scripting categories:
<!--todo: verify nse categories and suffixes-->
        - default (-sC)
        - auth
        - broadcast
        - brute
            `*-brute.nse`
        - default
        - discovery
            `*-safe.nse`
            `*-info.nse`
            `*-version.nse`
        - dos
        - exploit
            `*-vuln.nse`
            `*-intrusive.nse`
            `*-malware.nse`
        - external
        - fuzzer

notable references:
ipidseq.nse


nmap timing:
-T0 (paranoid)
-T1 (sneaky)
-T2 (sneaky)
-T3 (normal)
-T4 (aggressive)
-T5 (insane)
--max-retries 2
--host-timeout

recon:




scanning:
 [ ] hping3 -
     `hping3 --scan <port scan or comma-separated list> -S <ip>`
     `hping3 --scan 0-500 -S 10.10.10.1`

DoS:
     `hping3 --flood -S -V --rand-source www.fqdn.com`

  [ ] nmap -
        ping scan
        port scan
        service version / deteciton
        os detection
        nse execution
        timing tricks
        ips/ids evasion



OSI:
    - physical - ()
    - data link - (ethernet, wireless, 802.4, 802.11, token ring)
    - network - IP
    - transport - (TCP, UDP)
    - session - (SQL, RPC)
    - presentation - (ascii, mp3, jpg)
    - application (http, smtp, telnet, ftp, dns, snmp)


    TCP Flags
- Syn
- Ack
- RST
- FIN
- PSH
- URG
- SYN

    That means, the connection is full-­duplex.

    Oh you know what we have to take a break at this point and talk about TCP flags.

    There are 1-­‐bit flags in TCP headers which are called TCP flags. TCP flags are used within TCP packet

    transfers to indicate a particular connection state or provide additional information.

    Ignoring ECE, CWR and NS flags for now, there are basically 6 TCP flags:

    The SYN, or Synchronisation flag, is used as a first step in establishing a 3-­‐ way handshake between two hosts.

    Only the first packet from both the sender and receiver should have this flag set. The ACK flag, which

    stands for “Acknowledgment”, is used to acknowledge the successful receipt of a packet.

    The RST flag, which stands for “Reset”, gets sent from the receiver to the sender when a packet is sent to

    a particular host that was not expecting it. The FIN flag, which stands for “Finished”, means there is no more

    data from the sender.

    Therefore it is used in the last packet sent from the sender.

    The PSH flag, which stands for “Push”, is somewhat similar to the URG flag and tells the receiver to process these packets

    as they are received instead of buffering them. The URG flag is used to notify the receiver

    to process the urgent packets before processing all other packets.