---
# Machine-readable fields for downstream agents / dashboards.
stage: early-research   # exploration | early-research | applied-research | productization | shipped
research-area: agents   # Agentic Discovery & Creation | Models & Foundations | Trust & safety, security | Health & Biology Sciences | Society & Economy
last-updated: 2026-05-14
---

# SigmaCollab

**Team:** Interactive Multimodal Futures / Future Experiences / MSR Americas\
**Contributors:** Sean Andrist, Dan Bohus, Ann Paradiso, Nick Saw, Maia Stiber

---

## What it is

__`SigmaCollab`__ is a dataset that enables research on human-AI physically situated collaboration. The dataset consists of a set of 85 sessions in which untrained participants were guided by a mixed-reality assistive AI agent in performing procedural tasks in the physical world, plus an additional 8 sessions in which the system guided an expert in performing the same tasks.

The dataset, described in detail in [this arxiv paper](https://arxiv.org/abs/2511.02560), was collected with an open-source mixed-reality AI application called [Sigma](https://github.com/microsoft/psi/blob/master/Applications/Sigma/Readme.md).

## Core idea

__`SigmaCollab`__'s value-proposition lies in its _application-driven_ and _interactive_ nature. The data collection approach, in which participants interact with an AI application surfaces novel challenges that are not present in non-interactive datasets. As users engage with the system while pursuing meaningful and varied goals, the approach yields data with greater ecological validity. Finally, the [open-source nature of the AI application](https://github.com/microsoft/psi/blob/master/Applications/Sigma/Readme.md) used for collecting the data enables researchers to deploy models developed or evaluated based on this data in the context of the target application, and allows them to collect additional data to study their end-effects on metrics of overall task performance.

## Why it matters

**To the field:** The __`SigmaCollab`__ dataset marks a departure from passive, observation-based data collection toward an application-driven paradigm that prioritizes the nuances of active collaboration. While traditional egocentric datasets have excelled at providing the raw material for computer vision tasks, such as object detection or activity recognition, they often strip away the interactive loop that defines real-world AI assistance. By capturing users in the act of collaborating with a functional agent to achieve tangible goals, __`SigmaCollab`__ surfaces the messy, fragmented, and non-linear nature of human-AI coordination. This dataset demonstrates that when users are motivated by a task rather than a script, they exhibit many behaviors, from self-talk to referential ambiguity, that current "ping-pong" interaction models are ill-equipped to handle.

**Future directions:** By grounding data collection in functional tasks, the dataset facilitates future work in developing novel benchmarks that shift the focus from static perception to active, temporal coordination. These benchmarks can target critical interaction competencies, such as grounding, proactive intervention, and situated reference resolution. Furthermore, __`SigmaCollab`__ enables the community to address complex challenges in detecting user cognitive states, including frustration and confusion, thereby driving the development of agents that are not just perceptually aware, but interactively fluent.

## Publications & links

- [SigmaCollab: An Application-Driven Dataset for Human-AI Collaboration in the Physical World - NeurIPS, 2026 _in submission_](https://openreview.net/forum?id=hOfQXdBQVj)
- [SigmaCollab: An Application-Driven Dataset for Physically Situated Collaboration - arXiv, 2025](https://arxiv.org/abs/2511.02560)
- [GitHub: microsoft/sigmacollab](https://github.com/microsoft/SigmaCollab)
- [Hugging Face: microsoft/sigmacollab](https://huggingface.co/datasets/microsoft/sigmacollab)