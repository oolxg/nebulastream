## Setsum

Setsum is an order agnostic, commutative checksum. The order agnostic property of a Setsum means that
any two Setsums having the same elements should be the same, regardless of the sequence of elements
within their respective Setsums.

Each Setsum has 8 columns, which are arrays of 8 unsigned 32-bit integers. Every column within
a new Setsum is initialized with 0. Each column is assigned a large prime number, ideally as close
to the upper limit of the unsigned 32-bit integer datatype.

So when an item is being added to the Setsum, the hash of the item is computed. This hash is 
further split into 8 blocks of 4 bytes and these blocks are added to the corresponding column
of the Setsum. If the sum is greater than the column's prime number, the remainder is stored by
performing modular arithmetic on the sum using the corresponding prime number. Items that have
been addded to the Setsum can be removed by computing and adding the inverse of the hash of the
item to the Setsum. The inverse of a hash can be computed by subtracting the hash block from the
corresponding prime number.   

For an indepth understanding of setsum, click this link https://avi.im/blag/2025/setsum/

The logic implementation of a Setsum is done in Setsum.cpp and Setsum.hpp , and tested extensively
in SetsumTest.cpp.

The notables functions are  
- **add()** - allows addition of a given string or a setsum into the setsum
- **remove()** - allows removal of a given string or a setsum into the setsum


These are the following tests:

- **BasicFunctionality** - verifies add operations and equality between Setsums
- **EqualCheck** - tests equality comparison where two Setsums having same elements are the same and also two Setsums having different elements are unequal.
- **OrderAgnostic** - this critical test confirms the order-independent property of a Setsum
- **AddRemove** - validates removal functionality
- **AddRemoveOrderIndependent** - ensures after removal of an item, the Setsum remains order-agnostic
- **MultiThreaded** - stress test with 8 threads doing 800,000 operations
- **EmptySetsumEqual** - edge case for comparing empty Setsums
- **AddRemoveSameItem** - Test that adding and removing the same item returns to original state

The rest tests the functions add() and remove() where the input parameter is a Setsum instead of a string.    

- **AddSetsums** - verifies add operations
- **RemoveSetsums** - verifies remove operations
- **MultiThreadedSetsums**- stress test with 8 threads doing 800,000 operations
- **AddRemoveSetsums** - validates removal functionality



SetsumStarter.cpp is a CLI tool ,which is to calculate Setsums from files by using
line-based processing for text files to allow verifying the order-agnostic property.
This is mainly used for sink validation.




