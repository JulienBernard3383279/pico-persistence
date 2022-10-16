# pico-persistence

Framework to use the RP2040 flash as persistent storage. Stores data starting at offset 1.5MB (Pico has 2MB).

These function templates manipulate 4K pages of memory identified by their index (an enum defined in page_indexes.hpp) that are mapped to memory `[1.5MB+index*4K, 1.5MB+(index+1)*4K[`.
- `read` lets you read data member with no copy
- `clone` gives you a local copy of the page
- `commit` will write the flash page
- `set` lets you set an individual member of the page in one call (behind the scenes, it clones, modifies the local page, then commits it)

Call `set` if you only have one field to write. If you have several, manually `clone`, alter your copy then `commit` it, don't repeatedly call `set`.

The templates in functions.hpp expect an `index` field to be defined with the index in the page struct.

Leaving the runtime_remapping page from pico-rectangle as an example. For an example of usage in context, check pico-rectangle.
