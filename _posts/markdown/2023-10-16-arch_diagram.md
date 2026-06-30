---
title: Architecture Diagram Example
author: liuzhongyan
date: 2023-10-16
category: Jekyll
layout: post
mermaid: true
hide_in_sidebar: true
---


The following shows a example of architecture diagram:

```markdown
┌────────────────────────────────────────────────────────────────────┐
│                          XXX architecture                          │
│                                                                    │
│   ┌──────┐    ┌──────────────┐    ┌───────────┐    ┌───────────┐   │
│   │ SDK  │───▶│   Monitor    │◀──▶│BlobManager│◀──▶│ Placement │   │
│   │(SDK1)│    │ (Raft HA)    │    │(Raft 多组)│    │ (EC Codec)│    │
│   └──┬───┘    └──────────────┘    └───────────┘    └─────┬─────┘   │
│      │                                                    │        │
│      │              ┌──────────────┐                      │        │
│      └──────────────│  ChunkServer │◀─────────────────────┘        │
│                     │ (磁盘存储层)   │                               │
│                     └──────────────┘                               │
└────────────────────────────────────────────────────────────────────┘
```
