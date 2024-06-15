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

# Q3 #
```
 #include <iostream>
#include <fstream>
#include <sstream>
#include <map>
#include <set>
#include <vector>

using namespace std;

struct record {              //struct to store records information
    string type;
    string symbol;
    string price;
    string quantity;
    string expiry_date;
    string strike_price;
    string amendtime;
    string id;
    string parentid;

    record(string t, string s, string p, string q, string e, string sp, string a, string i, string pi) {     //initialise record with values
        type = t;
        symbol = s;
        price = p;
        quantity = q;
        expiry_date = e;
        strike_price = sp;
        amendtime = a;
        id = i;
        parentid = pi;
    }


    //default constructor
    record() : type(""), symbol(""), price(""), quantity(""), expiry_date(""), strike_price(""), amendtime(""), id(""), parentid("") {
    }
};

string trim(string str) {           //trim the extra spaces 
    string s = "";
    for(int i=0;i<str.length();i++){
        if(str[i]=='\t' || str[i]=='\n' || str[i]=='\r' || str[i]=='\f' || str[i]=='\v'){
            continue;
        }
        else{
            s += str[i];
        }
    }
    
    return s;
}


//to split the input file into output files
void splitInput(string input_file, int X) {

    ifstream infile(input_file);

    map<string, record> records;                // id mapped t0 complete record
    map<string, vector<string>> children;        //parent id mapped to children ids
    string line;

    while (getline(infile, line)) {
        stringstream ss(line);
        string type, symbol, price, quantity, expiry_date, strike_price, amendtime, id, parentid;

        getline(ss, type, ',');                 //read each entry delimited by comma
        getline(ss, symbol, ',');
        getline(ss, price, ',');
        getline(ss, quantity, ',');
        getline(ss, expiry_date, ',');
        getline(ss, strike_price, ',');
        getline(ss, amendtime, ',');
        getline(ss, id, ',');
        getline(ss, parentid);
        
        record r(type, symbol, price, quantity, expiry_date, strike_price, amendtime, id, parentid);
    
        records[id] = r;                //map id with record
        parentid = trim(parentid);      //trim the extra spaces in parentid
        
        if (type == "P") {
            if(children.find(parentid)!=children.end())     //map the parent id with its child
                children[parentid].push_back(id);           
            else{
              children.insert({parentid, {id}});   
            }
        } else if (type == "T") {
            if(children.find(id)==children.end())           //if parent id is not present, then create one to not miss parent without children
                children[id] = {};
        }
    }


    infile.close();

    int count = 0;                  //no of entries to be added in file
    vector<record> vec;
    int file = 0;

    for (auto &it : children) {
        string pid = it.first;
        vector<string> rec = it.second;         //ids of children

        vec.push_back(records[pid]);            //add the parent and then children
        count++;        

        for (int i = 0; i < rec.size(); i++) {
                vec.push_back(records[rec[i]]);
                count++;
        }

        if (count >= X) {
            file++;
            ofstream outfile("output_" + to_string(file) + ".txt");
            for (int i = 0; i < vec.size(); i++) {
                outfile << vec[i].type << "," << vec[i].symbol << "," << vec[i].price << "," << vec[i].quantity << "," << vec[i].expiry_date << "," << vec[i].strike_price << "," << vec[i].amendtime << "," << vec[i].id << "," << vec[i].parentid << "\n";
            }
            outfile.close();
            vec.clear();           
            count = 0;
        }
    }

    if (!vec.empty()) {                 //append to the last output file when no.of entries is less than X
        ofstream outfile("output_" + to_string(file) + ".txt", ios::app);
        for (int i = 0; i < vec.size(); i++) {
            outfile << vec[i].type << "," << vec[i].symbol << "," << vec[i].price << "," << vec[i].quantity << "," << vec[i].expiry_date << "," << vec[i].strike_price << "," << vec[i].amendtime << "," << vec[i].id << "," << vec[i].parentid << "\n";
        }
        outfile.close();
    }
}

int main() {
    string input_file = "input.txt";
    int X;
    cout << "Enter the value of X: ";
    cin >> X;

    splitInput(input_file, X);

    return 0;
}

```
