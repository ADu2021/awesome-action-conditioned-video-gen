<div align="center">

<img src="assets/banner.svg" alt="Awesome Action-Conditioned Video Generation" width="100%">

# Awesome Action-Conditioned Video Generation [![Awesome](https://cdn.rawgit.com/sindresorhus/awesome/d7305f38d29fed78fa85652e3a63e154dd8e8829/media/badge.svg)](https://github.com/sindresorhus/awesome)

[![Awesome](https://img.shields.io/badge/Awesome-List-fc60a8?logo=awesomelists)](https://github.com/sindresorhus/awesome) [![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md) [![License: CC0-1.0](https://img.shields.io/badge/License-CC0_1.0-lightgrey.svg)](LICENSE) ![Maintenance](https://img.shields.io/badge/Maintained%3F-yes-2ea44f.svg) ![Last Updated](https://img.shields.io/badge/Updated-2026--06-1e90ff.svg)

**📜 A curated, up-to-date list of papers, models, datasets, and benchmarks on _action-conditioned video generation_ — generative models that predict or synthesize future video conditioned on an action signal.**

_"What does the world look like if I take **this** action?"_ — Robotics & Embodied AI · Games & Interactive Worlds · Autonomous Driving · Controllable & Interactive Video

</div>

> [!NOTE]
> **Action-conditioned** is interpreted broadly: robot/agent motor commands, discrete controller / keyboard-mouse inputs, ego-vehicle trajectories & control, camera poses & motion, drag trajectories, and free-text actions. This list deliberately puts **Robotics & Embodied AI** first, then Games, Driving, and general controllable/interactive video. Contributions are very welcome — see [CONTRIBUTING.md](CONTRIBUTING.md).

---

## 🚩 News and Updates

- **[2026-06]** 🚀 Initial public release with **190+** curated entries across robotics, games, autonomous driving, controllable video generation, datasets, and benchmarks. Every arXiv ID has been verified against its abstract.
- **[Ongoing]** 💡 Spotted a missing paper, broken link, or wrong venue? Open an [Issue or PR](CONTRIBUTING.md) — corrections are as welcome as additions.

---

## 📖 Contents

- [🎯 What Is Action-Conditioned Video Generation?](#what-is-action-conditioned-video-generation)
- [📚 Surveys and Background](#surveys-and-background)
- [🤖 Robotics and Embodied AI](#robotics-and-embodied-ai) ⭐ _featured_
  - [Classic and Foundational Action-Conditioned Video Prediction](#classic-and-foundational-action-conditioned-video-prediction)
  - [Generative Robot World Models and Simulators](#generative-robot-world-models-and-simulators)
  - [Video-Generation Policies (Video-as-Plan)](#video-generation-policies-video-as-plan)
  - [Navigation and Egocentric World Models](#navigation-and-egocentric-world-models)
- [🎮 Games and Interactive World Models](#games-and-interactive-world-models)
  - [Real-Time Neural Game Engines](#real-time-neural-game-engines)
  - [Interactive and Playable World Models](#interactive-and-playable-world-models)
  - [Game Video Generation (Open-World and Controllable)](#game-video-generation-open-world-and-controllable)
  - [Classic Playable Video Generation](#classic-playable-video-generation)
- [🚗 Autonomous Driving World Models](#autonomous-driving-world-models)
  - [Foundational Driving World Models](#foundational-driving-world-models)
  - [Controllable Multi-View and Trajectory-Conditioned Generation](#controllable-multi-view-and-trajectory-conditioned-generation)
  - [Occupancy and 4D World Models](#occupancy-and-4d-world-models)
  - [Driving Simulation and Reconstruction](#driving-simulation-and-reconstruction)
- [🎥 General Controllable and Interactive Video Generation](#general-controllable-and-interactive-video-generation)
  - [Camera and Motion-Controlled Video Generation](#camera-and-motion-controlled-video-generation)
  - [General Interactive World Models](#general-interactive-world-models)
  - [Real-Time and Long-Horizon Interactive Video](#real-time-and-long-horizon-interactive-video)
- [🗂️ Datasets](#datasets)
- [📊 Benchmarks and Evaluation](#benchmarks-and-evaluation)
- [🔗 Related Awesome Lists](#related-awesome-lists)
- [🤝 Contributing](#contributing)
- [⭐ Citation](#citation)
- [🙏 Acknowledgements](#acknowledgements)

Badge legend: [![arXiv](https://img.shields.io/badge/arXiv-paper-b31b1b)](#) paper · [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](#) project page · [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](#) code · [![Report](https://img.shields.io/badge/Tech-Report-orange)](#) tech report / blog.

---

## What Is Action-Conditioned Video Generation?

**Action-conditioned video generation** studies models that, given past observations and an **action** (or sequence of actions), generate the resulting future video. Formally, the model approximates the visual dynamics `p(o_{t+1:t+k} | o_{≤t}, a_{t:t+k})`, where `o` are image/frame observations and `a` are actions. This sits at the intersection of **video generation** and **world models**: it is video generation made *controllable by actions*, and it is a world model whose state is rendered as pixels.

The **action** can take many forms, and the conditioning interface is what distinguishes this area from plain text-to-video:

| Action type | Example signal | Typical domain |
| --- | --- | --- |
| Low-level motor command | end-effector delta, joint torque | robot manipulation |
| Discrete control | keyboard / mouse / gamepad button | games, interactive worlds |
| Ego trajectory / control | steering, speed, waypoints | autonomous driving |
| Camera pose / motion | extrinsics, drag, pan/zoom | controllable video, NVS |
| Latent action | self-supervised action codes | cross-domain world models |
| Language as action | "pick up the cup", "turn left" | instruction-following |

Why it matters: an accurate action-conditioned video model is a **learned simulator**. It can roll out imagined futures for planning and model-based RL, generate synthetic training data, evaluate policies before real-world deployment, and power playable neural game engines and interactive worlds.

Foundational reading: the original **World Models** ([Ha & Schmidhuber, 2018](https://arxiv.org/abs/1803.10122)) and **"A Path Towards Autonomous Machine Intelligence"** ([LeCun, 2022](https://openreview.net/pdf?id=BZ5a1r-kVsf)) frame the broader world-model agenda this list specializes for the *video* + *action* setting.

---

## 📚 Surveys and Background

- **Understanding World or Predicting Future?** — *"Understanding World or Predicting Future? A Comprehensive Survey of World Models"*. `ACM CSUR 2025` [![arXiv](https://img.shields.io/badge/arXiv-2411.14499-b31b1b)](https://arxiv.org/abs/2411.14499) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/tsinghua-fib-lab/World-Model)  
  <sub>Categorizes world models by understanding vs. future-prediction across games, driving, robotics, and agents.</sub>
- **Is Sora a World Simulator?** — *"Is Sora a World Simulator? A Comprehensive Survey on General World Models and Beyond"*. `arXiv 2024` [![arXiv](https://img.shields.io/badge/arXiv-2405.03520-b31b1b)](https://arxiv.org/abs/2405.03520) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/GigaAI-research/General-World-Models-Survey)  
  <sub>Surveys general world models spanning video generation, autonomous driving, and autonomous-agent world models.</sub>
- **From Sora What We Can See** — *"From Sora What We Can See: A Survey of Text-to-Video Generation"*. `arXiv 2024` [![arXiv](https://img.shields.io/badge/arXiv-2405.10674-b31b1b)](https://arxiv.org/abs/2405.10674) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/soraw-ai/Awesome-Text-to-Video-Generation)  
  <sub>Survey of text-to-video generation covering generators, datasets, metrics, and open challenges in the Sora era.</sub>
- **Controllable Video Generation: A Survey** — *"Controllable Video Generation: A Survey"*. `arXiv 2025` [![arXiv](https://img.shields.io/badge/arXiv-2507.16869-b31b1b)](https://arxiv.org/abs/2507.16869) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/mayuelala/Awesome-Controllable-Video-Generation)  
  <sub>Taxonomizes controllable video generation by control signal (structure, image, audio, temporal, identity, universal).</sub>
- **A Survey of Interactive Generative Video** — *"A Survey of Interactive Generative Video"*. `arXiv 2025` [![arXiv](https://img.shields.io/badge/arXiv-2504.21853-b31b1b)](https://arxiv.org/abs/2504.21853)  
  <sub>Defines Interactive Generative Video via a 5-module framework (Generation, Control, Memory, Dynamics, Intelligence).</sub>
- **World Models for Autonomous Driving: An Initial Survey** — *"World Models for Autonomous Driving: An Initial Survey"*. `IEEE T-IV 2024` [![arXiv](https://img.shields.io/badge/arXiv-2403.02622-b31b1b)](https://arxiv.org/abs/2403.02622)  
  <sub>Early survey of driving world models covering foundations, applications, and open challenges.</sub>
- **A Survey of World Models for Autonomous Driving** — *"A Survey of World Models for Autonomous Driving"*. `arXiv 2025` [![arXiv](https://img.shields.io/badge/arXiv-2501.11260-b31b1b)](https://arxiv.org/abs/2501.11260)  
  <sub>Three-tiered taxonomy spanning future-world generation, behavior planning, and interaction.</sub>
- **Interplay Between Video Generation and World Models** — *"Exploring the Interplay Between Video Generation and World Models in Autonomous Driving: A Survey"*. `arXiv 2024` [![arXiv](https://img.shields.io/badge/arXiv-2411.02914-b31b1b)](https://arxiv.org/abs/2411.02914)  
  <sub>Survey on the structural parallels and integration of video generation and world models for driving.</sub>
- **Simulating the Visual World: A Roadmap** — *"Simulating the Visual World with Artificial Intelligence: A Roadmap"*. `arXiv 2025` [![arXiv](https://img.shields.io/badge/arXiv-2511.08585-b31b1b)](https://arxiv.org/abs/2511.08585) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://world-model-roadmap.github.io/)  
  <sub>Position/roadmap conceptualizing video foundation models as an implicit world model plus video renderer.</sub>

---

## 🤖 Robotics and Embodied AI

> The featured section. Here the **action is a robot/agent control** (motor command, end-effector delta, navigation move, or language instruction), and the generated video is used for planning, model-based RL, policy learning, data generation, or policy evaluation.

### Classic and Foundational Action-Conditioned Video Prediction

- **Oh et al.** — *"Action-Conditional Video Prediction using Deep Networks in Atari Games"*. `NeurIPS 2015` [![arXiv](https://img.shields.io/badge/arXiv-1507.08750-b31b1b)](https://arxiv.org/abs/1507.08750)  
  <sub>Encoder–transform–decoder network predicting the next Atari frame conditioned on the agent's discrete control action, enabling long rollouts.</sub>
- **CDNA / Finn et al.** — *"Unsupervised Learning for Physical Interaction through Video Prediction"*. `NeurIPS 2016` [![arXiv](https://img.shields.io/badge/arXiv-1605.07157-b31b1b)](https://arxiv.org/abs/1605.07157) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/tensorflow/models/tree/master/research/video_prediction)  
  <sub>Predicts future frames of a robot arm pushing objects by warping pixels (CDNA/DNA/STP) conditioned on the commanded action.</sub>
- **SV2P** — *"Stochastic Variational Video Prediction"*. `ICLR 2018` [![arXiv](https://img.shields.io/badge/arXiv-1710.11252-b31b1b)](https://arxiv.org/abs/1710.11252)  
  <sub>First effective stochastic multi-frame predictor for real-world video, supporting action-conditioned robot-pushing prediction via latent variables.</sub>
- **SVG-LP** — *"Stochastic Video Generation with a Learned Prior"*. `ICML 2018` [![arXiv](https://img.shields.io/badge/arXiv-1802.07687-b31b1b)](https://arxiv.org/abs/1802.07687) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://sites.google.com/view/svglp/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/edenton/svg)  
  <sub>VAE video prediction with a learned per-timestep latent prior; the backbone can be conditioned on actions for robot/interaction prediction.</sub>
- **SAVP** — *"Stochastic Adversarial Video Prediction"*. `arXiv 2018` [![arXiv](https://img.shields.io/badge/arXiv-1804.01523-b31b1b)](https://arxiv.org/abs/1804.01523) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://alexlee-gk.github.io/video_prediction/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/alexlee-gk/video_prediction)  
  <sub>Unifies VAE and GAN objectives for realistic and diverse action-conditioned future-frame prediction on the BAIR robot-pushing dataset.</sub>
- **Visual Foresight / Visual MPC** — *"Visual Foresight: Model-Based Deep RL for Vision-Based Robotic Control"*. `arXiv 2018` [![arXiv](https://img.shields.io/badge/arXiv-1812.00568-b31b1b)](https://arxiv.org/abs/1812.00568) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/SudeepDasari/visual_foresight)  
  <sub>Uses self-supervised action-conditioned video prediction inside visual MPC, planning action sequences whose predicted frames reach a goal.</sub>

### Generative Robot World Models and Simulators

- **UniSim** — *"Learning Interactive Real-World Simulators"*. `ICLR 2024 (Outstanding Paper)` [![arXiv](https://img.shields.io/badge/arXiv-2310.06114-b31b1b)](https://arxiv.org/abs/2310.06114) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://universal-simulator.github.io/unisim/)  
  <sub>Diffusion-based universal simulator generating the visual outcome of both high-level instructions and low-level motor controls to train transferable policies.</sub>
- **iVideoGPT** — *"iVideoGPT: Interactive VideoGPTs are Scalable World Models"*. `NeurIPS 2024` [![arXiv](https://img.shields.io/badge/arXiv-2405.15223-b31b1b)](https://arxiv.org/abs/2405.15223) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://thuml.github.io/iVideoGPT/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/thuml/iVideoGPT)  
  <sub>Autoregressive transformer interleaving observations, actions, and rewards as tokens for action-conditioned prediction, planning, and model-based RL.</sub>
- **IRASim** — *"IRASim: Learning Interactive Real-Robot Action Simulators"*. `arXiv 2024` [![arXiv](https://img.shields.io/badge/arXiv-2406.14540-b31b1b)](https://arxiv.org/abs/2406.14540) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://gen-irasim.github.io/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/bytedance/IRASim)  
  <sub>Given an initial frame and a full end-effector action trajectory, renders high-resolution long-horizon video of the arm executing that trajectory.</sub>
- **RoboDreamer** — *"RoboDreamer: Learning Compositional World Models for Robot Imagination"*. `ICML 2024` [![arXiv](https://img.shields.io/badge/arXiv-2404.12377-b31b1b)](https://arxiv.org/abs/2404.12377) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/rainbow979/robodreamer)  
  <sub>Factorizes video generation over language primitives so the model imagines future robot videos for unseen object/action combinations.</sub>
- **Cosmos (WFM Platform)** — *"Cosmos World Foundation Model Platform for Physical AI"*. `arXiv 2025` [![arXiv](https://img.shields.io/badge/arXiv-2501.03575-b31b1b)](https://arxiv.org/abs/2501.03575) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://www.nvidia.com/en-us/ai/cosmos/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/nvidia-cosmos/cosmos-predict1)  
  <sub>Open diffusion/autoregressive world-foundation models post-trainable with action or camera control to simulate physics-accurate future video.</sub>
- **Cosmos-Transfer1** — *"Cosmos-Transfer1: Conditional World Generation with Adaptive Multimodal Control"*. `arXiv 2025` [![arXiv](https://img.shields.io/badge/arXiv-2503.14492-b31b1b)](https://arxiv.org/abs/2503.14492) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://research.nvidia.com/labs/dir/cosmos-transfer1/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/nvidia-cosmos/cosmos-transfer1)  
  <sub>ControlNet-style multimodal (depth/segmentation/edge) conditional world generation for Sim2Real world-to-world transfer.</sub>
- **Cosmos-Predict2.5** — *"World Simulation with Video Foundation Models for Physical AI"*. `arXiv 2025` [![arXiv](https://img.shields.io/badge/arXiv-2511.00062-b31b1b)](https://arxiv.org/abs/2511.00062) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://research.nvidia.com/labs/cosmos-lab/cosmos-predict2.5/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/nvidia-cosmos/cosmos-predict2.5)  
  <sub>Flow-based unified Text/Image/Video-to-World model, fine-tunable with action control for closed-loop robot simulation and synthetic data.</sub>
- **HMA** — *"Learning Real-World Action-Video Dynamics with Heterogeneous Masked Autoregression"*. `arXiv 2025` [![arXiv](https://img.shields.io/badge/arXiv-2502.04296-b31b1b)](https://arxiv.org/abs/2502.04296) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://liruiw.github.io/hma/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/liruiw/HMA)  
  <sub>Masked autoregressive video model pre-trained across 40 embodiments predicting future frames from low-level actions; a fast simulator/evaluator.</sub>
- **WHALE** — *"WHALE: Towards Generalizable and Scalable World Models for Embodied Decision-making"*. `arXiv 2024` [![arXiv](https://img.shields.io/badge/arXiv-2411.05619-b31b1b)](https://arxiv.org/abs/2411.05619)  
  <sub>Behavior-conditioned spatio-temporal transformer (trained on Open X-Embodiment) predicting action-conditioned future video with uncertainty estimation.</sub>
- **AdaWorld** — *"AdaWorld: Learning Adaptable World Models with Latent Actions"*. `ICML 2025` [![arXiv](https://img.shields.io/badge/arXiv-2503.18938-b31b1b)](https://arxiv.org/abs/2503.18938) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://adaptable-world-model.github.io/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/Little-Podi/AdaWorld)  
  <sub>Pre-trains an autoregressive world model on self-supervised latent actions, enabling rapid adaptation to new heterogeneous action spaces.</sub>
- **Vid2World** — *"Vid2World: Crafting Video Diffusion Models to Interactive World Models"*. `arXiv 2025` [![arXiv](https://img.shields.io/badge/arXiv-2505.14357-b31b1b)](https://arxiv.org/abs/2505.14357) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://knightnemo.github.io/vid2world/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/thuml/Vid2World)  
  <sub>Causalizes pre-trained full-sequence video diffusion models into autoregressive, action-conditioned interactive world models.</sub>
- **AVID** — *"AVID: Adapting Video Diffusion Models to World Models"*. `RLC 2025` [![arXiv](https://img.shields.io/badge/arXiv-2410.12822-b31b1b)](https://arxiv.org/abs/2410.12822) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://sites.google.com/view/avid-world-model-adapters/home)  
  <sub>Trains a lightweight adapter + learned mask to convert a frozen (even closed-source) pretrained video diffusion model into an action-conditioned world model.</sub>
- **EnerVerse** — *"EnerVerse: Envisioning Embodied Future Space for Robotics Manipulation"*. `NeurIPS 2025` [![arXiv](https://img.shields.io/badge/arXiv-2501.01895-b31b1b)](https://arxiv.org/abs/2501.01895) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://sites.google.com/view/enerverse)  
  <sub>Chunk-wise autoregressive video diffusion with a Free-Anchor-View space predicting instruction-conditioned future embodied space, converted to actions.</sub>
- **EnerVerse-AC** — *"EnerVerse-AC: Envisioning Embodied Environments with Action Condition"*. `arXiv 2025` [![arXiv](https://img.shields.io/badge/arXiv-2505.09723-b31b1b)](https://arxiv.org/abs/2505.09723) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://annaj2178.github.io/EnerverseAC.github.io/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/AgibotTech/EnerVerse-AC)  
  <sub>Action-conditional multi-view world model using multi-level action conditioning and ray-map encoding as a data engine and policy evaluator.</sub>
- **Genie Envisioner** — *"Genie Envisioner: A Unified World Foundation Platform for Robotic Manipulation"*. `arXiv 2025` [![arXiv](https://img.shields.io/badge/arXiv-2508.05635-b31b1b)](https://arxiv.org/abs/2508.05635) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://genie-envisioner.github.io/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/AgibotTech/Genie-Envisioner)  
  <sub>Pairs an instruction-conditioned diffusion model (GE-Base) with an action-conditioned neural simulator (GE-Sim) and a flow-matching action decoder.</sub>
- **WorldVLA** — *"WorldVLA: Towards Autoregressive Action World Model"*. `arXiv 2025` [![arXiv](https://img.shields.io/badge/arXiv-2506.21539-b31b1b)](https://arxiv.org/abs/2506.21539) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/alibaba-damo-academy/WorldVLA)  
  <sub>Single autoregressive transformer unifying a VLA action model and a world model that predicts future images from action+image tokens.</sub>
- **GR00T N1** — *"GR00T N1: An Open Foundation Model for Generalist Humanoid Robots"*. `arXiv 2025` [![arXiv](https://img.shields.io/badge/arXiv-2503.14734-b31b1b)](https://arxiv.org/abs/2503.14734) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://research.nvidia.com/labs/lpr/publication/gr00tn1_2025/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/NVIDIA/Isaac-GR00T)  
  <sub>Dual-system VLA foundation model trained on egocentric human video, real/sim trajectories, and neural-trajectory synthetic data for cross-embodiment manipulation.</sub>
- **DreamGen** — *"DreamGen: Unlocking Generalization in Robot Learning through Video World Models"*. `CoRL 2025` [![arXiv](https://img.shields.io/badge/arXiv-2505.12705-b31b1b)](https://arxiv.org/abs/2505.12705) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://research.nvidia.com/labs/gear/dreamgen/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/NVIDIA/GR00T-Dreams)  
  <sub>Adapts image-to-video world models to a target robot to generate "neural trajectories," recovering pseudo-actions to train generalizing policies.</sub>
- **RoboTransfer** — *"RoboTransfer: Geometry-Consistent Video Diffusion for Robotic Visual Policy Transfer"*. `arXiv 2025` [![arXiv](https://img.shields.io/badge/arXiv-2505.23171-b31b1b)](https://arxiv.org/abs/2505.23171) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://horizonrobotics.github.io/robot_lab/robotransfer/index.html)  
  <sub>Multi-view geometry-consistent video diffusion synthesizing manipulation data with controllable backgrounds/objects to improve visual policy transfer.</sub>
- **1X World Model** — *"1X World Model"*. `Tech Report 2024` [![Report](https://img.shields.io/badge/Tech-Report-orange)](https://www.1x.tech/discover/1x-world-model)  
  <sub>Action-conditioned humanoid world model predicting future pixels/latents from past frames and robot states to evaluate policies before deployment.</sub>

### Video-Generation Policies (Video-as-Plan)

- **UniPi** — *"Learning Universal Policies via Text-Guided Video Generation"*. `NeurIPS 2023` [![arXiv](https://img.shields.io/badge/arXiv-2302.00111-b31b1b)](https://arxiv.org/abs/2302.00111) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://universal-policy.github.io/unipi/)  
  <sub>Casts decision-making as text-conditioned video generation: synthesize a goal-reaching video, then an inverse-dynamics model extracts the actions.</sub>
- **Seer** — *"Seer: Language Instructed Video Prediction with Latent Diffusion Models"*. `ICLR 2024` [![arXiv](https://img.shields.io/badge/arXiv-2303.14897-b31b1b)](https://arxiv.org/abs/2303.14897) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://seervideodiffusion.github.io/)  
  <sub>Inflated latent-diffusion model predicting future frames from reference frames and a language instruction to facilitate robot policy learning.</sub>
- **GR-1** — *"Unleashing Large-Scale Video Generative Pre-training for Visual Robot Manipulation"*. `ICLR 2024` [![arXiv](https://img.shields.io/badge/arXiv-2312.13139-b31b1b)](https://arxiv.org/abs/2312.13139) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://gr1-manipulation.github.io/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/bytedance/GR-1)  
  <sub>GPT-style model pre-trained on video prediction then finetuned to jointly predict future frames and robot actions from language and observations.</sub>
- **GR-2** — *"GR-2: A Generative Video-Language-Action Model with Web-Scale Knowledge"*. `arXiv 2024` [![arXiv](https://img.shields.io/badge/arXiv-2410.06158-b31b1b)](https://arxiv.org/abs/2410.06158) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://gr2-manipulation.github.io/)  
  <sub>Scales GR-1 with web-scale video pre-training (38M clips) and finetunes for joint video generation and action prediction.</sub>
- **GR-3** — *"GR-3 Technical Report"*. `arXiv 2025` [![arXiv](https://img.shields.io/badge/arXiv-2507.15493-b31b1b)](https://arxiv.org/abs/2507.15493) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://seed.bytedance.com/GR3)  
  <sub>Large VLA model co-trained on web vision-language, VR human trajectories, and robot data, generalizing to novel objects and environments.</sub>
- **VPP** — *"Video Prediction Policy: A Generalist Robot Policy with Predictive Visual Representations"*. `ICML 2025` [![arXiv](https://img.shields.io/badge/arXiv-2412.14803-b31b1b)](https://arxiv.org/abs/2412.14803) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://video-prediction-policy.github.io/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/roboterax/video-prediction-policy)  
  <sub>Uses the predictive future-frame representations inside a fine-tuned video diffusion model as features for an inverse-dynamics action head.</sub>
- **AVDC** — *"Learning to Act from Actionless Videos through Dense Correspondences"*. `ICLR 2024` [![arXiv](https://img.shields.io/badge/arXiv-2310.08576-b31b1b)](https://arxiv.org/abs/2310.08576) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://flow-diffusion.github.io/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/flow-diffusion/AVDC)  
  <sub>Synthesizes a task video then derives actions from optical-flow dense correspondences + depth, learning to act without any action labels.</sub>
- **SuSIE** — *"Zero-Shot Robotic Manipulation with Pretrained Image-Editing Diffusion Models"*. `ICLR 2024` [![arXiv](https://img.shields.io/badge/arXiv-2310.10639-b31b1b)](https://arxiv.org/abs/2310.10639) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://rail-berkeley.github.io/susie/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/kvablack/susie)  
  <sub>An image-editing diffusion model "edits" the observation into a subgoal image given a language command; a low-level policy realizes each subgoal.</sub>
- **Video Language Planning** — *"Video Language Planning"*. `ICLR 2024` [![arXiv](https://img.shields.io/badge/arXiv-2310.10625-b31b1b)](https://arxiv.org/abs/2310.10625) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://video-language-planning.github.io/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/video-language-planning/vlp_code)  
  <sub>Tree-search planner using VLMs as policy/value and text-to-video models as dynamics to produce long-horizon video plans converted to actions.</sub>
- **Dreamitate** — *"Dreamitate: Real-World Visuomotor Policy Learning via Video Generation"*. `CoRL 2024` [![arXiv](https://img.shields.io/badge/arXiv-2406.16862-b31b1b)](https://arxiv.org/abs/2406.16862) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://dreamitate.cs.columbia.edu/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/cvlab-columbia/dreamitate)  
  <sub>Fine-tunes a video diffusion model on human tool-use demos and 3D-tracks the tool in the generated video to directly control the robot.</sub>
- **This&That** — *"This&That: Language-Gesture Controlled Video Generation for Robot Planning"*. `ICRA 2025` [![arXiv](https://img.shields.io/badge/arXiv-2407.05530-b31b1b)](https://arxiv.org/abs/2407.05530) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://cfeng16.github.io/this-and-that/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/Kiteretsu77/This_and_That_VDM)  
  <sub>Generates robot-planning video conditioned on language plus pointing gestures, then a diffusion video-to-action policy executes the plan.</sub>
- **Unified Video Action (UVA)** — *"Unified Video Action Model"*. `RSS 2025` [![arXiv](https://img.shields.io/badge/arXiv-2503.00200-b31b1b)](https://arxiv.org/abs/2503.00200) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://unified-video-action-model.github.io/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/ShuangLI59/unified_video_action)  
  <sub>Learns a joint video-action latent with decoupled diffusion heads, serving as policy, forward/inverse dynamics, and action-conditioned video generator.</sub>
- **Unified World Models (UWM)** — *"Unified World Models: Coupling Video and Action Diffusion for Pretraining on Large Robotic Datasets"*. `arXiv 2025` [![arXiv](https://img.shields.io/badge/arXiv-2504.02792-b31b1b)](https://arxiv.org/abs/2504.02792) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://weirdlabuw.github.io/uwm/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/WEIRDLabUW/unified-world-model)  
  <sub>Single transformer with independent video- and action-diffusion timesteps acting as policy, dynamics, or video generator on action-labeled and action-free video.</sub>
- **Vidar** — *"Vidar: Embodied Video Diffusion Model for Generalist Bimanual Manipulation"*. `arXiv 2025` [![arXiv](https://img.shields.io/badge/arXiv-2507.12898-b31b1b)](https://arxiv.org/abs/2507.12898) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://embodiedfoundation.github.io/vidar_anypos) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/thu-ml/vidar)  
  <sub>Internet-pretrained, robot-adapted video diffusion prior plus a masked inverse-dynamics adapter that grounds predicted video into actions from ~20 min of demos.</sub>

### Navigation and Egocentric World Models

- **Pathdreamer** — *"Pathdreamer: A World Model for Indoor Navigation"*. `ICCV 2021` [![arXiv](https://img.shields.io/badge/arXiv-2105.08756-b31b1b)](https://arxiv.org/abs/2105.08756) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://google-research.github.io/pathdreamer/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/google-research/pathdreamer)  
  <sub>Generates 360° RGB/semantic/depth observations for unseen viewpoints conditioned on the agent's navigation action, supporting vision-and-language navigation.</sub>
- **Navigation World Models (NWM)** — *"Navigation World Models"*. `CVPR 2025` [![arXiv](https://img.shields.io/badge/arXiv-2412.03572-b31b1b)](https://arxiv.org/abs/2412.03572) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://www.amirbar.net/nwm/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/facebookresearch/nwm)  
  <sub>1B-parameter Conditional Diffusion Transformer predicting future egocentric observations from navigation actions, planning by simulating and scoring trajectories.</sub>
- **GenEx** — *"GenEx: Generating an Explorable World"*. `ICLR 2025` [![arXiv](https://img.shields.io/badge/arXiv-2412.09624-b31b1b)](https://arxiv.org/abs/2412.09624) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://www.genex.world/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/GenEx-world/genex)  
  <sub>Generates a 3D-consistent panoramic video world from one image and rolls it forward under exploration/navigation actions for goal-driven agents.</sub>
- **V-JEPA 2** — *"V-JEPA 2: Self-Supervised Video Models Enable Understanding, Prediction and Planning"*. `arXiv 2025` [![arXiv](https://img.shields.io/badge/arXiv-2506.09985-b31b1b)](https://arxiv.org/abs/2506.09985) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://ai.meta.com/research/publications/v-jepa-2-self-supervised-video-models-enable-understanding-prediction-and-planning/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/facebookresearch/vjepa2)  
  <sub>The action-conditioned variant (V-JEPA 2-AC) predicts next-frame latent representations from actions, enabling zero-shot pick-and-place planning on real arms.</sub>
- **Aether** — *"Aether: Geometric-Aware Unified World Modeling"*. `ICCV 2025` [![arXiv](https://img.shields.io/badge/arXiv-2503.18945-b31b1b)](https://arxiv.org/abs/2503.18945) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://aether-world.github.io/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/InternRobotics/Aether)  
  <sub>Jointly does 4D reconstruction, action-conditioned video prediction, and goal-conditioned planning using camera trajectories as the action space.</sub>

---

## 🎮 Games and Interactive World Models

> Here the **action is a user/controller input** (keyboard, mouse, gamepad). These models generate playable game frames one step at a time, turning a neural network into a real-time, controllable game engine or interactive environment.

### Real-Time Neural Game Engines

- **GameNGen** — *"Diffusion Models Are Real-Time Game Engines"*. `ICLR 2025` [![arXiv](https://img.shields.io/badge/arXiv-2408.14837-b31b1b)](https://arxiv.org/abs/2408.14837) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://gamengen.github.io/)  
  <sub>A diffusion model simulates DOOM at 20+ FPS, predicting each next frame conditioned on past frames and player actions recorded from an RL agent.</sub>
- **Oasis** — *"Oasis: A Universe in a Transformer"*. `Tech Report 2024` [![Report](https://img.shields.io/badge/Tech-Report-orange)](https://oasis-model.github.io/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/etched-ai/open-oasis)  
  <sub>An open-world Minecraft-like game generated by a diffusion transformer, autoregressively producing frames from live keyboard/mouse input at 20 FPS.</sub>
- **DIAMOND** — *"Diffusion for World Modeling: Visual Details Matter in Atari"*. `NeurIPS 2024 (Spotlight)` [![arXiv](https://img.shields.io/badge/arXiv-2405.12399-b31b1b)](https://arxiv.org/abs/2405.12399) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://diamond-wm.github.io/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/eloialonso/diamond)  
  <sub>Trains an RL agent inside a diffusion world model; the model doubles as a standalone playable neural engine for Counter-Strike conditioned on player actions.</sub>
- **WHAMM!** — *"WHAMM! Real-Time World Modelling of Interactive Environments"*. `Tech Report 2025` [![Report](https://img.shields.io/badge/Tech-Report-orange)](https://www.microsoft.com/en-us/research/articles/whamm-real-time-world-modelling-of-interactive-environments/)  
  <sub>A MaskGIT-based model renders a real-time (10+ FPS) playable Quake II in-browser, predicting each frame from player inputs.</sub>
- **PlayGen** — *"Playable Game Generation"*. `arXiv 2024` [![arXiv](https://img.shields.io/badge/arXiv-2412.00887-b31b1b)](https://arxiv.org/abs/2412.00887) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/GreatX3/Playable-Game-Generation)  
  <sub>A lightweight autoregressive DiT diffusion model running playable games at 20 FPS on a consumer GPU, generating frames from user actions.</sub>
- **NFD** — *"Playing with Transformer at 30+ FPS via Next-Frame Diffusion"*. `arXiv 2025` [![arXiv](https://img.shields.io/badge/arXiv-2506.01380-b31b1b)](https://arxiv.org/abs/2506.01380) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://nextframed.github.io/)  
  <sub>An autoregressive diffusion transformer with block-wise causal attention, consistency distillation, and speculative sampling for 30+ FPS action-conditioned game video.</sub>
- **Lucid v1** — *"Lucid v1 — Minecraft World Model"*. `Tech Report 2024` [![Report](https://img.shields.io/badge/Tech-Report-orange)](https://www.lucid.ai/notes/lucid-v1)  
  <sub>An action-conditioned diffusion video model emulating Minecraft at 20–30 FPS on a single GPU via aggressive tokenizer compression.</sub>
- **Multiverse** — *"Multiverse: The First AI Multiplayer World Model"*. `Tech Report 2025` [![Report](https://img.shields.io/badge/Tech-Report-orange)](https://enigma-labs.io/blog) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/EnigmaLabsAI/multiverse)  
  <sub>An open-source real-time diffusion world model trained on racing footage that simulates a shared environment for multiple players via joint-action modeling.</sub>

### Interactive and Playable World Models

- **Genie** — *"Genie: Generative Interactive Environments"*. `ICML 2024 (Best Paper)` [![arXiv](https://img.shields.io/badge/arXiv-2402.15391-b31b1b)](https://arxiv.org/abs/2402.15391) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://sites.google.com/view/genie-2024/)  
  <sub>An 11B foundation world model learning a latent action space from unlabeled internet videos for frame-by-frame action-controllable generation of 2D worlds.</sub>
- **Genie 2** — *"Genie 2: A Large-Scale Foundation World Model"*. `DeepMind Blog 2024` [![Report](https://img.shields.io/badge/Blog-Link-orange)](https://deepmind.google/blog/genie-2-a-large-scale-foundation-world-model/)  
  <sub>Turns a single prompt image into a playable, action-controllable (keyboard/mouse) 3D environment with long-horizon memory for training embodied agents.</sub>
- **Genie 3** — *"Genie 3: A New Frontier for World Models"*. `DeepMind Blog 2025` [![Report](https://img.shields.io/badge/Blog-Link-orange)](https://deepmind.google/blog/genie-3-a-new-frontier-for-world-models/)  
  <sub>A real-time general-purpose world model generating 720p/24fps navigable worlds from text, conditioned on navigation actions plus promptable world events.</sub>
- **Matrix-Game** — *"Matrix-Game: Interactive World Foundation Model"*. `arXiv 2025` [![arXiv](https://img.shields.io/badge/arXiv-2506.18701-b31b1b)](https://arxiv.org/abs/2506.18701) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://matrix-game-homepage.github.io/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/SkyworkAI/Matrix-Game)  
  <sub>A 17B interactive foundation model for Minecraft giving precise control over character actions and camera via keyboard/mouse.</sub>
- **Matrix-Game 2.0** — *"Matrix-Game 2.0: An Open-Source, Real-Time, and Streaming Interactive World Model"*. `arXiv 2025` [![arXiv](https://img.shields.io/badge/arXiv-2508.13009-b31b1b)](https://arxiv.org/abs/2508.13009) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://matrix-game-v2.github.io/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/SkyworkAI/Matrix-Game)  
  <sub>A few-step autoregressive diffusion model generating real-time 25fps streaming long video from frame-level keyboard/mouse inputs.</sub>
- **MineWorld** — *"MineWorld: A Real-Time and Open-Source Interactive World Model on Minecraft"*. `arXiv 2025` [![arXiv](https://img.shields.io/badge/arXiv-2504.08388-b31b1b)](https://arxiv.org/abs/2504.08388) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/microsoft/mineworld)  
  <sub>A visual-action autoregressive transformer generating Minecraft frames conditioned on paired scenes and actions, reaching real-time play via Diagonal Decoding.</sub>
- **Muse / WHAM** — *"World and Human Action Models towards Gameplay Ideation"*. `Nature 2025` [![Nature](https://img.shields.io/badge/Nature-2025-blueviolet)](https://www.microsoft.com/en-us/research/project/wham/) [![Code](https://img.shields.io/badge/Model-HuggingFace-yellow)](https://huggingface.co/microsoft/wham)  
  <sub>An autoregressive model trained on 7+ years of Bleeding Edge gameplay that predicts tokenized game visuals and/or controller actions from prompts.</sub>
- **PlayerOne** — *"PlayerOne: Egocentric World Simulator"*. `NeurIPS 2025 (Oral)` [![arXiv](https://img.shields.io/badge/arXiv-2506.09995-b31b1b)](https://arxiv.org/abs/2506.09995) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://playerone-hku.github.io/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/yuanpengtu/PlayerOne)  
  <sub>Generates first-person video strictly aligned to real human body motion captured by an exocentric camera, jointly modeling video and 4D scenes.</sub>
- **WorldMem** — *"WorldMem: Long-term Consistent World Simulation with Memory"*. `arXiv 2025` [![arXiv](https://img.shields.io/badge/arXiv-2504.12369-b31b1b)](https://arxiv.org/abs/2504.12369) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://xizaoqu.github.io/worldmem/)  
  <sub>A diffusion-forcing world model with a memory bank that autoregressively generates first-person Minecraft views from actions while preserving long-term 3D consistency.</sub>
- **GenieRedux** — *"Exploration-Driven Generative Interactive Environments"*. `CVPR 2025` [![arXiv](https://img.shields.io/badge/arXiv-2504.02515-b31b1b)](https://arxiv.org/abs/2504.02515) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://insait-institute.github.io/GenieRedux/)  
  <sub>An open Genie reimplementation plus an AutoExplore agent driven by world-model uncertainty for controllable, action-conditioned interactive video.</sub>

### Game Video Generation (Open-World and Controllable)

- **GameGen-X** — *"GameGen-X: Interactive Open-world Game Video Generation"*. `ICLR 2025` [![arXiv](https://img.shields.io/badge/arXiv-2411.00769-b31b1b)](https://arxiv.org/abs/2411.00769) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://gamegen-x.github.io/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/GameGen-X/GameGen-X)  
  <sub>The first diffusion transformer for generating and interactively controlling open-world game video, using an InstructNet to steer characters and events.</sub>
- **GameFactory** — *"GameFactory: Creating New Games with Generative Interactive Videos"*. `ICCV 2025` [![arXiv](https://img.shields.io/badge/arXiv-2501.08325-b31b1b)](https://arxiv.org/abs/2501.08325) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/KwaiVGI/GameFactory)  
  <sub>Decouples game-style learning from action control via an action module, transferring keyboard/mouse control onto pretrained video-diffusion priors.</sub>
- **Hunyuan-GameCraft** — *"Hunyuan-GameCraft: High-dynamic Interactive Game Video Generation with Hybrid History Condition"*. `arXiv 2025` [![arXiv](https://img.shields.io/badge/arXiv-2506.17201-b31b1b)](https://arxiv.org/abs/2506.17201) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://hunyuan-gamecraft.github.io/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/Tencent-Hunyuan/Hunyuan-GameCraft-1.0)  
  <sub>Unifies keyboard/mouse inputs into a shared camera-trajectory space with hybrid history-conditioned autoregression to produce playable game video.</sub>
- **Hunyuan-GameCraft-2** — *"Hunyuan-GameCraft-2: Instruction-following Interactive Game World Model"*. `arXiv 2025` [![arXiv](https://img.shields.io/badge/arXiv-2511.23429-b31b1b)](https://arxiv.org/abs/2511.23429) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://hunyuan-gamecraft-2.github.io/)  
  <sub>A 14B MoE diffusion world model adding text-driven conditioning so natural-language instructions plus keyboard/mouse control content at real-time 16 FPS.</sub>
- **Yan** — *"Yan: Foundational Interactive Video Generation"*. `Tech Report 2025` [![arXiv](https://img.shields.io/badge/arXiv-2508.08601-b31b1b)](https://arxiv.org/abs/2508.08601) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://greatx3.github.io/Yan/)  
  <sub>Renders a 3D game at 1080P/60 FPS, disentangling interactive mechanics simulation from visual rendering with text-driven multi-granularity editing.</sub>
- **GameGAN** — *"Learning to Simulate Dynamic Environments with GameGAN"*. `CVPR 2020` [![arXiv](https://img.shields.io/badge/arXiv-2005.12126-b31b1b)](https://arxiv.org/abs/2005.12126) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://nv-tlabs.github.io/gameGAN/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/nv-tlabs/GameGAN_code)  
  <sub>The first GAN-based neural game engine, recreating playable Pac-Man frame-by-frame from keyboard actions without a game engine.</sub>
- **DriveGAN** — *"DriveGAN: Towards a Controllable High-Quality Neural Simulation"*. `CVPR 2021 (Oral)` [![arXiv](https://img.shields.io/badge/arXiv-2104.15060-b31b1b)](https://arxiv.org/abs/2104.15060) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://research.nvidia.com/labs/toronto-ai/DriveGAN/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/nv-tlabs/DriveGAN_code)  
  <sub>A differentiable neural driving simulator generating frames from steering/acceleration actions while disentangling controllable scene factors.</sub>
- **AnimeGamer** — *"AnimeGamer: Infinite Anime Life Simulation with Next Game State Prediction"*. `ICCV 2025` [![arXiv](https://img.shields.io/badge/arXiv-2504.01014-b31b1b)](https://arxiv.org/abs/2504.01014) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/TencentARC/AnimeGamer)  
  <sub>An MLLM-based anime life simulator predicting the next game state from language instructions, decoded into video clips with consistent dynamics.</sub>
- **MarioVGG** — *"Video Game Generation: A Practical Study using Mario"*. `Tech Report 2024` [![Report](https://img.shields.io/badge/Tech-Report-orange)](https://virtual-protocol.github.io/mario-videogamegen/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/Virtual-Protocol/mario-videogamegen)  
  <sub>A text-to-video diffusion model taking an initial Mario frame plus a text action ("run right", "jump") and generating chained frames simulating physics.</sub>
- **Model as a Game** — *"Model as a Game: On Numerical and Spatial Consistency for Generative Games"*. `ICCV 2025 Workshop` [![arXiv](https://img.shields.io/badge/arXiv-2503.21172-b31b1b)](https://arxiv.org/abs/2503.21172)  
  <sub>Adds numerical (LogicNet) and spatial (map) modules to a DiT generative game so action-driven gameplay preserves correct scores and scene continuity.</sub>
- **IGV (Position)** — *"Position: Interactive Generative Video as Next-Generation Game Engine"*. `arXiv 2025` [![arXiv](https://img.shields.io/badge/arXiv-2503.17359-b31b1b)](https://arxiv.org/abs/2503.17359)  
  <sub>A position paper framing interactive generative video as Generative Game Engines, with an L0–L4 maturity roadmap for action-driven game video.</sub>
- **Mirage 2** — *"Mirage 2: General-Domain AI World Engine"*. `Tech Report 2025` [![Report](https://img.shields.io/badge/Tech-Report-orange)](https://blog.dynamicslab.ai/)  
  <sub>A real-time general-domain world engine turning any uploaded image into a playable world controllable via language, keyboard, or controller.</sub>

### Classic Playable Video Generation

- **PVG / CADDY** — *"Playable Video Generation"*. `CVPR 2021 (Oral)` [![arXiv](https://img.shields.io/badge/arXiv-2101.12195-b31b1b)](https://arxiv.org/abs/2101.12195) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://willi-menapace.github.io/playable-video-generation-website/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/willi-menapace/PlayableVideoGeneration)  
  <sub>Introduces the unsupervised PVG task: CADDY learns a discrete action space from unlabeled video, letting users control generated video by picking an action each step.</sub>
- **Playable Environments** — *"Playable Environments: Video Manipulation in Space and Time"*. `CVPR 2022` [![arXiv](https://img.shields.io/badge/arXiv-2203.01914-b31b1b)](https://arxiv.org/abs/2203.01914) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/willi-menapace/PlayableEnvironments)  
  <sub>Extends PVG to 3D with a per-frame environment state manipulated by unsupervised actions and decoded via style-modulated NeRF rendering.</sub>
- **Promptable Game Models** — *"Promptable Game Models: Text-Guided Game Simulation via Masked Diffusion Models"*. `ACM TOG 2024` [![arXiv](https://img.shields.io/badge/arXiv-2303.13472-b31b1b)](https://arxiv.org/abs/2303.13472) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://snap-research.github.io/promptable-game-models/)  
  <sub>Augments neural game models with language action/state prompts via masked diffusion, enabling both low-level play and a goal-driven "director's mode".</sub>

---

## 🚗 Autonomous Driving World Models

> Here the **action is the ego-vehicle's control or trajectory** (steering, speed, waypoints, high-level command). These models generate future driving video — often multi-view — to forecast, plan, simulate, and generate training data.

### Foundational Driving World Models

- **GAIA-1** — *"GAIA-1: A Generative World Model for Autonomous Driving"*. `arXiv 2023` [![arXiv](https://img.shields.io/badge/arXiv-2309.17080-b31b1b)](https://arxiv.org/abs/2309.17080) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://wayve.ai/science/gaia/)  
  <sub>Wayve's 9B autoregressive model tokenizing video and predicting future frames conditioned on past video plus text and ego-action (steering/speed).</sub>
- **GAIA-2** — *"GAIA-2: A Controllable Multi-View Generative World Model for Autonomous Driving"*. `arXiv 2025` [![arXiv](https://img.shields.io/badge/arXiv-2503.20523-b31b1b)](https://arxiv.org/abs/2503.20523) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://wayve.ai/science/gaia/)  
  <sub>Latent-diffusion successor generating high-res multi-camera video conditioned on ego-vehicle dynamics, agent layouts, road semantics, and environment.</sub>
- **Vista** — *"Vista: A Generalizable Driving World Model with High Fidelity and Versatile Controllability"*. `NeurIPS 2024` [![arXiv](https://img.shields.io/badge/arXiv-2405.17398-b31b1b)](https://arxiv.org/abs/2405.17398) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/OpenDriveLab/Vista)  
  <sub>High-fidelity long-horizon predictor controllable from high-level intent (command, goal point) down to low-level maneuvers (trajectory, angle, speed).</sub>
- **GenAD** — *"Generalized Predictive Model for Autonomous Driving"*. `CVPR 2024 (Highlight)` [![arXiv](https://img.shields.io/badge/arXiv-2403.09630-b31b1b)](https://arxiv.org/abs/2403.09630) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/OpenDriveLab/DriveAGI)  
  <sub>First large-scale (2000+ hr OpenDV-2K) video prediction model, adaptable into an action-conditioned predictor where ego trajectory/command conditions video.</sub>
- **DriveDreamer** — *"DriveDreamer: Towards Real-world-driven World Models for Autonomous Driving"*. `ECCV 2024` [![arXiv](https://img.shields.io/badge/arXiv-2309.09777-b31b1b)](https://arxiv.org/abs/2309.09777) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://drivedreamer.github.io/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/JeffWang987/DriveDreamer)  
  <sub>Diffusion world model predicting different future videos conditioned on input driving actions plus text and structured traffic constraints (HDMap, 3D boxes).</sub>
- **DriveDreamer-2** — *"DriveDreamer-2: LLM-Enhanced World Models for Diverse Driving Video Generation"*. `AAAI 2025` [![arXiv](https://img.shields.io/badge/arXiv-2403.06845-b31b1b)](https://arxiv.org/abs/2403.06845) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://drivedreamer2.github.io/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/f1yfisher/DriveDreamer2)  
  <sub>Adds an LLM to turn user text into agent trajectories and HDMaps that condition customized, uncommon multi-view driving video (e.g. sudden cut-ins).</sub>
- **ADriver-I** — *"ADriver-I: A General World Model for Autonomous Driving"*. `arXiv 2023` [![arXiv](https://img.shields.io/badge/arXiv-2311.13549-b31b1b)](https://arxiv.org/abs/2311.13549)  
  <sub>Couples an MLLM with a video diffusion model on interleaved vision-action pairs; the MLLM predicts speed/steering that condition recurrent frame generation.</sub>
- **DrivingWorld** — *"DrivingWorld: Constructing World Model for Autonomous Driving via Video GPT"*. `arXiv 2024` [![arXiv](https://img.shields.io/badge/arXiv-2412.19505-b31b1b)](https://arxiv.org/abs/2412.19505) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://huxiaotaostasy.github.io/DrivingWorld/index.html) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/YvanYin/DrivingWorld)  
  <sub>GPT-style autoregressive model with spatial-temporal fusion jointly generating ego state and 40s+ video, producing different futures from different trajectories.</sub>
- **Doe-1** — *"Doe-1: Closed-Loop Autonomous Driving with Large World Model"*. `arXiv 2024` [![arXiv](https://img.shields.io/badge/arXiv-2412.09627-b31b1b)](https://arxiv.org/abs/2412.09627) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/wzzheng/Doe)  
  <sub>Unified multimodal transformer autoregressively generating perception, prediction, and planning tokens, enabling action-conditioned video alongside VQA and planning.</sub>
- **Epona** — *"Epona: Autoregressive Diffusion World Model for Autonomous Driving"*. `ICCV 2025` [![arXiv](https://img.shields.io/badge/arXiv-2506.24113-b31b1b)](https://arxiv.org/abs/2506.24113) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://kevin-thu.github.io/Epona/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/Kevin-thu/Epona)  
  <sub>Decoupled spatiotemporal autoregressive-diffusion model jointly predicting future trajectory and scene, doubling as a real-time motion planner.</sub>
- **ProphetDWM** — *"ProphetDWM: A Driving World Model for Rolling Out Future Actions and Videos"*. `arXiv 2025` [![arXiv](https://img.shields.io/badge/arXiv-2505.18650-b31b1b)](https://arxiv.org/abs/2505.18650)  
  <sub>End-to-end model with a latent-action module and diffusion transition jointly predicting future actions and video, learning action dynamics rather than requiring given actions.</sub>
- **MaskGWM** — *"MaskGWM: A Generalizable Driving World Model with Video Mask Reconstruction"*. `CVPR 2025` [![arXiv](https://img.shields.io/badge/arXiv-2502.11663-b31b1b)](https://arxiv.org/abs/2502.11663) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/SenseTime-FVG/OpenDWM)  
  <sub>Scalable DiT combining diffusion generation with MAE-style mask reconstruction; long and multi-view variants forecast action-conditioned driving video.</sub>

### Controllable Multi-View and Trajectory-Conditioned Generation

- **Drive-WM** — *"Driving into the Future: Multiview Visual Forecasting and Planning with World Model"*. `CVPR 2024` [![arXiv](https://img.shields.io/badge/arXiv-2311.17918-b31b1b)](https://arxiv.org/abs/2311.17918) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://drive-wm.github.io/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/BraveGroup/Drive-WM)  
  <sub>First world model compatible with end-to-end planners; generates consistent multiview video of multiple futures from distinct ego maneuvers and selects the best trajectory.</sub>
- **MagicDrive** — *"MagicDrive: Street View Generation with Diverse 3D Geometry Control"*. `ICLR 2024` [![arXiv](https://img.shields.io/badge/arXiv-2310.02601-b31b1b)](https://arxiv.org/abs/2310.02601) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://gaoruiyuan.com/magicdrive/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/cure-lab/MagicDrive)  
  <sub>Multi-view street synthesis with cross-view attention conditioned on camera poses, BEV road maps, 3D boxes, and text; ego motion enters via camera-pose sequences.</sub>
- **MagicDriveDiT** — *"MagicDriveDiT: High-Resolution Long Video Generation for Autonomous Driving with Adaptive Control"*. `arXiv 2024` [![arXiv](https://img.shields.io/badge/arXiv-2411.13807-b31b1b)](https://arxiv.org/abs/2411.13807) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://gaoruiyuan.com/magicdrive-v2/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/flymin/MagicDriveDiT)  
  <sub>DiT + flow-matching scaling MagicDrive to 848×1600 / 241-frame multi-view video with spatial-temporal conditioning for geometry and ego-trajectory control.</sub>
- **Panacea** — *"Panacea: Panoramic and Controllable Video Generation for Autonomous Driving"*. `CVPR 2024` [![arXiv](https://img.shields.io/badge/arXiv-2311.16813-b31b1b)](https://arxiv.org/abs/2311.16813) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://panacea-ad.github.io/)  
  <sub>4D-attention two-stage diffusion producing temporally and cross-view consistent panoramic multi-view video controlled by BEV layout sequences (ego motion via trajectory). See also Panacea+ ([2408.07605](https://arxiv.org/abs/2408.07605)).</sub>
- **DrivingDiffusion** — *"DrivingDiffusion: Layout-Guided Multi-View Driving Scene Video Generation"*. `ECCV 2024` [![arXiv](https://img.shields.io/badge/arXiv-2310.07771-b31b1b)](https://arxiv.org/abs/2310.07771) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://drivingdiffusion.github.io/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/shalfun/DrivingDiffusion)  
  <sub>Cascaded multi-view-image, single-view-video, and post-processing pipeline generating multiview driving video controlled by 3D BEV layout sequences.</sub>
- **WoVoGen** — *"WoVoGen: World Volume-aware Diffusion for Controllable Multi-camera Driving Scene Generation"*. `ECCV 2024` [![arXiv](https://img.shields.io/badge/arXiv-2312.02934-b31b1b)](https://arxiv.org/abs/2312.02934) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/fudan-zvg/WoVoGen)  
  <sub>Predicts an explicit future 4D world volume from ego actions, then generates inter-sensor-consistent multi-camera video conditioned on that volume.</sub>
- **Delphi** — *"Unleashing Generalization of End-to-End Autonomous Driving with Controllable Long Video Generation"*. `arXiv 2024` [![arXiv](https://img.shields.io/badge/arXiv-2406.01349-b31b1b)](https://arxiv.org/abs/2406.01349) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://westlake-autolab.github.io/delphi.github.io/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/westlake-autolab/Delphi)  
  <sub>Diffusion model with shared-noise multi-view modeling generating ~40-frame controllable multi-view video to augment end-to-end driving data.</sub>
- **SubjectDrive** — *"SubjectDrive: Scaling Generative Data in Autonomous Driving via Subject Control"*. `arXiv 2024` [![arXiv](https://img.shields.io/badge/arXiv-2403.19438-b31b1b)](https://arxiv.org/abs/2403.19438) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://subjectdrive.github.io/)  
  <sub>Adds a subject-control mechanism to a multi-view video world model so diverse subjects plus BEV/trajectory conditions scale up generative training data.</sub>
- **DreamForge** — *"DreamForge: Motion-Aware Autoregressive Video Generation for Multi-View Driving Scenes"*. `arXiv 2024` [![arXiv](https://img.shields.io/badge/arXiv-2409.04003-b31b1b)](https://arxiv.org/abs/2409.04003) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://pjlab-adg.github.io/DriveArena/dreamforge/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/PJLab-ADG/DriveArena)  
  <sub>Diffusion-based autoregressive generator using motion frames and perspective guidance to produce 200+ frame multi-view video from text, poses, boxes, and layouts.</sub>
- **UniMLVG** — *"UniMLVG: Unified Framework for Multi-view Long Video Generation with Comprehensive Control"*. `arXiv 2024` [![arXiv](https://img.shields.io/badge/arXiv-2412.04842-b31b1b)](https://arxiv.org/abs/2412.04842) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://sensetime-fvg.github.io/UniMLVG/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/SenseTime-FVG/OpenDWM)  
  <sub>Three-stage DiT with cross-frame/cross-view modules generating long multi-view video from text, image, video, 3D boxes, and ego-pose conditions.</sub>
- **InfinityDrive** — *"InfinityDrive: Breaking Time Limits in Driving World Models"*. `arXiv 2024` [![arXiv](https://img.shields.io/badge/arXiv-2412.01522-b31b1b)](https://arxiv.org/abs/2412.01522) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://metadrivescape.github.io/papers_project/InfinityDrive/page.html)  
  <sub>Spatio-temporal co-modeling with memory injection enabling 1500+ frame (2 min) action/trajectory-conditioned 576×1024 driving video.</sub>
- **MiLA** — *"MiLA: Multi-view Intensive-fidelity Long-term Video Generation World Model"*. `arXiv 2025` [![arXiv](https://img.shields.io/badge/arXiv-2503.15875-b31b1b)](https://arxiv.org/abs/2503.15875) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/xiaomi-mlab/mila.github.io)  
  <sub>Coarse-to-(re)fine framework with temporal progressive denoising generating up to one-minute multi-view video conditioned on BEV layout / trajectory.</sub>
- **DrivePhysica** — *"Physical Informed Driving World Model"*. `arXiv 2024` [![arXiv](https://img.shields.io/badge/arXiv-2412.08410-b31b1b)](https://arxiv.org/abs/2412.08410) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://metadrivescape.github.io/papers_project/DrivePhysica/page.html)  
  <sub>Multi-view generator adding coordinate alignment, instance-flow, and box-coordinate guidance so video obeys relative/absolute ego motion and occlusion physics.</sub>
- **GeoDrive** — *"GeoDrive: 3D Geometry-Informed Driving World Model with Precise Action Control"*. `arXiv 2025` [![arXiv](https://img.shields.io/badge/arXiv-2505.22421-b31b1b)](https://arxiv.org/abs/2505.22421) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/antonioo-c/GeoDrive)  
  <sub>Extracts a 3D representation and renders it along the user-specified ego trajectory as an explicit condition for precise action control and object editing.</sub>
- **DriVerse** — *"DriVerse: Navigation World Model for Driving Simulation via Multimodal Trajectory Prompting"*. `ACM MM 2025` [![arXiv](https://img.shields.io/badge/arXiv-2504.18576-b31b1b)](https://arxiv.org/abs/2504.18576) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/shalfun/DriVerse)  
  <sub>Generates driving video from one image plus a future trajectory by tokenizing the trajectory into prompts and projecting the 3D path into 2D motion priors.</sub>
- **Glad** — *"Glad: A Streaming Scene Generator for Autonomous Driving"*. `ICLR 2025` [![arXiv](https://img.shields.io/badge/arXiv-2503.00045-b31b1b)](https://arxiv.org/abs/2503.00045) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/xb534/Glad)  
  <sub>Stable-Diffusion-based streaming simulator using latent variable propagation for frame-by-frame temporally consistent scene generation conditioned on layout/trajectory.</sub>
- **GEM** — *"GEM: A Generalizable Ego-Vision Multimodal World Model"*. `CVPR 2025` [![arXiv](https://img.shields.io/badge/arXiv-2412.11198-b31b1b)](https://arxiv.org/abs/2412.11198) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://vita-epfl.github.io/GEM.github.io/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/vita-epfl/GEM)  
  <sub>Multimodal (RGB+depth) world model trained across driving/egocentric/drone data with explicit control over ego-trajectory, object dynamics, and human poses.</sub>

### Occupancy and 4D World Models

- **OccWorld** — *"OccWorld: Learning a 3D Occupancy World Model for Autonomous Driving"*. `ECCV 2024` [![arXiv](https://img.shields.io/badge/arXiv-2311.16038-b31b1b)](https://arxiv.org/abs/2311.16038) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/wzzheng/OccWorld)  
  <sub>VQVAE-based GPT in 3D semantic occupancy space that jointly forecasts evolving occupancy and the ego-car's future trajectory.</sub>
- **OccSora** — *"OccSora: 4D Occupancy Generation Models as World Simulators"*. `arXiv 2024` [![arXiv](https://img.shields.io/badge/arXiv-2405.20337-b31b1b)](https://arxiv.org/abs/2405.20337) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/wzzheng/OccSora)  
  <sub>4D-scene-tokenizer + diffusion transformer generating 16s 4D semantic occupancy conditioned on a trajectory prompt.</sub>
- **Drive-OccWorld** — *"Driving in the Occupancy World: Vision-Centric 4D Occupancy Forecasting and Planning"*. `AAAI 2025` [![arXiv](https://img.shields.io/badge/arXiv-2408.14197-b31b1b)](https://arxiv.org/abs/2408.14197) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://drive-occworld.github.io/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/yuyang-cloud/Drive-OccWorld)  
  <sub>Vision-centric 4D occupancy+flow forecaster injecting velocity, steering, trajectory, and command as flexible action conditions for controllable generation and planning.</sub>
- **DriveWorld** — *"DriveWorld: 4D Pre-trained Scene Understanding via World Models"*. `CVPR 2024` [![arXiv](https://img.shields.io/badge/arXiv-2405.04390-b31b1b)](https://arxiv.org/abs/2405.04390)  
  <sub>Memory State-Space world model pre-trained on multi-camera video to learn 4D spatio-temporal occupancy/motion representations for detection, tracking, and planning.</sub>
- **NeMo** — *"Neural Volumetric World Models for Autonomous Driving"*. `ECCV 2024` [![Paper](https://img.shields.io/badge/Paper-ECCV-8a2be2)](https://link.springer.com/chapter/10.1007/978-3-031-73247-8_12)  
  <sub>Self-supervised volumetric world model fusing RGB reconstruction and occupancy/motion-flow prediction into 4D features for imitation-based ego action planning.</sub>

### Driving Simulation and Reconstruction

- **DriveArena** — *"DriveArena: A Closed-loop Generative Simulation Platform for Autonomous Driving"*. `arXiv 2024` [![arXiv](https://img.shields.io/badge/arXiv-2408.00415-b31b1b)](https://arxiv.org/abs/2408.00415) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://pjlab-adg.github.io/DriveArena/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/PJLab-ADG/DriveArena)  
  <sub>Closed-loop platform pairing a Traffic Manager with a generative "World Dreamer"; agent trajectories update the layout that re-conditions the next frames.</sub>
- **DriveDreamer4D** — *"DriveDreamer4D: World Models Are Effective Data Machines for 4D Driving Scene Representation"*. `CVPR 2025` [![arXiv](https://img.shields.io/badge/arXiv-2410.13571-b31b1b)](https://arxiv.org/abs/2410.13571) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://drivedreamer4d.github.io/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/GigaAI-research/DriveDreamer4D)  
  <sub>Uses a video world model as a data machine to synthesize novel-trajectory videos (lane change, acceleration) to improve 4D Gaussian reconstruction.</sub>
- **ReconDreamer** — *"ReconDreamer: Crafting World Models for Driving Scene Reconstruction via Online Restoration"*. `CVPR 2025` [![arXiv](https://img.shields.io/badge/arXiv-2411.19548-b31b1b)](https://arxiv.org/abs/2411.19548) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://recondreamer.github.io/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/GigaAI-research/ReconDreamer)  
  <sub>Integrates world-model priors via online restoration plus progressive data update to render large ego maneuvers for closed-loop simulation.</sub>
- **ReconDreamer++** — *"ReconDreamer++: Harmonizing Generative and Reconstructive Models for Driving Scene Representation"*. `arXiv 2025` [![arXiv](https://img.shields.io/badge/arXiv-2503.18438-b31b1b)](https://arxiv.org/abs/2503.18438) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://recondreamer-plus.github.io/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/GigaAI-research/ReconDreamer-Plus)  
  <sub>Adds a Novel Trajectory Deformable Network bridging the gap between synthesized novel-trajectory views and sensor data for better novel-view rendering.</sub>
- **MagicDrive3D** — *"MagicDrive3D: Controllable 3D Generation for Any-View Rendering in Street Scenes"*. `arXiv 2024` [![arXiv](https://img.shields.io/badge/arXiv-2405.14475-b31b1b)](https://arxiv.org/abs/2405.14475) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://gaoruiyuan.com/magicdrive3d/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/flymin/MagicDrive3D)  
  <sub>Trains a controllable video generator (BEV maps, 3D objects, text) then reconstructs a 3D Gaussian scene from generated frames for any-view rendering.</sub>
- **Nexus** — *"Decoupled Diffusion Sparks Adaptive Scene Generation"*. `ICCV 2025` [![arXiv](https://img.shields.io/badge/arXiv-2504.10485-b31b1b)](https://arxiv.org/abs/2504.10485) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/OpenDriveLab/Nexus)  
  <sub>Noise-decoupled token-level diffusion steering generation with low-noise goals while ingesting environment updates for reactive goal-conditioned closed-loop simulation.</sub>
- **Cosmos-Drive-Dreams** — *"Cosmos-Drive-Dreams: Scalable Synthetic Driving Data Generation with World Foundation Models"*. `arXiv 2025` [![arXiv](https://img.shields.io/badge/arXiv-2506.09042-b31b1b)](https://arxiv.org/abs/2506.09042) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://research.nvidia.com/labs/toronto-ai/cosmos_drive_dreams/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/nv-tlabs/Cosmos-Drive-Dreams)  
  <sub>NVIDIA Cosmos-Drive suite generating controllable, multi-view, spatiotemporally consistent driving video (conditioned on HDMap/trajectory) for edge-case training data.</sub>
- **HoloDrive** — *"HoloDrive: Holistic 2D-3D Multi-Modal Street Scene Generation"*. `arXiv 2024` [![arXiv](https://img.shields.io/badge/arXiv-2412.01407-b31b1b)](https://arxiv.org/abs/2412.01407)  
  <sub>Jointly generates camera images and LiDAR point clouds with BEV-camera transforms and a temporal extension predicting future multi-modal scenes.</sub>

---

## 🎥 General Controllable and Interactive Video Generation

> Domain-agnostic methods where the **action is a camera pose, motion trajectory, drag, or free-text instruction**, plus general interactive world models and the real-time / long-horizon machinery that makes interactive generation feasible.

### Camera and Motion-Controlled Video Generation

- **MotionCtrl** — *"MotionCtrl: A Unified and Flexible Motion Controller for Video Generation"*. `SIGGRAPH 2024` [![arXiv](https://img.shields.io/badge/arXiv-2312.03641-b31b1b)](https://arxiv.org/abs/2312.03641) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://wzhouxiff.github.io/projects/MotionCtrl/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/TencentARC/MotionCtrl)  
  <sub>Unified controller independently conditioning camera poses and object trajectories for video diffusion models.</sub>
- **CameraCtrl** — *"CameraCtrl: Enabling Camera Control for Text-to-Video Generation"*. `ICLR 2025` [![arXiv](https://img.shields.io/badge/arXiv-2404.02101-b31b1b)](https://arxiv.org/abs/2404.02101) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://hehao13.github.io/projects-CameraCtrl/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/hehao13/CameraCtrl)  
  <sub>Plug-and-play camera-pose encoder using Plücker embeddings injected into the temporal attention of a text-to-video diffusion model.</sub>
- **CameraCtrl II** — *"CameraCtrl II: Dynamic Scene Exploration via Camera-controlled Video Diffusion Models"*. `ICCV 2025` [![arXiv](https://img.shields.io/badge/arXiv-2503.10592-b31b1b)](https://arxiv.org/abs/2503.10592)  
  <sub>Extends camera control to large-scale dynamic scene exploration with iterative trajectory-conditioned clip generation.</sub>
- **DragNUWA** — *"DragNUWA: Fine-grained Control in Video Generation by Integrating Text, Image, and Trajectory"*. `arXiv 2023` [![arXiv](https://img.shields.io/badge/arXiv-2308.08089-b31b1b)](https://arxiv.org/abs/2308.08089) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://www.microsoft.com/en-us/research/project/dragnuwa/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/ProjectNUWA/DragNUWA)  
  <sub>Open-domain video generation controlled jointly by text, image, and user-drawn drag trajectories.</sub>
- **Motion-I2V** — *"Motion-I2V: Consistent and Controllable Image-to-Video Generation with Explicit Motion Modeling"*. `SIGGRAPH 2024` [![arXiv](https://img.shields.io/badge/arXiv-2401.15977-b31b1b)](https://arxiv.org/abs/2401.15977)  
  <sub>Two-stage image-to-video with an explicit motion-field predictor enabling sparse-trajectory and region motion control.</sub>
- **Boximator** — *"Boximator: Generating Rich and Controllable Motions for Video Synthesis"*. `ICML 2024` [![arXiv](https://img.shields.io/badge/arXiv-2402.01566-b31b1b)](https://arxiv.org/abs/2402.01566)  
  <sub>Fine-grained motion control via hard/soft bounding-box constraints defining object positions and paths.</sub>
- **Direct-a-Video** — *"Direct-a-Video: Customized Video Generation with User-Directed Camera Movement and Object Motion"*. `SIGGRAPH 2024` [![arXiv](https://img.shields.io/badge/arXiv-2402.03162-b31b1b)](https://arxiv.org/abs/2402.03162)  
  <sub>Independently directs multi-object motion and camera pan/zoom in customized video generation.</sub>
- **DragAnything** — *"DragAnything: Motion Control for Anything using Entity Representation"*. `ECCV 2024` [![arXiv](https://img.shields.io/badge/arXiv-2403.07420-b31b1b)](https://arxiv.org/abs/2403.07420) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://weijiawu.github.io/draganything_page/)  
  <sub>Uses diffusion latent entity representations to give precise drag-based motion control for any object.</sub>
- **CamCo** — *"CamCo: Camera-Controllable 3D-Consistent Image-to-Video Generation"*. `arXiv 2024` [![arXiv](https://img.shields.io/badge/arXiv-2406.02509-b31b1b)](https://arxiv.org/abs/2406.02509) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://ir1d.github.io/CamCo/)  
  <sub>Parameterizes camera pose with Plücker coordinates and adds epipolar attention for 3D-consistent image-to-video.</sub>
- **CamTrol** — *"Training-free Camera Control for Video Generation"*. `arXiv 2024` [![arXiv](https://img.shields.io/badge/arXiv-2406.10126-b31b1b)](https://arxiv.org/abs/2406.10126) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://lifedecoder.github.io/CamTrol/)  
  <sub>Training-free camera control modeling motion as 3D point-cloud rendering and exploiting noisy-latent layout priors.</sub>
- **MotionBooth** — *"MotionBooth: Motion-Aware Customized Text-to-Video Generation"*. `NeurIPS 2024` [![arXiv](https://img.shields.io/badge/arXiv-2406.17758-b31b1b)](https://arxiv.org/abs/2406.17758)  
  <sub>Fine-tunes a text-to-video model on a subject and controls both object motion (attention maps) and camera motion (latent shift).</sub>
- **Image Conductor** — *"Image Conductor: Precision Control for Interactive Video Synthesis"*. `AAAI 2025` [![arXiv](https://img.shields.io/badge/arXiv-2406.15339-b31b1b)](https://arxiv.org/abs/2406.15339)  
  <sub>Separates camera and object motion via dedicated LoRAs for precise trajectory-driven interactive video synthesis.</sub>
- **VD3D** — *"VD3D: Taming Large Video Diffusion Transformers for 3D Camera Control"*. `arXiv 2024` [![arXiv](https://img.shields.io/badge/arXiv-2407.12781-b31b1b)](https://arxiv.org/abs/2407.12781)  
  <sub>Adds spatiotemporal camera conditioning (ControlNet-style Plücker tokens) to large video diffusion transformers.</sub>
- **Collaborative Video Diffusion (CVD)** — *"Collaborative Video Diffusion: Consistent Multi-video Generation with Camera Control"*. `NeurIPS 2024` [![arXiv](https://img.shields.io/badge/arXiv-2405.17414-b31b1b)](https://arxiv.org/abs/2405.17414) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://collaborativevideodiffusion.github.io/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/CollaborativeVideoDiffusion/CVD)  
  <sub>Generates multiple camera-controlled videos of the same scene kept consistent via cross-video epipolar attention.</sub>
- **Cavia** — *"Cavia: Camera-controllable Multi-view Video Diffusion with View-Integrated Attention"*. `arXiv 2024` [![arXiv](https://img.shields.io/badge/arXiv-2410.10774-b31b1b)](https://arxiv.org/abs/2410.10774)  
  <sub>View-integrated attention extending spatial/temporal modules for camera-controllable, multi-view-consistent video.</sub>
- **AC3D** — *"AC3D: Analyzing and Improving 3D Camera Control in Video Diffusion Transformers"*. `CVPR 2025` [![arXiv](https://img.shields.io/badge/arXiv-2411.18673-b31b1b)](https://arxiv.org/abs/2411.18673)  
  <sub>Analyzes camera motion as a low-frequency signal to improve 3D camera control with fewer trainable parameters.</sub>
- **SynCamMaster** — *"SynCamMaster: Synchronizing Multi-Camera Video Generation from Diverse Viewpoints"*. `ICLR 2025` [![arXiv](https://img.shields.io/badge/arXiv-2412.07760-b31b1b)](https://arxiv.org/abs/2412.07760)  
  <sub>Plug-and-play module enabling synchronized multi-camera video generation from diverse viewpoints.</sub>
- **GS-DiT** — *"GS-DiT: Advancing Video Generation with Pseudo 4D Gaussian Fields"*. `arXiv 2025` [![arXiv](https://img.shields.io/badge/arXiv-2501.02690-b31b1b)](https://arxiv.org/abs/2501.02690) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://wkbian.github.io/Projects/GS-DiT/)  
  <sub>Builds a pseudo-4D Gaussian field via dense 3D point tracking to guide a DiT for 4D / camera-controllable video.</sub>
- **Go-with-the-Flow** — *"Go-with-the-Flow: Motion-Controllable Video Diffusion Models Using Real-Time Warped Noise"*. `CVPR 2025` [![arXiv](https://img.shields.io/badge/arXiv-2501.08331-b31b1b)](https://arxiv.org/abs/2501.08331)  
  <sub>Replaces i.i.d. noise with optical-flow-warped correlated noise to control local, camera, and transfer motion.</sub>
- **ReCamMaster** — *"ReCamMaster: Camera-Controlled Generative Rendering from A Single Video"*. `ICCV 2025` [![arXiv](https://img.shields.io/badge/arXiv-2503.11647-b31b1b)](https://arxiv.org/abs/2503.11647) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://jianhongbai.github.io/ReCamMaster/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/KlingAIResearch/ReCamMaster)  
  <sub>Re-renders a single input video's dynamic scene along novel camera trajectories via video-conditioned text-to-video.</sub>
- **TrajectoryCrafter** — *"TrajectoryCrafter: Redirecting Camera Trajectory for Monocular Videos via Diffusion Models"*. `ICCV 2025 (Oral)` [![arXiv](https://img.shields.io/badge/arXiv-2503.05638-b31b1b)](https://arxiv.org/abs/2503.05638) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/TrajectoryCrafter/TrajectoryCrafter)  
  <sub>Dual-stream diffusion disentangling deterministic view transforms from content generation to redirect camera paths.</sub>
- **Uni3C** — *"Uni3C: Unifying Precisely 3D-Enhanced Camera and Human Motion Controls for Video Generation"*. `arXiv 2025` [![arXiv](https://img.shields.io/badge/arXiv-2504.14899-b31b1b)](https://arxiv.org/abs/2504.14899)  
  <sub>Unifies 3D-enhanced camera control and human-motion control in a single video generation framework.</sub>
- **ViewCrafter** — *"ViewCrafter: Taming Video Diffusion Models for High-fidelity Novel View Synthesis"*. `arXiv 2024` [![arXiv](https://img.shields.io/badge/arXiv-2409.02048-b31b1b)](https://arxiv.org/abs/2409.02048) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/Drexubery/ViewCrafter)  
  <sub>Combines point-based 3D priors with video diffusion for high-fidelity, pose-controllable novel view synthesis.</sub>

### General Interactive World Models

- **Pandora** — *"Pandora: Towards General World Model with Natural Language Actions and Video States"*. `arXiv 2024` [![arXiv](https://img.shields.io/badge/arXiv-2406.09455-b31b1b)](https://arxiv.org/abs/2406.09455) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://world-model.maitrix.org/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/maitrix-org/Pandora)  
  <sub>Hybrid autoregressive-diffusion world model simulating future video states controllable in real time by free-text actions across domains.</sub>
- **WorldDreamer** — *"WorldDreamer: Towards General World Models for Video Generation via Predicting Masked Tokens"*. `arXiv 2024` [![arXiv](https://img.shields.io/badge/arXiv-2401.09985-b31b1b)](https://arxiv.org/abs/2401.09985) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://world-dreamer.github.io/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/JeffWang987/WorldDreamer)  
  <sub>Tokenizes video and predicts masked tokens with multimodal prompts, supporting action-to-video alongside text/image-to-video across natural and driving scenes.</sub>
- **Owl-1** — *"Owl-1: Omni World Model for Consistent Long Video Generation"*. `arXiv 2024` [![arXiv](https://img.shields.io/badge/arXiv-2412.09600-b31b1b)](https://arxiv.org/abs/2412.09600)  
  <sub>Models long-term world dynamics in a latent state decoded into consistent long videos.</sub>
- **WonderJourney** — *"WonderJourney: Going from Anywhere to Anywhere"*. `CVPR 2024` [![arXiv](https://img.shields.io/badge/arXiv-2312.03884-b31b1b)](https://arxiv.org/abs/2312.03884) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://kovenyu.com/WonderJourney/)  
  <sub>Generates a perpetual sequence of connected, diverse 3D scenes for explorable journey-style world generation.</sub>
- **WonderWorld** — *"WonderWorld: Interactive 3D Scene Generation from a Single Image"*. `CVPR 2025` [![arXiv](https://img.shields.io/badge/arXiv-2406.09394-b31b1b)](https://arxiv.org/abs/2406.09394) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://kovenyu.com/wonderworld/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/KovenYu/WonderWorld)  
  <sub>Interactive single-image 3D world generation using Fast Layered Gaussian Surfels in under 10 seconds per scene.</sub>
- **The Matrix** — *"The Matrix: Infinite-Horizon World Generation with Real-Time Moving Control"*. `arXiv 2024` [![arXiv](https://img.shields.io/badge/arXiv-2412.03568-b31b1b)](https://arxiv.org/abs/2412.03568) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://thematrix1999.github.io/)  
  <sub>A 2.7B diffusion model generating infinite-horizon 720p driving/navigation video at 16 FPS with real-time movement control.</sub>
- **Yume** — *"Yume: An Interactive World Generation Model"*. `arXiv 2025` [![arXiv](https://img.shields.io/badge/arXiv-2507.17744-b31b1b)](https://arxiv.org/abs/2507.17744) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://stdstu12.github.io/YUME-Project/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/stdstu12/YUME)  
  <sub>Masked video diffusion transformer turning an image into a keyboard-explorable interactive world.</sub>
- **HunyuanWorld 1.0** — *"HunyuanWorld 1.0: Generating Immersive, Explorable, Interactive 3D Worlds from Words or Pixels"*. `arXiv 2025` [![arXiv](https://img.shields.io/badge/arXiv-2507.21809-b31b1b)](https://arxiv.org/abs/2507.21809) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/Tencent-Hunyuan/HunyuanWorld-1.0)  
  <sub>Generates explorable 3D worlds via a semantically-layered mesh representation from panoramic proxies.</sub>
- **Voyager** — *"Voyager: Long-Range and World-Consistent Video Diffusion for Explorable 3D Scene Generation"*. `arXiv 2025` [![arXiv](https://img.shields.io/badge/arXiv-2506.04225-b31b1b)](https://arxiv.org/abs/2506.04225) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/Tencent-Hunyuan/HunyuanWorld-Voyager)  
  <sub>Camera-conditioned RGBD video diffusion producing world-consistent point-cloud sequences with real-time 3D reconstruction.</sub>
- **Matrix-3D** — *"Matrix-3D: Omnidirectional Explorable 3D World Generation"*. `arXiv 2025` [![arXiv](https://img.shields.io/badge/arXiv-2508.08086-b31b1b)](https://arxiv.org/abs/2508.08086) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://matrix-3d.github.io/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/SkyworkAI/Matrix-3D)  
  <sub>Trajectory-guided panoramic video diffusion plus panoramic reconstruction for wide-coverage explorable 3D worlds.</sub>

### Real-Time and Long-Horizon Interactive Video

- **Diffusion Forcing** — *"Diffusion Forcing: Next-token Prediction Meets Full-Sequence Diffusion"*. `NeurIPS 2024` [![arXiv](https://img.shields.io/badge/arXiv-2407.01392-b31b1b)](https://arxiv.org/abs/2407.01392) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://boyuan.space/diffusion-forcing/)  
  <sub>Trains sequence diffusion with independent per-token noise levels, enabling causal action-conditioned rollouts of video past the training horizon — a backbone for many interactive world models.</sub>
- **CausVid** — *"From Slow Bidirectional to Fast Autoregressive Video Diffusion Models"*. `CVPR 2025` [![arXiv](https://img.shields.io/badge/arXiv-2412.07772-b31b1b)](https://arxiv.org/abs/2412.07772) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/tianweiy/CausVid)  
  <sub>Distills a bidirectional diffusion model into a few-step causal autoregressive generator for low-latency streaming video.</sub>
- **History-Guided Video Diffusion** — *"History-Guided Video Diffusion"*. `ICML 2025` [![arXiv](https://img.shields.io/badge/arXiv-2502.06764-b31b1b)](https://arxiv.org/abs/2502.06764)  
  <sub>Diffusion Forcing Transformer with history guidance conditioning on variable history for stable extremely-long rollouts.</sub>
- **MAGI-1** — *"MAGI-1: Autoregressive Video Generation at Scale"*. `arXiv 2025` [![arXiv](https://img.shields.io/badge/arXiv-2505.13211-b31b1b)](https://arxiv.org/abs/2505.13211) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/SandAI-org/MAGI-1)  
  <sub>A 24B chunk-wise autoregressive diffusion world model with monotonic per-chunk noise for streaming, controllable generation.</sub>
- **Self-Forcing** — *"Self Forcing: Bridging the Train-Test Gap in Autoregressive Video Diffusion"*. `NeurIPS 2025 (Spotlight)` [![arXiv](https://img.shields.io/badge/arXiv-2506.08009-b31b1b)](https://arxiv.org/abs/2506.08009) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/guandeh17/Self-Forcing)  
  <sub>Aligns training with inference via student self-rollout and a rolling KV cache for sub-second real-time streaming video.</sub>
- **FramePack** — *"Packing Input Frame Context in Next-Frame Prediction Models for Video Generation"*. `arXiv 2025` [![arXiv](https://img.shields.io/badge/arXiv-2504.12626-b31b1b)](https://arxiv.org/abs/2504.12626)  
  <sub>Compresses frame context to a fixed length with drift prevention, enabling thousands-of-frame next-frame-prediction video.</sub>

---

## 🗂️ Datasets

Datasets frequently used to train and evaluate action-conditioned video models, grouped by domain.

**Robotics & Embodied**

- **Open X-Embodiment / RT-X** — *"Open X-Embodiment: Robotic Learning Datasets and RT-X Models"*. `ICRA 2024` [![arXiv](https://img.shields.io/badge/arXiv-2310.08864-b31b1b)](https://arxiv.org/abs/2310.08864) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://robotics-transformer-x.github.io/)  
  <sub>Largest open real-robot dataset pooling 60 datasets (1M+ trajectories, 22 embodiments) for cross-embodiment learning.</sub>
- **BridgeData V2** — *"BridgeData V2: A Dataset for Robot Learning at Scale"*. `CoRL 2023` [![arXiv](https://img.shields.io/badge/arXiv-2308.12952-b31b1b)](https://arxiv.org/abs/2308.12952) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://rail-berkeley.github.io/bridgedata/)  
  <sub>60,096 language/goal-conditioned manipulation trajectories across 24 environments on a low-cost robot.</sub>
- **DROID** — *"DROID: A Large-Scale In-The-Wild Robot Manipulation Dataset"*. `RSS 2024` [![arXiv](https://img.shields.io/badge/arXiv-2403.12945-b31b1b)](https://arxiv.org/abs/2403.12945) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://droid-dataset.github.io/)  
  <sub>76k in-the-wild teleoperated manipulation trajectories (564 scenes, 84 tasks) with multi-view RGB and language.</sub>
- **RoboNet** — *"RoboNet: Large-Scale Multi-Robot Learning"*. `CoRL 2019` [![arXiv](https://img.shields.io/badge/arXiv-1910.11215-b31b1b)](https://arxiv.org/abs/1910.11215) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/SudeepDasari/RoboNet)  
  <sub>15M video frames across 7 robot platforms, a staple for action-conditioned video prediction / visual foresight.</sub>
- **Language-Table** — *"Interactive Language: Talking to Robots in Real Time"*. `RA-L 2023` [![arXiv](https://img.shields.io/badge/arXiv-2210.06407-b31b1b)](https://arxiv.org/abs/2210.06407) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/google-research/language-table)  
  <sub>~600k language-annotated tabletop manipulation trajectories with a real-time language-instructable benchmark.</sub>
- **Ego4D** — *"Ego4D: Around the World in 3,000 Hours of Egocentric Video"*. `CVPR 2022` [![arXiv](https://img.shields.io/badge/arXiv-2110.07058-b31b1b)](https://arxiv.org/abs/2110.07058) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://ego4d-data.org/)  
  <sub>3,670 hours of daily-life egocentric video across 74 locations, widely used for egocentric world modeling.</sub>
- **Something-Something** — *"The 'Something Something' Video Database for Learning and Evaluating Visual Common Sense"*. `ICCV 2017` [![arXiv](https://img.shields.io/badge/arXiv-1706.04261-b31b1b)](https://arxiv.org/abs/1706.04261)  
  <sub>100k+ videos over 174 human-object interaction action templates for fine-grained temporal/action understanding.</sub>

**Autonomous Driving**

- **nuScenes** — *"nuScenes: A Multimodal Dataset for Autonomous Driving"*. `CVPR 2020` [![arXiv](https://img.shields.io/badge/arXiv-1903.11027-b31b1b)](https://arxiv.org/abs/1903.11027)  
  <sub>Multimodal driving dataset (camera, LiDAR, radar) ubiquitously used to condition and evaluate driving world models.</sub>
- **Waymo Open Dataset** — *"Scalability in Perception for Autonomous Driving: Waymo Open Dataset"*. `CVPR 2020` [![arXiv](https://img.shields.io/badge/arXiv-1912.04838-b31b1b)](https://arxiv.org/abs/1912.04838)  
  <sub>Large, diverse driving dataset (1150 20s scenes) with synchronized LiDAR/camera and exhaustive 3D annotations.</sub>
- **nuPlan** — *"nuPlan: A Closed-Loop ML-Based Planning Benchmark for Autonomous Vehicles"*. `arXiv 2021` [![arXiv](https://img.shields.io/badge/arXiv-2106.11810-b31b1b)](https://arxiv.org/abs/2106.11810)  
  <sub>Large-scale (~1500h) closed-loop planning benchmark, used for trajectory-conditioned simulation.</sub>
- **OpenDV-2K** — *"GenAD: Generalized Predictive Model for Autonomous Driving"*. `CVPR 2024` [![arXiv](https://img.shields.io/badge/arXiv-2403.09630-b31b1b)](https://arxiv.org/abs/2403.09630) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/OpenDriveLab/DriveAGI)  
  <sub>2059-hour multimodal driving video dataset accompanying a generalized action/language-conditioned predictive model.</sub>

**Games**

- **VPT** — *"Video PreTraining (VPT): Learning to Act by Watching Unlabeled Online Videos"*. `NeurIPS 2022` [![arXiv](https://img.shields.io/badge/arXiv-2206.11795-b31b1b)](https://arxiv.org/abs/2206.11795) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/openai/Video-Pre-Training)  
  <sub>Semi-supervised inverse-dynamics labeling of 70k+ hours of Minecraft video, a key action-labeled gameplay dataset.</sub>
- **MineDojo** — *"MineDojo: Building Open-Ended Embodied Agents with Internet-Scale Knowledge"*. `NeurIPS 2022 (D&B)` [![arXiv](https://img.shields.io/badge/arXiv-2206.08853-b31b1b)](https://arxiv.org/abs/2206.08853) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://minedojo.org/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/MineDojo/MineDojo)  
  <sub>Minecraft simulation suite with an internet-scale knowledge base (730k videos, 7k wiki pages, 340k Reddit posts).</sub>
- **DIAMOND (CS:GO / Atari)** — *"Diffusion for World Modeling: Visual Details Matter in Atari"*. `NeurIPS 2024` [![arXiv](https://img.shields.io/badge/arXiv-2405.12399-b31b1b)](https://arxiv.org/abs/2405.12399) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/eloialonso/diamond)  
  <sub>Ships a CS:GO dataset of 5.5M frames (95h) plus Atari, the data behind its real-time neural game engine.</sub>

---

## 📊 Benchmarks and Evaluation

- **VBench** — *"VBench: Comprehensive Benchmark Suite for Video Generative Models"*. `CVPR 2024` [![arXiv](https://img.shields.io/badge/arXiv-2311.17982-b31b1b)](https://arxiv.org/abs/2311.17982) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://vchitect.github.io/VBench-project/)  
  <sub>Decomposes video-generation quality into 16 disentangled, human-preference-aligned dimensions.</sub>
- **VBench-2.0** — *"VBench-2.0: Advancing Video Generation Benchmark Suite for Intrinsic Faithfulness"*. `arXiv 2025` [![arXiv](https://img.shields.io/badge/arXiv-2503.21755-b31b1b)](https://arxiv.org/abs/2503.21755)  
  <sub>Evaluates intrinsic faithfulness across human fidelity, controllability, creativity, physics, and commonsense.</sub>
- **EvalCrafter** — *"EvalCrafter: Benchmarking and Evaluating Large Video Generation Models"*. `CVPR 2024` [![arXiv](https://img.shields.io/badge/arXiv-2310.11440-b31b1b)](https://arxiv.org/abs/2310.11440) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://evalcrafter.github.io/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/evalcrafter/EvalCrafter)  
  <sub>700-prompt benchmark with 17 objective metrics across visual, content, motion, and text-video alignment.</sub>
- **WorldModelBench** — *"WorldModelBench: Judging Video Generation Models As World Models"*. `arXiv 2025` [![arXiv](https://img.shields.io/badge/arXiv-2502.20694-b31b1b)](https://arxiv.org/abs/2502.20694) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/WorldModelBench-Team/WorldModelBench)  
  <sub>350 condition pairs over 7 application domains scoring instruction following and physics adherence with a trained judger.</sub>
- **WorldScore** — *"WorldScore: A Unified Evaluation Benchmark for World Generation"*. `arXiv 2025` [![arXiv](https://img.shields.io/badge/arXiv-2504.00983-b31b1b)](https://arxiv.org/abs/2504.00983)  
  <sub>Decomposes world generation into next-scene tasks with camera-trajectory layouts, scoring controllability, quality, and dynamics.</sub>
- **WorldSimBench** — *"WorldSimBench: Towards Video Generation Models as World Simulators"*. `arXiv 2024` [![arXiv](https://img.shields.io/badge/arXiv-2410.18072-b31b1b)](https://arxiv.org/abs/2410.18072) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://iranqin.github.io/WorldSimBench.github.io/)  
  <sub>Dual explicit-perceptual and implicit-manipulative evaluation of video models acting as actionable world simulators.</sub>
- **EWMBench** — *"EWMBench: Evaluating Scene, Motion, and Semantic Quality in Embodied World Models"*. `arXiv 2025` [![arXiv](https://img.shields.io/badge/arXiv-2505.09694-b31b1b)](https://arxiv.org/abs/2505.09694)  
  <sub>Benchmarks embodied world models on scene consistency, motion correctness, and semantic alignment.</sub>
- **ACT-Bench** — *"ACT-Bench: Towards Action Controllable World Models for Autonomous Driving"*. `arXiv 2024` [![arXiv](https://img.shields.io/badge/arXiv-2412.05337-b31b1b)](https://arxiv.org/abs/2412.05337) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://turingmotors.github.io/actbench/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/turingmotors/ACT-Bench)  
  <sub>Quantifies trajectory action-fidelity of driving world models, pairing nuScenes context with future trajectories.</sub>
- **Physics-IQ** — *"Do Generative Video Models Understand Physical Principles?"*. `WACV 2026` [![arXiv](https://img.shields.io/badge/arXiv-2501.09038-b31b1b)](https://arxiv.org/abs/2501.09038) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://physics-iq.github.io/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/google-deepmind/physics-IQ-benchmark)  
  <sub>396 real-video benchmark testing physical understanding (fluids, optics, mechanics, magnetism, thermodynamics).</sub>
- **VideoPhy** — *"VideoPhy: Evaluating Physical Commonsense for Video Generation"*. `arXiv 2024` [![arXiv](https://img.shields.io/badge/arXiv-2406.03520-b31b1b)](https://arxiv.org/abs/2406.03520) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/Hritikbansal/videophy)  
  <sub>688-prompt benchmark for physical-commonsense adherence with the VideoCon-Physics auto-evaluator.</sub>
- **VideoPhy-2** — *"VideoPhy-2: A Challenging Action-Centric Physical Commonsense Evaluation"*. `arXiv 2025` [![arXiv](https://img.shields.io/badge/arXiv-2503.06800-b31b1b)](https://arxiv.org/abs/2503.06800)  
  <sub>3,940-prompt action-centric extension scoring physical plausibility on a 5-point scale.</sub>
- **PhyGenBench** — *"Towards World Simulator: Crafting Physical Commonsense-Based Benchmark for Video Generation"*. `arXiv 2024` [![arXiv](https://img.shields.io/badge/arXiv-2410.05363-b31b1b)](https://arxiv.org/abs/2410.05363) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://phygenbench123.github.io/) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](https://github.com/OpenGVLab/PhyGenBench)  
  <sub>160 prompts over 27 physical laws with the hierarchical PhyGenEval automated evaluator.</sub>
- **ChronoMagic-Bench** — *"ChronoMagic-Bench: A Benchmark for Metamorphic Evaluation of Text-to-Time-lapse Video Generation"*. `NeurIPS 2024 (D&B)` [![arXiv](https://img.shields.io/badge/arXiv-2406.18522-b31b1b)](https://arxiv.org/abs/2406.18522) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](https://pku-yuangroup.github.io/ChronoMagic-Bench/)  
  <sub>Benchmarks metamorphic amplitude and temporal coherence of time-lapse generation via MTScore and CHScore.</sub>

---

## 🔗 Related Awesome Lists

- [Awesome World Models](https://github.com/knightnemo/Awesome-World-Models) — broad world-model list across embodied AI, driving, NLP, and agents.
- [Awesome World Model for Autonomous Driving](https://github.com/LMD0311/Awesome-World-Model) — driving-focused world models.
- [Awesome World Models for Robotics](https://github.com/leofan90/Awesome-World-Models) — robotics-focused world models.
- [Awesome Controllable Video Generation](https://github.com/mayuelala/Awesome-Controllable-Video-Generation) — companion to the controllable-video survey.
- [Awesome Text-to-Video Generation](https://github.com/soraw-ai/Awesome-Text-to-Video-Generation) — general text-to-video.
- [Awesome Video Diffusion](https://github.com/showlab/Awesome-Video-Diffusion) — video diffusion models broadly.
- [Awesome Game Generation](https://github.com/JingyeChen/awesome-game-generation) — generative game / interactive-environment works.

---

## 🤝 Contributing

Contributions are warmly welcomed! Please read [CONTRIBUTING.md](CONTRIBUTING.md) for the entry format, badge templates, and inclusion criteria, then open a Pull Request or Issue. Corrections (wrong links, IDs, venues) are just as valuable as new additions.

This list is organized to put **Robotics & Embodied AI** first by design; within each subsection, entries are ordered roughly by influence and recency.

---

## ⭐ Citation

If this list is useful for your research, please consider giving it a star ⭐ and citing it:

```bibtex
@misc{awesome_action_conditioned_video_gen,
  title        = {Awesome Action-Conditioned Video Generation},
  author       = {Contributors},
  howpublished = {\url{https://github.com/<your-username>/awesome-action-conditioned-video-gen}},
  year         = {2026},
  note         = {A curated list of action-conditioned video generation models}
}
```

---

## 🙏 Acknowledgements

This list draws structure and inspiration from [Awesome World Models](https://github.com/knightnemo/Awesome-World-Models) and the broader [Awesome](https://github.com/sindresorhus/awesome) ecosystem. All credit belongs to the authors of the listed works. Released under [CC0 1.0](LICENSE) — to the extent possible under law, contributors have waived all copyright to this compilation.

<div align="center">

**[⬆ Back to top](#awesome-action-conditioned-video-generation)**

_Made with care for the action-conditioned video generation community._

</div>
