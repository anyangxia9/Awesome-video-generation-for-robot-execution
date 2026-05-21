# Awesome Video Generation for Real-World Robot Execution [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

A curated paper list for **Video Generation for Real-World Robot Execution**, organized around the perspective of the **video-to-action interface**.

This repository collects representative papers discussed in the survey:

> **Video Generation for Real-World Robot Execution: A Survey**  
> Jiwen Yu, Quande Liu, Xintao Wang, Pengfei Wan, Di Zhang, Kun Gai, Hao Chen, Xihui Liu.

The list focuses on methods where generated videos, predicted visual futures, or video-native representations play an operational role in robotic execution, planning, action inference, or control.

---

## Table of Contents

- [Overview](#overview)
- [Survey Paper](#survey-paper)
- [Execution-Relevant Supervision](#execution-relevant-supervision)
  - [Supervision Expansion](#supervision-expansion)
  - [Supervision Alignment](#supervision-alignment)
  - [Standardized Large-Scale Resources](#standardized-large-scale-resources)
- [Robot-Centric Video Generation](#robot-centric-video-generation)
- [Video-to-Action Execution Interfaces](#video-to-action-execution-interfaces)
  - [Explicit Geometric Decoding](#explicit-geometric-decoding)
    - [3D Object Flow Interfaces](#3d-object-flow-interfaces)
    - [6D Pose Trajectory Interfaces](#6d-pose-trajectory-interfaces)
  - [Inverse Dynamics Models](#inverse-dynamics-models)
    - [Pixel-Space Future Conditioning](#pixel-space-future-conditioning)
    - [Latent-Space Future Conditioning](#latent-space-future-conditioning)
  - [Direct Action Heads](#direct-action-heads)
    - [Discrete Video-Token Interfaces](#discrete-video-token-interfaces)
    - [Continuous Latent Feature Interfaces](#continuous-latent-feature-interfaces)
    - [Adjacent Method](#adjacent-method)
  - [Unified Video-to-Action Generative Models](#unified-video-to-action-generative-models)
- [Evaluation Benchmarks](#evaluation-benchmarks)
  - [Video Generation Quality](#video-generation-quality)
  - [Physics Adherence and Instruction Following](#physics-adherence-and-instruction-following)
  - [Downstream Robot Execution](#downstream-robot-execution)
- [Deployment and Closed-Loop Control](#deployment-and-closed-loop-control)
- [Background and Related Foundations](#background-and-related-foundations)
  - [Visual Foresight and Video-Prediction-Based Planning](#visual-foresight-and-video-prediction-based-planning)
  - [Action-Readable Representation Learning](#action-readable-representation-learning)
- [Contributing](#contributing)
- [Citation](#citation)
- [License](#license)

---

## Overview

The central question of this repository is:

> How can generated visual futures be converted into executable robot actions?

Following the survey, papers are organized by the **interface exposed between video generation and robot control**.

| Category | Interface Variable | Action Recovery Mechanism | Representative Papers |
|---|---|---|---|
| Explicit Geometric Decoding | Flow, depth, 3D motion, 6D pose trajectory | Tracking, pose recovery, trajectory optimization | NovaFlow, Dream2Flow, RIGVid |
| Inverse Dynamics Models | Future visual states or future-conditioned representations | Future-conditioned inverse action inference | UniPi, ARDuP, RoboDreamer, CLOVER, Seer, VPP |
| Direct Action Heads | Video tokens or video-native latent features | Learned action decoder / action head | VPDD, VidMan, Genie Envisioner |
| Unified Video-to-Action Generative Models | Joint world-action latent variables | Actions generated as native rollout variables | Cosmos Policy, DreamZero |

---

## Survey Paper

- **Video Generation for Real-World Robot Execution: A Survey**  
  Jiwen Yu, Quande Liu, Xintao Wang, Pengfei Wan, Di Zhang, Kun Gai, Hao Chen, Xihui Liu.  
  A survey organized around the video-to-action interface, covering execution-relevant supervision, robot-centric video generation, video-to-action execution pathways, evaluation, deployment, and open research questions.

---

## Execution-Relevant Supervision

Execution-oriented video generation requires not only large-scale video data, but supervision that preserves task structure, embodiment compatibility, temporal evolution, and physically meaningful interaction outcomes.

### Supervision Expansion

- [MimicGen: A Data Generation System for Scalable Robot Learning using Human Demonstrations](https://arxiv.org/abs/2310.17596) (CoRL 2023)  
  [![Star](https://img.shields.io/github/stars/NVlabs/mimicgen.svg?style=social&label=Star)](https://github.com/NVlabs/mimicgen) [![arXiv](https://img.shields.io/badge/arXiv-b31b1b.svg)](https://arxiv.org/abs/2310.17596) [![Website](https://img.shields.io/badge/Website-9cf)](https://mimicgen.github.io/)  
  Programmatic demonstration expansion for scalable robot learning.

- [AHA: A Vision-Language-Model for Detecting and Reasoning over Failures in Robotic Manipulation](https://openreview.net/forum?id=JVkdSi7Ekg) (ICLR 2025)  
  [![Star](https://img.shields.io/github/stars/NVlabs/AHA.svg?style=social&label=Star)](https://github.com/NVlabs/AHA) [![Paper](https://img.shields.io/badge/Paper-4c72b0.svg)](https://openreview.net/forum?id=JVkdSi7Ekg) [![Website](https://img.shields.io/badge/Website-9cf)](https://aha-vlm.github.io/)  
  Failure-aware supervision expansion for robotic manipulation.

- [DRAW2ACT: Turning Depth-Encoded Trajectories into Robotic Demonstration Videos](https://arxiv.org/abs/2512.14217) (arXiv 2025)  
  [![arXiv](https://img.shields.io/badge/arXiv-b31b1b.svg)](https://arxiv.org/abs/2512.14217)  
  Depth-guided synthetic demonstration generation.

### Supervision Alignment

- [VITRA: Scalable Vision-Language-Action Model Pretraining for Robotic Manipulation with Real-Life Human Activity Videos](https://arxiv.org/abs/2510.21571) (arXiv 2025)  
  [![Star](https://img.shields.io/github/stars/microsoft/VITRA.svg?style=social&label=Star)](https://github.com/microsoft/VITRA) [![arXiv](https://img.shields.io/badge/arXiv-b31b1b.svg)](https://arxiv.org/abs/2510.21571) [![Website](https://img.shields.io/badge/Website-9cf)](https://microsoft.github.io/VITRA/)  
  Human-video-to-robot supervision alignment.

- [X-Humanoid: Robotize Human Videos to Generate Humanoid Videos at Scale](https://arxiv.org/abs/2512.04537) (arXiv 2025)  
  [![Star](https://img.shields.io/github/stars/showlab/X-Humanoid.svg?style=social&label=Star)](https://github.com/showlab/X-Humanoid) [![arXiv](https://img.shields.io/badge/arXiv-b31b1b.svg)](https://arxiv.org/abs/2512.04537) [![Website](https://img.shields.io/badge/Website-9cf)](https://showlab.github.io/X-Humanoid/)  
  Human-to-humanoid video alignment.

- [H2R: A Human-to-Robot Data Augmentation for Robot Pre-training from Videos](https://arxiv.org/abs/2505.11920) (arXiv 2025)  
  [![arXiv](https://img.shields.io/badge/arXiv-b31b1b.svg)](https://arxiv.org/abs/2505.11920) [![Website](https://img.shields.io/badge/Website-9cf)](https://sites.google.com/view/h2r-robotics)  
  Human-to-robot data augmentation from videos.

- [RoVi-Aug: Robot and Viewpoint Augmentation for Cross-Embodiment Robot Learning](https://proceedings.mlr.press/v270/chen25a.html) (CoRL 2024)  
  [![Star](https://img.shields.io/github/stars/BerkeleyAutomation/rovi-aug.svg?style=social&label=Star)](https://github.com/BerkeleyAutomation/rovi-aug) [![Paper](https://img.shields.io/badge/Paper-4c72b0.svg)](https://proceedings.mlr.press/v270/chen25a.html) [![Website](https://img.shields.io/badge/Website-9cf)](https://rovi-aug.github.io/)  
  Robot and viewpoint augmentation for cross-embodiment learning.

- [MimicDreamer: Aligning Human and Robot Demonstrations for Scalable VLA Training](https://arxiv.org/abs/2509.22199) (arXiv 2025)  
  [![arXiv](https://img.shields.io/badge/arXiv-b31b1b.svg)](https://arxiv.org/abs/2509.22199) [![Paper](https://img.shields.io/badge/Paper-4c72b0.svg)](https://openreview.net/forum?id=xCAum9gOkj)  
  Cross-view and cross-embodiment demonstration alignment.

### Standardized Large-Scale Resources

- [RBench / RoVid-X: Rethinking Video Generation Model for the Embodied World](https://arxiv.org/abs/2601.15282) (arXiv 2026)  
  [![Star](https://img.shields.io/github/stars/DAGroup-PKU/ReVidgen.svg?style=social&label=Star)](https://github.com/DAGroup-PKU/ReVidgen/) [![arXiv](https://img.shields.io/badge/arXiv-b31b1b.svg)](https://arxiv.org/abs/2601.15282) [![Website](https://img.shields.io/badge/Website-9cf)](https://dagroup-pku.github.io/ReVidgen.github.io/)  
  Large-scale robotics video resource and embodied video-generation benchmark.

---

## Robot-Centric Video Generation

Robot-centric video generation aims to produce visual futures that better reflect robot-object interaction, manipulation dynamics, and action-conditioned scene evolution.

- [RoboMaster: Learning Video Generation for Robotic Manipulation with Collaborative Trajectory Control](https://arxiv.org/abs/2506.01943) (ICLR 2026)  
  [![Star](https://img.shields.io/github/stars/KlingAIResearch/RoboMaster.svg?style=social&label=Star)](https://github.com/KlingAIResearch/RoboMaster) [![arXiv](https://img.shields.io/badge/arXiv-b31b1b.svg)](https://arxiv.org/abs/2506.01943) [![Website](https://img.shields.io/badge/Website-9cf)](https://fuxiao0719.github.io/projects/robomaster/)  
  Generates robot-centric manipulation videos with collaborative trajectory control.

- [IRASim: A Fine-Grained World Model for Robot Manipulation](https://arxiv.org/abs/2406.14540) (ICCV 2025)  
  [![Star](https://img.shields.io/github/stars/bytedance/IRASim.svg?style=social&label=Star)](https://github.com/bytedance/IRASim) [![arXiv](https://img.shields.io/badge/arXiv-b31b1b.svg)](https://arxiv.org/abs/2406.14540) [![Website](https://img.shields.io/badge/Website-9cf)](https://gen-irasim.github.io/)  
  Generates robot-object interaction videos with fine-grained action-frame correspondence.

---

## Video-to-Action Execution Interfaces

This section is the core of the repository. Papers are organized by how generated futures or video-native representations are converted into executable robot actions.

---

### Explicit Geometric Decoding

This pathway converts generated video into explicit geometric or motion variables, such as 3D flow, depth, or 6D pose trajectories, before recovering robot actions.

#### 3D Object Flow Interfaces

- [NovaFlow: Zero-Shot Manipulation via Actionable Flow from Generated Videos](https://arxiv.org/abs/2510.08568) (ICRA 2026)  
  [![Star](https://img.shields.io/github/stars/bdaiinstitute/NovaFlow.svg?style=social&label=Star)](https://github.com/bdaiinstitute/NovaFlow) [![arXiv](https://img.shields.io/badge/arXiv-b31b1b.svg)](https://arxiv.org/abs/2510.08568) [![Website](https://img.shields.io/badge/Website-9cf)](https://novaflow.lhy.xyz/)  
  Recovers actionable 3D object flow from generated videos for zero-shot manipulation.

- [Dream2Flow: Bridging Video Generation and Open-World Manipulation with 3D Object Flow](https://arxiv.org/abs/2512.24766) (arXiv 2025)  
  [![Star](https://img.shields.io/github/stars/KDharmarajanDev/Dream2Flow.svg?style=social&label=Star)](https://github.com/KDharmarajanDev/Dream2Flow/) [![arXiv](https://img.shields.io/badge/arXiv-b31b1b.svg)](https://arxiv.org/abs/2512.24766) [![Website](https://img.shields.io/badge/Website-9cf)](https://dream2flow.github.io/)  
  Bridges generated visual futures and robot execution through 3D object flow.

#### 6D Pose Trajectory Interfaces

- [RIGVid: Robotic Manipulation by Imitating Generated Videos without Physical Demonstrations](https://arxiv.org/abs/2507.00990) (arXiv 2025)  
  [![Star](https://img.shields.io/github/stars/shivanshpatel35/rigvid.svg?style=social&label=Star)](https://github.com/shivanshpatel35/rigvid) [![arXiv](https://img.shields.io/badge/arXiv-b31b1b.svg)](https://arxiv.org/abs/2507.00990) [![Website](https://img.shields.io/badge/Website-9cf)](https://rigvid-robot.github.io/)  
  Extracts 6D object pose trajectories from generated videos and retargets them to robot actions.

- [Geometry-aware 4D Video Generation for Robot Manipulation](https://arxiv.org/abs/2507.01099) (ICLR 2026)  
  [![arXiv](https://img.shields.io/badge/arXiv-b31b1b.svg)](https://arxiv.org/abs/2507.01099) [![Paper](https://img.shields.io/badge/Paper-4c72b0.svg)](https://openreview.net/forum?id=18gC6pZVVc) [![Website](https://img.shields.io/badge/Website-9cf)](https://robotgen4d.github.io/)  
  Generates geometry-aware 4D-consistent videos and recovers 6DoF trajectories for robot manipulation.

---

### Inverse Dynamics Models

This pathway treats generated futures as conditions for action inference. The generated future is not directly the action, but an imagined future from which actions are recovered by an inverse dynamics model or a closely related future-conditioned control module.

#### Pixel-Space Future Conditioning

- [UniPi: Learning Universal Policies via Text-Guided Video Generation](https://arxiv.org/abs/2302.00111) (NeurIPS 2023)  
  [![arXiv](https://img.shields.io/badge/arXiv-b31b1b.svg)](https://arxiv.org/abs/2302.00111) [![Website](https://img.shields.io/badge/Website-9cf)](https://universal-policy.github.io/)  
  Generates future observations and maps them to actions through a task-specific inverse dynamics model.

- [ARDuP: Active Region Video Diffusion for Universal Policies](https://arxiv.org/abs/2406.13301) (IROS 2024)  
  [![arXiv](https://img.shields.io/badge/arXiv-b31b1b.svg)](https://arxiv.org/abs/2406.13301)  
  Improves future-conditioned action inference by focusing generation on manipulation-relevant active regions.

- [RoboDreamer: Learning Compositional World Models for Robot Imagination](https://arxiv.org/abs/2404.12377) (ICML 2024)  
  [![Star](https://img.shields.io/github/stars/rainbow979/robodreamer.svg?style=social&label=Star)](https://github.com/rainbow979/robodreamer) [![arXiv](https://img.shields.io/badge/arXiv-b31b1b.svg)](https://arxiv.org/abs/2404.12377) [![Website](https://img.shields.io/badge/Website-9cf)](https://robovideo.github.io/)  
  Uses compositional imagination and inverse dynamics to infer actions from generated future frames.

- [CLOVER: Closed-Loop Visuomotor Control with Generative Expectation for Robotic Manipulation](https://arxiv.org/abs/2409.09016) (NeurIPS 2024)  
  [![Star](https://img.shields.io/github/stars/OpenDriveLab/CLOVER.svg?style=social&label=Star)](https://github.com/OpenDriveLab/CLOVER) [![arXiv](https://img.shields.io/badge/arXiv-b31b1b.svg)](https://arxiv.org/abs/2409.09016) [![Paper](https://img.shields.io/badge/Paper-4c72b0.svg)](https://proceedings.neurips.cc/paper_files/paper/2024/hash/fad8962279154544ed69bb63eb14d677-Abstract-Conference.html)  
  Uses generated visual subgoals with feedback and replanning for closed-loop manipulation.

#### Latent-Space Future Conditioning

- [Seer: Predictive Inverse Dynamics Models are Scalable Learners for Robotic Manipulation](https://arxiv.org/abs/2412.15109) (ICLR 2025)  
  [![Star](https://img.shields.io/github/stars/InternRobotics/Seer.svg?style=social&label=Star)](https://github.com/InternRobotics/Seer) [![arXiv](https://img.shields.io/badge/arXiv-b31b1b.svg)](https://arxiv.org/abs/2412.15109) [![Website](https://img.shields.io/badge/Website-9cf)](https://nimolty.github.io/Seer/)  
  Predicts actions from forecast visual states using predictive inverse dynamics.

- [Video Prediction Policy: A Generalist Robot Policy with Predictive Visual Representations](https://arxiv.org/abs/2412.14803) (ICML 2025)  
  [![Star](https://img.shields.io/github/stars/roboterax/video-prediction-policy.svg?style=social&label=Star)](https://github.com/roboterax/video-prediction-policy) [![arXiv](https://img.shields.io/badge/arXiv-b31b1b.svg)](https://arxiv.org/abs/2412.14803) [![Website](https://img.shields.io/badge/Website-9cf)](https://video-prediction-policy.github.io/)  
  Conditions action inference on predictive visual representations extracted from video prediction models.

---

### Direct Action Heads

This pathway decodes actions directly from video-native representations, without explicit geometric recovery or a separate future-to-action inverse dynamics stage.

#### Discrete Video-Token Interfaces

- [VPDD: Learning an Actionable Discrete Diffusion Policy via Large-Scale Actionless Video Pre-Training](https://arxiv.org/abs/2402.14407) (NeurIPS 2024)  
  [![Star](https://img.shields.io/github/stars/tinnerhrhe/VPDD.svg?style=social&label=Star)](https://github.com/tinnerhrhe/VPDD) [![arXiv](https://img.shields.io/badge/arXiv-b31b1b.svg)](https://arxiv.org/abs/2402.14407) [![Website](https://img.shields.io/badge/Website-9cf)](https://video-diff.github.io/)  
  Learns actionable discrete video-token dynamics from large-scale actionless video pretraining.

#### Continuous Latent Feature Interfaces

- [VidMan: Exploiting Implicit Dynamics from Video Diffusion Model for Effective Robot Manipulation](https://arxiv.org/abs/2411.09153) (NeurIPS 2024)  
  [![Star](https://img.shields.io/github/stars/jirufengyu/VidMan.svg?style=social&label=Star)](https://github.com/jirufengyu/VidMan) [![arXiv](https://img.shields.io/badge/arXiv-b31b1b.svg)](https://arxiv.org/abs/2411.09153) [![Website](https://img.shields.io/badge/Website-9cf)](https://jirufengyu.github.io/VidMan/)  
  Uses latent features of a pretrained video diffusion transformer and decodes low-level actions through an action-prediction adapter.

- [Genie Envisioner: A Unified World Foundation Platform for Robotic Manipulation](https://arxiv.org/abs/2508.05635) (ICLR 2026)  
  [![Star](https://img.shields.io/github/stars/AgibotTech/Genie-Envisioner.svg?style=social&label=Star)](https://github.com/AgibotTech/Genie-Envisioner) [![arXiv](https://img.shields.io/badge/arXiv-b31b1b.svg)](https://arxiv.org/abs/2508.05635) [![Website](https://img.shields.io/badge/Website-9cf)](https://genie-envisioner.github.io/)  
  Uses structured video latent representations and a lightweight action decoder for robotic manipulation.

- [Video Generators are Robot Policies](https://arxiv.org/abs/2508.00795) (arXiv 2025)  
  [![arXiv](https://img.shields.io/badge/arXiv-b31b1b.svg)](https://arxiv.org/abs/2508.00795) [![Website](https://img.shields.io/badge/Website-9cf)](https://videopolicy.cs.columbia.edu/)  
  Conditions action generation on intermediate video-network features, treating video generators as policy backbones.

#### Adjacent Method

- **This&That: Video-to-Action Behavioral Cloning**  
  Mentioned as a planning- or behavior-cloning-adjacent method in the survey figure.  
  Note: it is kept separate from the core direct-action-head group to avoid conflating adjacent behavior-cloning formulations with the main interface form.

---

### Unified Video-to-Action Generative Models

This pathway treats action as a native variable inside the generative rollout itself. Instead of first generating a future and then recovering action through an external module, future states and actions are generated within a shared world-action representation.

- [Cosmos Policy: Fine-Tuning Video Models for Visuomotor Control and Planning](https://arxiv.org/abs/2601.16163) (ICLR 2026)  
  [![Star](https://img.shields.io/github/stars/nvlabs/cosmos-policy.svg?style=social&label=Star)](https://github.com/nvlabs/cosmos-policy) [![arXiv](https://img.shields.io/badge/arXiv-b31b1b.svg)](https://arxiv.org/abs/2601.16163) [![Website](https://img.shields.io/badge/Website-9cf)](https://research.nvidia.com/labs/dir/cosmos-policy/)  
  Integrates future states, actions, and decision-relevant variables into a unified latent-frame interface.

- [DreamZero: World Action Models are Zero-Shot Policies](https://arxiv.org/abs/2602.15922) (ICLR Workshop 2026)  
  [![Star](https://img.shields.io/github/stars/dreamzero0/dreamzero.svg?style=social&label=Star)](https://github.com/dreamzero0/dreamzero) [![arXiv](https://img.shields.io/badge/arXiv-b31b1b.svg)](https://arxiv.org/abs/2602.15922) [![Website](https://img.shields.io/badge/Website-9cf)](https://dreamzero0.github.io/)  
  Jointly predicts future world states and actions using a large world-action model.

---

## Evaluation Benchmarks

Evaluation for video generation in robotic execution should go beyond visual fidelity. The survey organizes benchmarks into three layers: visual reliability, task-conditioned validity, and downstream embodied utility.

---

### Video Generation Quality

- [VBench: Comprehensive Benchmark Suite for Video Generative Models](https://arxiv.org/abs/2311.17982) (CVPR 2024)  
  [![Star](https://img.shields.io/github/stars/Vchitect/VBench.svg?style=social&label=Star)](https://github.com/Vchitect/VBench) [![arXiv](https://img.shields.io/badge/arXiv-b31b1b.svg)](https://arxiv.org/abs/2311.17982) [![Website](https://img.shields.io/badge/Website-9cf)](https://vchitect.github.io/VBench-project/)  
  Evaluates video generation quality across structured dimensions such as subject consistency, temporal coherence, motion smoothness, and spatial relationships.

- [BrokenVideos: A Benchmark Dataset for Fine-Grained Artifact Localization in AI-Generated Videos](https://arxiv.org/abs/2506.20103) (ACM MM 2025)  
  [![arXiv](https://img.shields.io/badge/arXiv-b31b1b.svg)](https://arxiv.org/abs/2506.20103)  
  Provides fine-grained artifact localization for diagnosing failures in generated videos.

---

### Physics Adherence and Instruction Following

- [WorldModelBench: Judging Video Generation Models as World Models](https://arxiv.org/abs/2502.20694) (NeurIPS Datasets and Benchmarks 2025)  
  [![Star](https://img.shields.io/github/stars/WorldModelBench-Team/WorldModelBench.svg?style=social&label=Star)](https://github.com/WorldModelBench-Team/WorldModelBench) [![arXiv](https://img.shields.io/badge/arXiv-b31b1b.svg)](https://arxiv.org/abs/2502.20694) [![Paper](https://img.shields.io/badge/Paper-4c72b0.svg)](https://openreview.net/forum?id=a3hafrDzuA)  
  Evaluates generated videos as world models, focusing on world-model reasoning, instruction following, and physics adherence.

- [RBench: Rethinking Video Generation Model for the Embodied World](https://arxiv.org/abs/2601.15282) (arXiv 2026)  
  [![Star](https://img.shields.io/github/stars/DAGroup-PKU/ReVidgen.svg?style=social&label=Star)](https://github.com/DAGroup-PKU/ReVidgen/) [![arXiv](https://img.shields.io/badge/arXiv-b31b1b.svg)](https://arxiv.org/abs/2601.15282) [![Website](https://img.shields.io/badge/Website-9cf)](https://dagroup-pku.github.io/ReVidgen.github.io/)  
  Evaluates embodied video generation with emphasis on structural consistency, physical plausibility, and action completeness.

---

### Downstream Robot Execution

- [LIBERO: Benchmarking Knowledge Transfer for Lifelong Robot Learning](https://proceedings.neurips.cc/paper_files/paper/2023/hash/8c3c666820ea055a77726d66fc7d447f-Abstract-Datasets_and_Benchmarks.html) (NeurIPS Datasets and Benchmarks 2023)  
  [![Paper](https://img.shields.io/badge/Paper-4c72b0.svg)](https://proceedings.neurips.cc/paper_files/paper/2023/hash/8c3c666820ea055a77726d66fc7d447f-Abstract-Datasets_and_Benchmarks.html) [![Website](https://img.shields.io/badge/Website-9cf)](https://libero-project.github.io/main.html)  
  Language-conditioned manipulation benchmark for evaluating transfer across structured task variations.

- [ManiSkill: Generalizable Manipulation Skill Benchmark with Large-Scale Demonstrations](https://arxiv.org/abs/2107.14483) (NeurIPS Datasets and Benchmarks 2021)  
  [![Star](https://img.shields.io/github/stars/haosulab/ManiSkill.svg?style=social&label=Star)](https://github.com/haosulab/ManiSkill) [![arXiv](https://img.shields.io/badge/arXiv-b31b1b.svg)](https://arxiv.org/abs/2107.14483) [![Website](https://img.shields.io/badge/Website-9cf)](https://www.maniskill.ai/)  
  A manipulation benchmark with large-scale demonstrations.

- [ManiSkill2: A Unified Benchmark for Generalizable Manipulation Skills](https://openreview.net/forum?id=b_CQDy9vrD1) (ICLR 2023)  
  [![Star](https://img.shields.io/github/stars/haosulab/ManiSkill2-task-dev.svg?style=social&label=Star)](https://github.com/haosulab/ManiSkill2-task-dev) [![Paper](https://img.shields.io/badge/Paper-4c72b0.svg)](https://openreview.net/forum?id=b_CQDy9vrD1) [![Website](https://img.shields.io/badge/Website-9cf)](https://maniskill2.github.io/)  
  A unified benchmark for generalizable manipulation skills.

- [RLBench: The Robot Learning Benchmark & Learning Environment](https://arxiv.org/abs/1909.12271) (RA-L 2020)  
  [![Star](https://img.shields.io/github/stars/stepjam/RLBench.svg?style=social&label=Star)](https://github.com/stepjam/RLBench) [![arXiv](https://img.shields.io/badge/arXiv-b31b1b.svg)](https://arxiv.org/abs/1909.12271) [![Website](https://img.shields.io/badge/Website-9cf)](https://sites.google.com/view/rlbench)  
  A multi-task robot learning benchmark and learning environment.

---

## Deployment and Closed-Loop Control

Deployment-oriented methods emphasize timing, uncertainty handling, closed-loop feedback, and recovery under execution failure.

- [CLOVER: Closed-Loop Visuomotor Control with Generative Expectation for Robotic Manipulation](https://arxiv.org/abs/2409.09016) (NeurIPS 2024)  
  [![Star](https://img.shields.io/github/stars/OpenDriveLab/CLOVER.svg?style=social&label=Star)](https://github.com/OpenDriveLab/CLOVER) [![arXiv](https://img.shields.io/badge/arXiv-b31b1b.svg)](https://arxiv.org/abs/2409.09016) [![Paper](https://img.shields.io/badge/Paper-4c72b0.svg)](https://proceedings.neurips.cc/paper_files/paper/2024/hash/fad8962279154544ed69bb63eb14d677-Abstract-Conference.html)  
  Uses generated expectations for closed-loop visuomotor control.

- [DreamZero: World Action Models are Zero-Shot Policies](https://arxiv.org/abs/2602.15922) (ICLR Workshop 2026)  
  [![Star](https://img.shields.io/github/stars/dreamzero0/dreamzero.svg?style=social&label=Star)](https://github.com/dreamzero0/dreamzero) [![arXiv](https://img.shields.io/badge/arXiv-b31b1b.svg)](https://arxiv.org/abs/2602.15922) [![Website](https://img.shields.io/badge/Website-9cf)](https://dreamzero0.github.io/)  
  Demonstrates world-action rollout generation for zero-shot policy execution.

- [VidArc: Embodied Video Diffusion Model for Closed-Loop Control](https://arxiv.org/abs/2512.17661) (arXiv 2025)  
  [![Star](https://img.shields.io/github/stars/thu-ml/vidar.svg?style=social&label=Star)](https://github.com/thu-ml/vidar) [![arXiv](https://img.shields.io/badge/arXiv-b31b1b.svg)](https://arxiv.org/abs/2512.17661)  
  An embodied video diffusion model designed for closed-loop control.

---

## Background and Related Foundations

This section includes background works explicitly referenced in the survey to clarify the lineage of video prediction, visual foresight, and action-readable representation learning.

---

### Visual Foresight and Video-Prediction-Based Planning

- [Deep Visual Foresight for Planning Robot Motion](https://ieeexplore.ieee.org/document/7989324) (ICRA 2017)  
  [![Paper](https://img.shields.io/badge/Paper-4c72b0.svg)](https://ieeexplore.ieee.org/document/7989324)  
  Early visual foresight framework for planning robot motion using predicted visual futures.

- [Unsupervised Learning for Physical Interaction through Video Prediction](https://proceedings.neurips.cc/paper/2016/hash/d9d4f495e875a2e075a1a4a6e1b9770f-Abstract.html) (NeurIPS 2016)  
  [![Paper](https://img.shields.io/badge/Paper-4c72b0.svg)](https://proceedings.neurips.cc/paper/2016/hash/d9d4f495e875a2e075a1a4a6e1b9770f-Abstract.html)  
  Learns physical interaction dynamics through video prediction.

- [Visual Foresight: Model-Based Deep Reinforcement Learning for Vision-Based Robotic Control](http://arxiv.org/abs/1812.00568) (arXiv 2018)  
  [![arXiv](https://img.shields.io/badge/arXiv-b31b1b.svg)](http://arxiv.org/abs/1812.00568)  
  Uses predictive visual models for model-based robotic control.

- [Robot Motion Planning as Video Prediction: A Spatio-Temporal Neural Network-Based Motion Planner](https://doi.org/10.1109/IROS47612.2022.9981769) (IROS 2022)  
  [![Paper](https://img.shields.io/badge/Paper-4c72b0.svg)](https://doi.org/10.1109/IROS47612.2022.9981769)  
  Frames robot motion planning as a video prediction problem.

---

### Action-Readable Representation Learning

- [Time-Contrastive Networks: Self-Supervised Learning from Video](https://doi.org/10.1109/ICRA.2018.8462891) (ICRA 2018)  
  [![Paper](https://img.shields.io/badge/Paper-4c72b0.svg)](https://doi.org/10.1109/ICRA.2018.8462891)  
  Learns temporally aligned representations from video.

- [Particle Video Revisited: Tracking through Occlusions using Point Trajectories](https://doi.org/10.1007/978-3-031-20047-2_4) (ECCV 2022)  
  [![Paper](https://img.shields.io/badge/Paper-4c72b0.svg)](https://doi.org/10.1007/978-3-031-20047-2_4)  
  Tracks point trajectories through occlusions, relevant to motion-sensitive and action-readable video representations.

---

## Contributing

Contributions are welcome.

To keep the list rigorous and aligned with the survey scope, please follow these rules:

1. Add only papers that are directly related to video generation, visual future prediction, video-native representation learning, or generated-video-based robot execution.
2. Prefer papers with clear connections to one of the following categories:
   - execution-relevant supervision,
   - robot-centric video generation,
   - explicit geometric decoding,
   - inverse dynamics models,
   - direct action heads,
   - unified video-to-action generative models,
   - evaluation benchmarks,
   - deployment or closed-loop control.
3. Do not add unrelated general-purpose video generation papers unless they are explicitly used for robotic execution or action grounding.
4. Please provide an official paper link, such as arXiv, OpenReview, PMLR, CVF, NeurIPS, IEEE, or DOI.
5. Avoid duplicate entries. If a paper fits multiple categories, place it under the most central category and mention the connection in the description.

Recommended format:

```markdown
- [Paper Title](paper_link) (Venue Year)  
  [![Star](https://img.shields.io/github/stars/OWNER/REPO.svg?style=social&label=Star)](github_link) [![arXiv](https://img.shields.io/badge/arXiv-b31b1b.svg)](arxiv_link) [![Website](https://img.shields.io/badge/Website-9cf)](website_link)  
  One-sentence description of why the paper is relevant to video generation for robot execution.
```

---

## Citation

If you find this repository useful, please consider citing the survey:

```bibtex
@article{yu2026video_generation_robot_execution_survey,
  title   = {Video Generation for Real-World Robot Execution: A Survey},
  author  = {Yu, Jiwen and Liu, Quande and Wang, Xintao and Wan, Pengfei and Zhang, Di and Gai, Kun and Chen, Hao and Liu, Xihui},
  journal = {arXiv preprint},
  year    = {2026}
}
```

---

## License

This repository is released for academic and non-commercial research use. Please refer to the original papers and project pages for their respective licenses.
