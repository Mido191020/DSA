Sure, let's go through your code and address the questions in the comments:

1. **Why use `const` and `&` in function parameters?**
   ```cpp
   int CollisionHandling(const string& key, int hash);
   ```
   - **`const`**: This keyword indicates that the parameter `key` will not be modified within the function. It helps in preventing accidental changes and can also aid in optimization by the compiler.
   - **`&` (Reference)**: This is used to avoid copying the parameter `key`. Since `string` can be large, passing it by reference avoids the overhead of copying the entire string, improving performance.

2. **Purpose of `CollisionHandling` method**
   ```cpp
   int CollisionHandling(const string& key, int hash) {
       int newHash;
       for (int i = 1; i < this->size; ++i) {
           newHash = (hash + i) % this->size;
           if (this->entries[newHash].empty() || this->entries[newHash] == key) {
               return newHash;
           }
       }
       return -1;
   }
   ```
   - This method is used to handle collisions using linear probing. If a collision occurs (i.e., the hash index is already occupied), it tries the next index in the array until it finds an empty slot or the same key.
   - The method returns the new hash index where the key can be inserted or found. If no suitable slot is found, it returns `-1`.

3. **Purpose of `ResizeOrNot` method**
   ```cpp
   void ResizeOrNot() {
       if (this->enterCount < this->entries.size()) {
           return;
       }
       int newSize = this->entries.size() * 2;
       std::cout << "[resize] from " << this->size << " to " << newSize << std::endl;
       vector<string> copy = this->entries;
       this->entries.clear();
       this->entries.resize(newSize);
       for (int i = 0; i < this->size; ++i) {
           if (!copy[i].empty()) {
               this->AddToEntries(copy[i]);
           }
       }
       this->size = newSize;
   }
   ```
   - This method checks if resizing is necessary by comparing the number of entries (`enterCount`) with the current size of the entries array. If the array is full, it doubles the size of the array.
   - It copies the existing entries to a temporary vector, clears the current entries array, resizes it, and then rehashes and reinserts all the non-empty entries from the temporary vector into the new array.

4. **Explanation of `Add` method**
   ```cpp
   void Add(const std::string& key) {
       this->ResizeOrNot();
       this->AddToEntries(key);
   }
   ```
   - This method is the public interface for adding a key to the HashSet.
   - It first checks if resizing is necessary by calling `ResizeOrNot`.
   - It then adds the key to the entries array using `AddToEntries`.

5. **Why Resize by 2?**
   - Doubling the size of the array (`newSize = this->entries.size() * 2`) is a common strategy to keep the time complexity of insertion operations amortized O(1). It reduces the frequency of resize operations while maintaining performance.

6. **Explanation of `contains` method**
   ```cpp
   bool contains(const string& key) {
       int index = GetHash(key);
       if (index < this->entries.size() && this->entries[index] != key) {
           index = CollisionHandling(key, index);
       }
       if (index == -1 || index >= this->entries.size()) {
           return false;
       }
       return this->entries[index] == key;
   }
   ```
   - This method checks if a key exists in the HashSet.
   - It calculates the initial hash index of the key.
   - If the key at the hash index is not the one being searched for, it uses `CollisionHandling` to find the key's actual position.
   - If the key is found, it returns `true`; otherwise, it returns `false`.

7. **Why call `CollisionHandling` in `Remove`?**
   ```cpp
   void Remove(const string& key) {
       int index = GetHash(key);
       if (index < this->entries.size() && entries[index] != key) {
           index = CollisionHandling(key, index);
       }
       if (index != -1 && index < this->entries.size() && this->entries[index] == key) {
           this->entries[index] = "";
           this->enterCount--;
       }
   }
   ```
   - The `Remove` method first calculates the hash index of the key.
   - If the key at that index is not the one to be removed, it uses `CollisionHandling` to find the correct position of the key.
   - If the key is found, it removes it by setting the entry to an empty string and decreases the entry count.

8. **Purpose of `Search` method**
   ```cpp
   int Search(const string& key) {
       int index = GetHash(key);
       if (index < this->entries.size() && entries[index] != key) {
           index = CollisionHandling(key, index);
       }
       if (index != -1 && index < this->entries.size() && entries[index] == key) {
           return index;
       }
       return -1;
   }
   ```
   - This method returns the index of the key if it exists in the HashSet, otherwise, it returns `-1`.
   - It first calculates the hash index of the key and uses `CollisionHandling` if necessary to find the key's position.

### Summary Notes

- **HashSet Construction**: Initializes with a default size of 3 and an empty entries vector.
- **Destructor**: Clears the entries vector.
- **Hash Function (`GetHash`)**: Computes a hash value using the FNV-1a hash algorithm.
- **Collision Handling (`CollisionHandling`)**: Resolves collisions using linear probing.
- **Adding Elements (`AddToEntries`)**: Adds an element to the HashSet, handling collisions and resizing as needed.
- **Resizing (`ResizeOrNot`)**: Doubles the size of the entries vector when it's full and rehashes all elements.
- **Public Add Method (`Add`)**: Checks for resize and adds the element.
- **Contains Method (`contains`)**: Checks if an element exists in the HashSet.
- **Removing Elements (`Remove`)**: Removes an element from the HashSet by setting its entry to an empty string.
- **Searching Elements (`Search`)**: Returns the index of an element if it exists.

These notes should help you understand and review the concepts of designing a `HashSet` in C++.