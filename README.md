## Tree sitter for neovim

changes made to `unicode.h`

```c
#include <stdint.h>

#ifndef le16toh
// On little-endian machines, no conversion needed
#define le16toh(x) (x)
#endif

#ifndef be16toh
// Swap bytes to convert big-endian to host order
#define be16toh(x) __builtin_bswap16(x)
#endif

// #include "portable/endian.h" 
```

On some HPC environments, `le16toh` and `be16toh` have undefined reference. This file contains a modified version of the v0.25.6 tree sitter that comes bundled with neovim. 

Make sure that neovim fetches this file while building dependencies, 

```bash
grep -r ".tar.gz" .
```

To list all references of `tar.gz` files. You'll find a `cmake.deps/deps.txt` file where you need to replace `TREESITTER_URL` with `https://github.com/grussdorian/tree-sitter/raw/main/v0.25.6.tar.gz` and change `TREESITTER_SHA256` to the hash obtained as follows

```bash
sha256sum v0.25.6.tar.gz
```

Note find the hash by first downloading the file then replace the existing hash found in `cmake.deps/deps.txt` under key `TREESITTER_URL`
