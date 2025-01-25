# DreamHack: shiftalloc
## Variables
### chunks
- 24bytes (8byte long * 3)
- Addresses of allocated memory space
### sizes
- 12bytes (4byte int * 3)
- Sizes of allocated memory space
### Index
- `index` = 0, 1, 2

## Functions
### 1. alloc
- Input size to `sizes[index]`
- Allocate memory space to `chunks[index]` as much as `sizes[index]`
- Read input to `chunks[index]` as much as `sizes[index]`

### 2. shrink
- SHR `sizes[index]` as much as `shrink_size` (input < 32)

### 3. expand
- Free & Initialize `chunks[index]` (**UAF bug**)
- SHL `sizes[index]` as much as `shrink_size` (input < 32)

### 4. chunk_read
- Write output from `chunks[index]` as much as `sizes[index]`

### 5. chunk_write
- Read input to `chunks[index]` as much as `sizes[index]`

### 6. delete
- Free & Initialize `chunks[index]` (**UAF bug**)

* * *

## Solution
> 1. Tcache Poisoning (`alloc` -> ``)
> 2. Leak libc
> 3. Hook Overwrite (free/malloc hook)
> 4. One-gadget