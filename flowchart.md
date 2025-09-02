# VyOS ファイアウォールルール

```mermaid
%%{init: {"themeVariables": {"nodeTextAlignment": "center"}}}%%
flowchart TD
    %% WAN-IN インターフェイス
    WANIN["WAN-IN<br/>受信トラフィック<br/>バインド: eth0, eth1, pppoe0"]

    %% ルール10: VPNクライアントのみ
    WAN_rule10["ルール10<br/>ソース: VPN-clients<br/>状態: new/established/related<br/>アクション: 許可"]
    WANIN --> WAN_rule10

    %% ルール20: LAN-Clientsからの戻りトラフィック
    WAN_rule20["ルール20<br/>ソース: LAN-Clients<br/>状態: established/related<br/>アクション: 許可"]
    WANIN --> WAN_rule20

    %% デフォルトドロップ
    WAN_default["デフォルト<br/>アクション: drop"]
    WANIN --> WAN_default

    %% LAN-OUT インターフェイス
    LANOUT["LAN-OUT<br/>送信トラフィック<br/>バインド: br0 (VLAN101-105)"]

    %% ルール10: LAN-Clients HTTP通信
    LAN_rule10["ルール10<br/>ソース: LAN-Clients<br/>宛先ポート: 80<br/>プロトコル: TCP<br/>状態: new/established/related<br/>アクション: 許可"]
    LANOUT --> LAN_rule10

    %% デフォルトドロップ
    LAN_default["デフォルト<br/>アクション: drop"]
    LANOUT --> LAN_default


