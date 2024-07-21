The use of `this` in C++ refers to the current instance of the class within its member functions. It's a pointer to the object for which the member function is called. Let's break down why and where `this` is used in the provided `HashTable` class:

1. **Accessing Member Variables:**
   - `this->entries`, `this->size`, and `this->entrCount` are used to access the member variables of the `HashTable` class within its member functions. This makes it clear that we are referring to the instance variables rather than any local variables or parameters that might have the same name.

2. **Calling Member Functions:**
   - `this->ResizeOrNot()`, `this->AddToEntries(key, value)`, and other similar calls use `this` to call other member functions within the class. This ensures that the function is called on the current instance of the class.

Here are the specific instances in your code:

### Constructor and Destructor
```cpp
HashTable() : size(3), entrCount(0) {
    this->entries = vector<pair<string, string>>(this->size);
}

~HashTable() { this->entries.clear(); }
```
- **Purpose:** Initialize member variables. Using `this` helps differentiate between member variables and parameters or local variables.

### Accessing Member Variables
```cpp
int CollisionHandling(const string& key, int hash, bool set) {
    int newHash;
    for (int i = 1; i < this->size; ++i) {
        newHash = (hash + i) % this->size;
        if (set && (this->entries[newHash].first == "" && this->entries[newHash].second == "") ||
            this->entries[newHash].first == key) {
            return newHash;
        } else if (!set && this->entries[newHash].first == key) {
            return newHash;
        }
    }
    return -1;
}
```
- **Purpose:** Access the `size` and `entries` member variables of the current `HashTable` instance.

### Calling Member Functions
```cpp
void AddToEntries(const string& key, const string& value) {
    int index = GetHash(key);
    auto item = entries[index];
    if (index == -1) {
        throw "Invalid Hashtable!!!!";
    }
    if (this->entries[index].first != "" && this->entries[index].second != "" && entries[index].first != key) {
        index = this->CollisionHandling(key, index, true);
    }
    if (index < this->entries.size() && this->entries[index].second != value && this->entries[index].first != key) {
        this->entries[index] = pair<string, string>({key, value});
        this->entrCount++;
    }
    else if (this->entries[index].first == key) {
        this->entries[index].second = value;
    } else {
        throw "Invalid Hashtable!!!!";
    }
}
```
- **Purpose:** Call `CollisionHandling` within `AddToEntries` to handle collisions. Using `this` makes it clear that `CollisionHandling` is a member function.

### Resizing the HashTable
```cpp
void ResizeOrNot() {
    if (this->entrCount < this->entries.size()) {
        return;
    }
    int newSize = this->entries.size() * 2;
    vector<pair<string, string>> copy(this->size);
    copy = this->entries;
    this->entries.clear();
    this->entries.resize(newSize);
    this->entrCount = 0;
    for (int i = 0; i < this->size; ++i) {
        if (copy[i].first == "" && copy[i].second == "") {
            continue;
        }
        this->AddToEntries(copy[i].first, copy[i].second);
    }
    this->size = newSize;
    copy.clear();
}
```
- **Purpose:** Call `AddToEntries` within `ResizeOrNot` to rehash all elements after resizing the hashtable. Using `this` ensures the method is called on the current instance.

### Setting and Getting Values
```cpp
void Set(const string& key, const string& value) {
    this->ResizeOrNot();
    this->AddToEntries(key, value);
}

string Get(const string& key) {
    int index = GetHash(key);
    if (index < (int)(this->entries.size()) && entries[index].first != key) {
        index = CollisionHandling(key, index, false);
    }
    if (index == -1 || index >= this->entries.size()) {
        return " ";
    }
    if (entries[index].first == key) {
        return entries[index].second;
    } else {
        throw "Invalid Hashtable!!!!";
    }
}
```
- **Purpose:** Ensure the correct member functions are called for setting and getting values.

### Printing the HashTable
```cpp
void Print() {
    cout << "-----------" << endl;
    cout << "[Size] " << Size() << endl;

    for (int i = 0; i < Size(); i++) {
        if (entries[i].second == "") {
            cout << "[" << i << "] null" << endl;
        } else {
            cout << "[" << i << "] " << entries[i].first << ":" << entries[i].second << endl;
        }
    }

    cout << "============" << endl;
}
```
- **Purpose:** Print the contents of the hashtable, accessing the member variable `entries`.

### Main Function
```cpp
int main() {
    HashTable table;
    table.Print();
    table.Set("Sinar", "sinar@gmail.com");
    table.Set("Elvis", "elvis@gmail.com");
    table.Set("Tane", "tane@gmail.com");
    cout << "[get] " << table.Get("Sinar") << endl;
    table.Set("Gerti", "gerti@gmail.com");
    table.Set("Arist", "arist@gmail.com");
    cout << "[get] " << table.Get("Sinar") << endl;
    return 0;
}
```
- **Purpose:** Demonstrate usage of the `HashTable` class and its functions.

In summary, `this` is used throughout the code to ensure that the member variables and functions of the `HashTable` instance are accessed and modified correctly. It helps avoid ambiguity and makes the code clearer, especially when variable names might overlap with parameters or local variables.
# [[what if not use it]]
