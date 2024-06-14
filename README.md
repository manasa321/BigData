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
