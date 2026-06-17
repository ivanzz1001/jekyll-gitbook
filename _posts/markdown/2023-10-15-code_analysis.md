
---
title: Code Analysis Example
author: liuzhongyan
date: 2023-10-15
category: Jekyll
layout: post
hide_in_sidebar: true
---


This is a code analysis example:

```markdown
OpenBlobObject(bucket, path, flag, ret_blob_id, options)
    │
    └─ BlobClient::OpenBlob(bucket, path, openflags, ret_errcode, options)
                     │
                     ▼
OpenBlob(bucket, path, openflags, ret_errcode, options)
    │
    ├─ 1. 构造BlobID
    │     select_id_ = MD5(bucket + "-object-" + path)
    │     blob_id_str_ = bucket + "-object-" + path
    │
    ├─ 2. 创建 BlobInstance
    │     ├─ 初始化 IoTracker（IO 分发器）
    │     └─ 注册 EC 策略：{2+1, 4+2, 8+2, 8+3}
    │
    ├─ 3. BlobInstance::OpenBlob()
    │     └─ 一致性哈希定位 → RPC 调用 BlobManager.OpenBlob
    │         ├─ 带重试（指数退避：2^retry-1 秒）
    │         ├─ 返回 BlobInfo（blob_type, blob_size, extent 列表...）
    │         └─ 返回全部已存在的 ExtentInfo
    │
    └─ 4. 写入 blob_map_[blob_id] = instance
```
