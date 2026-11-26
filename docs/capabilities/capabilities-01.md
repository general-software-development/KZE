---
title: capabilities(1)
version: 1
---

## Synopsis

All processes should have a 64-bit (or bigger) integer representing its capabilities.

Capabilities are to be represented as bit masks, for example:

```c
#define CAP_SYS_ADMIN (1ULL << 1)
#define CAP_DAC_OVERRIDE (1ULL << 2)
```

## Capabilities

The minimum capabilities that should be present are:

| Capability |
| :-: |
| `CAP_SYS_ADMIN` [^1] |
| `CAP_KERNEL` [^2] |
| `CAP_CHOWN` |
| `CAP_DAC_OVERRIDE` |
| `CAP_DAC_READ_SEARCH` |
| `CAP_SYS_BOOT` |

## Implementation Details

Capabilities, except for where stated otherwise, are inherited by children created through `fork()`.

[^1]: View [capabilities(2)](./capabilities-02.md)
[^2]: View [capabilities(3)](./capabilities-03.md)
