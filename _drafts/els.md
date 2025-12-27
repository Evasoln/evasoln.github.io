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
    %% 定义样式类：模拟原图的灰色背景和圆角
    classDef default fill:#e6e6e6,stroke:#666,stroke-width:2px,rx:5,ry:5,color:#333;
    classDef root fill:#ccc,stroke:#333,stroke-width:2px,font-size:16px,font-weight:bold;
    classDef redText color:#c00,font-weight:bold;

    %% --- 根节点 ---
    Root[门 / 急 诊]:::root

    %% --- 第一层：科室分流 ---
    Root --> Hepato[肝胆外科<br/><span class='redText'>85%</span>]
    Root --> Onco[肿瘤科<br/><span class='redText'>10%</span>]
    Root --> Other[其他科室<br/><span class='redText'>5%</span>]

    %% --- 肝胆外科分支 ---
    Hepato --> Hepato_In[初步诊断后收住院<br/><span class='redText'>95%</span>]
    Hepato --> Hepato_Out[流失掉<br/><span class='redText'>5%</span>]

    %% --- 住院后分支 ---
    Hepato_In --> Surg[手 术<br/><span class='redText'>70%</span>]
    Hepato_In --> NonSurg[非手术<br/><span class='redText'>30%</span>]

    %% --- 手术后续 (带医生分布) ---
    Surg --> Surg_Follow[术后一个月内回院定期回访<br/>梁霄 40%<br/>梁岳龙 20%<br/>陈鸣宇 15%<br/>虞洪 10%<br/>蔡柳新 5%]

    %% --- 非手术分支 ---
    NonSurg --> Local[局部治疗 <span class='redText'>5%</span><br/>介入治疗/不出科]
    NonSurg --> Trial[临床试验 <span class='redText'>25%</span><br/>按实验要求CRC定期回访<br/>(梁霄 90%)]
    NonSurg --> Systemic[局部+系统治疗 <span class='redText'>70%</span>]

    %% --- 系统治疗药物细分 ---
    Systemic --> Drug1[贝伐类似物+免疫<br/><span class='redText'>35%</span>]
    Systemic --> Drug2[TKI + 免疫<br/><span class='redText'>50%</span>]
    Systemic --> Drug3[双免疫<br/><span class='redText'>2%</span>]
    Systemic --> Drug4[T + A<br/><span class='redText'>13%</span>]

    %% --- 肿瘤科分支 ---
    Onco --> Onco_Transfer[需手术转去肝胆外科<br/><span class='redText'>10%</span>]
    Onco --> Onco_Stay[药物治疗留本科室<br/><span class='redText'>90%</span>]

    %% --- 其他科室分支 ---
    Other --> Other_Transfer[诊断HCC后直接转肝胆外科<br/><span class='redText'>100%</span>]

    %% 连接线样式调整（可选，使其看起来更像层级图）
    linkStyle default stroke:#666,stroke-width:1px;

> **趋势向上，观察顶端的行为；趋势向下，观察底部的处境。  
城市的脆弱性，决定了危机的顺序。**

---
