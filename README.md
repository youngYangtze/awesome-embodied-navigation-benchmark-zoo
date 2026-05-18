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

The zoo groups benchmarks by task family rather than by paper chronology. Each family is shown with the icon used in the benchmark list below.

| Icon | Family | Core question | Examples |
| --- | --- | --- | --- |
| 🧭 | Point / Image / Object Navigation | Can the agent reach a coordinate, image goal, object instance, or object category? | Habitat PointNav, ObjectNav, Instance-ImageNav, RoboTHOR ObjectNav, ProcTHOR ObjectNav |
| 🌐 | Open-Vocabulary / Universal Navigation | Can the agent navigate to free-form, image, or language-specified goals beyond a closed category set? | HM3D-OVON, GOAT-Bench |
| 🗣 | Vision-Language Navigation | Can the agent follow natural-language instructions through an environment? | R2R, RxR, REVERIE, VLN-CE, CVDN, Touchdown |
| 🤖 | Physical / Cross-Embodiment VLN | Does VLN still work under realistic robot embodiment, physics, and visual shifts? | VLN-CE-Isaac, VLN-PE |
| ❓ | Embodied QA / Spatial QA / Exploration | Can the agent explore, use memory, or reason in 3D scenes to answer questions about a space? | OpenEQA, Explore-EQA, SQA3D |
| 🧱 | Spatial Scene Understanding | Can a model understand egocentric 3D scenes enough to support downstream navigation? | EmbodiedScan, MMScan |
| 👥 | Social / Human-Aware Navigation | Can the agent move safely and appropriately around humans or other agents? | SocNavBench, Habitat 3.0 Social, HabiCrowd, iGibson Challenge, SMM Challenge |
| 🦾 | Mobile Manipulation Navigation | Can the agent navigate as part of open-vocabulary manipulation? | HomeRobot OVMM |
| 📦 | Rearrangement / Long-Horizon Embodied | Can the agent chain navigation and interaction across a long household-style task? | ALFRED, TEACh, Habitat Rearrange, BEHAVIOR-1K, GRUtopia |
| 🔊 | Audio-Visual Navigation | Can the agent use sound and vision to localize and navigate to goals? | SoundSpaces |
| 🚁 | Aerial / Outdoor Navigation | Can a UAV or outdoor agent navigate using language, goals, or spatial reasoning? | AerialVLN, AVDN, CityNav |
| 🧪 | Foundation-Model Navigation | Can MLLMs / VLMs / VLAs comprehend and execute navigation tasks? | NavBench |

See [docs/taxonomy.md](docs/taxonomy.md) for the working taxonomy.

### 2. Benchmark Profiles

The structured source of truth is [data/benchmarks.yml](data/benchmarks.yml). Each entry is annotated with four badges:

- `year-YYYY` — first public release of the benchmark.
- `repro-{verified|partial|archival|needs-review}` — reproducibility status (see §3).
- `sim-{Simulator}` — primary simulator or environment.
- `FM-{high|medium|low}` — relevance to foundation-model (MLLM/VLM/VLA) navigation research.

#### 🧭 Point / Image / Object Navigation

##### 🧭 Habitat PointNav Challenge 2020

