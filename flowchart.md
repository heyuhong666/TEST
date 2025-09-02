flowchart TD
    subgraph LAN-Clients [LANクライアントネットワーク]
        A1(192.168.101.0/24)
        A2(192.168.102.0/24)
        A3(192.168.103.0/24)
        A4(192.168.104.0/24)
        A5(192.168.105.0/24)
    end

    subgraph VPN-Clients [VPNクライアントネットワーク]
        V1(172.0.0.0/8)
    end

    subgraph LAN-OUT [LAN→外部アウトバウンド防火墙]
        L1["Rule10: TCP 80<br>Source: LAN-Clients<br>State: new/established/related"]
        L2["Default: drop"]
    end

    subgraph WAN-IN [外部→WANインバウンド防火墙]
        W1["Rule10: VPN-Clients 允许<br>State: new/established/related"]
        W2["Rule20: LAN-Clients 返回包允许<br>State: established/related"]
        W3["Default: drop"]
    end

    %% データフロー
    A1 -->|HTTP/HTTPS/DNS| L1 --> Internet[インターネット]
    A2 -->|HTTP/HTTPS/DNS| L1 --> Internet
    A3 -->|HTTP/HTTPS/DNS| L1 --> Internet
    A4 -->|HTTP/HTTPS/DNS| L1 --> Internet
    A5 -->|HTTP/HTTPS/DNS| L1 --> Internet

    V1 --> W1 --> LAN[内部ネットワーク]

    LAN --> W2 --> V1
