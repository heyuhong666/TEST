# VyOS ファイアウォールルール

```mermaid
flowchart TD
    %% WAN-IN インターフェイス
    WANIN[WAN-IN\n受信トラフィック\nバインド: eth0, eth1]

    %% ルール10: VPNクライアントのみ
    rule10[ルール10\nソース: VPNクライアント\n状態: new, established, related\nアクション: 許可]
    WANIN -->|VPN接続元のみ許可| rule10

    %% ルール20: LAN-Clientsからの戻りトラフィック
    rule20[ルール20\nソース: LAN-Clients\n状態: established, related\nアクション: 許可]
    WANIN -->|LAN内部からの応答のみ| rule20

    %% デフォルトドロップ
    defaultDrop[デフォルト: drop]
    WANIN -->|その他のトラフィック| defaultDrop

    %% LAN-OUT インターフェイス
    LANOUT[LAN-OUT\n送信トラフィック\nバインド: br0 (VLAN101-105)]

    %% ルール10: LAN-Clients HTTP通信
    lanRule10[ルール10\nソース: LAN-Clients\n宛先ポート: 80\nプロトコル: TCP\n状態: new, established, related\nアクション: 許可]
    LANOUT --> lanRule10

    %% デフォルトドロップ
    lanDefaultDrop[デフォルト: drop]
    LANOUT -->|その他のトラフィック| lanDefaultDrop

