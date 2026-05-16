# Awesome Embodied Navigation Benchmark Zoo

[English](README.md) | [简体中文](README.zh-CN.md)

<p align="center">
  <img src="assets/zoo.png" alt="Awesome Embodied Navigation Benchmark Zoo" width="100%">
</p>

A curated awesome list and benchmark zoo for embodied navigation, ObjectNav, vision-language navigation, robot navigation, spatial AI, datasets, metrics, leaderboards, and reproducibility notes.

This repository's goal is to help researchers and builders answer practical benchmark questions:

- Which navigation task should I evaluate on?
- What simulator, dataset, observations, action space, and metrics does it use?
- Is there a public leaderboard?
- Is there starter code or a baseline that can be reproduced?
- Which benchmarks test foundation models, open-vocabulary reasoning, social interaction, audio, or aerial navigation?

## Scope

Included:

- Navigation-centric embodied AI benchmarks.
- Benchmarks where navigation is a core component of a broader embodied task.
- Navigation-adjacent spatial understanding and mobile-manipulation benchmarks when they directly support embodied navigation evaluation.
- Dataset, simulator, evaluation, and baseline-code links.
- Practical reproducibility notes.

Not included:

- Generic robotics navigation libraries without a benchmark.
- Pure mapping, perception, manipulation, or autonomous driving benchmarks unless navigation is central or the entry is explicitly marked navigation-adjacent.
- Paper-only entries without enough public benchmark information.

## Repository Plan

### 1. Task Taxonomy

The zoo groups benchmarks by task family rather than by paper chronology.

| Family                            | Core question                                                                      | Examples                                                  |
| --------------------------------- | ---------------------------------------------------------------------------------- | --------------------------------------------------------- |
| Point / Image / Object Navigation | Can the agent reach a coordinate, image goal, object instance, or object category? | Habitat PointNav, ObjectNav, ImageNav; RoboTHOR ObjectNav |
| Open-Vocabulary / Universal Navigation | Can the agent navigate to free-form, image, or language-specified goals beyond a closed category set? | HM3D-OVON, GOAT-Bench |
| Vision-Language Navigation        | Can the agent follow natural-language instructions through an environment?         | R2R, RxR, REVERIE, VLN-CE                                 |
| Physical / Cross-Embodiment VLN   | Does VLN still work under realistic robot embodiment, physics, and visual shifts? | VLN-CE-Isaac, VLN-PE                                      |
| Embodied QA / Exploration         | Can the agent explore or use memory to answer questions about a space?             | OpenEQA                                                   |
| Spatial Scene Understanding       | Can a model understand egocentric 3D scenes enough to support downstream navigation? | EmbodiedScan, MMScan                                      |
| Social / Human-Aware Navigation   | Can the agent move safely and appropriately around humans or other agents?         | SocNavBench, SMM Challenge                                |
| Mobile Manipulation Navigation    | Can the agent navigate as part of open-vocabulary manipulation or rearrangement?   | HomeRobot OVMM                                            |
| Audio-Visual Navigation           | Can the agent use sound and vision to localize and navigate to goals?              | SoundSpaces                                               |
| Aerial / Outdoor Navigation       | Can a UAV or outdoor agent navigate using language, goals, or spatial reasoning?   | AerialVLN, AVDN                                           |

See [docs/taxonomy.md](docs/taxonomy.md) for the working taxonomy.

### 2. Benchmark Profiles

The structured source of truth is [data/benchmarks.yml](data/benchmarks.yml).

#### ▸ Habitat Navigation Challenge 2023