![year-2020](https://img.shields.io/badge/year-2020-blue) ![repro-verified](https://img.shields.io/badge/repro-verified-brightgreen) ![sim-Habitat](https://img.shields.io/badge/sim-Habitat-informational) ![FM-low](https://img.shields.io/badge/FM-low-lightgrey)

AI Habitat team  
Challenge, 2020. [Project](https://aihabitat.org/challenge/2020/) | [Code](https://github.com/facebookresearch/habitat-challenge) | [Leaderboard](https://eval.ai/web/challenges/challenge-page/802/overview) | [Paper](https://arxiv.org/abs/1912.06321)

**Framework**

- Simulator: Habitat-Sim.
- Dataset: Gibson and MP3D PointNav splits (72 train / 18 val MP3D scenes).
- Action space: discrete and continuous-velocity tracks.
- Metrics: Success, SPL, SoftSPL, distance-to-goal.
- License: MIT (challenge code); MP3D and Gibson research terms.
- Reproducibility: `verified`.

<details>
<summary>Expand Summary and Benchmark focus</summary>

**Summary**

Habitat PointNav 2020 is the canonical PointNav benchmark on Habitat, evaluating agents that navigate to a goal coordinate using egocentric sensing and odometry. The track also introduced ObjectNav.

**Benchmark focus**

- Coordinate-goal navigation with GPS/compass and RGB-D.
- Reference protocol for sim-to-real PointNav transfer.
- Useful as a baseline-friendly entry point before moving to ObjectNav or VLN.

</details>

##### 🧭 Habitat Navigation Challenge 2023

![year-2023](https://img.shields.io/badge/year-2023-blue) ![repro-verified](https://img.shields.io/badge/repro-verified-brightgreen) ![sim-Habitat](https://img.shields.io/badge/sim-Habitat-informational) ![FM-medium](https://img.shields.io/badge/FM-medium-blue)

AI Habitat team  
Challenge, 2023. [Project](https://aihabitat.org/challenge/2023/) | [Code](https://github.com/facebookresearch/habitat-challenge) | [Leaderboard](https://eval.ai/) | [Paper](https://arxiv.org/abs/1904.01201)

**Framework**

- Simulator: Habitat.
- Dataset: HM3D-Semantics v0.2 (~145 train / 36 val scenes).
- Action space: continuous velocity, waypoint, and discrete-waypoint variants.
- Metrics: Success, SPL, SoftSPL, distance-to-goal, collisions.
- License: MIT (challenge code); HM3D research terms.
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

##### 🧭 Habitat ObjectNav Challenge 2024/2025 Protocol

![year-2024](https://img.shields.io/badge/year-2024-blue) ![repro-archival](https://img.shields.io/badge/repro-archival-lightgrey) ![sim-Habitat](https://img.shields.io/badge/sim-Habitat-informational) ![FM-medium](https://img.shields.io/badge/FM-medium-blue)

AI Habitat team / community leaderboard users  
Challenge protocol, 2024. [Project](https://aihabitat.org/challenge/2023/) | [Code](https://github.com/facebookresearch/habitat-challenge) | [Leaderboard](https://eval.ai/web/challenges/challenge-page/1992/overview) | [Paper](https://arxiv.org/abs/2006.13171)

**Framework**

- Simulator: Habitat.
- Dataset: HM3D-Semantics v0.2 ObjectNav (~80k train + several thousand val episodes).
- Action space: continuous velocity, waypoint, and discrete-waypoint variants.
- Metrics: Success, SPL, SoftSPL, distance-to-goal, collisions.
- License: MIT (challenge code); HM3D research terms.
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

##### 🧭 Instance-ImageNav (HM3D)

![year-2023](https://img.shields.io/badge/year-2023-blue) ![repro-partial](https://img.shields.io/badge/repro-partial-yellow) ![sim-Habitat](https://img.shields.io/badge/sim-Habitat-informational) ![FM-high](https://img.shields.io/badge/FM-high-orange)

Krantz et al.  
Benchmark, 2023. [Project](https://jacobkrantz.github.io/modular_iin) | [Code](https://github.com/Jbwasse2/modular_iin) | [Paper](https://arxiv.org/abs/2304.01192)

**Framework**

- Simulator: Habitat.
- Dataset: Instance-ImageNav on HM3D-Semantics (~1k validation episodes; full HM3D train split).
- Action space: discrete.
- Metrics: Success, SPL, distance-to-goal.
- License: MIT (code); HM3D research terms.
- Reproducibility: `partial`.

<details>
<summary>Expand Summary and Benchmark focus</summary>

**Summary**

Instance-ImageNav asks an agent to navigate to a specific object instance shown in a goal image, rather than any instance of a category. The Modular IIN protocol (Krantz et al., ICCV 2023) defines the canonical HM3D evaluation.

**Benchmark focus**

- Instance-level visual matching grounded in 3D scenes.
- Strong fit for image-goal foundation models and re-identification approaches.
- Bridges ObjectNav and ImageNav by emphasizing identity rather than category.

</details>

##### 🧭 RoboTHOR ObjectNav

![year-2020](https://img.shields.io/badge/year-2020-blue) ![repro-partial](https://img.shields.io/badge/repro-partial-yellow) ![sim-AI2--THOR](https://img.shields.io/badge/sim-AI2--THOR-informational) ![FM-medium](https://img.shields.io/badge/FM-medium-blue)

Allen Institute for AI  
Benchmark, 2020. [Project](https://ai2thor.allenai.org/robothor/) | [Code](https://github.com/allenai/robothor-challenge) | [Paper](https://arxiv.org/abs/2004.06799)

**Framework**

- Simulator: AI2-THOR / RoboTHOR.
- Dataset: 75 simulated apartments paired with real RoboTHOR apartments; 12 object categories.
- Action space: discrete.
- Metrics: Success, SPL.
- License: Apache-2.0 (AI2-THOR / RoboTHOR).
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

##### 🧭 ProcTHOR ObjectNav

![year-2022](https://img.shields.io/badge/year-2022-blue) ![repro-verified](https://img.shields.io/badge/repro-verified-brightgreen) ![sim-AI2--THOR](https://img.shields.io/badge/sim-AI2--THOR-informational) ![FM-medium](https://img.shields.io/badge/FM-medium-blue)

Deitke et al.  
Benchmark, 2022. [Project](https://procthor.allenai.org/) | [Code](https://github.com/allenai/procthor-10k) | [Paper](https://arxiv.org/abs/2206.06994)

**Framework**

- Simulator: AI2-THOR / ProcTHOR.
- Dataset: ProcTHOR-10K (10,000 procedurally generated multi-room houses; 1,633 assets in 18 semantic groups).
- Action space: discrete.
- Metrics: Success, SPL.
- License: Apache-2.0 (code and procedural assets).
- Reproducibility: `verified`.

<details>
<summary>Expand Summary and Benchmark focus</summary>

**Summary**

ProcTHOR generates large-scale procedural indoor environments to pre-train and evaluate ObjectNav agents. The NeurIPS 2022 paper showed that scaling procedural training improves transfer to RoboTHOR, ArchitecTHOR, and Habitat ObjectNav.

**Benchmark focus**

- ObjectNav under massive scene-diversity scaling.
- Procedural data as a substitute for real-scene scarcity.
- Strong fit for studies of generalization, scene priors, and pretraining recipes.

</details>

##### 🧭 MultiON

![year-2020](https://img.shields.io/badge/year-2020-blue) ![repro-partial](https://img.shields.io/badge/repro-partial-yellow) ![sim-Habitat](https://img.shields.io/badge/sim-Habitat-informational) ![FM-medium](https://img.shields.io/badge/FM-medium-blue)

MultiON Challenge team  
Challenge, 2020. [Project](https://multion-challenge.cs.sfu.ca/2023.html) | [Code](https://github.com/saimwani/multiON) | [Leaderboard](https://eval.ai/) | [Paper](https://arxiv.org/abs/2012.11736)

**Framework**

- Simulator: Habitat.
- Dataset: MultiON episodes with 3-5 sequential object goals over MP3D scenes.
- Action space: discrete.
- Metrics: Success, progress, SPL variants.
- License: MIT (code); MP3D research terms.
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

#### 🌐 Open-Vocabulary / Universal Navigation

##### 🌐 HM3D-OVON

![year-2024](https://img.shields.io/badge/year-2024-blue) ![repro-partial](https://img.shields.io/badge/repro-partial-yellow) ![sim-Habitat](https://img.shields.io/badge/sim-Habitat-informational) ![FM-high](https://img.shields.io/badge/FM-high-orange)

Yokoyama et al.  
Benchmark, 2024. [Project](https://naoki.io/portfolio/ovon) | [Code](https://github.com/naokiyokoyama/ovon) | [Paper](https://arxiv.org/abs/2409.14296)

**Framework**

- Simulator: Habitat.
- Dataset: HM3D-OVON (379 categories, ~15k annotated instances across HM3D-Semantics scenes).
- Action space: discrete.
- Metrics: Success, SPL, distance-to-goal.
- License: MIT (code); HM3D research terms.
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

##### 🌐 GOAT-Bench

![year-2024](https://img.shields.io/badge/year-2024-blue) ![repro-partial](https://img.shields.io/badge/repro-partial-yellow) ![sim-Habitat](https://img.shields.io/badge/sim-Habitat-informational) ![FM-high](https://img.shields.io/badge/FM-high-orange)

Khanna et al.  
Benchmark, 2024. [Project](https://mukulkhanna.github.io/goat-bench/) | [Code](https://github.com/Ram81/goat-bench) | [Paper](https://openaccess.thecvf.com/content/CVPR2024/html/Khanna_GOAT-Bench_A_Benchmark_for_Multi-Modal_Lifelong_Navigation_CVPR_2024_paper.html)

**Framework**

- Simulator: Habitat.
- Dataset: GOAT-Bench lifelong episodes with 5-10 sequential subtasks across HM3D-Semantics scenes.
- Action space: discrete.
- Metrics: Success, SPL, subtask success, lifelong progress.
- License: MIT (code); HM3D research terms.
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

#### 🗣 Vision-Language Navigation

##### 🗣 Room-to-Room (R2R)

![year-2018](https://img.shields.io/badge/year-2018-blue) ![repro-verified](https://img.shields.io/badge/repro-verified-brightgreen) ![sim-MP3D](https://img.shields.io/badge/sim-MP3D-informational) ![FM-high](https://img.shields.io/badge/FM-high-orange)

Anderson et al.  
Benchmark, 2018. [Project](https://bringmeaspoon.org/) | [Code](https://github.com/peteanderson80/Matterport3DSimulator) | [Leaderboard](https://eval.ai/) | [Paper](https://arxiv.org/abs/1711.07280)

**Framework**

- Simulator: Matterport3D Simulator.
- Dataset: R2R (21,567 instructions over 7,189 paths in 90 MP3D buildings).
- Action space: graph-discrete viewpoints.
- Metrics: navigation error, success rate, SPL, nDTW, sDTW.
- License: BSD-3-Clause (simulator); MP3D research terms.
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

##### 🗣 Room-Across-Room (RxR)

![year-2020](https://img.shields.io/badge/year-2020-blue) ![repro-archival](https://img.shields.io/badge/repro-archival-lightgrey) ![sim-MP3D](https://img.shields.io/badge/sim-MP3D-informational) ![FM-high](https://img.shields.io/badge/FM-high-orange)

Ku et al.  
Benchmark, 2020. [Project](https://research.google/pubs/room-across-room-multilingual-vision-and-language-navigation-with-dense-spatiotemporal-grounding/) | [Code](https://github.com/google-research-datasets/RxR) | [Leaderboard](https://eval.ai/) | [Paper](https://arxiv.org/abs/2010.07954)

**Framework**

- Simulator: Matterport3D / Habitat variants.
- Dataset: RxR (~126k instructions in English, Hindi, Telugu over 16,522 paths).
- Action space: graph-discrete viewpoints and continuous variants.
- Metrics: navigation error, success rate, SPL, nDTW, sDTW.
- License: CC-BY-4.0 (dataset); MP3D research terms.
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

##### 🗣 REVERIE

![year-2020](https://img.shields.io/badge/year-2020-blue) ![repro-partial](https://img.shields.io/badge/repro-partial-yellow) ![sim-MP3D](https://img.shields.io/badge/sim-MP3D-informational) ![FM-high](https://img.shields.io/badge/FM-high-orange)

Qi et al.  
Benchmark, 2020. [Project](https://github.com/YuankaiQi/REVERIE) | [Code](https://github.com/YuankaiQi/REVERIE) | [Paper](https://arxiv.org/abs/1904.10151)

**Framework**

- Simulator: Matterport3D Simulator.
- Dataset: REVERIE (21,702 instructions over 4,140 target objects in 86 MP3D buildings).
- Action space: graph-discrete viewpoints.
- Metrics: navigation error, oracle success rate, remote grounding success, SPL.
- License: see project; MP3D research terms.
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

##### 🗣 Vision-and-Language Navigation in Continuous Environments (VLN-CE)

![year-2020](https://img.shields.io/badge/year-2020-blue) ![repro-partial](https://img.shields.io/badge/repro-partial-yellow) ![sim-Habitat](https://img.shields.io/badge/sim-Habitat-informational) ![FM-high](https://img.shields.io/badge/FM-high-orange)

Krantz et al.  
Benchmark, 2020. [Project](https://github.com/jacobkrantz/VLN-CE) | [Code](https://github.com/jacobkrantz/VLN-CE) | [Paper](https://arxiv.org/abs/2004.02857)

**Framework**

- Simulator: Habitat.
- Dataset: VLN-CE (~16k instructions ported from R2R and RxR into continuous Habitat episodes on MP3D).
- Action space: continuous or low-level discrete.
- Metrics: success rate, SPL, nDTW, sDTW.
- License: MIT (code); MP3D research terms.
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

##### 🗣 Cooperative Vision-and-Dialog Navigation (CVDN)

![year-2019](https://img.shields.io/badge/year-2019-blue) ![repro-partial](https://img.shields.io/badge/repro-partial-yellow) ![sim-MP3D](https://img.shields.io/badge/sim-MP3D-informational) ![FM-high](https://img.shields.io/badge/FM-high-orange)

Thomason et al.  
Benchmark, 2019. [Project](https://cvdn.dev/) | [Code](https://github.com/mmurray/cvdn) | [Paper](https://arxiv.org/abs/1907.04957)

**Framework**

- Simulator: Matterport3D Simulator.
- Dataset: CVDN (2,050 human-human dialog sessions over MP3D with 7,000+ navigation episodes).
- Action space: graph-discrete viewpoints.
- Metrics: goal progress, navigation error.
- License: see project; MP3D research terms.
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

##### 🗣 Touchdown

![year-2019](https://img.shields.io/badge/year-2019-blue) ![repro-partial](https://img.shields.io/badge/repro-partial-yellow) ![sim-StreetLearn](https://img.shields.io/badge/sim-StreetLearn-informational) ![FM-high](https://img.shields.io/badge/FM-high-orange)

Chen et al.  
Benchmark, 2019. [Project](https://github.com/lil-lab/touchdown) | [Code](https://github.com/lil-lab/touchdown) | [Paper](https://arxiv.org/abs/1811.12354)

**Framework**

- Simulator: StreetLearn (Manhattan Street View panoramas).
- Dataset: Touchdown (9,326 instruction+spatial-description examples over ~29k panoramas).
- Action space: graph-discrete street-view navigation.
- Metrics: task completion, sDTW, spatial-description accuracy.
- License: CC-BY-4.0 (dataset); StreetLearn panorama access form required.
- Reproducibility: `partial`.

<details>
<summary>Expand Summary and Benchmark focus</summary>

**Summary**

Touchdown brings VLN outdoors: an agent navigates a real Manhattan street-view graph following natural-language instructions, then resolves a spatial description to localize the goal.

**Benchmark focus**

- Outdoor street-view instruction following at city scale.
- Joint navigation and spatial-description resolution.
- Useful for testing language grounding outside indoor scans and for street-view foundation models.

</details>

#### 🤖 Physical / Cross-Embodiment VLN

##### 🤖 VLN-CE-Isaac / NaVILA-Bench

![year-2025](https://img.shields.io/badge/year-2025-blue) ![repro-partial](https://img.shields.io/badge/repro-partial-yellow) ![sim-Isaac](https://img.shields.io/badge/sim-Isaac-informational) ![FM-high](https://img.shields.io/badge/FM-high-orange)

Cheng et al.  
Benchmark, 2025. [Project](https://navila-bot.github.io/) | [Code](https://github.com/yang-zj1026/NaVILA-Bench) | [Paper](https://arxiv.org/abs/2412.04453)

**Framework**

- Simulator: Isaac Lab / Isaac Sim.
- Dataset: VLN-CE episodes ported to Isaac Lab with quadruped and humanoid embodiments.
- Action space: high-level language actions and low-level continuous locomotion control.
- Metrics: success rate, SPL, navigation error.
- License: see project (Isaac Sim assets follow NVIDIA terms).
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

##### 🤖 VLN-PE

![year-2025](https://img.shields.io/badge/year-2025-blue) ![repro-partial](https://img.shields.io/badge/repro-partial-yellow) ![sim-Isaac](https://img.shields.io/badge/sim-Isaac-informational) ![FM-high](https://img.shields.io/badge/FM-high-orange)

Wang et al.  
Benchmark, 2025. [Project](https://crystalsixone.github.io/vln_pe.github.io/) | [Code](https://github.com/InternRobotics/InternNav) | [Paper](https://openaccess.thecvf.com/content/ICCV2025/html/Wang_Rethinking_the_Embodied_Gap_in_Vision-and-Language_Navigation_A_Holistic_Study_ICCV_2025_paper.html)

**Framework**

- Simulator: Isaac Sim / InternNav.
- Dataset: VLN-PE, GRU-VLN10, and 3DGS-Lab-VLN (humanoid, quadruped, wheeled embodiments).
- Action space: discrete action prediction, dense waypoint prediction, map-based planning, physical controller.
- Metrics: navigation error, oracle success rate, success rate, SPL.
- License: see project (Isaac Sim and external scene assets follow upstream terms).
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

#### ❓ Embodied QA / Spatial QA / Exploration

##### ❓ OpenEQA

![year-2024](https://img.shields.io/badge/year-2024-blue) ![repro-verified](https://img.shields.io/badge/repro-verified-brightgreen) ![sim-Habitat](https://img.shields.io/badge/sim-Habitat-informational) ![FM-high](https://img.shields.io/badge/FM-high-orange)

Meta AI / FAIR  
Benchmark, 2024. [Project](https://open-eqa.github.io/) | [Code](https://github.com/facebookresearch/open-eqa) | [Paper](https://open-eqa.github.io/assets/pdfs/paper.pdf)

**Framework**

- Environment: real-world scans and HM3D-style simulation.
- Dataset: OpenEQA (~1,600 questions over 180+ scans; episodic-memory and active-exploration splits).
- Action setting: episodic-memory-only and active-exploration variants.
- Metrics: LLM-Match, human agreement.
- License: MIT (code); CC-BY-4.0 (annotations).
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

##### ❓ Explore-EQA

![year-2024](https://img.shields.io/badge/year-2024-blue) ![repro-partial](https://img.shields.io/badge/repro-partial-yellow) ![sim-Habitat](https://img.shields.io/badge/sim-Habitat-informational) ![FM-high](https://img.shields.io/badge/FM-high-orange)

Ren et al.  
Benchmark, 2024. [Project](https://explore-eqa.github.io/) | [Code](https://github.com/Stanford-ILIAD/explore-eqa) | [Paper](https://arxiv.org/abs/2403.15941)

**Framework**

- Simulator: Habitat.
- Dataset: HM-EQA (500 questions across 267 HM3D scenes).
- Action space: active exploration.
- Metrics: answer accuracy, exploration efficiency, confidence calibration.
- License: MIT (code); HM3D research terms.
- Reproducibility: `partial`.

<details>
<summary>Expand Summary and Benchmark focus</summary>

**Summary**

Explore-EQA (RSS 2024) introduces VLM-driven active EQA with a confidence-aware stopping rule. The HM-EQA dataset stress-tests when an embodied VLM should keep exploring versus answer.

**Benchmark focus**

- Active exploration tied to model confidence.
- Open-vocabulary EQA over HM3D scenes.
- Useful for foundation-model agents that plan exploration based on epistemic uncertainty.

</details>

##### ❓ SQA3D

![year-2023](https://img.shields.io/badge/year-2023-blue) ![repro-verified](https://img.shields.io/badge/repro-verified-brightgreen) ![sim-Dataset](https://img.shields.io/badge/sim-Dataset-lightgrey) ![FM-high](https://img.shields.io/badge/FM-high-orange)

Ma et al.  
Benchmark, 2023. [Project](https://sqa3d.github.io/) | [Code](https://github.com/SilongYong/SQA3D) | [Paper](https://arxiv.org/abs/2210.07474)

**Framework**

- Environment: real-world 3D scans (ScanNet).
- Dataset: SQA3D (650 scenes, 6.8k situations, 20.4k descriptions, 33.4k question-answer pairs).
- Action setting: offline dataset evaluation.
- Metrics: answer accuracy, top-k accuracy.
- License: MIT (code); ScanNet research terms.
- Reproducibility: `verified`.

<details>
<summary>Expand Summary and Benchmark focus</summary>

**Summary**

SQA3D (ICLR 2023) introduces situated question answering: an agent is placed in a 3D scene with a specified pose and answers questions that depend on its viewpoint and context.

**Benchmark focus**

- Pose- and viewpoint-grounded QA over 3D scenes.
- Foundational testbed for spatial reasoning in MLLMs / 3D-LLMs.
- Complements active EQA by isolating reasoning from exploration.

</details>

#### 🧱 Spatial Scene Understanding

##### 🧱 EmbodiedScan

![year-2024](https://img.shields.io/badge/year-2024-blue) ![repro-partial](https://img.shields.io/badge/repro-partial-yellow) ![sim-Dataset](https://img.shields.io/badge/sim-Dataset-lightgrey) ![FM-high](https://img.shields.io/badge/FM-high-orange)

Wang et al.  
Benchmark suite, 2024. [Project](https://tai-wang.github.io/embodiedscan/) | [Code](https://github.com/InternRobotics/EmbodiedScan) | [Paper](https://arxiv.org/abs/2312.16170)

**Framework**

- Environment: egocentric RGB-D real-world scans.
- Dataset: EmbodiedScan (5,185 scans across ScanNet, 3RScan, MP3D; oriented 3D boxes, occupancy, language prompts).
- Action setting: offline dataset evaluation.
- Metrics: 3D detection, semantic occupancy, visual grounding, language-grounded understanding.
- License: Apache-2.0 (code); upstream scan datasets follow their own research terms.
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

##### 🧱 MMScan

![year-2024](https://img.shields.io/badge/year-2024-blue) ![repro-partial](https://img.shields.io/badge/repro-partial-yellow) ![sim-Dataset](https://img.shields.io/badge/sim-Dataset-lightgrey) ![FM-high](https://img.shields.io/badge/FM-high-orange)

Lyu et al.  
Benchmark suite, 2024. [Project](https://tai-wang.github.io/mmscan/) | [Code](https://github.com/InternRobotics/EmbodiedScan) | [Paper](https://arxiv.org/abs/2406.09401)

**Framework**

- Environment: real-world 3D scans with grounded language annotations.
- Dataset: MMScan (~109k object-level and ~7.7k region-level descriptions; 3.04M grounded QA pairs).
- Action setting: offline dataset evaluation.
- Metrics: visual grounding, question answering, grounded captioning.
- License: Apache-2.0 (code); upstream scan datasets follow their own research terms.
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

#### 👥 Social / Human-Aware Navigation

##### 👥 SocNavBench

![year-2021](https://img.shields.io/badge/year-2021-blue) ![repro-partial](https://img.shields.io/badge/repro-partial-yellow) ![sim-SocNavBench](https://img.shields.io/badge/sim-SocNavBench-informational) ![FM-medium](https://img.shields.io/badge/FM-medium-blue)

CMU TBD Lab  
Benchmark framework, 2021. [Project](https://github.com/CMU-TBD/SocNavBench) | [Code](https://github.com/CMU-TBD/SocNavBench) | [Paper](https://www.ri.cmu.edu/publications/socnavbench-a-grounded-simulation-testing-framework-for-evaluating-social-navigation/)

**Framework**

- Simulator: SocNavBench.
- Dataset: curated scenarios grounded in ETH/UCY pedestrian datasets.
- Action space: planner-dependent.
- Metrics: path efficiency, safety, comfort, personal-space intrusion.
- License: MIT (code); upstream pedestrian datasets follow their own terms.
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

##### 👥 Habitat 3.0 Social Navigation

![year-2024](https://img.shields.io/badge/year-2024-blue) ![repro-partial](https://img.shields.io/badge/repro-partial-yellow) ![sim-Habitat](https://img.shields.io/badge/sim-Habitat-informational) ![FM-high](https://img.shields.io/badge/FM-high-orange)

Puig et al. / FAIR  
Benchmark, 2024. [Project](https://aihabitat.org/habitat3/) | [Code](https://github.com/facebookresearch/habitat-lab) | [Paper](https://arxiv.org/abs/2310.13724)

**Framework**

- Simulator: Habitat 3.0.
- Dataset: Social Navigation and Social Rearrangement tasks over HSSD-Sem and ReplicaCAD scenes with humanoid avatars.
- Action space: continuous velocity, high-level skill, manipulation.
- Metrics: success rate, social SPL, human collision.
- License: MIT (Habitat-Lab); HSSD and ReplicaCAD research terms.
- Reproducibility: `partial`.

<details>
<summary>Expand Summary and Benchmark focus</summary>

**Summary**

Habitat 3.0 (ICLR 2024) introduces humanoid avatars in indoor scenes and benchmarks human-robot collaboration tasks including Social Navigation (find-and-follow human) and Social Rearrangement.

**Benchmark focus**

- Robot-humanoid coexistence at simulation scale.
- Joint navigation and manipulation in shared spaces.
- Useful for studies of cooperative behavior and personal-space-aware policies.

</details>

##### 👥 HabiCrowd

![year-2024](https://img.shields.io/badge/year-2024-blue) ![repro-partial](https://img.shields.io/badge/repro-partial-yellow) ![sim-Habitat](https://img.shields.io/badge/sim-Habitat-informational) ![FM-medium](https://img.shields.io/badge/FM-medium-blue)

Nguyen et al.  
Benchmark, 2024. [Project](https://habicrowd.github.io/) | [Code](https://github.com/Fsoft-AIC/HabiCrowd) | [Paper](https://arxiv.org/abs/2306.11377)

**Framework**

- Simulator: HabiCrowd (Habitat 2.0 extension).
- Dataset: Crowd-aware PointNav and ObjectNav episodes over HM3D scenes with five baselines.
- Action space: discrete and continuous velocity.
- Metrics: success, SPL, human collision, personal-space intrusion.
- License: MIT (code); HM3D research terms.
- Reproducibility: `partial`.

<details>
<summary>Expand Summary and Benchmark focus</summary>

**Summary**

HabiCrowd (IROS 2024) extends Habitat 2.0 with high-performance pedestrian crowd simulation and benchmarks both PointNav and ObjectNav agents in dynamic human environments.

**Benchmark focus**

- Crowd navigation at simulation scale.
- Standardized social metrics alongside SPL.
- Useful for testing robustness of indoor navigation under moving humans.

</details>

##### 👥 iGibson Challenge 2021

![year-2021](https://img.shields.io/badge/year-2021-blue) ![repro-archival](https://img.shields.io/badge/repro-archival-lightgrey) ![sim-iGibson](https://img.shields.io/badge/sim-iGibson-informational) ![FM-low](https://img.shields.io/badge/FM-low-lightgrey)

Stanford SVL  
Challenge, 2021. [Project](https://svl.stanford.edu/igibson/challenge2021.html) | [Code](https://github.com/StanfordVL/iGibsonChallenge2021) | [Paper](https://arxiv.org/abs/2012.02924)

**Framework**

- Simulator: iGibson 1.0.
- Dataset: 8 fully interactive iGibson scenes; Interactive Nav + Social Nav (pedestrian-crowd) tracks.
- Action space: continuous velocity.
- Metrics: Success, SPL, interactive SPL, personal-space intrusion.
- License: MIT (iGibson); upstream scan datasets follow their own terms.
- Reproducibility: `archival`.

<details>
<summary>Expand Summary and Benchmark focus</summary>

**Summary**

The iGibson Challenge 2021 (CVPR Embodied AI Workshop) benchmarks interactive and social navigation in fully physics-simulated scenes where the agent may push, displace, and otherwise interact with the environment.

**Benchmark focus**

- Interactive navigation with articulated and movable objects.
- Social navigation with simulated pedestrian crowds.
- Historically important reference for interactive + social navigation evaluation.

</details>

##### 👥 Social Mobile Manipulation Challenge

![year-2025](https://img.shields.io/badge/year-2025-blue) ![repro-needs--review](https://img.shields.io/badge/repro-needs--review-orange) ![sim-Isaac](https://img.shields.io/badge/sim-Isaac-informational) ![FM-high](https://img.shields.io/badge/FM-high-orange)

SMM Challenge organizers  
Challenge, 2025. [Project](https://smm-challenge.github.io/) | [Leaderboard](https://smm-challenge.github.io/)

**Framework**

- Simulator: Isaac Sim.
- Dataset: Open World Social Mobile Manipulation challenge setup (full size pending public release).
- Action space: simulator API.
- Metrics: task success, social interaction quality, planning efficiency.
- License: see project (challenge registration required).
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

#### 🦾 Mobile Manipulation Navigation

##### 🦾 HomeRobot Open-Vocabulary Mobile Manipulation (OVMM)

![year-2023](https://img.shields.io/badge/year-2023-blue) ![repro-partial](https://img.shields.io/badge/repro-partial-yellow) ![sim-Habitat](https://img.shields.io/badge/sim-Habitat-informational) ![FM-high](https://img.shields.io/badge/FM-high-orange)

Yenamandra et al. / HomeRobot team  
Benchmark and challenge, 2023. [Project](https://ovmm.github.io/) | [Code](https://github.com/facebookresearch/home-robot) | [Leaderboard](https://aihabitat.org/challenge/2023_homerobot_ovmm/) | [Paper](https://arxiv.org/abs/2306.11565)

**Framework**

- Simulator: Habitat / HomeRobot.
- Dataset: OVMM Dataset (200 simulated scenes; 7,892 object instances across 150 categories and 21 receptacle types).
- Action space: continuous navigation and manipulation with interactive actions.
- Metrics: overall success, partial success, number of steps.
- License: MIT (HomeRobot code); HSSD and OVMM research terms.
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

#### 📦 Rearrangement / Long-Horizon Embodied

##### 📦 ALFRED

![year-2020](https://img.shields.io/badge/year-2020-blue) ![repro-verified](https://img.shields.io/badge/repro-verified-brightgreen) ![sim-AI2--THOR](https://img.shields.io/badge/sim-AI2--THOR-informational) ![FM-high](https://img.shields.io/badge/FM-high-orange)

Shridhar et al.  
Benchmark, 2020. [Project](https://askforalfred.com/) | [Code](https://github.com/askforalfred/alfred) | [Leaderboard](https://leaderboard.allenai.org/alfred/submissions/public) | [Paper](https://arxiv.org/abs/1912.01734)

**Framework**

- Simulator: AI2-THOR.
- Dataset: ALFRED (8,055 expert demos, 25,743 directives, 120 scenes, ~428k image-action pairs).
- Action space: discrete navigation and object interaction.
- Metrics: task success, goal-condition success, path-length-weighted success.
- License: MIT (code and data).
- Reproducibility: `verified`.

<details>
<summary>Expand Summary and Benchmark focus</summary>

**Summary**

ALFRED tasks an agent with completing long-horizon household goals described in natural language, chaining navigation and object interaction across many steps in AI2-THOR scenes.

**Benchmark focus**

- Language-conditioned household task completion.
- Navigation tightly coupled to object interaction.
- Strong fit for instruction-following foundation models and VLA pipelines.

</details>

##### 📦 TEACh

![year-2022](https://img.shields.io/badge/year-2022-blue) ![repro-verified](https://img.shields.io/badge/repro-verified-brightgreen) ![sim-AI2--THOR](https://img.shields.io/badge/sim-AI2--THOR-informational) ![FM-high](https://img.shields.io/badge/FM-high-orange)

Padmakumar et al.  
Benchmark, 2022. [Project](https://github.com/alexa/teach) | [Code](https://github.com/alexa/teach) | [Leaderboard](https://eval.ai/web/challenges/challenge-page/1652/overview) | [Paper](https://arxiv.org/abs/2110.00534)

**Framework**

- Simulator: AI2-THOR.
- Dataset: TEACh (3,215 human-human dialog sessions, ~39.5k utterances).
- Action space: discrete navigation and object interaction.
- Metrics: task success, goal-condition success, mission progress.
- License: MIT (code and data, Amazon Alexa AI).
- Reproducibility: `verified`.

<details>
<summary>Expand Summary and Benchmark focus</summary>

**Summary**

TEACh (AAAI 2022) studies dialog-driven household task completion, with EDH (Execution from Dialog History) and TfD (Trajectory from Dialog) tracks that test how well an agent follows free-form collaborative instructions.

**Benchmark focus**

- Dialog-conditioned household task completion.
- Long horizons with mixed navigation and interaction.
- Useful for evaluating LLM-driven planning, dialog grounding, and tool-use-style action prediction.

</details>

##### 📦 Habitat Rearrangement Challenge 2022

![year-2022](https://img.shields.io/badge/year-2022-blue) ![repro-archival](https://img.shields.io/badge/repro-archival-lightgrey) ![sim-Habitat](https://img.shields.io/badge/sim-Habitat-informational) ![FM-medium](https://img.shields.io/badge/FM-medium-blue)

Habitat team  
Challenge, 2022. [Project](https://aihabitat.org/challenge/2022_rearrange/) | [Code](https://github.com/facebookresearch/habitat-challenge) | [Leaderboard](https://eval.ai/web/challenges/challenge-page/1820/overview) | [Paper](https://arxiv.org/abs/2106.14405)

**Framework**

- Simulator: Habitat 2.0.
- Dataset: 50k train episodes over 63 ReplicaCAD scenes; 1k val and 1k test episodes in 21 unseen scenes; Fetch robot.
- Action space: continuous base, continuous arm, grip.
- Metrics: success, partial success, efficiency.
- License: MIT (challenge code); ReplicaCAD research terms.
- Reproducibility: `archival`.

<details>
<summary>Expand Summary and Benchmark focus</summary>

**Summary**

The Habitat Rearrangement Challenge (NeurIPS 2022 competition) evaluates pick-and-place at home scale, where the agent must navigate to an object, grasp it, navigate to the target, and place it accurately.

**Benchmark focus**

- Navigation as a required subproblem inside rearrangement.
- Mobile manipulation with a Fetch-style robot.
- Reference protocol for later rearrangement and mobile manipulation work.

</details>

##### 📦 BEHAVIOR-1K

![year-2022](https://img.shields.io/badge/year-2022-blue) ![repro-partial](https://img.shields.io/badge/repro-partial-yellow) ![sim-OmniGibson](https://img.shields.io/badge/sim-OmniGibson-informational) ![FM-high](https://img.shields.io/badge/FM-high-orange)

Li et al. / Stanford SVL  
Benchmark, 2022. [Project](https://behavior.stanford.edu/) | [Code](https://github.com/StanfordVL/BEHAVIOR-1K) | [Paper](https://arxiv.org/abs/2403.09227)

**Framework**

- Simulator: OmniGibson (Isaac Sim).
- Dataset: BEHAVIOR-1K (1,000 everyday activities over 50 fully interactive scenes; >9,000 annotated objects).
- Action space: continuous base and arm, articulated interaction.
- Metrics: task success, goal-condition success, efficiency.
- License: MIT (code and assets); upstream scan datasets follow their own terms.
- Reproducibility: `partial`.

<details>
<summary>Expand Summary and Benchmark focus</summary>

**Summary**

BEHAVIOR-1K (CoRL 2022, extended 2024) defines a thousand everyday human activities formalized with logical goal conditions. Navigation, manipulation, and articulated object interaction are required to solve full activities.

**Benchmark focus**

- Long-horizon embodied activity at scale.
- Logical goal conditions instead of free-form rewards.
- Useful for evaluating planners, VLA stacks, and skill libraries.

</details>

##### 📦 GRUtopia / GRScenes

![year-2024](https://img.shields.io/badge/year-2024-blue) ![repro-partial](https://img.shields.io/badge/repro-partial-yellow) ![sim-Isaac](https://img.shields.io/badge/sim-Isaac-informational) ![FM-high](https://img.shields.io/badge/FM-high-orange)

Shanghai AI Lab / OpenRobotLab  
Benchmark suite, 2024. [Project](https://github.com/OpenRobotLab/GRUtopia) | [Code](https://github.com/OpenRobotLab/GRUtopia) | [Paper](https://arxiv.org/abs/2407.10943)

**Framework**

- Simulator: GRUtopia (Isaac Sim).
- Dataset: GRScenes (100k interactive annotated scenes across 89 categories).
- Action space: continuous base and arm, high-level skill.
- Metrics: task success, sub-goal success, efficiency.
- License: MIT (platform code); CC-BY-NC-SA 4.0 (GRScenes data).
- Reproducibility: `partial`.

<details>
<summary>Expand Summary and Benchmark focus</summary>

**Summary**

GRUtopia is Shanghai AI Lab's city-scale digital world for general robots, with the GRScenes dataset and benchmarks covering social navigation, mobile manipulation, and long-horizon tasks.

**Benchmark focus**

- Scene scale and asset diversity beyond ReplicaCAD or HSSD.
- Multi-task evaluation including navigation, social interaction, and manipulation.
- Strong fit for VLA / generalist robot research.

</details>

#### 🔊 Audio-Visual Navigation

##### 🔊 SoundSpaces

![year-2020](https://img.shields.io/badge/year-2020-blue) ![repro-verified](https://img.shields.io/badge/repro-verified-brightgreen) ![sim-SoundSpaces](https://img.shields.io/badge/sim-SoundSpaces-informational) ![FM-medium](https://img.shields.io/badge/FM-medium-blue)

Chen et al. / Meta AI  
Benchmark, 2020. [Project](https://soundspaces.org/) | [Code](https://github.com/facebookresearch/sound-spaces) | [Paper](https://vision.cs.utexas.edu/projects/audio_visual_navigation/)

**Framework**

- Simulator: SoundSpaces / Habitat.
- Dataset: Acoustic simulation over 85 MP3D and 18 Replica scenes; SoundSpaces 2.0 adds continuous on-the-fly rendering.
- Action space: discrete, with continuous variants in SoundSpaces 2.0.
- Metrics: success, SPL, distance-to-goal.
- License: CC-BY-4.0 (audio data); MIT (code); MP3D and Replica research terms.
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

#### 🚁 Aerial / Outdoor Navigation

##### 🚁 AerialVLN

![year-2023](https://img.shields.io/badge/year-2023-blue) ![repro-partial](https://img.shields.io/badge/repro-partial-yellow) ![sim-AirVLN](https://img.shields.io/badge/sim-AirVLN-informational) ![FM-high](https://img.shields.io/badge/FM-high-orange)

AirVLN team  
Benchmark, 2023. [Project](https://github.com/AirVLN/AirVLN) | [Code](https://github.com/AirVLN/AirVLN) | [Paper](https://arxiv.org/abs/2308.06735)

**Framework**

- Simulator: AirVLN Simulator.
- Dataset: AerialVLN (25 city-scale environments with ~8k UAV navigation instructions).
- Action space: continuous UAV control.
- Metrics: success rate, SPL-like metrics, trajectory error.
- License: see project; upstream simulator assets follow their own terms.
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

##### 🚁 Aerial Vision-and-Dialog Navigation (AVDN)

![year-2023](https://img.shields.io/badge/year-2023-blue) ![repro-partial](https://img.shields.io/badge/repro-partial-yellow) ![sim-AVDN](https://img.shields.io/badge/sim-AVDN-informational) ![FM-high](https://img.shields.io/badge/FM-high-orange)

Eric AI Lab  
Benchmark, 2023. [Project](https://github.com/eric-ai-lab/Aerial-Vision-and-Dialog-Navigation) | [Code](https://github.com/eric-ai-lab/Aerial-Vision-and-Dialog-Navigation) | [Leaderboard](https://eval.ai/web/challenges/challenge-page/2049/overview) | [Paper](https://arxiv.org/abs/2205.12219)

**Framework**

- Simulator: AVDN Simulator.
- Dataset: AVDN (~3,000 dialog-driven sessions over xView aerial imagery with human-attention annotations).
- Action space: waypoint prediction.
- Metrics: waypoint error, navigation success.
- License: see project; xView access terms required.
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

##### 🚁 CityNav

![year-2024](https://img.shields.io/badge/year-2024-blue) ![repro-partial](https://img.shields.io/badge/repro-partial-yellow) ![sim-SensatUrban](https://img.shields.io/badge/sim-SensatUrban-informational) ![FM-high](https://img.shields.io/badge/FM-high-orange)

Lee et al.  
Benchmark, 2024. [Project](https://water-cookie.github.io/city-nav-proj/) | [Code](https://github.com/water-cookie/citynav) | [Paper](https://arxiv.org/abs/2406.14240)

**Framework**

- Simulator: CityNav (SensatUrban-based).
- Dataset: CityNav (32,637 natural-language descriptions and human trajectories over ~5.8k objects).
- Action space: continuous UAV and waypoint.
- Metrics: success rate, trajectory error, landmark-grounding accuracy.
- License: see project; SensatUrban research terms.
- Reproducibility: `partial`.

<details>
<summary>Expand Summary and Benchmark focus</summary>

**Summary**

CityNav grounds language-goal aerial navigation in real city 3D point clouds with geographic priors, providing a more realistic outdoor counterpart to AerialVLN.

**Benchmark focus**

- Outdoor language-goal aerial navigation.
- Real city 3D point clouds plus geographic context.
- Useful for testing aerial agents on real-world urban scale.

</details>

#### 🧪 Foundation-Model Navigation

##### 🧪 NavBench

![year-2025](https://img.shields.io/badge/year-2025-blue) ![repro-needs--review](https://img.shields.io/badge/repro-needs--review-orange) ![sim-Custom](https://img.shields.io/badge/sim-Custom-informational) ![FM-high](https://img.shields.io/badge/FM-high-orange)

NavBench team  
Benchmark, 2025. [Project](https://navbench.github.io/) | [Leaderboard](https://navbench.github.io/)

**Framework**

- Environment: benchmark-specific indoor navigation episodes.
- Dataset: NavBench (complexity-stratified comprehension and execution episodes; full size pending release).
- Action space: converted robot actions.
- Metrics: QA accuracy, execution success, complexity-stratified score.
- License: see project.
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

| Status | Badge | Meaning |
| --- | --- | --- |
| `verified` | ![repro-verified](https://img.shields.io/badge/repro-verified-brightgreen) | Public data, code, evaluation instructions, and at least one baseline are available. |
| `partial` | ![repro-partial](https://img.shields.io/badge/repro-partial-yellow) | Some parts are public, but reproduction needs manual setup, private data access, or missing scripts. |
| `archival` | ![repro-archival](https://img.shields.io/badge/repro-archival-lightgrey) | Useful historically, but code/data/leaderboard may be stale or read-only. |
| `needs-review` | ![repro-needs--review](https://img.shields.io/badge/repro-needs--review-orange) | Added as a candidate and still needs verification. |

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
- `dataset_size`
- `license`
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
- dataset size (episodes / scenes / instructions)
- license
- reproducibility status

See [CONTRIBUTING.md](CONTRIBUTING.md).

## License

MIT. Individual benchmark datasets and code repositories keep their own licenses and terms.
