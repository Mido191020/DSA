```
class HashSet {  
public:  
    vector<string>entries;  
    int size;  
    int enterCount;  
    HashSet():size(3),enterCount(0){  
        this->entries=vector<string >(this->size);  
    }  
    ~HashSet(){  
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
    //why const ,why&  
    int CollisionHandling(const string&key,int hash){  
        int newHash;  
        for (int i = 1; i < this->size; ++i) {  
            newHash=(hash+i)% this->size;  
            if (this->entries[newHash].empty()|| this->entries[newHash]==key){  
                return newHash;  
            }  
  
        }  
        return -1;  
    }  
   void AddToEntries(const string &key){  
        int index= GetHash(key);  
       if (index==-1){  
           throw std::runtime_error("Invalid HashSet!!!!");  
       }  
       //mean there is a key in this index so we should handling collesion  
       if (!this->entries[index].empty()&& this->entries[index]!=key){  
           index=this->CollisionHandling(key,index);  
       }  
       //mean there is no key in this index  
       if (index<this->entries.size()&&this->entries[index]!=key){  
           this->entries[index]=key;  
           //to know ifI should resize the array or not  
           this->enterCount++;  
       }  
    }  
    void ResizeOrNot(){  
        if (this->enterCount< this->entries.size()){  
            return;  
        }  
        //why *2? becuse the cose of resize  
        int newSiz=this->entries.size()*2;  
        std::cout << "[resize] from " << this->size << " to " << newSiz << std::endl;  
        vector<string >copy= this->entries;  
        this->entries.clear();  
        this->entries.resize(newSiz);  
        for (int i = 0; i < this->size; ++i) {  
            if (!copy.empty()){  
                this->AddToEntries(copy[i]);  
            }  
        }  
        this->size=newSiz;  
    }  
    //explain what is this and the purpose  
    void Add(const std::string& key) {  
        this->ResizeOrNot();  
        this->AddToEntries(key);  
    }  
    bool contains(const string&key){  
        int index= GetHash(key);  
        if (index< this->entries.size()&&this->entries[index]!=key){  
            index= CollisionHandling(key,index);  
        }  
        if (index==-1||index>= this->entries.size()){  
            return false;  
        }  
        return this->entries[index]==key;  
    }  
    void Remove(const string&key){  
        int index= GetHash(key);  
        //why  
        if (index < this->entries.size() && entries[index] != key) {  
            index = CollisionHandling(key, index);  
        }  
        if (index!=-1  
        &&index<this->entries.size()  
        &&this->entries[index]==key  
        ){  
            this->entries[index]="";  
            this->enterCount--;  
        }  
    }  
   int Search(const string&key){  
        int index = GetHash(key);  
        if (index < this->entries.size() && entries[index] != key) {  
            index = CollisionHandling(key, index);  
        }  
        if (index != -1 && index < this->entries.size() && entries[index] == key) {  
            return index;  
        }  
        return -1;  
    }  
    int Size() { return this->enterCount; }  
    void Print() {  
        std::cout << "-----------" << std::endl;  
        std::cout << "[Size] " << Size() << std::endl;  
  
        for (int i = 0; i < this->entries.size(); i++) {  
            if (entries[i].empty()) {  
                std::cout << "[" << i << "] null" << std::endl;  
            } else {  
                std::cout << "[" << i << "] " << entries[i] << std::endl;  
            }  
        }  
  
        std::cout << "============" << std::endl;  
    }  
};
```
