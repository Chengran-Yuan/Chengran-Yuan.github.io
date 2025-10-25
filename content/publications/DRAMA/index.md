---
title: 'Drama: An efficient end-to-end motion planner for autonomous driving with mamba'

# Authors
# If you created a profile for a user (e.g. the default `admin` user), write the username (folder name) here
# and it will be replaced with their full name and linked to their profile.
authors:
  - admin
  - Zhanqi Zhang, Jiawei Sun, Shuo Sun, Zefan Huang, Christina Dao Wen Lee, Dongen Li, Yuhang Han, Anthony Wong, Keng Peng Tee and Marcelo H Ang Jr

# Author notes (optional)
author_notes:
  # - 'Equal contribution'
  # - 'Equal contribution'

date: '2024-10-01T00:00:00Z'
doi: ''

# Schedule page publish date (NOT publication's date).
publishDate: '2025-07-30T00:00:00Z'

# Publication type.
# Accepts a single type but formatted as a YAML list (for Hugo requirements).
# Enter a publication type from the CSL standard.
publication_types: ['paper-conference']

# Publication name and optional abbreviated publication name.
publication: In *International Symposium of Robotics Research 2024*
publication_short: In *ISRR 2024*

abstract: Motion planning is a challenging task to generate safe and feasible trajectories in highly dynamic and complex environments, forming a core capability for autonomous vehicles. In this paper, we propose DRAMA, the first Mamba-based end-to-end motion planner for autonomous vehicles.DRAMA fuses camera, LiDAR Bird's Eye View images in the feature space, as well as ego status information, to generate a series of future ego trajectories. Unlike traditional transformer-based methods with quadratic attention complexity for sequence length, DRAMA is able to achieve a less computationally intensive attention complexity, demonstrating potential to deal with increasingly complex scenarios. Leveraging our Mamba fusion module, DRAMA efficiently and effectively fuses the features of the camera and LiDAR modalities. In addition, we introduce a Mamba-Transformer decoder that enhances the overall planning performance. This module is universally adaptable to any Transformer-based model, especially for tasks with long sequence inputs. We further introduce a novel feature state dropout which improves the planner's robustness without increasing training and inference times. Extensive experimental results show that DRAMA achieves higher accuracy on the NAVSIM dataset compared to the baseline Transfuser, with fewer parameters and lower computational costs.

# Summary. An optional shortened abstract.
summary: DRAMA introduces a Mamba-based motion planning approach for autonomous vehicles that addresses key challenges in trajectory generation. 

tags:
  - End-to-end Autonomous Driving, Motion Planning, Mamba

# Display this page in the Featured widget?
featured: true

# Custom links (uncomment lines below)
# links:
# - name: Custom Link
#   url: http://example.org


links:
  - type: pdf
    url: https://arxiv.org/pdf/2408.03601
  - type: code
    url: https://github.com/Chengran-Yuan/DRAMA
  # - type: dataset
  #   url: ""
  # - type: poster
  #   url: ""
  - type: project
    url: https://chengran-yuan.github.io/DRAMA/
  # - type: slides
  #   url: ""
  # - type: source
  #   url: ""
  # - type: video
  #   url: ""


# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
image:
  caption: 'Image credit: [**Unsplash**](https://unsplash.com/photos/pLCdAaMFLTE)'
  focal_point: ''
  preview_only: false

# Associated Projects (optional).
#   Associate this publication with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `internal-project` references `content/project/internal-project/index.md`.
#   Otherwise, set `projects: []`.
projects:
  - example

# Slides (optional).
#   Associate this publication with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides: "example"` references `content/slides/example/index.md`.
#   Otherwise, set `slides: ""`.
slides: ""
---