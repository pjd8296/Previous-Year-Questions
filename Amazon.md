## Favorite Genre
Visit [here](https://www.google.com/url?q=https://leetcode.com/discuss/interview-question/373006&sa=D&ust=1602672883036000&usg=AOvVaw16XOb-wL6mszWwy96jQLKX) for explanation
```c++
    unordered_map<string,vector<string>> songsAndGenre(unordered_map<string,vector<string>>& users, unordered_map<string,vector<string>>& genres){
    unordered_map<string,string> songToGenre;
    unordered_map<string,unordered_map<string,int>> userToGenre;
    unordered_map<string,vector<string>> result;
    unordered_map<string,int> max;
    for(auto genre:genres)
    {
        for(auto song: genre.second)
        {
            songToGenre[song] = genre.first;
        }
    }
    
    for(auto user:users)
    {
        for(auto item:user.second)
        {
            userToGenre[user.first][songToGenre[item]]++;
            auto tempMax = userToGenre.at(user.first).at(songToGenre[item]);
            max[user.first] = std::max(tempMax,max[user.first]);
        }
    }
    
    for(auto user:userToGenre)
    {
        for(auto genre:user.second)
        {
            if(genre.second==max.at(user.first))
            {
                result[user.first].push_back(genre.first);
            }
        }
    }
    
    return result;
}

int main() {
    unordered_map<string,vector<string>> users;
    users["David"] = {"song1", "song2", "song3", "song4", "song8"};
    users["Emma"] = {"song5", "song6", "song7"};
    
    unordered_map<string,vector<string>> songs;
    songs["Rock"] = {"song1", "song3"};
    songs["Dubstep"] = {"song7"};
    songs["Techno"] = {"song2", "song4"};
    songs["Pop"] = {"song5", "song6"};
    songs["Jazz"] = {"song8", "song9"};

    auto result = songsAndGenre(users,songs);
    for(auto x: result)
    {
        cout<<x.first<<" : ";
        for(auto song:x.second)
        {
            cout<<song<<" ";
        }
        cout<<endl;
    }
    
    users.clear();
    songs.clear();
    
    users["David"] = {"song1", "song2"};
    users["Emma"] = {"song3", "song4"};
    
    result = songsAndGenre(users,songs);
    for(auto x: result)
    {
        cout<<x.first<<" : ";
        for(auto song:x.second)
        {
            cout<<song<<" ";
        }
        cout<<endl;
    } 
}
```
## Subtree of another tree
<details>
    <summary>Solution</summary>

```c++
class Solution {
public:
    bool inorder(TreeNode* s, TreeNode* t) {
        if(!s and !t) return true;
        if(!s or !t) return false;
        bool b1 = inorder(s->left, t->left);
        if(s->val!= t->val)
            return false;
        bool b2 = inorder(s->right, t->right);
        return b1 and b2;
    }
    bool isSubtree(TreeNode* s, TreeNode* t) {
        if(!s) return false;
        bool b1 = isSubtree(s->left, t);
        if(s->val == t->val and inorder(s, t)) return true;
        bool b2 = isSubtree(s->right, t);
        return b1 or b2;
    }
};
```
</details>

## Critical Connections
<details>
    <summary>Solution</summary>

```c++
class Solution {
public:
    vector<vector<int>> graph;
    vector<int> ranks;

    vector<vector<int>> criticalConnections(int n, vector<vector<int>>& connections) {
        graph.resize(n);
        for (auto& conn : connections) {
            graph[conn[0]].push_back(conn[1]);
            graph[conn[1]].push_back(conn[0]);
        }
        ranks.resize(n, -2);

        vector<vector<int>> res;
        dfs(0, 0, res);  
        return res;
    }

    int dfs(int node, int rank, vector<vector<int>>& res) {
        if (ranks[node] >= 0) return ranks[node];

        ranks[node] = rank;
        int minRank = rank;
        
        for (auto neighbor : graph[node]) {
            if (ranks[neighbor] == rank - 1 || ranks[neighbor] > rank) continue;
            int neighborRank = dfs(neighbor, rank + 1, res);
            minRank = min(minRank, neighborRank);
            if (neighborRank > rank) res.push_back({node, neighbor});
        }
        return minRank;
    }
};
```