---
title: capabilities(3)
version: 1
---

# CAP_KERNEL

## Synopsis

CAP_KERNEL acts as a capability granting a userspace process access to an interface for direct kernel operations.

## Implementation Details

CAP_KERNEL is to only be granted to processes directly by kernel space, and not be inherited by children.

CAP_KERNEL is not to be granted automatically to the root user or other such "super-admins".

The interface granted access to by CAP_KERNEL shall have the following APIs:

* `map_page_self(void* virtual_addr, u64 physical_addr)`: Maps a page, worth 4KiB, in the current process, from a 64-bit physical address to a target virtual address
* `map_page_other(pid_t target_pid, void* virtual_addr, u64 physical_addr)`: Maps a page, worth 4KiB, in the target process (selected by PID), from a 64-bit physical address to a target virtual address
* `unmap_page_self(void* virtual_addr)`: Unmaps a page by its virtual address from the current process
* `unmap_page_other(pid_t target_pid, void* virtual_addr)`: Unmaps a page by its virtual address from the current process
* `reverse_virtual(pid_t target_pid, u64 physical_addr)`: From a physical address, returns one of the virtual addresses mapped (no guarantee as to which) in the target process that map to that physical address
* `resolve_virtual(pid_t target_pid, void* virtual_addr)`: From a virtual address, figure out and return the physical address it is mapped to in the target process

???+ warning
    `CAP_KERNEL` is not to be granted automatically by the `setuid` flag (if implemented by the filesystem), and no process shall be able to give it to itself.

    However, the standard does allow for the kernel to implement a separate filesystem binary flag that automatically grants the process this capability.

## Notes

Processes with this capability are to be considered part of the OS's TCB (Trusted Computing Base). If a process with `CAP_KERNEL` is compromised, all userspace is to be treated as compromised.

Additionally, the following interfaces are to be *containerized* if the process is part of a PID namespace. That means, if a process with CAP_KERNEL is part of a PID namespace, the kernel should resolve PIDs as part of that PID namespace:

* `map_page_other`
* `unmap_page_other`
* `reverse_virtual`
* `resolve_virtual`
