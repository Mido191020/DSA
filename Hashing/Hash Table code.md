```
#include <iostream>  
#include <string>  
#include <vector>  
#include <cstring>  
#include <cstdint>  
#include <stdexcept>  
  
using namespace std;  
  
class Hash {  
public:  
    uint32_t Hash32(const std::string& str) {  
        uint32_t OffsetBasis = 2166136261;  
        uint32_t FNVPrime = 16777619;  
        const char* data = str.c_str();  
        size_t len = str.length();  
        uint8_t* bytes = new uint8_t[len];  
        memcpy(bytes, data, len);  
  
        uint32_t hash = OffsetBasis;  
        for (size_t i = 0; i < len; ++i) {  
            hash = hash ^ bytes[i];  
            hash = hash * FNVPrime;  
        }  
  
        cout << str << ", " << hash << " , " << hex << hash << dec << endl;  
        delete[] bytes;  
        return hash;  
    }  
  
    uint64_t Hash64(const std::string& str) {  
        uint64_t OffsetBasis = 14695981039346656037ull;  
        uint64_t FNVPrime = 1099511628211ull;  
        const char* data = str.c_str();  
        size_t len = str.length();  
        uint8_t* bytes = new uint8_t[len];  
        memcpy(bytes, data, len);  
  
        uint64_t hash = OffsetBasis;  
        for (size_t i = 0; i < len; i++) {  
            hash = hash ^ bytes[i];  
            hash = hash * FNVPrime;  
        }  
  
        cout << str << ", " << hash << ", " << hex << hash << dec << endl;  
        delete[] bytes;  
        return hash;  
    }  
};  
  
class HashTable {  
public:  
    vector<pair<string, string>> entries;  
    int size;  
    int entrCount;  
  
    HashTable() : size(3), entrCount(0) {  
        this->entries = vector<pair<string, string>>(this->size);  
    }  
  
    ~HashTable() { this->entries.clear(); }  
  
    int GetHash(const string& key) {  
        uint32_t FnvOffsetBasis = 2166136261;  
        uint32_t FNVPrime = 16777619;  
        const char* data = key.c_str();  
        uint32_t hash = FnvOffsetBasis;  
        for (size_t i = 0; i < strlen(data); ++i) {  
            hash = hash ^ data[i];  
            hash = hash * FNVPrime;  
        }  
  
        cout << "[hash] " << key << " hash : " << hash << " hex : " << hex << hash << dec << " "  
             << hash % static_cast<uint32_t>(this->size) << endl;  
        return hash % static_cast<uint32_t>(this->size);  
    }  
  
    int CollisionHandling(const string& key, int hash, bool set) {  
     int newHash;  
        for (int i = 1; i <this->size ; ++i) {  
            //Linear probing checks subsequent  
            newHash=(hash+i)% this->size;  
            cout << "[coll] " << key << " " << hash << ", new hash: " << newHash  
                 << endl;  
            if (set&&(this->entries[newHash].first==""&&  
                    this->entries[newHash].second=="")||  
                    this->entries[newHash].first==key){  
             return newHash;  
            } else if (!set&&this->entries[newHash].first==key){  
                return newHash;  
            }  
        }  
        return -1;  
    }  
  
    void AddToEntries(const string& key, const string& value) {  
       int index= GetHash(key);  
       auto iteam=entries[index];  
        if (index==-1){  
            throw "Invalid Hashtable!!!!";  
  
        }  
       //handel if there is a Collision if place مش مناسب  
        if (this->entries[index].first!=""&&  
        this->entries[index].second!=""  
        &&entries[index].first!=key){  
            index= this->CollisionHandling(key,index, true);  
        }  
  
        //لو المكان فاضي بنحط value        if (index< this->entries.size()  
        && this->entries[index].second!=value  
        && this->entries[index].first!=key){  
            this->entries[index]=pair<string ,string >({key,value});  
            this->entrCount++;  
        }  
//if not we update the key  
        else if(this->entries[index].first==key){  
            this->entries[index].second=value;  
        } else{  
            throw "Invalid Hashtable!!!!";  
        }  
    }  
  
    void ResizeOrNot() {  
        if (this->entrCount< this->entries.size()){  
            return;  
        }  
        int newSize= this->entries.size()*2;  
        cout << "[resize] from " << this->size << " to " << newSize << endl;  
       //why add the old size  
        vector<pair<string ,string >>copy(this->size);  
       copy= this->entries;  
        this->entries.clear();  
        //بنعمل array جديدة بن copy فيها حجات القديمة وبعدين نمسح الarray القديمة ونعدل ال size بتعها وبعدها نضيف العناصر فيها تاني ونمسح ال copy        this->entries.resize(newSize);  
        this->entrCount=0;  
        for (int i = 0; i < this->size; ++i) {  
            if (copy[i].first==""&&copy[i].second==""){  
                continue;  
            }  
            //why we use this  
            this->AddToEntries(copy[i].first,copy[i].second);  
        }  
        this->size=newSize;  
        copy.clear();  
  
    }  
  
    void Set(const string& key, const string& value) {  
        this->ResizeOrNot();  
        this->AddToEntries(key,value);  
    }  
  
    string Get(const string& key) {  
       int index= GetHash(key);  
       vector<pair<string ,string >>item(this->entries.size());  
        if (index< (int)(this->entries.size()) && entries[index].first != key){  
            //why false  
            index= CollisionHandling(key,index, false);}  
            if (index==-1||index>= this->entries.size()){  
                return " ";  
        }  
        if (entries[index].first==key){  
            return entries[index].second;  
        } else{  
            throw "Invalid Hashtable!!!!";  
        }  
    }  
  
    int Size() { return this->entries.size(); }  
  
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
};  
  
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
}
```
[[Why we use this]]
[[CollisionHandling  When to Use true and false]]
