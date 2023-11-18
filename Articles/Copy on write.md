# Abstract
---
Из оф документации:
Arrays, like all variable-size collections in the standard library, use copy-on-write optimization. Multiple copies of an array share the same storage until you modify one of the copies. When that happens, the array being modified replaces its storage with a uniquely owned copy of itself, which is then modified in place. Optimizations are sometimes applied that can reduce the amount of copying.

This means that if an array is sharing storage with other copies, the first mutating operation on that array incurs the cost of copying the array. An array that is the sole owner of its storage can perform mutating operations in place.
#tbd


# Questions
---
#need_research/development 
- [ ] 



# Learning materials
---
## Articles & Links
- [Copy on write in Swift](https://medium.com/@nitingeorge_39047/copy-on-write-in-swift-b44949436e4f)
## Videos:
- 