---
layout: post
title: "中国房地产危机：最先爆发的城市在哪里？"
date: 2025-11-23 00:00:00
categories: [房地产]         # 主分类 / 副分类
tags: [房地产] # 关键词标签
description: "一场由边缘向中心传导的结构性下行"
image: "https://blog-evasoln-1257350348.cos.ap-singapore.myqcloud.com/posts/20251123-1.png"  # 封面图（选填）或者引用方式: "{{ site.cos_img_base }}/stream/m1-cover.jpg"
toc: true                # 是否生成目录
comments: true           # 是否开启评论
---

> 过去数年间，中国房地产经历了自 1998 年住房商品化以来最深刻的一次系统性调整。  
但值得注意的是，这场危机并不是从北上深等核心城市开始的，而是有着非常清晰的 **“由弱到强、由边缘到中心”** 的内部传导顺序。

如果把这轮危机比作一场地震，那么：

graph TD
    %% 节点样式定义
    classDef startNode fill:#333,color:#fff,stroke:#333,stroke-width:2px;
    classDef mainDept fill:#e3f2fd,stroke:#1565c0,stroke-width:2px;
    classDef subDept fill:#f3e5f5,stroke:#7b1fa2;
    classDef process fill:#fff,stroke:#333;
    classDef drugNode fill:#fff9c4,stroke:#fbc02d,stroke-dasharray: 0;
    classDef transfer fill:#ffebee,stroke:#c62828,stroke-dasharray: 5 5;

    %% --- 主入口 ---
    Start[HCC患者 / 门急诊] :::startNode

    %% --- 一级分流 ---
    Start -->|85%| Hep[肝胆外科] :::mainDept
    Start -->|10%| Onco[肿瘤科] :::subDept
    Start -->|5%| Other[其他科室] :::subDept

    %% --- 1. 肝胆外科流程 ---
    Hep -->|5%| Lost[流失掉]
    Hep -->|95%| Admitted[初步诊断后收住院] :::process

    %% 住院后分流
    Admitted -->|70%| Surgery[手术]
    Surgery --> PostOp[术后一个月内回院定期回访]

    Admitted -->|30%| NonSurgery[非手术]
    
    %% 非手术细分
    NonSurgery -->|5%| Local[局部治疗]
    Local --> LocalDetail[介入治疗 (不出科)]

    NonSurgery -->|25%| Trial[临床试验]
    Trial --> TrialDetail[按试验要求CRC定期回访]

    NonSurgery -->|70%| SysTherapy[局部 + 系统治疗]
    
    %% 药物具体方案 (基于表格黄色高亮列)
    SysTherapy -->|50%| Drug1[TKI + 免疫] :::drugNode
    SysTherapy -->|35%| Drug2[贝伐类似物 + 免疫] :::drugNode
    SysTherapy -->|13%| Drug3[T + A] :::drugNode
    SysTherapy -->|2%| Drug4[双重免疫] :::drugNode

    %% --- 2. 肿瘤科流程 ---
    Onco --> OncoDiag[门诊初步诊断]
    OncoDiag -->|10%| TransHep1[需要手术 -> 转去肝胆外科] :::transfer
    OncoDiag -->|90%| StayOnco[药物治疗 -> 留本科室] :::process

    %% --- 3. 其他科室流程 ---
    Other --> OtherDiag[门诊初步诊断]
    OtherDiag -->|100%| TransHep2[诊断HCC后 -> 直接转肝胆外科] :::transfer

> **趋势向上，观察顶端的行为；趋势向下，观察底部的处境。  
城市的脆弱性，决定了危机的顺序。**

---
