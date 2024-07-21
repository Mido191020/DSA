Here’s a detailed breakdown of your `HashMap` class, including answers to the specific questions you posed:

### HashMap Class Overview

**Definition:**
The `HashMap` class is an implementation of a hash table that stores key-value pairs. It uses open addressing with linear probing to handle collisions and dynamically resizes when the load factor exceeds a threshold.

### Key Components

1. **Data Members:**
   - `vector<pair<string, int>> entries;`  
     Stores the key-value pairs. Each entry is a `pair<string, int>`, where `string` is the key and `int` is the value.
   - `int size;`  
     The current size of the hash table (number of buckets).
   - `int enterCount;`  
     The number of entries (key-value pairs) currently in the hash table.

2. **Constructor and Destructor:**
   - `HashMap()`  
     Initializes the hash table with a default size of 3 and an empty vector of entries.
   - `~HashMap()`  
     Clears the entries vector to free up memory.

### Methods

1. **`GetHash` Method:**
   ```cpp
   int GetHash(const std::string& key) const
   ```
   **Purpose:** Computes a hash index for the given key using the FNV-1a hash function.

   **Why `const` and `&`:**  
   - **`const`** ensures that `GetHash` does not modify the `HashMap` object.
   - **`&`** avoids copying the `key` string, which is more efficient, especially for large strings.

2. **`CollisionHandling` Method:**
   ```cpp
   int CollisionHandling(const string& key, int hash) const
   ```
   **Purpose:** Resolves collisions using linear probing. It searches for an open slot or an existing entry with the same key.

   **Why `const`:** Ensures that `CollisionHandling` does not modify the `HashMap` object.

3. **`AddToEntries` Method:**
   ```cpp
   void AddToEntries(const string& key, int value)
   ```
   **Purpose:** Inserts a key-value pair into the hash table, handling collisions as needed.

   **Why `AddToEntries` in `Add`:** This method is used within `Add` to handle the internal logic of adding an entry, including collision handling and resizing.

4. **`ResizeOrNot` Method:**
   ```cpp
   void ResizeOrNot()
   ```
   **Purpose:** Resizes the hash table if the number of entries exceeds the current size. It doubles the size of the hash table and rehashes all existing entries.

   **Why Resize by *2:** Doubling the size helps maintain a balance between space and time complexity during resizing. It helps to keep the load factor manageable and improves performance.

5. **`Add` Method:**
   ```cpp
   void Add(const string& key, int value)
   ```
   **Purpose:** Adds a key-value pair to the hash table. It calls `ResizeOrNot` to ensure there is enough capacity before adding the entry.

6. **`Contains` Method:**
   ```cpp
   bool Contains(const string& key) const
   ```
   **Purpose:** Checks if a key is present in the hash table.

   **Why not just return `true`:** To ensure that the key exists at the computed index or its collision-resolved index. It also checks for an empty slot which may contain no valid key.

7. **`Get` Method:**
   ```cpp
   bool Get(const string& key, int &value) const
   ```
   **Purpose:** Retrieves the value associated with a key if it exists. It populates the `value` reference and returns `true` if the key is found.

   **Purpose:** Allows you to fetch the value for a given key without modifying the hash map. It distinguishes between a non-existent key and an empty slot.

8. **`Remove` Method:**
   ```cpp
   void Remove(const string& key)
   ```
   **Purpose:** Removes the key-value pair from the hash table. It sets the entry to an empty state and decrements the count of entries.

9. **`Size` Method:**
   ```cpp
   int Size() const
   ```
   **Purpose:** Returns the number of key-value pairs currently in the hash table.

10. **`Print` Method:**
    ```cpp
    void Print() const
    ```
    **Purpose:** Prints the contents of the hash table for debugging purposes.

11. **`Find` Method:**
    ```cpp
    bool Find(const string& key, int& value) const
    ```
    **Purpose:** Finds a key and retrieves its value without modifying the hash table.

    **Explanation:**  
    - **Purpose:** The `Find` method is used to check if a key exists and to retrieve its value. It is similar to `Get` but is specifically intended for searching without altering the state of the hash table.

### Example Usage

Here’s a simple usage example of the `HashMap` class:

```cpp
int main() {
    HashMap map;
    map.Add("key1", 10);
    map.Add("key2", 20);

    int value;
    if (map.Get("key1", value)) {
        std::cout << "Value for key1: " << value << std::endl;
    }

    if (map.Contains("key2")) {
        std::cout << "Key2 exists in the map." << std::endl;
    }

    map.Remove("key1");
    map.Print();

    return 0;
}
```

In this example, a `HashMap` instance is created, keys are added, and values are retrieved and printed. The `Remove` method is used to delete a key, and the `Print` method shows the current state of the hash map.