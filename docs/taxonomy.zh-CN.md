# 任务分类

[English](taxonomy.md) | [简体中文](taxonomy.zh-CN.md)

这个 taxonomy 面向 benchmark 比较而设计。一个 benchmark 可以同时属于多个任务族。

## Point、Image 与 Object Navigation

智能体接收低层目标、目标图像、物体实例或物体类别，并需要导航到一个有效的停止位置。

关键比较维度：

- goal type：坐标、图像、物体实例、物体类别、有序物体列表
- observation：RGB、depth、semantic mask、GPS/compass、map
- action space：discrete、continuous velocity、waypoint
- metrics：Success、SPL、SoftSPL、distance-to-goal、collisions

## Vision-Language Navigation

智能体根据自然语言路线指令导航。经典设置使用全景图节点构成的离散图，新变体更多使用连续 3D 控制。

关键比较维度：

- language type：单条指令、多语言指令、对话、指代表达
- environment：Matterport3D、Habitat、户外 UAV 场景
- action space：graph-discrete、continuous、waypoint
- metrics：navigation error、success rate、SPL、nDTW、sDTW

## Embodied QA 与 Active Exploration

智能体通过探索环境或使用 episodic memory，回答关于环境的 open-vocabulary 问题。

关键比较维度：

- setting：episodic memory、active exploration、hybrid
- answer type：closed-set、open-vocabulary
- evaluator：exact match、LLM judge、human agreement
- metrics：answer correctness、exploration efficiency、coverage

## Social 与 Human-Aware Navigation

智能体在包含人类或其他智能体的动态环境中导航。评测应覆盖社会规范、安全性和任务成功率。

关键比较维度：

- human model：scripted、data-driven、interactive、real human
- social signal：personal space、intent、groups、norms、verbal interaction
- metrics：success、collisions、intrusion、comfort、time-to-goal

## Audio-Visual Navigation

智能体结合 audio 与 visual observation，定位或导航到发声目标。

关键比较维度：

- audio type：binaural、ambisonic、reverberation、multi-source noise
- target：semantic source、sound source、speaker
- simulator：precomputed RIR、real-time acoustic rendering
- metrics：success、SPL、distance-to-goal、source localization

## Aerial 与 Outdoor Navigation

智能体通常是 UAV，在户外或城市环境中基于语言、对话、目标或空间推理导航。

关键比较维度：

- platform：drone、ground robot、abstract agent
- environment scale：building、street、city、airspace
- goal type：instruction、dialog、coordinate、landmark、object
- metrics：route success、waypoint error、trajectory similarity、safety

## Foundation-Model Navigation

benchmark 用于评估 MLLM、VLM、LLM、VLA 或 navigation foundation models。

关键比较维度：

- model role：planner、policy、world model、evaluator、memory
- supervision：zero-shot、few-shot、fine-tuned、RL fine-tuned
- embodiment：graph agent、mobile robot、drone、humanoid
- metrics：comprehension、execution、reasoning trace quality、task success
