```mermaid
graph TD
    %% Main flowchart for the two-level optimization framework

    subgraph Outer_Loop [NSGA-II 优化框架 (外层)]
        A(开始 初始化种群) --> B{迭代次数 < 最大代数?};
        B -- 是 --> C(遗传操作 选择, 交叉, 变异);
        C --> D(合并父代与子代种群);
        D --> E((进行适应度评估));
        E --> F(非支配排序与拥挤度计算);
        F --> G(选择新一代父代种群);
        G --> B;
        B -- 否 --> H(结束 输出帕累托最优解集);
    end

    subgraph Inner_Loop [适应度评估 (内层)]
        E_Start(输入 单个候选解 'x') --> E_Sim1[执行长期可靠性SMC仿真];
        E_Sim1 --> E_Res1(计算 年均成本, EENS, 碳排放);
        
        E_Start --> E_Sim2[执行短期韧性情景分析];
        E_Sim2 --> E_Res2(计算 韧性损失);

        E_Res1 --> E_Combine((组合四维目标值));
        E_Res2 --> E_Combine;
        E_Combine --> E_End(输出 目标函数向量);
    end

    %% Style the link node to show the connection between loops
    style E fill:#e6f3ff,stroke:#0066cc,stroke-width:2px,stroke-dasharray: 5 5
```
