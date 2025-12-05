# Leetcode ：207.课程表

## 一、题目链接
# 示例：[LeetCode 208. 实现Trie（前缀树）](https://leetcode.cn/problems/implement-trie-prefix-tree/description/?envType=study-plan-v2&envId=top-100-liked)

## 二、题目描述
完善Trie类的初始化，插入，查找字符串和查找前缀的函数


## 三、解题思路与代码实现
### 1. 核心思路
实现Trie即前缀树类，定义一个包含26个Trie类的vector容器，分别表示每一个小写字母，当插入时，头节点为首个类，循环字符串的每一个字母，将该节点指向下一个字母节点，即node->children[ch-'a']，并定义一个类成员isEnd，当插入字符串最后一个字母时，设为True，方便查找前缀和字符串


### 2. 代码实现
```C++
# 深度优先算法：
class Trie {
private:
    vector<Trie*> children;
    bool isEnd;
    Trie* searchPrefix(string prefix)
    {
        Trie* node = this;
        for( auto ch : prefix )
        {
            if( node->children[ch-'a'] == nullptr )
                return nullptr;
            node = node->children[ch-'a'];
        }
        return node;
    }
public:
    Trie() : children(26) , isEnd(false) {}
    
    void insert(string word) {
        Trie* node = this;
        for( auto ch : word ) {
            if( node->children[ch - 'a'] == nullptr )
                node->children[ch - 'a'] = new Trie();
            node = node->children[ch-'a']; 
        }
        node->isEnd = true;
    }
    
    bool search(string word) {
        Trie* node = searchPrefix(word);
        return node && node->isEnd; 
    }
    
    bool startsWith(string prefix) {
        Trie* node = searchPrefix(prefix);
        return node ;
    }
};

/**
 * Your Trie object will be instantiated and called as such:
 * Trie* obj = new Trie();
 * obj->insert(word);
 * bool param_2 = obj->search(word);
 * bool param_3 = obj->startsWith(prefix);
 */