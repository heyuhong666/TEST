```mermaid
%%{init: {"themeVariables": {"nodeTextAlignment": "center"}}}%%
flowchart TD
    subgraph NetBox
        A[初期投入申请]
        K[request_webhook];
        K -- pull_request.merged: true --> M[処理待ちタスクリスト];
        K -- pull_request.merged: false --> T[gmail通知];
        M --> B{create};
        M --> E{delete};
        B --> C[初期投入タスク];
        E --> C;
        C --> N{投入};
        C --> Q[接続チェックアラート];
        C --> S[投入処理失敗アラート];
        T --> A;
    end
    
    subgraph GitHub CI/CD
        A --> D[diff/create_PR/gmail通知];
        D --> G{PR};
        G -- commit --> I[webhook_post];
        G -- reject --> I;
        I --> K;
    end

    subgraph Ansible          
        N --> O[192.0.2.1疎通確認];
        O -- yes --> P{playbook投入処理};
        O -- no --> Q;
        P -- fail --> S;
        P -- sucess --> E;
    end