AI Habitat team
Challenge, 2023. [Project](https://aihabitat.org/challenge/2023/) | [Code](https://github.com/facebookresearch/habitat-challenge) | [Leaderboard](https://eval.ai/) | [Paper](https://arxiv.org/abs/1904.01201)

**Framework**

- Simulator: Habitat.
- Dataset: HM3D-Semantics v0.2.
- Action space: continuous velocity, waypoint, and discrete-waypoint variants.
- Metrics: Success, SPL, SoftSPL, distance-to-goal, collisions.
- Reproducibility: `verified`.

<details>
<summary>Expand Summary and Benchmark focus</summary>

**Summary**

Habitat Navigation Challenge 2023 evaluates ObjectNav and ImageNav in HM3D-Semantics using the Habitat ecosystem, with an emphasis on embodied navigation policies that can operate under realistic sensing and embodiment constraints.

**Benchmark focus**

- Object-category and goal-image navigation.
- Indoor simulation with RGB, depth, and GPS/compass observations.
- Useful for comparing classical navigation pipelines, learned policies, and sim-to-real-oriented agents.

</details>

#### ▸ Habitat ObjectNav Challenge 2024/2025 Protocol

AI Habitat team / community leaderboard users
Challenge protocol, 2024. [Project](https://aihabitat.org/challenge/2023/) | [Code](https://github.com/facebookresearch/habitat-challenge) | [Leaderboard](https://eval.ai/web/challenges/challenge-page/1992/overview) | [Paper](https://arxiv.org/abs/2006.13171)

**Framework**

- Simulator: Habitat.
- Dataset: HM3D-Semantics v0.2 ObjectNav.
- Action space: continuous velocity, waypoint, and discrete-waypoint variants.
- Metrics: Success, SPL, SoftSPL, distance-to-goal, collisions.
- Reproducibility: `archival`.

<details>
<summary>Expand Summary and Benchmark focus</summary>

**Summary**

This entry tracks later 2024/2025 use of the Habitat ObjectNav benchmark protocol built around the 2023 HM3D-Semantics v0.2 challenge. The official challenge repository is read-only, so the entry is marked archival rather than treated as a new official annual challenge page.

**Benchmark focus**

- Closed-set ObjectNav over HM3D-Semantics goal categories.
- Useful for comparing later ObjectNav papers against the established Habitat leaderboard protocol.
- Important caveat: no separate official 2024/2025 ObjectNav challenge page was found during curation.

</details>

#### ▸ HM3D-OVON

Yokoyama et al.
Benchmark, 2024. [Project](https://naoki.io/portfolio/ovon) | [Code](https://github.com/naokiyokoyama/ovon) | [Paper](https://arxiv.org/abs/2409.14296)

**Framework**

- Simulator: Habitat.
- Dataset: HM3D-OVON.
- Action space: discrete.
- Metrics: Success, SPL, distance-to-goal.
- Reproducibility: `partial`.

<details>
<summary>Expand Summary and Benchmark focus</summary>

**Summary**

HM3D-OVON extends HM3D-Semantics ObjectNav to open-vocabulary object goals, with free-form language targets over hundreds of object categories rather than a small closed set.

**Benchmark focus**

- Open-vocabulary object-goal navigation in real-world indoor scans.
- Free-form text goal specification at test time.
- Strong fit for VLM/LLM-assisted semantic exploration and open-set object grounding.

</details>

#### ▸ GOAT-Bench

Khanna et al.
Benchmark, 2024. [Project](https://mukulkhanna.github.io/goat-bench/) | [Code](https://github.com/Ram81/goat-bench) | [Paper](https://openaccess.thecvf.com/content/CVPR2024/html/Khanna_GOAT-Bench_A_Benchmark_for_Multi-Modal_Lifelong_Navigation_CVPR_2024_paper.html)

**Framework**

- Simulator: Habitat.
- Dataset: GOAT-Bench on HM3D.
- Action space: discrete.
- Metrics: Success, SPL, subtask success, lifelong progress.
- Reproducibility: `partial`.

<details>
<summary>Expand Summary and Benchmark focus</summary>

**Summary**

GOAT-Bench evaluates GO to AnyThing: an agent must solve 5-10 sequential navigation subtasks in a persistent indoor environment, with targets specified by category, language description, or instance image.

**Benchmark focus**

- Multi-modal goal specification across object, language, and image goals.
- Lifelong navigation with memory reused across sequential subtasks.
- Useful for universal navigation agents and foundation-model semantic memory systems.

</details>

#### ▸ RoboTHOR ObjectNav

Allen Institute for AI
Benchmark, 2020. [Project](https://ai2thor.allenai.org/robothor/) | [Code](https://github.com/allenai/robothor-challenge) | [Paper](https://arxiv.org/abs/2004.06799)

**Framework**

- Simulator: AI2-THOR / RoboTHOR.
- Dataset: RoboTHOR.
- Action space: discrete.
- Metrics: Success, SPL.
- Reproducibility: `partial`.

<details>
<summary>Expand Summary and Benchmark focus</summary>

**Summary**

RoboTHOR studies ObjectNav under a paired simulation and real-robot setup, making it important for evaluating whether navigation agents trained or tested in simulation transfer to physical indoor scenes.

**Benchmark focus**

- Object-category navigation with RGB and depth observations.
- Sim-to-real evaluation using AI2-THOR and RoboTHOR environments.
- Strong fit for agents that claim real-world robustness.

</details>

#### ▸ MultiON

MultiON Challenge team
Challenge, 2020. [Project](https://multion-challenge.cs.sfu.ca/2023.html) | [Code](https://github.com/saimwani/multiON) | [Leaderboard](https://eval.ai/) | [Paper](https://arxiv.org/abs/2012.11736)

**Framework**

- Simulator: Habitat.
- Dataset: MultiON Challenge episodes.
- Action space: discrete.
- Metrics: Success, progress, SPL variants.
- Reproducibility: `partial`.

<details>
<summary>Expand Summary and Benchmark focus</summary>

**Summary**

MultiON extends ObjectNav from a single goal to a sequence of object goals, testing long-horizon semantic exploration, memory, and route planning.

**Benchmark focus**

- Ordered multi-object navigation.
- Requires remembering previously visited spaces and planning efficient goal sequences.
- Useful for evaluating semantic maps, episodic memory, and hierarchical policies.

</details>

#### ▸ Room-to-Room (R2R)

Anderson et al.
Benchmark, 2018. [Project](https://bringmeaspoon.org/) | [Code](https://github.com/peteanderson80/Matterport3DSimulator) | [Leaderboard](https://eval.ai/) | [Paper](https://arxiv.org/abs/1711.07280)

**Framework**

- Simulator: Matterport3D Simulator.
- Dataset: R2R.
- Action space: graph-discrete viewpoints.
- Metrics: navigation error, success rate, SPL, nDTW, sDTW.
- Reproducibility: `verified`.

<details>
<summary>Expand Summary and Benchmark focus</summary>

**Summary**

R2R is the canonical Vision-Language Navigation benchmark: an agent follows human-written route instructions through Matterport3D environments.

**Benchmark focus**

- Natural-language route following.
- Graph-discrete panoramic navigation.
- Core testbed for instruction grounding, cross-modal alignment, and route progress estimation.

</details>

#### ▸ Room-Across-Room (RxR)

Ku et al.
Benchmark, 2020. [Project](https://research.google/pubs/room-across-room-multilingual-vision-and-language-navigation-with-dense-spatiotemporal-grounding/) | [Code](https://github.com/google-research-datasets/RxR) | [Leaderboard](https://eval.ai/) | [Paper](https://arxiv.org/abs/2010.07954)

**Framework**

- Simulator: Matterport3D / Habitat variants.
- Dataset: RxR.
- Action space: graph-discrete viewpoints and continuous variants.
- Metrics: navigation error, success rate, SPL, nDTW, sDTW.
- Reproducibility: `archival`.

<details>
<summary>Expand Summary and Benchmark focus</summary>

**Summary**

RxR scales VLN to multilingual instructions and dense spatiotemporal grounding, making it useful for evaluating language diversity and fine-grained instruction alignment.

**Benchmark focus**

- Multilingual route instructions.
- Dense alignment between language and trajectories.
- Useful for multilingual VLN and foundation-model grounding studies.

</details>

#### ▸ REVERIE

Qi et al.
Benchmark, 2020. [Project](https://github.com/YuankaiQi/REVERIE) | [Code](https://github.com/YuankaiQi/REVERIE) | [Paper](https://arxiv.org/abs/1904.10151)

**Framework**

- Simulator: Matterport3D Simulator.
- Dataset: REVERIE.
- Action space: graph-discrete viewpoints.
- Metrics: navigation error, oracle success rate, remote grounding success, SPL.
- Reproducibility: `partial`.

<details>
<summary>Expand Summary and Benchmark focus</summary>

**Summary**

REVERIE combines remote object localization with language-guided navigation. The agent must interpret a referring expression, navigate near the target region, and identify the referenced object.

**Benchmark focus**

- Referring-expression navigation.
- Joint evaluation of navigation and object grounding.
- Strong fit for open-vocabulary object grounding and VLN models.

</details>

#### ▸ Vision-and-Language Navigation in Continuous Environments (VLN-CE)

Krantz et al.
Benchmark, 2020. [Project](https://github.com/jacobkrantz/VLN-CE) | [Code](https://github.com/jacobkrantz/VLN-CE) | [Paper](https://arxiv.org/abs/2004.02857)

**Framework**

- Simulator: Habitat.
- Dataset: VLN-CE.
- Action space: continuous or low-level discrete.
- Metrics: success rate, SPL, nDTW, sDTW.
- Reproducibility: `partial`.

<details>
<summary>Expand Summary and Benchmark focus</summary>

**Summary**

VLN-CE converts instruction-following from graph-discrete navigation into continuous 3D control, exposing the gap between VLN route reasoning and embodied low-level navigation.

**Benchmark focus**

- Continuous-space instruction following.
- RGB-D navigation with natural-language instructions.
- Useful for models that combine language grounding with embodied control.

</details>

#### ▸ VLN-CE-Isaac / NaVILA-Bench

Cheng et al.
Benchmark, 2025. [Project](https://navila-bot.github.io/) | [Code](https://github.com/yang-zj1026/NaVILA-Bench) | [Paper](https://arxiv.org/abs/2412.04453)

**Framework**

- Simulator: Isaac Lab / Isaac Sim.
- Dataset: VLN-CE-Isaac.
- Action space: high-level language actions and low-level continuous locomotion control.
- Metrics: success rate, SPL, navigation error.
- Reproducibility: `partial`.

<details>
<summary>Expand Summary and Benchmark focus</summary>

**Summary**

VLN-CE-Isaac is the NaVILA benchmark for evaluating VLN-CE-style instruction following under physics-realistic low-level robot control in Isaac Lab.

**Benchmark focus**

- Vision-language navigation with quadruped and humanoid robot control.
- Tests the gap between high-level VLN decisions and executable locomotion.
- Useful for VLA navigation systems that combine language planning with learned robot skills.

</details>

#### ▸ VLN-PE

Wang et al.
Benchmark, 2025. [Project](https://crystalsixone.github.io/vln_pe.github.io/) | [Code](https://github.com/InternRobotics/InternNav) | [Paper](https://openaccess.thecvf.com/content/ICCV2025/html/Wang_Rethinking_the_Embodied_Gap_in_Vision-and-Language_Navigation_A_Holistic_Study_ICCV_2025_paper.html)

**Framework**

- Simulator: Isaac Sim / InternNav.
- Dataset: VLN-PE, GRU-VLN10, and 3DGS-Lab-VLN.
- Action space: discrete action prediction, dense waypoint prediction, map-based planning, physical controller.
- Metrics: navigation error, oracle success rate, success rate, SPL.
- Reproducibility: `partial`.

<details>
<summary>Expand Summary and Benchmark focus</summary>

**Summary**

VLN-PE studies the embodied gap in VLN by evaluating humanoid, quadruped, and wheeled robots under realistic locomotion, observation, lighting, and environment shifts.

**Benchmark focus**

- Cross-embodiment VLN across multiple robot morphologies.
- Physical and visual disparities beyond standard VLN-CE assumptions.
- Useful for testing whether VLN models can transfer from simulator-friendly motion to deployable robot control.

</details>

#### ▸ Cooperative Vision-and-Dialog Navigation (CVDN)

Thomason et al.
Benchmark, 2019. [Project](https://cvdn.dev/) | [Code](https://github.com/mmurray/cvdn) | [Paper](https://arxiv.org/abs/1907.04957)

**Framework**

- Simulator: Matterport3D Simulator.
- Dataset: CVDN.
- Action space: graph-discrete viewpoints.
- Metrics: goal progress, navigation error.
- Reproducibility: `partial`.

<details>
<summary>Expand Summary and Benchmark focus</summary>

**Summary**

CVDN evaluates navigation through dialog: a navigator must use conversation history with an oracle to infer the route and move toward the goal.

**Benchmark focus**

- Interactive vision-and-dialog navigation.
- Dialog history as the primary task context.
- Useful for studying clarification, instruction repair, and conversational grounding.

</details>

#### ▸ OpenEQA

Meta AI / FAIR
Benchmark, 2024. [Project](https://open-eqa.github.io/) | [Code](https://github.com/facebookresearch/open-eqa) | [Paper](https://open-eqa.github.io/assets/pdfs/paper.pdf)

**Framework**

- Environment: real-world scans and HM3D-style simulation.
- Dataset: OpenEQA.
- Action setting: episodic-memory-only and active-exploration variants.
- Metrics: LLM-Match, human agreement.
- Reproducibility: `verified`.

<details>
<summary>Expand Summary and Benchmark focus</summary>

**Summary**

OpenEQA evaluates whether embodied agents can answer open-vocabulary questions about an environment using episodic memory or active exploration.

**Benchmark focus**

- Embodied question answering in real-world and simulated environments.
- Foundation-model evaluation with open-vocabulary answers.
- Useful for studying spatial memory, exploration, and environment understanding.

</details>

#### ▸ EmbodiedScan

Wang et al.
Benchmark suite, 2024. [Project](https://tai-wang.github.io/embodiedscan/) | [Code](https://github.com/InternRobotics/EmbodiedScan) | [Paper](https://arxiv.org/abs/2312.16170)

**Framework**

- Environment: egocentric RGB-D real-world scans.
- Dataset: EmbodiedScan.
- Action setting: offline dataset evaluation.
- Metrics: 3D detection, semantic occupancy, visual grounding, language-grounded understanding.
- Reproducibility: `partial`.

<details>
<summary>Expand Summary and Benchmark focus</summary>

**Summary**

EmbodiedScan is a navigation-adjacent 3D perception suite for holistic egocentric scene understanding, with multi-view RGB-D observations, 3D annotations, and language prompts.

**Benchmark focus**

- Egocentric 3D perception for embodied agents.
- Scene understanding and language-grounded spatial perception.
- Useful as a perception and memory substrate for navigation systems, but it does not evaluate active navigation policies directly.

</details>

#### ▸ MMScan

Lyu et al.
Benchmark suite, 2024. [Project](https://tai-wang.github.io/mmscan/) | [Code](https://github.com/InternRobotics/EmbodiedScan) | [Paper](https://arxiv.org/abs/2406.09401)

**Framework**

- Environment: real-world 3D scans with grounded language annotations.
- Dataset: MMScan.
- Action setting: offline dataset evaluation.
- Metrics: visual grounding, question answering, grounded captioning.
- Reproducibility: `partial`.

<details>
<summary>Expand Summary and Benchmark focus</summary>

**Summary**

MMScan builds hierarchical grounded language annotations for 3D scenes, covering object-level and region-level captions, visual grounding, and spatial question answering.

**Benchmark focus**

- Multi-modal 3D scene understanding with language.
- Spatial reasoning over objects, regions, attributes, and relationships.
- Useful for evaluating the language-grounded scene understanding needed by embodied navigation agents.

</details>

#### ▸ SoundSpaces

Chen et al. / Meta AI
Benchmark, 2020. [Project](https://soundspaces.org/) | [Code](https://github.com/facebookresearch/sound-spaces) | [Paper](https://vision.cs.utexas.edu/projects/audio_visual_navigation/)

**Framework**

- Simulator: SoundSpaces / Habitat.
- Dataset: Matterport3D and Replica acoustic environments.
- Action space: discrete, with continuous variants in SoundSpaces 2.0.
- Metrics: success, SPL, distance-to-goal.
- Reproducibility: `verified`.

<details>
<summary>Expand Summary and Benchmark focus</summary>

**Summary**

SoundSpaces adds realistic audio simulation to embodied navigation, enabling agents to navigate toward sound-emitting targets using binaural audio and visual observations.

**Benchmark focus**

- AudioGoal and audio-visual navigation.
- Navigation under reverberation and spatial acoustics.
- Useful for multimodal policies that exploit sound as a spatial cue.

</details>

#### ▸ SocNavBench

CMU TBD Lab
Benchmark framework, 2021. [Project](https://github.com/CMU-TBD/SocNavBench) | [Code](https://github.com/CMU-TBD/SocNavBench) | [Paper](https://www.ri.cmu.edu/publications/socnavbench-a-grounded-simulation-testing-framework-for-evaluating-social-navigation/)

**Framework**

- Simulator: SocNavBench.
- Dataset: curated social navigation scenarios.
- Action space: planner-dependent.
- Metrics: path efficiency, safety, comfort, personal-space intrusion.
- Reproducibility: `partial`.

<details>
<summary>Expand Summary and Benchmark focus</summary>

**Summary**

SocNavBench is a simulation testing framework for social navigation, designed to evaluate how navigation policies behave around pedestrians and socially constrained spaces.

**Benchmark focus**

- Human-aware navigation evaluation.
- Safety, comfort, and personal-space behavior.
- Useful for comparing planners and learned policies beyond shortest-path efficiency.

</details>

#### ▸ Social Mobile Manipulation Challenge

SMM Challenge organizers
Challenge, 2025. [Project](https://smm-challenge.github.io/) | [Leaderboard](https://smm-challenge.github.io/)

**Framework**

- Simulator: Isaac Sim.
- Dataset: Open World Social Mobile Manipulation challenge setup.
- Action space: simulator API.
- Metrics: task success, social interaction quality, planning efficiency.
- Reproducibility: `needs-review`.

<details>
<summary>Expand Summary and Benchmark focus</summary>

**Summary**

The Social Mobile Manipulation Challenge evaluates long-horizon embodied agents in socially dynamic environments where navigation is part of mobile manipulation and interaction.

**Benchmark focus**

- Navigation under social interaction constraints.
- Scene-graph prompts and multi-agent dynamics.
- Useful for foundation-model agents that combine planning, navigation, and interaction.

</details>

#### ▸ HomeRobot Open-Vocabulary Mobile Manipulation (OVMM)

Yenamandra et al. / HomeRobot team
Benchmark and challenge, 2023. [Project](https://ovmm.github.io/) | [Code](https://github.com/facebookresearch/home-robot) | [Leaderboard](https://aihabitat.org/challenge/2023_homerobot_ovmm/) | [Paper](https://arxiv.org/abs/2306.11565)

**Framework**

- Simulator: Habitat / HomeRobot.
- Dataset: OVMM Dataset.
- Action space: continuous navigation and manipulation with interactive actions.
- Metrics: overall success, partial success, number of steps.
- Reproducibility: `partial`.

<details>
<summary>Expand Summary and Benchmark focus</summary>

**Summary**

HomeRobot OVMM evaluates whether a mobile manipulator can navigate unfamiliar homes, find novel objects and receptacles, grasp the object, and place it in the requested location.

**Benchmark focus**

- Navigation as a required subproblem inside open-vocabulary mobile manipulation.
- Simulation plus real-world Stretch robot counterpart.
- Useful for agents that integrate open-vocabulary perception, exploration, navigation, grasping, and placement.

</details>

#### ▸ AerialVLN

AirVLN team
Benchmark, 2023. [Project](https://github.com/AirVLN/AirVLN) | [Code](https://github.com/AirVLN/AirVLN) | [Paper](https://arxiv.org/abs/2308.06735)

**Framework**

- Simulator: AirVLN Simulator.
- Dataset: AerialVLN.
- Action space: continuous UAV control.
- Metrics: success rate, SPL-like metrics, trajectory error.
- Reproducibility: `partial`.

<details>
<summary>Expand Summary and Benchmark focus</summary>

**Summary**

AerialVLN moves language-guided navigation into UAV environments, testing whether agents can follow route instructions in outdoor aerial scenes.

**Benchmark focus**

- UAV-based vision-language navigation.
- Outdoor and city-scale trajectory following.
- Useful for testing language grounding under aerial viewpoints and continuous control.

</details>

#### ▸ Aerial Vision-and-Dialog Navigation (AVDN)

Eric AI Lab
Benchmark, 2023. [Project](https://github.com/eric-ai-lab/Aerial-Vision-and-Dialog-Navigation) | [Code](https://github.com/eric-ai-lab/Aerial-Vision-and-Dialog-Navigation) | [Leaderboard](https://eval.ai/web/challenges/challenge-page/2049/overview) | [Paper](https://arxiv.org/abs/2205.12219)

**Framework**

- Simulator: AVDN Simulator.
- Dataset: AVDN with xView-related access constraints.
- Action space: waypoint prediction.
- Metrics: waypoint error, navigation success.
- Reproducibility: `partial`.

<details>
<summary>Expand Summary and Benchmark focus</summary>

**Summary**

AVDN evaluates dialog-guided UAV navigation over aerial imagery, combining visual observations, dialog history, and waypoint prediction.

**Benchmark focus**

- Aerial vision-and-dialog navigation.
- Human attention and dialog-based route inference.
- Useful for outdoor interactive navigation and UAV instruction following.

</details>

#### ▸ NavBench

NavBench team
Benchmark, 2025. [Project](https://navbench.github.io/) | [Leaderboard](https://navbench.github.io/)

**Framework**

- Environment: benchmark-specific indoor navigation episodes.
- Dataset: NavBench.
- Action space: converted robot actions.
- Metrics: QA accuracy, execution success, complexity-stratified score.
- Reproducibility: `needs-review`.

<details>
<summary>Expand Summary and Benchmark focus</summary>

**Summary**

NavBench probes multimodal large language models on embodied navigation comprehension and step-by-step execution, emphasizing whether models understand navigational situations before acting.

**Benchmark focus**

- Foundation-model navigation evaluation.
- Comprehension and execution under varying task complexity.
- Useful for comparing MLLM navigation reasoning beyond final success alone.

</details>
### 3. Reproducibility Levels

Each benchmark entry receives a practical status:

| Status           | Meaning                                                                                              |
| ---------------- | ---------------------------------------------------------------------------------------------------- |
| `verified`     | Public data, code, evaluation instructions, and at least one baseline are available.                 |
| `partial`      | Some parts are public, but reproduction needs manual setup, private data access, or missing scripts. |
| `archival`     | Useful historically, but code/data/leaderboard may be stale or read-only.                            |
| `needs-review` | Added as a candidate and still needs verification.                                                   |

See [docs/reproducibility.md](docs/reproducibility.md).

### 4. Curation Axes

Each entry is tagged along these axes:

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

milestones:

- Build the benchmark seed table.
- Split benchmark entries into task-family pages.
- Add reproducibility checklists for major benchmarks.
- Add a comparison table for foundation-model navigation evaluation.
- Add contribution templates and review rules.

See [docs/roadmap.md](docs/roadmap.md).

## How To Contribute

Please open an issue using the benchmark template or submit a pull request that updates [data/benchmarks.yml](data/benchmarks.yml). A benchmark entry should include at least:

- official project or paper link
- code or dataset link, if public
- task family
- observation and action space
- metrics
- reproducibility status

See [CONTRIBUTING.md](CONTRIBUTING.md).

## License

MIT. Individual benchmark datasets and code repositories keep their own licenses and terms.
