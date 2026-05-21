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
  - [Inverse Dynamics Models](#inverse-dynamics-models)
  - [Direct Action Heads](#direct-action-heads)
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

---

## Execution-Relevant Supervision

Execution-oriented video generation requires not only large-scale video data, but supervision that preserves task structure, embodiment compatibility, temporal evolution, and physically meaningful interaction outcomes.

### Supervision Expansion

- [MimicGen: A Data Generation System for Scalable Robot Learning using Human Demonstrations](https://proceedings.mlr.press/v229/mandlekar23a.html) (CoRL 2023)  
  Programmatic demonstration expansion for scalable robot learning.

- [AHA: A Vision-Language-Model for Detecting and Reasoning over Failures in Robotic Manipulation](https://openreview.net/forum?id=JVkdSi7Ekg) (ICLR 2025)  
  Failure-aware supervision expansion for robotic manipulation.

- [DRAW2ACT: Turning Depth-Encoded Trajectories into Robotic Demonstration Videos](https://arxiv.org/abs/2512.14217) (arXiv 2025)  
  Depth-guided synthetic demonstration generation.

### Supervision Alignment

- [Scalable Vision-Language-Action Model Pretraining for Robotic Manipulation with Real-Life Human Activity Videos](https://arxiv.org/abs/2510.21571) (arXiv 2025)  
  Human-video-to-robot supervision alignment.

- [X-Humanoid: Robotize Human Videos to Generate Humanoid Videos at Scale](https://arxiv.org/abs/2512.04537) (arXiv 2025)  
  Human-to-humanoid video alignment.

- [H2R: A Human-to-Robot Data Augmentation for Robot Pre-training from Videos](https://openreview.net/forum?id=meY9nInitM) (CVPR Workshop 2025)  
  Human-to-robot data augmentation from videos.

- [RoVi-Aug: Robot and Viewpoint Augmentation for Cross-Embodiment Robot Learning](https://proceedings.mlr.press/v270/chen25a.html) (CoRL 2024)  
  Robot and viewpoint augmentation for cross-embodiment learning.

- [MimicDreamer: Aligning Human and Robot Demonstrations for Scalable VLA Training](https://arxiv.org/abs/2509.22199) (arXiv 2025)  
  Cross-view and cross-embodiment demonstration alignment.

### Standardized Large-Scale Resources

- [RBench / RoVid-X: Rethinking Video Generation Model for the Embodied World](https://openreview.net/forum?id=LH2Fixs2so) (ICLR Workshop 2026)  
  Large-scale robotics video resource and embodied video-generation benchmark.

---

## Robot-Centric Video Generation

Robot-centric video generation aims to produce visual futures that better reflect robot-object interaction, manipulation dynamics, and action-conditioned scene evolution.

- [Learning Video Generation for Robotic Manipulation with Collaborative Trajectory Control](https://openreview.net/forum?id=OeDwYtp8n1) (ICLR 2026)  
  Also referred to as **RoboMaster**. Generates robot-centric manipulation videos with collaborative trajectory control.

- [IRASim: A Fine-Grained World Model for Robot Manipulation](https://openaccess.thecvf.com/content/ICCV2025/html/Zhu_IRASim_A_Fine-Grained_World_Model_for_Robot_Manipulation_ICCV_2025_paper.html) (ICCV 2025)  
  Generates robot-object interaction videos with fine-grained action-frame correspondence.

---

## Video-to-Action Execution Interfaces

This section is the core of the repository. Papers are organized by how generated futures or video-native representations are converted into executable robot actions.

---

### Explicit Geometric Decoding

This pathway converts generated video into explicit geometric or motion variables, such as 3D flow, depth, or 6D pose trajectories, before recovering robot actions.

#### 3D Object Flow Interfaces

- [NovaFlow: Zero-Shot Manipulation via Actionable Flow from Generated Videos](https://arxiv.org/abs/2510.08568) (arXiv 2025)  
  Recovers actionable 3D object flow from generated videos for zero-shot manipulation.

- [Dream2Flow: Bridging Video Generation and Open-World Manipulation with 3D Object Flow](https://arxiv.org/abs/2512.24766) (arXiv 2025)  
  Bridges generated visual futures and robot execution through 3D object flow.

#### 6D Pose Trajectory Interfaces

- [Robotic Manipulation by Imitating Generated Videos without Physical Demonstrations](https://openreview.net/forum?id=zjjVQDUgZr) (CVPR Workshop 2025)  
  Also referred to as **RIGVid**. Extracts 6D object pose trajectories from generated videos and retargets them to robot actions.

- [Geometry-aware 4D Video Generation for Robot Manipulation](https://openreview.net/forum?id=18gC6pZVVc) (ICLR 2026)  
  Generates geometry-aware 4D-consistent videos and recovers 6DoF trajectories for robot manipulation.

---

### Inverse Dynamics Models

This pathway treats generated futures as conditions for action inference. The generated future is not directly the action, but an imagined future from which actions are recovered by an inverse dynamics model or a closely related future-conditioned control module.

#### Pixel-Space Future Conditioning

- [Learning Universal Policies via Text-Guided Video Generation](https://proceedings.neurips.cc/paper_files/paper/2023/hash/1d5b9233ad716a43be5c0d3023cb82d0-Abstract-Conference.html) (NeurIPS 2023)  
  Also referred to as **UniPi**. Generates future observations and maps them to actions through a task-specific inverse dynamics model.

- [ARDuP: Active Region Video Diffusion for Universal Policies](https://arxiv.org/abs/2406.13301) (IROS 2024)  
  Improves future-conditioned action inference by focusing generation on manipulation-relevant active regions.

- [RoboDreamer: Learning Compositional World Models for Robot Imagination](https://proceedings.mlr.press/v235/zhou24x.html) (ICML 2024)  
  Uses compositional imagination and inverse dynamics to infer actions from generated future frames.

- [Closed-loop Visuomotor Control with Generative Expectation for Robotic Manipulation](https://proceedings.neurips.cc/paper_files/paper/2024/hash/fad8962279154544ed69bb63eb14d677-Abstract-Conference.html) (NeurIPS 2024)  
  Also referred to as **CLOVER**. Uses generated visual subgoals with feedback and replanning for closed-loop manipulation.

#### Latent-Space Future Conditioning

- [Predictive Inverse Dynamics Models are Scalable Learners for Robotic Manipulation](https://openreview.net/forum?id=meRCKuUpmc) (ICLR 2025)  
  Also referred to as **Seer / PIDM**. Predicts actions from forecast visual states using predictive inverse dynamics.

- [Video Prediction Policy: A Generalist Robot Policy with Predictive Visual Representations](https://proceedings.mlr.press/v267/hu25g.html) (ICML 2025)  
  Also referred to as **VPP**. Conditions action inference on predictive visual representations extracted from video prediction models.

---

### Direct Action Heads

This pathway decodes actions directly from video-native representations, without explicit geometric recovery or a separate future-to-action inverse dynamics stage.

#### Discrete Video-Token Interfaces

- [Learning an Actionable Discrete Diffusion Policy via Large-Scale Actionless Video Pre-Training](https://proceedings.neurips.cc/paper_files/paper/2024/hash/378226e5df7eded3e401de5c9493143c-Abstract-Conference.html) (NeurIPS 2024)  
  Also referred to as **VPDD**. Learns actionable discrete video-token dynamics from large-scale actionless video pretraining.

#### Continuous Latent Feature Interfaces

- [VidMan: Exploiting Implicit Dynamics from Video Diffusion Model for Effective Robot Manipulation](https://proceedings.neurips.cc/paper_files/paper/2024/hash/481c70828a4ff20d31a646cc6cc95f3d-Abstract-Conference.html) (NeurIPS 2024)  
  Uses latent features of a pretrained video diffusion transformer and decodes low-level actions through an action-prediction adapter.

- [Genie Envisioner: A Unified World Foundation Platform for Robotic Manipulation](https://openreview.net/forum?id=fHLtSxDFKC) (ICLR 2026)  
  Uses structured video latent representations and a lightweight action decoder for robotic manipulation.

- [Video Generators are Robot Policies](https://arxiv.org/abs/2508.00795) (arXiv 2025)  
  Conditions action generation on intermediate video-network features, treating video generators as policy backbones.

#### Adjacent Method

- **This&That: Video-to-Action Behavioral Cloning**  
  Mentioned as a planning- or behavior-cloning-adjacent method in the survey figure.  
  Note: it is kept separate from the core direct-action-head group to avoid conflating adjacent behavior-cloning formulations with the main interface form.

---

### Unified Video-to-Action Generative Models

This pathway treats action as a native variable inside the generative rollout itself. Instead of first generating a future and then recovering action through an external module, future states and actions are generated within a shared world-action representation.

- [Cosmos Policy: Fine-tuning Video Models for Visuomotor Control and Planning](https://openreview.net/forum?id=wPEIStHxYH) (ICLR 2026)  
  Integrates future states, actions, and decision-relevant variables into a unified latent-frame interface.

- [World Action Models are Zero-Shot Policies](https://openreview.net/forum?id=cd33uUB609) (ICLR Workshop 2026)  
  Also referred to as **DreamZero**. Jointly predicts future world states and actions using a large world-action model.

---

## Evaluation Benchmarks

Evaluation for video generation in robotic execution should go beyond visual fidelity. The survey organizes benchmarks into three layers: visual reliability, task-conditioned validity, and downstream embodied utility.

---

### Video Generation Quality

- [VBench: Comprehensive Benchmark Suite for Video Generative Models](https://doi.org/10.1109/CVPR52733.2024.02060) (CVPR 2024)  
  Evaluates video generation quality across structured dimensions such as subject consistency, temporal coherence, motion smoothness, and spatial relationships.

- [BrokenVideos: A Benchmark Dataset for Fine-Grained Artifact Localization in AI-Generated Videos](https://arxiv.org/abs/2506.20103) (ACM MM 2025)  
  Provides fine-grained artifact localization for diagnosing failures in generated videos.

---

### Physics Adherence and Instruction Following

- [WorldModelBench: Judging Video Generation Models as World Models](https://openreview.net/forum?id=a3hafrDzuA) (NeurIPS Datasets and Benchmarks 2025)  
  Evaluates generated videos as world models, focusing on world-model reasoning, instruction following, and physics adherence.

- [Rethinking Video Generation Model for the Embodied World](https://openreview.net/forum?id=LH2Fixs2so) (ICLR Workshop 2026)  
  Also referred to as **RBench**. Evaluates embodied video generation with emphasis on structural consistency, physical plausibility, and action completeness.

---

### Downstream Robot Execution

- [LIBERO: Benchmarking Knowledge Transfer for Lifelong Robot Learning](https://proceedings.neurips.cc/paper_files/paper/2023/hash/8c3c666820ea055a77726d66fc7d447f-Abstract-Datasets_and_Benchmarks.html) (NeurIPS Datasets and Benchmarks 2023)  
  Language-conditioned manipulation benchmark for evaluating transfer across structured task variations.

- [ManiSkill: Generalizable Manipulation Skill Benchmark with Large-Scale Demonstrations](https://openreview.net/forum?id=zQIvkXHS_U5) (NeurIPS Datasets and Benchmarks 2021)  
  A manipulation benchmark with large-scale demonstrations.

- [ManiSkill2: A Unified Benchmark for Generalizable Manipulation Skills](https://openreview.net/forum?id=b_CQDy9vrD1) (ICLR 2023)  
  A unified benchmark for generalizable manipulation skills.

- [RLBench: The Robot Learning Benchmark & Learning Environment](https://doi.org/10.1109/LRA.2020.2974707) (RA-L 2020)  
  A multi-task robot learning benchmark and learning environment.

---

## Deployment and Closed-Loop Control

Deployment-oriented methods emphasize timing, uncertainty handling, closed-loop feedback, and recovery under execution failure.

- [Closed-loop Visuomotor Control with Generative Expectation for Robotic Manipulation](https://proceedings.neurips.cc/paper_files/paper/2024/hash/fad8962279154544ed69bb63eb14d677-Abstract-Conference.html) (NeurIPS 2024)  
  Uses generated expectations for closed-loop visuomotor control.

- [World Action Models are Zero-Shot Policies](https://openreview.net/forum?id=cd33uUB609) (ICLR Workshop 2026)  
  Demonstrates world-action rollout generation for zero-shot policy execution.

- [VidArc: Embodied Video Diffusion Model for Closed-Loop Control](https://arxiv.org/abs/2512.17661) (arXiv 2025)  
  An embodied video diffusion model designed for closed-loop control.

---

## Background and Related Foundations

This section includes background works explicitly referenced in the survey to clarify the lineage of video prediction, visual foresight, and action-readable representation learning.

---

### Visual Foresight and Video-Prediction-Based Planning

- [Deep Visual Foresight for Planning Robot Motion](https://ieeexplore.ieee.org/document/7989324) (ICRA 2017)  
  Early visual foresight framework for planning robot motion using predicted visual futures.

- [Unsupervised Learning for Physical Interaction through Video Prediction](https://proceedings.neurips.cc/paper/2016/hash/d9d4f495e875a2e075a1a4a6e1b9770f-Abstract.html) (NeurIPS 2016)  
  Learns physical interaction dynamics through video prediction.

- [Visual Foresight: Model-Based Deep Reinforcement Learning for Vision-Based Robotic Control](http://arxiv.org/abs/1812.00568) (arXiv 2018)  
  Uses predictive visual models for model-based robotic control.

- [Robot Motion Planning as Video Prediction: A Spatio-Temporal Neural Network-Based Motion Planner](https://doi.org/10.1109/IROS47612.2022.9981769) (IROS 2022)  
  Frames robot motion planning as a video prediction problem.

---

### Action-Readable Representation Learning

- [Time-Contrastive Networks: Self-Supervised Learning from Video](https://doi.org/10.1109/ICRA.2018.8462891) (ICRA 2018)  
  Learns temporally aligned representations from video.

- [Particle Video Revisited: Tracking through Occlusions using Point Trajectories](https://doi.org/10.1007/978-3-031-20047-2_4) (ECCV 2022)  
  Tracks point trajectories through occlusions, relevant to motion-sensitive and action-readable video representations.
