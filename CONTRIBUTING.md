# Contributing

Thanks for helping keep **Awesome Action-Conditioned Video Generation** up to date! 🎉

Contributions of all kinds are welcome: adding a new paper/model/dataset/benchmark, fixing a broken link, correcting an arXiv ID or venue, improving a description, or proposing a new category.

## How to add an entry

1. Fork this repository and create a branch.
2. Find the most appropriate section. If your paper spans multiple areas (e.g. a robot world model that is also a benchmark), put it in the section that best matches its **primary contribution** and, if helpful, mention the cross-cutting aspect in the one-line description.
3. Add your entry using the format below. Keep entries ordered roughly by **influence and recency** within a subsection (foundational/landmark works can stay near the top).
4. Open a Pull Request with a short note on why the work belongs here.

## Entry format

Each entry is a single bullet with a name, full title, venue/year, badges, and a one-sentence description that states **how the action conditions the generated video**:

```markdown
- **ShortName** — *"Full Paper Title"*. `Venue Year`  
  [![arXiv](https://img.shields.io/badge/arXiv-XXXX.XXXXX-b31b1b)](https://arxiv.org/abs/XXXX.XXXXX) [![Project](https://img.shields.io/badge/Project-Page-1e90ff)](PROJECT_URL) [![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](CODE_URL)  
  <sub>One sentence: what it does and what action signal (motor command, controller input, trajectory, camera pose, language) drives the video.</sub>
```

### Badge templates

| Resource | Badge markdown |
| --- | --- |
| arXiv | `[![arXiv](https://img.shields.io/badge/arXiv-XXXX.XXXXX-b31b1b)](https://arxiv.org/abs/XXXX.XXXXX)` |
| Project page | `[![Project](https://img.shields.io/badge/Project-Page-1e90ff)](URL)` |
| Code | `[![Code](https://img.shields.io/badge/Code-GitHub-2ea44f)](URL)` |
| Tech report / blog | `[![Report](https://img.shields.io/badge/Tech-Report-orange)](URL)` |
| Journal (e.g. Nature) | `[![Nature](https://img.shields.io/badge/Nature-2025-blueviolet)](URL)` |

Omit any badge you don't have a verified link for — please do **not** guess arXiv IDs or repository URLs. If a code or project page does not exist, simply leave that badge out.

## Inclusion criteria

This list focuses on **action-conditioned video generation**: generative models that synthesize future visual observations (frames/video) conditioned on an **action** signal. "Action" is interpreted broadly — robot/agent motor commands, discrete controller or keyboard/mouse inputs, ego-vehicle trajectories or control, camera poses/motion, drag trajectories, and free-text actions all qualify.

A work is in scope if a viewer can meaningfully ask *"what video does this action produce?"*. Pure text-to-video, image-to-video, or video editing without an action/control axis is generally **out of scope** unless it introduces a control mechanism that functions as an action.

## Quality checklist

- [ ] The entry is in the correct (sub)section.
- [ ] The arXiv ID resolves and matches the title (check `https://arxiv.org/abs/<ID>`).
- [ ] Project and code links are official and load correctly.
- [ ] The description is one sentence and names the action/conditioning signal.
- [ ] No duplicate of an existing entry.

## Reporting errors

Spotted a wrong link, ID, or venue? Please open an Issue or PR — corrections are just as valuable as additions.
