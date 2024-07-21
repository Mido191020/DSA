Let's dive deeper into why we use `this` and what could happen if we don't use it.

### Why We Use `this`

1. **Disambiguation:**
   `this` is used to distinguish member variables from local variables or parameters with the same name. For example:
   ```cpp
   class Example {
   private:
       int size;

   public:
       Example(int size) {
           this->size = size; // Uses this->size to refer to the member variable
       }
   };
   ```
   Without `this`, the compiler would not be able to differentiate between the parameter `size` and the member variable `size`.

2. **Clarification:**
   Using `this` makes it clear that a variable or function belongs to the instance of the class. This improves code readability and maintainability.

3. **Function Chaining:**
   `this` can be used to return the current object instance, allowing for method chaining.
   ```cpp
   class Example {
   public:
       Example& setValue(int value) {
           this->value = value;
           return *this;
       }
   };
   ```

4. **Passing the Current Object:**
   Sometimes, it's necessary to pass the current object to another function or method.
   ```cpp
   void anotherFunction(Example* example) {
       // Do something with example
   }

   void aMethod() {
       anotherFunction(this);
   }
   ```

### What If We Don't Use `this`

1. **Potential Ambiguity:**
   If a member variable has the same name as a local variable or parameter, the compiler will prioritize the local scope. This can lead to bugs.
   ```cpp
   class Example {
   private:
       int size;

   public:
       Example(int size) {
           size = size; // This sets the parameter size to itself, not the member variable
       }
   };
   ```

2. **Less Readable Code:**
   Without `this`, it can be unclear whether a variable or function is a member of the class or a local variable. This decreases code readability.
   ```cpp
   class Example {
   private:
       int value;

   public:
       void setValue(int value) {
           // Without this->, it's unclear which value is which
           value = value; // This is a no-op; it doesn't set the member variable
       }
   };
   ```

3. **Errors in Member Function Calls:**
   When calling member functions within other member functions, omitting `this` can sometimes lead to errors if there are local functions or variables with the same name.
   ```cpp
   class Example {
   public:
       void methodA() {
           // Calls the member function methodB
           this->methodB();
       }

       void methodB() {
           // Some implementation
       }
   };
   ```

### Examples in Your Code

Here are specific examples from your `HashTable` class where `this` is essential:

1. **Constructor Initialization:**
   ```cpp
   HashTable() : size(3), entrCount(0) {
       this->entries = vector<pair<string, string>>(this->size);
   }
   ```
   - **Without `this`:** The member variable `entries` might be confused with a local variable if such a local variable existed.
   
2. **Member Function Calls:**
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
       // ... more code ...
   }
   ```
   - **Without `this`:** The call to `CollisionHandling` could be ambiguous if there were a local function or variable with the same name.

3. **Accessing Member Variables:**
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
   - **Without `this`:** The member variables `entrCount`, `entries`, and `size` could be confused with local variables if such local variables existed.

### Summary

Using `this` ensures clarity and correctness in your code. It makes it explicit that you are referring to member variables or member functions, avoiding potential conflicts with local variables or parameters. It also aids in code readability and maintainability, making it easier for others (and yourself) to understand and work with the code.