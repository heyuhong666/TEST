flowchart TD
    %% LAN-OUT: 内部 → 外部
    subgraph LAN-OUT ["LAN-OUT (内部 → 外部)"]
        LANClients["LAN-Clients<br>192.168.101-105/24"] -->|HTTP TCP 80| Rule10LAN["ルール10: 新規 / 確立 / 関連状態を許可"]
        LANClients -->|その他ポート| DropLAN["デフォルト動作: ドロップ"]
    end

    %% WAN-IN: 外部 → 内部
    subgraph WAN-IN ["WAN-IN (外部 → 内部)"]
        VPNClients["VPN-Clients<br>172.0.0.0/8"] -->|VPN UDP 1194| Rule10WAN["ルール10: 新規 / 確立 / 関連状態を許可"]
        LANClients -->|返送パケット TCP/UDP 80,443,DNS| Rule20WAN["ルール20: 確立 / 関連状態を許可"]
        Others["その他のIP"] -->|許可しない| DropWAN["デフォルト動作: ドロップ"]
    end

    %% 
    LANClients -.-> WAN-IN
    VPNClients -.-> LAN-OUT

    %% 
    style LAN-OUT fill:#e0f7fa,stroke:#00796b,stroke-width:2px
    style WAN-IN fill:#fff3e0,stroke:#f57c00,stroke-width:2px
    style DropLAN fill:#ffcdd2,stroke:#b71c1c,stroke-width:2px
    style DropWAN fill:#ffcdd2,stroke:#b71c1c,stroke-width:2px
