# VyOS ファイアウォールルール

```mermaid
flowchart TD
    %% WAN-IN インターフェイス
    WANIN["WAN-IN\n受信トラフィック\nバインド: eth0, eth1, pppoe0"]

    %% WAN-IN ルール10: VPNクライアントのみ
    WAN_rule10["ルール10\nソース: VPN-clients\n状態: new, established, related\nアクション: 許可"]
    WANIN -->|VPN接続元のみ許可| WAN_rule10

    %% WAN-IN ルール20: LAN-Clientsからの戻りトラフィック
    WAN_rule20["ルール20\nソース: LAN-Clients\n状態: established, related\nアクション: 許可"]
    WANIN -->|LAN内部からの応答のみ許可| WAN_rule20

    %% WAN-IN デフォルトドロップ
    WAN_default["デフォルト: drop"]
    WANIN -->|その他のトラフィック| WAN_default

    %% LAN-OUT インターフェイス
    LANOUT["LAN-OUT\n送信トラフィック\nバインド: br0 VLAN101-105"]

    %% LAN-OUT ルール10: HTTP/TCP 送信許可
    LAN_rule10["ルール10\nソース: LAN-Clients\n宛先ポート: 80\nプロトコル: TCP\n状態: new, established, related\nアクション: 許可"]
    LANOUT --> LAN_rule10

    %% LAN-OUT デフォルトドロップ
    LAN_default["デフォルト: drop"]
    LANOUT -->|その他のトラフィック| LAN_default


