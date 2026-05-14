# Awesome Embodied Navigation Benchmark Zoo

[English](README.md) | [简体中文](README.zh-CN.md)

<p align="center">
  <img src="assets/zoo.png" alt="Awesome Embodied Navigation Benchmark Zoo" width="100%">
</p>

面向 embodied navigation、ObjectNav、vision-language navigation、robot navigation、spatial AI 的 curated awesome list 与 benchmark zoo，系统整理数据集、指标、排行榜和可复现信息。

本仓库的目标是帮助研究者和工程实践者快速回答这些实际问题：

- 我应该在哪个导航任务上评测？
- 这个 benchmark 使用什么 simulator、dataset、observation、action space 和 metric？
- 是否有公开 leaderboard？
- 是否有 starter code 或可复现 baseline？
- 哪些 benchmark 适合评估 foundation model、open-vocabulary reasoning、social interaction、audio 或 aerial navigation？

## 范围

包含：

- 以导航为核心的具身智能 benchmark。
- 导航是更大具身任务核心组成部分的 benchmark。
- dataset、simulator、evaluation、baseline code 链接。
- 面向实践的可复现说明。

不包含：

- 没有 benchmark 的通用机器人导航库。
- 纯 mapping、perception、manipulation 或 autonomous driving benchmark，除非导航是核心任务。
- 只有论文、缺少公开 benchmark 信息的条目。

## 仓库规划

### 1. 任务分类

本仓库按任务族组织 benchmark，而不是按论文时间线堆叠。

| 任务族                            | 核心问题                                           | 示例                                                      |
| --------------------------------- | -------------------------------------------------- | --------------------------------------------------------- |
| Point / Image / Object Navigation | 智能体能否到达坐标、图像目标、物体实例或物体类别？ | Habitat PointNav、ObjectNav、ImageNav；RoboTHOR ObjectNav |
| Vision-Language Navigation        | 智能体能否根据自然语言指令在环境中导航？           | R2R、RxR、REVERIE、VLN-CE                                 |
| Embodied QA / Exploration         | 智能体能否探索环境或使用记忆回答空间相关问题？     | OpenEQA                                                   |
| Social / Human-Aware Navigation   | 智能体能否在人类或其他智能体周围安全、合适地移动？ | SocNavBench、SMM Challenge                                |
| Audio-Visual Navigation           | 智能体能否结合声音和视觉定位并导航到目标？         | SoundSpaces                                               |
| Aerial / Outdoor Navigation       | UAV 或户外智能体能否基于语言、目标或空间推理导航？ | AerialVLN、AVDN                                           |

工作版 taxonomy 见 [docs/taxonomy.zh-CN.md](docs/taxonomy.zh-CN.md)。

### 2. Benchmark 条目

本部分结构化数据源是 [data/benchmarks.yml](data/benchmarks.yml)。

#### <span style="color: #d73a49;">Habitat Navigation Challenge 2023</span>

