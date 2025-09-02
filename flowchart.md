# VyOS ファイアウォールルール

```mermaid
flowchart TD
    %% WAN-IN インターフェイス
    WANIN[WAN-IN - 受信トラフィック - バインド: eth0, eth1]

    %% ルール10: VPNクライアントのみ
    rule10[ルール10<br/>ソース: VPNクライアント<br/>状態: new, established, related<br/>アクション: 許可]
    WANIN -->|VPN接続元のみ許可| rule10

    %% ルール20: LAN-Clientsからの戻りトラフィック
    rule20[ルール20<br/>ソース: LAN-Clients<br/>状態: established, related<br/>アクション: 許可]
    WANIN -->|LAN内部からの応答のみ| rule20

    %% デフォルトドロップ
    defaultDrop[デフォルト: drop]
    WANIN -->|その他のトラフィック| defaultDrop

    %% LAN-OUT インターフェイス
    WANIN[WAN-IN - 受信トラフィック - バインド: br0 (VLAN101-105)]

    %% ルール10: LAN-Clients HTTP通信
    lanRule10[ルール10<br/>ソース: LAN-Clients<br/>宛先ポート: 80<br/>プロトコル: TCP<br/>状態: new, established, related<br/>アクション: 許可]
    LANOUT --> lanRule10

    %% デフォルトドロップ
    lanDefaultDrop[デフォルト: drop]
    LANOUT -->|その他のトラフィック| lanDefaultDrop
