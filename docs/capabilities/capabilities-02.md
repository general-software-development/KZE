---
title: capabilities(2)
version: 1
---

# CAP_SYS_ADMIN

## Synopsis

CAP_SYS_ADMIN shall act as a catch-all capability for small, finely-grained capabilities that don't fit into other capabilities, and that shouldn't reasonably have their own capabilities.

## Implementation Details

CAP_SYS_ADMIN is to only be given to the root user, or other "super-admins" of the kind.
