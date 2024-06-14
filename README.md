# Q1 #

```
// Online C++ compiler to run C++ program online
#include <iostream>
#include <map>
#include <vector>
#include <climits>

using namespace std;

int abs(int &x){
    if(x<0)
        return -1*x;
    return x;
}

void findpair(long long target, vector<int>& nums, pair<int,int> &p, int min_diff){
    map<int,vector<int>> mp;
    for(int i=0;i<nums.size();i++){
        if(mp.find(target-nums[i])==mp.end())
            mp[target-nums[i]] = {i};
        else
            mp[target-nums[i]].push_back(i);
    }
    
    for(int i=0;i<nums.size();i++){
        if(mp.find(nums[i])!=mp.end()){
            vector<int> vec = mp[nums[i]];
            for(int j=0;j<vec.size();j++){
                int diff = abs(vec[j]-i);
                if(diff<min_diff){
                    min_diff = diff;
                    if(i>vec[j])
                        p = {nums[vec[j]], nums[i]};
                    else
                        p = {nums[i], nums[vec[j]]};
                }
            }
        }
    }
}

int main() {
    // Write C++ code here
    int n;
    cin>>n;
    vector<int> nums;
    for(int i=0;i<n;i++){
        int x;
        cin>>x;
        nums.push_back(x);
    }
    
    long long target;
    cin>>target;
    
    pair<int, int> p;
    int min_diff = INT_MAX;
    
    findpair(target, nums, p, min_diff);
    cout<<p.first<<" "<<p.second;

    return 0;
}

```

# Q2 #
```
// Online C++ compiler to run C++ program online
#include <iostream>

using namespace std;

struct Node{
    int data;
    Node *next;
    Node(int a){
        data = a;
        next = NULL;
    }
};

struct Queue {
    Node *front;
    Node *rear;
    void Enqueue(int);
    int Dequeue();
    Queue() {front = rear = NULL;}
    Queue(const Queue&);
    int version = 0;
}; 

struct QueueListNode {
    Queue *QNode;
    QueueListNode* next;
    void Print(int,QueueListNode*);
    Queue* deepcopy(Queue*);
    QueueListNode(Queue* q) {
        QNode = q;
        next = NULL;
    }
};

Queue :: Queue(const Queue& q) {
    if (q.front == nullptr) {
        front = rear = nullptr;
    } else {
        front = new Node(q.front->data);
        Node* current = front;
        Node* qCurrent = q.front->next;
        while (qCurrent != nullptr) {
            current->next = new Node(qCurrent->data);
            current = current->next;
            qCurrent = qCurrent->next;
        }
        rear = current;
    }
}

void Queue:: Enqueue(int x){
        version++;
        Node* t = new Node(x);
        if(front==NULL){
            front = t;
        }
        if(rear == NULL){
            rear = t;
        }
        else{
            rear->next = t;
            rear = rear->next;
        }
}

int Queue :: Dequeue(){
        version++; 
        
        if(front==NULL){
            return -1;
        }
        int x = front->data;
        front = front->next;
        
        return x;
}

Queue* QueueListNode :: deepcopy(Queue* q){
    return new Queue(*q);
}

void QueueListNode :: Print(int v, QueueListNode* qhead){
    QueueListNode* temp = qhead;
    
    while(v>0 && temp!=NULL){
        v--;
        temp = temp->next;
    }
    
    Node* ptr = temp->QNode->front;
    while(ptr!=NULL){
        int val = ptr->data;
        ptr = ptr->next;
        cout<<val<<" ";
    }
    cout<<endl;
}

int main() {
    // Write C++ code here
    
    Queue *q = new Queue();
    QueueListNode *ql = new QueueListNode(q);
    QueueListNode *qhead = ql;
    
    int n;
    cin>>n;
    
    for(int i=0; i<n;i++){
        string query;
        cin>>query;
        if(query=="Enqueue"){
            int x;
            cin>>x;
            q->Enqueue(x);
            Queue* t = qhead->deepcopy(q);
            ql->next = new QueueListNode(t);
            ql = ql->next;
        
        }
        else if(query=="Dequeue"){
            q->Dequeue();
            Queue* t = qhead->deepcopy(q);
            ql->next = new QueueListNode(t);
            ql = ql->next;
        
        }
        else if(query=="Print"){
            int x;
            cin>>x;
            try {
                if(x>q->version){
                    throw runtime_error("input can't be greater than version number");
                }
            }
            catch (const exception& e) {
                cout<<"Exception caught: "<< e.what()<<endl;
            }
            qhead->Print(x, qhead);
        }
    }
    
    
    return 0;
}
```
