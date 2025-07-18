---
title: "A Practical Guide to HPC on Grid5000"
permalink: /blog/hpc-and-cloud/a-practical-guide-to-hpc-on-grid5000/a-practical-guide-to-hpc-on-grid5000.md
author_profile: true
---

## How to create an account ?

## How to set up VSCode for a remote connexion ?

## Architecture

What you need to know at this stage is that you have access to two types of storage: personal and shared team storage. 

- Your personal workspace is located at `/home/nmonir`, where you can store your individual files and project data.
- The team "multispeech" has a dedicated shared storage area located at `/srv/storage/talc3@storage4.nancy.grid5000.fr/multispeech/`. Within this directory, there are two main subfolders.
    - The first is `calcul/`, which provides additional storage space allocated to users and projects, including both current and former team members.
    - The second is `corpus/`, which contains datasets and corpora that have been used or downloaded by the team. Be aware that some of the resources in this folder may be protected or subject to licensing restrictions.

✅ As a required setup step, please go to `/srv/storage/talc3@storage4.nancy.grid5000.fr/multispeech/calcul/users` and create your personal subdirectory. This directory should follow the naming convention: the first letter of your first name followed by your full last name (e.g., for *Nasser-Eddine Monir*, the correct directory name would be `nmonir`).

## Where do I install (mini) conda ? 