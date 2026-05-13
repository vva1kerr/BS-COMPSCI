# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Repo Is

Personal CS reference repository. No build system, no test suite, no server. Content is static reference material organized by topic.

## Running Code

No unified runner — each file is standalone. Run by language:

```bash
# Python
python3 DSA-CODE/Python/Sorting/bubble_sort.py

# C++
g++ -o out DSA-CODE/cpp/Sorting\ Algorithms/merge_sort.cpp && ./out

# C
gcc -o out DSA-CODE/c/Sorting\ Algorithms/bubble_sort.c && ./out

# Go
go run DSA-CODE/golang/Sorting\ Algorithms/bubble_sort.go

# Java
javac DSA-CODE/Java/Sorting\ Algorithms/BubbleSort.java && java -cp DSA-CODE/Java/Sorting\ Algorithms BubbleSort

# Advent of Code (Python, input files co-located)
python3 DSA-CODE/Advent-of-Code/2022/1.py < DSA-CODE/Advent-of-Code/2022/1.in
```

## Structure

```
CHEATSHEETs/      Reference sheets by topic (AIML, BASH, C, CPP, DSA, GIT, GOLANG,
                  JAVA, JAVASCRIPT, LINUX, PYTHON, TYPESCRIPT, + more)
DSA-CODE/         Algorithm implementations
  Advent-of-Code/ AoC solutions (2021, 2022) — each day has N.py + N.in (input)
                  and Ne.py + Ne.in (example input)
  c/ cpp/ Dart/ golang/ Haskell/ Java/ JavaScript/ Python/
                  Language-partitioned algo implementations
  CONFERENCE_PAPERS/  PDFs (CVPR, ICDAR)
  jupyter-notebook/   Jupyter notebooks
  Roadmaps/       Learning path diagrams/docs
INTERVIEWs/       HackerRank prep solutions (Python + Bash)
PENTESTING/       Kali Linux reference
DISTROs/          Linux post-install scripts (Arch, Ubuntu)
tools/            Misc tool cheatsheets/scripts (drush, elasticsearch, pm2, etc.)
READMEs/          READMEs from upstream source repos
LICENSEs/         Licenses from upstream source repos
commands.txt      Linux sysadmin command reference
```

## Conventions

- AoC files: `N.py` = real input solution, `Ne.py` = example input solution; input files end in `.in`
- Algo implementations are self-contained — no shared utilities across language dirs
- CHEATSHEETs mix formats: `.md`, `.sh`, `.pdf`, `.txt`, `.jpg` — format matches content type
- `requirements.txt` is a placeholder — no Python package dependencies tracked here