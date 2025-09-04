```mermaid
%%{init: {"themeVariables": {"nodeTextAlignment": "center"}}}%%
flowchart TD
    subgraph NetBox插件与API
        I[插件: 接收PR合并通知] --> J(插件: 检查授权记录);
        J --> K{有授权记录?};
        K -- Yes --> L[插件: 更新任务状态];
        L --> M[NetBox UI: 显示'投入'按钮];
        K -- No --> N[插件: 创建新的待处理任务];
        N --> L;
    end
    
    subgraph GitHub & CI/CD
        A[create_PR/gmail] --> B{PR};
        B -- No --> C[GitHub: 关闭PR];
        C --> D[Webhook触发后端];
        D --> E[后端: 获取修改建议];
        E --> F[后端: 向NetBox API发送请求];
        F --> G[NetBox UI: 显示'修改任务'];
        G --> H[工程师: 重新提交PR];
        H --> A;
        B -- Yes --> S;
        S --> U;
    end
    
    subgraph NETBOX
        H1[初期KITTING] --> A;
        U[処理待ちタスクリスト:初期投入タスク+1 ];
        K1[在NetBox UI上] --> W;
        Y1[收到失败通知] --> A;
    end
    
    subgraph Ansible
        Z --> Z1[192.0.2.1接続];
        Z1 --> Z2[执行配置并提交];
        Z2 --> Z3[后端: 将结果反馈给NetBox];
        Z3 --> Z4[NetBox: 删除待处理任务];
    end
    
    style A fill:#BCEE68,stroke:#000000,stroke-width:2px;
    style B fill:#87CEEB,stroke:#000000,stroke-width:2px;
    style C fill:#FF9999,stroke:#000000,stroke-width:2px;
    style D fill:#FFA07A,stroke:#000000,stroke-width:2px;
    style E fill:#FFFACD,stroke:#000000,stroke-width:2px;
    style F fill:#E0FFFF,stroke:#000000,stroke-width:2px;
    style G fill:#FFB6C1,stroke:#000000,stroke-width:2px;
    style H fill:#BCEE68,stroke:#000000,stroke-width:2px;
    style I fill:#87CEEB,stroke:#000000,stroke-width:2px;
    style J fill:#FFA07A,stroke:#000000,stroke-width:2px;
    style K fill:#87CEEB,stroke:#000000,stroke-width:2px;
    style L fill:#FFB6C1,stroke:#000000,stroke-width:2px;
    style M fill:#98FB98,stroke:#000000,stroke-width:2px;
    style N fill:#FFD700,stroke:#000000,stroke-width:2px;
    style S fill:#FFA07A,stroke:#000000,stroke-width:2px;
    style T fill:#FFFACD,stroke:#000000,stroke-width:2px;
    style U fill:#FFD700,stroke:#000000,stroke-width:2px;
    style V fill:#E0FFFF,stroke:#000000,stroke-width:2px;
    style W fill:#98FB98,stroke:#000000,stroke-width:2px;
    style X fill:#FFA07A,stroke:#000000,stroke-width:2px;
    style Y fill:#87CEEB,stroke:#000000,stroke-width:2px;
    style Z fill:#FF7F50,stroke:#000000,stroke-width:2px;
    style Z1 fill:#FF7F50,stroke:#000000,stroke-width:2px;
    style Z2 fill:#FF7F50,stroke:#000000,stroke-width:2px;
    style Z3 fill:#E0FFFF,stroke:#000000,stroke-width:2px;
    style Z4 fill:#FFB6C1,stroke:#000000,stroke-width:2px;
    style AA fill:#FFD700,stroke:#000000,stroke-width:2px;
    style H1 fill:#BCEE68,stroke:#000000,stroke-width:2px;
    style K1 fill:#BCEE68,stroke:#000000,stroke-width:2px;
    style Y1 fill:#BCEE68,stroke:#000000,stroke-width:2px;
