*****Notizen*****
https://www.youtube.com/watch?v=nPHP3heBzMU

VirusTotal Engines https://en.wikipedia.org/wiki/VirusTotal:

    AegisLab (AegisLab)
    Antiy Labs (Antiy-AVL)
    Aladdin (eSafe)
    AVAST Software (Avast Antivirus)
    AVG Technologies (AVG AntiVirus)
    Avira
    BluePex (AVware)
    Baidu (Baidu-International)
    BitDefender GmbH (BitDefender)
    Bkav Corporation (Bkav)
    ByteHero Information Security Technology Team (ByteHero)
    Cat Computer Services (Quick Heal)
    CMC InfoSec (CMC Antivirus)
    CYREN
    ClamAV
    Comodo (Comodo)
    Criminal IP
    CrowdStrike
    Cybereason
    Doctor Web Ltd. (Dr.Web)
    Emsisoft Ltd. (Emsisoft)
    Endgame
    Eset Software (ESET NOD32)
    Fortinet
    FRISK Software (F-Prot)
    F-Secure
    Gridinsoft
    G Data CyberDefense (G Data)
    Hacksoft (The Hacker)
    Hauri (ViRobot)
    IKARUS Security Software (IKARUS)
    INCA Internet (nProtect)
    Invincea (Invincea, acquired by Sophos)
    Jiangmin (KV Antivirus)
    Kaspersky Lab (Kaspersky Anti-Virus)
    Kingsoft
    Malwarebytes Corporation (Malwarebytes' Anti-Malware)
    McAfee
    Microsoft (Malware Protection)
    MicroWorld (eScan)
    NANO Security (NANO Antivirus)
    Norman (Norman Antivirus)
    Panda Security (Panda Platinum)
    Palo Alto Networks (Palo Alto Networks Threat Intelligence Cloud)
    Qihoo 360
    Rising Antivirus (Rising)
    SentinelOne
    Sophos (SAV)
    SUPERAntiSpyware
    Symantec Corporation (Symantec)
    Tencent
    ThreatTrack Security (VIPRE Antivirus)
    TotalDefense
    Trend Micro (TrendMicro, TrendMicro-HouseCall)
    VirusBlokAda (VBA32)
    Webroot
    WhiteArmor
    Yandex
    Zillya! (Zillya)
    Zoner Software (Zoner Antivirus)

============
PlagueScanner
=============
PlagueScanner is a multiple AV scanner framework for orchestrating a group of individual AV scanners into one contiguous scanner. There are two basic components in this initial release: Core and Agents.

All PlagueScanner components have the following dependencies:

1. Python3: https://www.python.org/
2. ZeroMQ: http://zeromq.org/
3. pyzmq: https://github.com/zeromq/pyzmq

The Agents have the following additional dependency:

1. Requests: http://docs.python-requests.org/en/latest/

And the Core has the following dependency.

5. Web Server (NGINX recommended): http://nginx.org/

In the same directory as each .py file, there needs to be a config file with the following format.
```
[PlagueScanner]
IP = 
Port = 5556
OutboundSamplesDir = /usr/local/www/plaguescanner
[ClamAV]
IP = 
[ESET]
IP = 
[Bitdefender]
IP = 
```

The scanners used were the following:

1. ClamAV: http://www.clamav.net/index.html
2. ESET: http://www.eset.com/us/business/server-antivirus/file-security-linux/
3. Bitdefender: http://www.bitdefender.com/business/antivirus-for-unices.html

**Note**: The Trend Micro agent is missing the regex. This will be fixed shortly.

The directory that NGINX serves needs to have group permissions set +w and the user that you run plaguescanner.py as added to that same group.

This has been tested with each scanner installed on separate VMs with the Core also separate. The Core and each of the other VMs should all be on the same closed network segment. After starting each agent, scan a file like so:

```
$ ./plaguescanner.py sample.exe
```
