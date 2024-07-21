```
class HashMap {  
public:  
    vector<pair<string ,int>>entries;  
    int size;  
    int enterCount;  
    HashMap():size(3),enterCount(0){  
        this->entries=vector<pair<string ,int>>(this->size,{"",0});  
    }  
    ~HashMap(){  
        this->entries.clear();  
    }  
    int GetHash(const std::string& key) {  
        uint32_t FnvOffsetBasis = 2166136261;  
        uint32_t FNVPrime = 16777619;  
        const char* data = key.c_str();  
        uint32_t hash = FnvOffsetBasis;  
        for (size_t i = 0; i < strlen(data); ++i) {  
            hash = hash ^ data[i];  
            hash = hash * FNVPrime;  
        }  
        return hash % static_cast<uint32_t>(this->size);  
    }  
    int CollisionHandling(const string&key,int hash){  
        int newHash;  
        for (int i = 1; i < this->size ; ++i) {  
            newHash=(hash+i)%this->size;  
            if (this->entries[newHash].first.empty()|| this->entries[newHash].first==key){  
                return newHash;  
            }  
        }  
        return -1;  
    }  
    void AddToEntries(const string&key,int value){  
        int index= GetHash(key);  
        if (index==-1){  
            throw std::runtime_error("Invalid HashMap!");  
        }  
        if (!this->entries[index].first.empty()&& this->entries[index].first!=key){  
            index= this->CollisionHandling(key,index);  
        }  
        if (index< this->entries.size()&&  
                (this->entries[index].first.empty()|| this->entries[index].first!=key)){  
            this->AddToEntries(key,value);  
            this->enterCount++;  
        }  
    }  
    void ResizeOrNot(){  
        if (this->enterCount<this->entries.size()){  
            return;  
        }  
        int newSize= this->entries.size()*2;  
        vector<pair<string ,int>>copy= this->entries;  
        this->entries.clear();  
        this->entries.resize(newSize,{"",0});  
        for (int i = 0; i < this->size; ++i) {  
            if (!copy[i].first.empty()){  
                this->AddToEntries(copy[i].first,copy[i].second);  
            }  
        }  
        this->size=newSize;  
    }  
    //why we make this Add  
    void Add(const string& key, int value){  
        this->ResizeOrNot();  
        this->AddToEntries(key,value);  
    }  
    bool Contains(const string&key){  
        int index= GetHash(key);  
        if (index< this->entries.size()  
        && this->entries[index].first!=key){  
            index= this->CollisionHandling(key,index);  
        }  
        if (index==-1||index> this->entries.size()){  
            return false;  
        }  
        //why we dont just return true?  
        return this->entries[index].first==key;  
    }  
    //Get purpose?  
    bool Get(const string&key,int &value){  
        int index= GetHash(key);  
        if (index< this->entries.size()  
        && this->entries[index].first!=key){  
            index= this->CollisionHandling(key,index);  
        }  
        if (index != -1 && index < this->entries.size() && this->entries[index].first == key) {  
            value = this->entries[index].second;  
            return true;  
        }  
        return false;  
    }  
    void Remove(const string&key){  
        int index = GetHash(key);  
        if (index < this->entries.size() && this->entries[index].first != key) {  
            index = CollisionHandling(key, index);  
        }  
        if (index != -1 && index < this->entries.size() && this->entries[index].first == key) {  
            this->entries[index] = {"", 0};  
            this->enterCount--;  
        }  
  
    }  
    int Size() const { return this->enterCount; }  
    void Print() {  
        std::cout << "-----------" << std::endl;  
        std::cout << "[Size] " << Size() << std::endl;  
        for (int i = 0; i < this->entries.size(); i++) {  
            if (entries[i].first.empty()) {  
                std::cout << "[" << i << "] null" << std::endl;  
            } else {  
                std::cout << "[" << i << "] " << entries[i].first << " -> " << entries[i].second << std::endl;  
            }  
        }  
        std::cout << "============" << std::endl;  
    }  
    bool find(const string&key,int & value){  
        int index = GetHash(key);  
        if (index < this->entries.size() && this->entries[index].first != key) {  
            index = this->CollisionHandling(key, index);  
        }  
        if (index != -1 && index < this->entries.size() && this->entries[index].first == key) {  
            value = this->entries[index].second;  
            return true;  
        }  
        return false;  
    }  
};
```