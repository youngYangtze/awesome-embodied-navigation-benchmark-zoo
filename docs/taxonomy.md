# Task Taxonomy

[English](taxonomy.md) | [简体中文](taxonomy.zh-CN.md)

This taxonomy is designed for benchmark comparison. A benchmark may belong to multiple families.

## Point, Image, and Object Navigation

The agent receives a low-level goal, goal image, object instance, or object category and must navigate to a valid stopping location.

Key comparison axes:

- goal type: coordinate, image, object instance, object category, ordered object list
- observation: RGB, depth, semantic mask, GPS/compass, map
- action space: discrete, continuous velocity, waypoint
- metrics: Success, SPL, SoftSPL, distance-to-goal, collisions

## Vision-Language Navigation

The agent follows natural-language route instructions. The classic setup uses panoramic graph viewpoints, while newer variants use continuous 3D control.

Key comparison axes:

- language type: single instruction, multilingual instruction, dialog, referring expression
- environment: Matterport3D, Habitat, outdoor UAV scenes
- action space: graph-discrete, continuous, waypoint
- metrics: navigation error, success rate, SPL, nDTW, sDTW

## Embodied QA and Active Exploration

The agent explores or uses episodic memory to answer open-vocabulary questions about an environment.

Key comparison axes:

- setting: episodic memory, active exploration, hybrid
- answer type: closed-set, open-vocabulary
- evaluator: exact match, LLM judge, human agreement
- metrics: answer correctness, exploration efficiency, coverage

## Social and Human-Aware Navigation

The agent navigates in dynamic environments with humans or other agents. Evaluation should include social compliance, safety, and task success.

Key comparison axes:

- human model: scripted, data-driven, interactive, real human
- social signal: personal space, intent, groups, norms, verbal interaction
- metrics: success, collisions, intrusion, comfort, time-to-goal

## Audio-Visual Navigation

The agent uses audio and visual observations to localize or navigate to a sounding object.

Key comparison axes:

- audio type: binaural, ambisonic, reverberation, multi-source noise
- target: semantic source, sound source, speaker
- simulator: precomputed RIR, real-time acoustic rendering
- metrics: success, SPL, distance-to-goal, source localization

## Aerial and Outdoor Navigation

The agent, often a UAV, navigates in outdoor or urban environments using language, dialog, goals, or spatial reasoning.

Key comparison axes:

- platform: drone, ground robot, abstract agent
- environment scale: building, street, city, airspace
- goal type: instruction, dialog, coordinate, landmark, object
- metrics: route success, waypoint error, trajectory similarity, safety

## Foundation-Model Navigation

The benchmark is designed to evaluate MLLM, VLM, LLM, VLA, or navigation foundation models.

Key comparison axes:

- model role: planner, policy, world model, evaluator, memory
- supervision: zero-shot, few-shot, fine-tuned, RL fine-tuned
- embodiment: graph agent, mobile robot, drone, humanoid
- metrics: comprehension, execution, reasoning trace quality, task success
