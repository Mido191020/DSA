
#### General Concepts
1. **Hash Tables**: Data structures that provide fast insertion, deletion, and lookup operations by using a hash function to compute an index into an array of buckets or slots, from which the desired value can be found.

2. **Hash Function**: Converts input (like a string) into a fixed-size integer, which is used as an index in the hash table. In the provided code, the Fowler–Noll–Vo (FNV) hash function is used.

3. **Collisions**: Occur when two keys hash to the same index. Collision resolution strategies are necessary to handle such cases.

4. **Linear Probing**: A collision resolution method where, upon a collision, the algorithm checks the next slot in the array (and wraps around to the beginning if necessary) until an empty slot is found.

#### Key Components in Your Code

1. **Hash Function Implementation**
   - **Hash32 and Hash64 Methods**: Implement the FNV-1a hash function for 32-bit and 64-bit hashes respectively. These functions initialize with an offset basis and then process each byte of the input, updating the hash with each byte.
   ```cpp
   uint32_t Hash32(const std::string& str) { ... }
   uint64_t Hash64(const std::string& str) { ... }
   ```

2. **Hash Table Class**
   - **Member Variables**: 
     - `entries`: A vector of pairs to store key-value pairs.
     - `size`: The size of the hash table.
     - `entrCount`: The count of entries in the hash table.

   - **GetHash Method**: Computes the hash for a given key.
     ```cpp
     int GetHash(const string& key) { ... }
     ```

   - **CollisionHandling Method**: Resolves collisions using linear probing.
     - **`set = true`**: Indicates an add or update operation. The method searches for an empty slot or the existing key slot.
     - **`set = false`**: Indicates a get operation. The method searches for the existing key slot.
     ```cpp
     int CollisionHandling(const string& key, int hash, bool set) { ... }
     ```

   - **AddToEntries Method**: Adds or updates entries in the hash table. It handles collisions by calling `CollisionHandling` with `set = true`.
     ```cpp
     void AddToEntries(const string& key, const string& value) { ... }
     ```

   - **ResizeOrNot Method**: Resizes the hash table when the load factor reaches a threshold. The new size is double the current size.
     ```cpp
     void ResizeOrNot() { ... }
     ```

   - **Set Method**: Adds or updates an entry, resizing the table if necessary.
     ```cpp
     void Set(const string& key, const string& value) { ... }
     ```

   - **Get Method**: Retrieves the value for a given key, handling collisions by calling `CollisionHandling` with `set = false`.
     ```cpp
     string Get(const string& key) { ... }
     ```

   - **Print Method**: Prints the current state of the hash table.
     ```cpp
     void Print() { ... }
     ```

3. **Usage of `this`**
   - **Disambiguation**: Differentiates between member variables and local variables/parameters with the same name.
   - **Clarification**: Makes it clear that a variable or function is a member of the class, improving readability and maintainability.

#### When to Use `this`
1. **Disambiguate Member Variables**: When a parameter or local variable has the same name as a member variable.
2. **Clarify Member Function Calls**: When calling a member function within another member function.
3. **Pass the Current Object**: When the current object instance needs to be passed to another function or method.

### Summary
- **Hash Tables**: Efficient data structure for fast lookups, insertions, and deletions.
- **Hash Function**: Converts input to a fixed-size integer.
- **Collisions**: Handled using linear probing in your code.
- **`this` Keyword**: Essential for clarity, correctness, and disambiguation between member variables and local variables/parameters.