AI Habitat team
Challenge, 2023. [Project](https://aihabitat.org/challenge/2023/) | [Code](https://github.com/facebookresearch/habitat-challenge) | [Leaderboard](https://eval.ai/) | [Paper](https://arxiv.org/abs/1904.01201)

**Framework**

- Simulator：Habitat。
- Dataset：HM3D-Semantics v0.2。
- Action space：continuous velocity、waypoint 和 discrete-waypoint variants。
- Metrics：Success、SPL、SoftSPL、distance-to-goal、collisions。
- Reproducibility：`verified`。

<details>
<summary>展开 Summary 与 Benchmark focus</summary>

**Summary**

Habitat Navigation Challenge 2023 在 Habitat 生态中使用 HM3D-Semantics 评估 ObjectNav 和 ImageNav，重点关注在真实感知与机体约束下运行的具身导航策略。

**Benchmark focus**

- 物体类别导航与目标图像导航。
- 室内仿真，包含 RGB、depth 和 GPS/compass observations。
- 适合比较经典导航 pipeline、学习型 policy 和面向 sim-to-real 的 agent。

</details>

#### RoboTHOR ObjectNav

Allen Institute for AI
Benchmark, 2020. [Project](https://ai2thor.allenai.org/robothor/) | [Code](https://github.com/allenai/robothor-challenge) | [Paper](https://arxiv.org/abs/2004.06799)

**Framework**

- Simulator：AI2-THOR / RoboTHOR。
- Dataset：RoboTHOR。
- Action space：discrete。
- Metrics：Success、SPL。
- Reproducibility：`partial`。

<details>
<summary>展开 Summary 与 Benchmark focus</summary>

**Summary**

RoboTHOR 研究 paired simulation 与真实机器人设置下的 ObjectNav，因此适合评估在仿真中训练或测试的导航 agent 能否迁移到真实室内场景。

**Benchmark focus**

- 基于 RGB 和 depth observations 的物体类别导航。
- 使用 AI2-THOR 与 RoboTHOR 环境做 sim-to-real 评估。
- 适合检验宣称具备真实世界鲁棒性的 agent。

</details>

#### MultiON

MultiON Challenge team
Challenge, 2020. [Project](https://multion-challenge.cs.sfu.ca/2023.html) | [Code](https://github.com/saimwani/multiON) | [Leaderboard](https://eval.ai/) | [Paper](https://arxiv.org/abs/2012.11736)

**Framework**

- Simulator：Habitat。
- Dataset：MultiON Challenge episodes。
- Action space：discrete。
- Metrics：Success、progress、SPL variants。
- Reproducibility：`partial`。

<details>
<summary>展开 Summary 与 Benchmark focus</summary>

**Summary**

MultiON 将 ObjectNav 从单一目标扩展到有序物体目标序列，用来测试长时程 semantic exploration、memory 和 route planning。

**Benchmark focus**

- 有序多物体导航。
- 需要记忆已访问空间，并规划高效的目标访问顺序。
- 适合评估 semantic map、episodic memory 和 hierarchical policy。

</details>

#### Room-to-Room (R2R)

Anderson et al.
Benchmark, 2018. [Project](https://bringmeaspoon.org/) | [Code](https://github.com/peteanderson80/Matterport3DSimulator) | [Leaderboard](https://eval.ai/) | [Paper](https://arxiv.org/abs/1711.07280)

**Framework**

- Simulator：Matterport3D Simulator。
- Dataset：R2R。
- Action space：graph-discrete viewpoints。
- Metrics：navigation error、success rate、SPL、nDTW、sDTW。
- Reproducibility：`verified`。

<details>
<summary>展开 Summary 与 Benchmark focus</summary>

**Summary**

R2R 是经典 Vision-Language Navigation benchmark：agent 根据人类写作的路线指令在 Matterport3D 环境中导航。

**Benchmark focus**

- 自然语言路线跟随。
- 基于 panoramic graph 的离散导航。
- 是 instruction grounding、cross-modal alignment 和 route progress estimation 的核心 testbed。

</details>

#### Room-Across-Room (RxR)

Ku et al.
Benchmark, 2020. [Project](https://research.google/pubs/room-across-room-multilingual-vision-and-language-navigation-with-dense-spatiotemporal-grounding/) | [Code](https://github.com/google-research-datasets/RxR) | [Leaderboard](https://eval.ai/) | [Paper](https://arxiv.org/abs/2010.07954)

**Framework**

- Simulator：Matterport3D / Habitat variants。
- Dataset：RxR。
- Action space：graph-discrete viewpoints 和 continuous variants。
- Metrics：navigation error、success rate、SPL、nDTW、sDTW。
- Reproducibility：`archival`。

<details>
<summary>展开 Summary 与 Benchmark focus</summary>

**Summary**

RxR 将 VLN 扩展到多语言指令和 dense spatiotemporal grounding，适合评估语言多样性和细粒度指令对齐。

**Benchmark focus**

- 多语言路线指令。
- 语言与轨迹之间的 dense alignment。
- 适合 multilingual VLN 和 foundation-model grounding 研究。

</details>

#### REVERIE

Qi et al.
Benchmark, 2020. [Project](https://github.com/YuankaiQi/REVERIE) | [Code](https://github.com/YuankaiQi/REVERIE) | [Paper](https://arxiv.org/abs/1904.10151)

**Framework**

- Simulator：Matterport3D Simulator。
- Dataset：REVERIE。
- Action space：graph-discrete viewpoints。
- Metrics：navigation error、oracle success rate、remote grounding success、SPL。
- Reproducibility：`partial`。

<details>
<summary>展开 Summary 与 Benchmark focus</summary>

**Summary**

REVERIE 结合 remote object localization 与 language-guided navigation。agent 需要理解 referring expression，导航到目标区域附近，并识别被指代物体。

**Benchmark focus**

- 指代表达导航。
- 联合评估 navigation 与 object grounding。
- 适合 open-vocabulary object grounding 和 VLN 模型。

</details>

#### Vision-and-Language Navigation in Continuous Environments (VLN-CE)

Krantz et al.
Benchmark, 2020. [Project](https://github.com/jacobkrantz/VLN-CE) | [Code](https://github.com/jacobkrantz/VLN-CE) | [Paper](https://arxiv.org/abs/2004.02857)

**Framework**

- Simulator：Habitat。
- Dataset：VLN-CE。
- Action space：continuous 或 low-level discrete。
- Metrics：success rate、SPL、nDTW、sDTW。
- Reproducibility：`partial`。

<details>
<summary>展开 Summary 与 Benchmark focus</summary>

**Summary**

VLN-CE 将 instruction-following 从图节点上的离散导航转为连续 3D 控制，暴露 VLN route reasoning 与具身低层控制之间的差距。

**Benchmark focus**

- 连续空间指令跟随。
- 基于 RGB-D 与自然语言指令的导航。
- 适合评估同时处理 language grounding 与 embodied control 的模型。

</details>

#### Cooperative Vision-and-Dialog Navigation (CVDN)

Thomason et al.
Benchmark, 2019. [Project](https://cvdn.dev/) | [Code](https://github.com/mmurray/cvdn) | [Paper](https://arxiv.org/abs/1907.04957)

**Framework**

- Simulator：Matterport3D Simulator。
- Dataset：CVDN。
- Action space：graph-discrete viewpoints。
- Metrics：goal progress、navigation error。
- Reproducibility：`partial`。

<details>
<summary>展开 Summary 与 Benchmark focus</summary>

**Summary**

CVDN 通过对话评估导航：navigator 需要利用与 oracle 的 conversation history 推断路线并向目标移动。

**Benchmark focus**

- 交互式 vision-and-dialog navigation。
- dialog history 是主要任务上下文。
- 适合研究 clarification、instruction repair 和 conversational grounding。

</details>

#### OpenEQA

Meta AI / FAIR
Benchmark, 2024. [Project](https://open-eqa.github.io/) | [Code](https://github.com/facebookresearch/open-eqa) | [Paper](https://open-eqa.github.io/assets/pdfs/paper.pdf)

**Framework**

- Environment：real-world scans 和 HM3D-style simulation。
- Dataset：OpenEQA。
- Action setting：episodic-memory-only 与 active-exploration variants。
- Metrics：LLM-Match、human agreement。
- Reproducibility：`verified`。

<details>
<summary>展开 Summary 与 Benchmark focus</summary>

**Summary**

OpenEQA 评估具身 agent 能否基于 episodic memory 或 active exploration 回答关于环境的 open-vocabulary 问题。

**Benchmark focus**

- 真实世界与仿真环境中的 embodied question answering。
- 使用 open-vocabulary answer 评估 foundation model。
- 适合研究 spatial memory、exploration 和 environment understanding。

</details>

#### SoundSpaces

Chen et al. / Meta AI
Benchmark, 2020. [Project](https://soundspaces.org/) | [Code](https://github.com/facebookresearch/sound-spaces) | [Paper](https://vision.cs.utexas.edu/projects/audio_visual_navigation/)

**Framework**

- Simulator：SoundSpaces / Habitat。
- Dataset：Matterport3D 与 Replica acoustic environments。
- Action space：discrete，SoundSpaces 2.0 中包含 continuous variants。
- Metrics：success、SPL、distance-to-goal。
- Reproducibility：`verified`。

<details>
<summary>展开 Summary 与 Benchmark focus</summary>

**Summary**

SoundSpaces 为具身导航加入 realistic audio simulation，使 agent 能结合 binaural audio 和 visual observations 导航到发声目标。

**Benchmark focus**

- AudioGoal 与 audio-visual navigation。
- 在 reverberation 和 spatial acoustics 下导航。
- 适合评估利用声音作为空间线索的 multimodal policy。

</details>

#### SocNavBench

CMU TBD Lab
Benchmark framework, 2021. [Project](https://github.com/CMU-TBD/SocNavBench) | [Code](https://github.com/CMU-TBD/SocNavBench) | [Paper](https://www.ri.cmu.edu/publications/socnavbench-a-grounded-simulation-testing-framework-for-evaluating-social-navigation/)

**Framework**

- Simulator：SocNavBench。
- Dataset：curated social navigation scenarios。
- Action space：planner-dependent。
- Metrics：path efficiency、safety、comfort、personal-space intrusion。
- Reproducibility：`partial`。

<details>
<summary>展开 Summary 与 Benchmark focus</summary>

**Summary**

SocNavBench 是面向 social navigation 的仿真测试框架，用于评估导航 policy 在行人和社会约束空间中的行为。

**Benchmark focus**

- Human-aware navigation evaluation。
- Safety、comfort 和 personal-space behavior。
- 适合在 shortest-path efficiency 之外比较 planner 和 learned policy。

</details>

#### Social Mobile Manipulation Challenge

SMM Challenge organizers
Challenge, 2025. [Project](https://smm-challenge.github.io/) | [Leaderboard](https://smm-challenge.github.io/)

**Framework**

- Simulator：Isaac Sim。
- Dataset：Open World Social Mobile Manipulation challenge setup。
- Action space：simulator API。
- Metrics：task success、social interaction quality、planning efficiency。
- Reproducibility：`needs-review`。

<details>
<summary>展开 Summary 与 Benchmark focus</summary>

**Summary**

Social Mobile Manipulation Challenge 在社会动态环境中评估长时程具身 agent，其中导航是 mobile manipulation 与 interaction 的组成部分。

**Benchmark focus**

- 带有社会交互约束的导航。
- Scene-graph prompts 与 multi-agent dynamics。
- 适合评估结合 planning、navigation 和 interaction 的 foundation-model agent。

</details>

#### AerialVLN

AirVLN team
Benchmark, 2023. [Project](https://github.com/AirVLN/AirVLN) | [Code](https://github.com/AirVLN/AirVLN) | [Paper](https://arxiv.org/abs/2308.06735)

**Framework**

- Simulator：AirVLN Simulator。
- Dataset：AerialVLN。
- Action space：continuous UAV control。
- Metrics：success rate、SPL-like metrics、trajectory error。
- Reproducibility：`partial`。

<details>
<summary>展开 Summary 与 Benchmark focus</summary>

**Summary**

AerialVLN 将 language-guided navigation 放到 UAV 环境中，测试 agent 能否在户外航拍场景里跟随路线指令。

**Benchmark focus**

- 基于 UAV 的 vision-language navigation。
- 户外与城市尺度 trajectory following。
- 适合测试 aerial viewpoint 与 continuous control 下的 language grounding。

</details>

#### Aerial Vision-and-Dialog Navigation (AVDN)

Eric AI Lab
Benchmark, 2023. [Project](https://github.com/eric-ai-lab/Aerial-Vision-and-Dialog-Navigation) | [Code](https://github.com/eric-ai-lab/Aerial-Vision-and-Dialog-Navigation) | [Leaderboard](https://eval.ai/web/challenges/challenge-page/2049/overview) | [Paper](https://arxiv.org/abs/2205.12219)

**Framework**

- Simulator：AVDN Simulator。
- Dataset：AVDN，带有 xView 相关访问限制。
- Action space：waypoint prediction。
- Metrics：waypoint error、navigation success。
- Reproducibility：`partial`。

<details>
<summary>展开 Summary 与 Benchmark focus</summary>

**Summary**

AVDN 在 aerial imagery 上评估 dialog-guided UAV navigation，结合 visual observations、dialog history 和 waypoint prediction。

**Benchmark focus**

- Aerial vision-and-dialog navigation。
- Human attention 与 dialog-based route inference。
- 适合 outdoor interactive navigation 与 UAV instruction following。

</details>

#### NavBench

NavBench team
Benchmark, 2025. [Project](https://navbench.github.io/) | [Leaderboard](https://navbench.github.io/)

**Framework**

- Environment：benchmark-specific indoor navigation episodes。
- Dataset：NavBench。
- Action space：converted robot actions。
- Metrics：QA accuracy、execution success、complexity-stratified score。
- Reproducibility：`needs-review`。

<details>
<summary>展开 Summary 与 Benchmark focus</summary>

**Summary**

NavBench 从 embodied navigation comprehension 与 step-by-step execution 角度测试 multimodal large language models，强调模型在行动前是否理解导航情境。

**Benchmark focus**

- Foundation-model navigation evaluation。
- 不同任务复杂度下的 comprehension 与 execution。
- 适合在最终成功率之外比较 MLLM 的导航推理能力。

</details>

### 3. 可复现等级

每个 benchmark 条目都会给出实践意义上的可复现状态：

| 状态             | 含义                                                      |
| ---------------- | --------------------------------------------------------- |
| `verified`     | 公开数据、代码、评测说明和至少一个 baseline 都可用。      |
| `partial`      | 部分公开，但复现需要手动设置、私有数据访问或缺失脚本。    |
| `archival`     | 有历史价值，但代码、数据或 leaderboard 可能已陈旧或只读。 |
| `needs-review` | 候选条目，仍需验证。                                      |

详见 [docs/reproducibility.zh-CN.md](docs/reproducibility.zh-CN.md)。

### 4. 策展维度

每个条目会按这些维度标注：

- `task_family`
- `environment_type`
- `simulator`
- `goal_type`
- `observation_modalities`
- `action_space`
- `metrics`
- `dataset_access`
- `leaderboard_status`
- `baseline_code_status`
- `foundation_model_relevance`
- `sim_to_real_relevance`

### 5. Roadmap

里程碑：

- 建立 benchmark seed table。
- 按任务族拆分 benchmark 页面。
- 为主要 benchmark 添加可复现 checklist。
- 添加 foundation-model navigation evaluation 对比表。
- 添加贡献模板和 review 规则。

见 [docs/roadmap.zh-CN.md](docs/roadmap.zh-CN.md)。

## 如何贡献

请使用 benchmark issue template 创建 issue，或提交 pull request 更新 [data/benchmarks.yml](data/benchmarks.yml)。一个 benchmark 条目至少应包含：

- 官方项目或论文链接
- 代码或数据链接，如果公开
- 任务族
- observation 与 action space
- metrics
- reproducibility status

详见 [CONTRIBUTING.zh-CN.md](CONTRIBUTING.zh-CN.md)。

## License

MIT。各 benchmark 的数据集和代码仓库保留其原始 license 与使用条款。
