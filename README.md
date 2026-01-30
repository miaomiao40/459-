graph TD
    %% 定义样式
    classDef prosumer fill:#e3f2fd,stroke:#1565c0,stroke-width:2px,color:#000;
    classDef contract fill:#fff3e0,stroke:#ef6c00,stroke-width:2px,color:#000;
    classDef consumer fill:#e8f5e9,stroke:#2e7d32,stroke-width:2px,color:#000;
    classDef note fill:#fff,stroke:#999,stroke-dasharray: 5 5,color:#666;

    %% 泳道：产消者
    subgraph Prosumer_Lane [产消者 (Prosumer)]
        direction TB
        P1[1. 智能电表监测<br/>输出 5 kWh]:::prosumer
        P2(2. 数据加密上链):::note
        P3[5. 发起卖出挂单<br/>设定价格]:::prosumer
    end

    %% 泳道：智能合约
    subgraph Contract_Lane [智能合约 (Smart Contract)]
        direction TB
        SC1[3. 验证数据<br/>Verify Data]:::contract
        SC2[4. 铸造代币<br/>Mint 5 eKW]:::contract
        SC3[7. 撮合引擎<br/>Matching Engine]:::contract
        SC4{8. 原子结算<br/>Atomic Settlement}:::contract
        
        subgraph Atomic_Action [事务一致性]
            direction TB
            ActionA[动作A: 资金转给产消者]:::contract
            ActionB[动作B: 代币转给消费者]:::contract
        end
    end

    %% 泳道：消费者
    subgraph Consumer_Lane [消费者 (Consumer)]
        direction TB
        C1[6. 充值 & 发起买入请求]:::consumer
        C2[10. 确认收电<br/>交易完结]:::consumer
    end

    %% 阶段一：发电与资产化
    P1 -->|加密读数| P2
    P2 --> SC1
    SC1 -->|签名合法| SC2
    SC2 -.->|存入钱包| P3

    %% 阶段二：挂单与撮合
    P3 --> SC3
    C1 --> SC3

    %% 阶段三：原子结算
    SC3 -->|匹配成功| SC4
    SC4 --> ActionA & ActionB

    %% 阶段四：物理交付与反馈
    ActionA & ActionB ====>|9. 物理电网交付| C2

    %% 链接样式调整
    linkStyle default stroke:#333,stroke-width:1.5px;
