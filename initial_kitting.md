%%{init: {"themeVariables": {"nodeTextAlignment": "center"}}}%%
flowchart TD
    subgraph 工程师操作
        A[创建包含初始配置的Git PR] --> B{PR审核};
    end

    subgraph GitHub & CI/CD
        B -- 审核通过并合并 --> C[GitHub Webhook];
        C --> D[CI/CD任务运行];
        D --> E{任务成功?};
        E -- No --> F[发送失败通知];
        E -- Yes --> G[生成有时效性的API令牌];
        G --> H[向NetBox API发送请求];
    end
    
    subgraph NetBox
        H --> I[NetBox存储授权信息];
        I --> J[NetBox UI显示“投入”按钮];
    end

    subgraph 人工操作
        J --> K[人工确认设备并点击“投入”按钮];
    end

    subgraph 自动化执行
        K --> L[NetBox向Ansible发送任务];
        L --> M[Ansible使用API令牌];
        M --> N[使用硬编码IP 192.0.2.1连接];
        N --> O[执行初始化配置并提交commit/save];
    end

    subgraph 结果反馈
        O --> P[将结果反馈给NetBox];
        P --> Q[NetBox更新设备状态];
    end

    style A fill:#BCEE68,stroke:#000000,stroke-width:2px;
    style B fill:#87CEEB,stroke:#000000,stroke-width:2px;
    style C fill:#FFA07A,stroke:#000000,stroke-width:2px;
    style D fill:#FFFACD,stroke:#000000,stroke-width:2px;
    style G fill:#FFD700,stroke:#000000,stroke-width:2px;
    style H fill:#E0FFFF,stroke:#000000,stroke-width:2px;
    style I fill:#87CEEB,stroke:#000000,stroke-width:2px;
    style J fill:#FFB6C1,stroke:#000000,stroke-width:2px;
    style K fill:#BCEE68,stroke:#000000,stroke-width:2px;
    style L fill:#98FB98,stroke:#000000,stroke-width:2px;
    style M fill:#E0FFFF,stroke:#000000,stroke-width:2px;
    style N fill:#FFFACD,stroke:#000000,stroke-width:2px;
    style O fill:#FF7F50,stroke:#000000,stroke-width:2px;
    style P fill:#E0FFFF,stroke:#000000,stroke-width:2px;
    style Q fill:#87CEEB,stroke:#000000,stroke-width:2px;
