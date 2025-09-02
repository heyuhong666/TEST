# VyOS ファイアウォールルール

```mermaid
flowchart TD
    %% WAN-IN インターフェイス受信トラフィック
    WANIN[WAN-IN<br/>受信トラフィック] 

    %% ルール10: VPNクライアントのみ
    rule10[ルール10<br/>ソース: VPNクライアント<br/>状態: new, established, related<br/>アクション: 許可]
    WANIN -->|VPN接続元のみ許可| rule10

    %% ルール20: LAN-Clientsからの戻りトラフィック
    rule20[ルール20<br/>ソース: LAN-Clients<br/>状態: established, related<br/>アクション: 許可]
    WANIN -->|LAN内部からの応答のみ| rule20

    %% デフォルトドロップ
    defaultDrop[デフォルト: drop]
    WANIN -->|その他のトラフィック| defaultDrop

    %% LAN-OUT インターフェイス発信トラフィック
    LANOUT[LAN-OUT<br/>発信トラフィック]
    
    %% ルール10: LAN-Clients HTTP通信
    lanRule10[ルール10<br/>ソース: LAN-Clients<br/>宛先ポート: 80<br/>プロトコル: TCP<br/>状態: new, established, related<br/>アクション: 許可]
    LANOUT --> lanRule10

    %% デフォルトドロップ
    lanDefaultDrop[デフォルト: drop]
    LANOUT -->|その他のトラフィック| lanDefaultDrop
