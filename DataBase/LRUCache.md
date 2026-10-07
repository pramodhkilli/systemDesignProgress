# LRU cache

this is more of a how you kind of solve it, instead of what it is

so as the name suggests, it is just a cache with a fixed storage, and the eviction policy is that the Least Recently Used one should be evicted

so we use doubly linkedlist to achieve this, because when we use a object that is already there in cache, but it got used recently, we have to put it at the start, so to know where it is, and its neighbours, we have to have pointers to the neighbours and we store the key to object mapping in a map

so when inserting, as it is the recently used as well, we create a new object if it is not present already, and insert it at the head of the linkedlist, and kind of move everything to the right

if it is already present, we remove it first from that spot, adjust its neighbours(pointer manipulation), then insert this at the start of the list

and we do have checks if it hits the size, if so, we remove the last object at the tail

while readind the cache, we remove the object from its position and adjust neighbours, and insert this at the start of the list, that is the basic idea

```
class dll{
public:
    int key,val;
    dll* next;
    dll* prev;
    dll(int key, int value){
        this->key = key;
        this->val = value;
    }
};

class LRUCache {
public:
    dll* head;
    dll* tail;
    int size;
    unordered_map<int,dll*> mappa;
    LRUCache(int capacity) {
        this->size = capacity;
        head = new dll(-1,-1);
        tail = new dll(-1,-1);
        head->next = tail;
        head->prev = tail;
        tail->next = head;
        tail->prev = head;
    }
    void remove(dll* cur){
        dll* curNext = cur->next;
        dll* curPrev = cur->prev;
        curNext->prev = curPrev;
        curPrev->next = curNext;
    }
    void addAfterHead(dll* cur){
        dll* next = head->next;
        next->prev = cur;
        cur->next = next;
        cur->prev = head;
        head->next = cur;
    }
    int get(int key) {
        if(mappa.find(key)==mappa.end()){
            return -1;
        }
        dll* cur = mappa[key];
        remove(cur);
        addAfterHead(cur);
        return mappa[key]->val;
    }
    
    void put(int key, int value) {
        if(mappa.find(key)!=mappa.end()){
            dll* cur = mappa[key];
            cur->val = value;
            remove(cur);
            addAfterHead(cur);
        }else{
            dll* cur = new dll(key,value);
            if(mappa.size()<size){
                addAfterHead(cur);
            }else{
                int lastKey = tail->prev->key;
                remove(tail->prev);
                mappa.erase(lastKey);
                addAfterHead(cur);
            }
            mappa[key] = cur;
        }

        // dll* temp = head->next;
        // while(temp!=tail){
        //     cout<<temp->key<<" ";
        //     temp = temp->next;
        // }
        // cout<<"\n";
    }
};

/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache* obj = new LRUCache(capacity);
 * int param_1 = obj->get(key);
 * obj->put(key,value);
 */
```
