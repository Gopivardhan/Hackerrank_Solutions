<h1>DSBS hacker rank</h1>

<h2>Compare two linked lists</h2>

<h3>You’re given the pointer to the head nodes of two linked lists. Compare the data in the nodes of the linked lists to check if they are equal. If all data attributes are equal and the lists are the same length, return . Otherwise, return .

Example



The two lists have equal data attributes for the first  nodes.  is longer, though, so the lists are not equal. Return .

Function Description

Complete the compare_lists function in the editor below.

compare_lists has the following parameters:

SinglyLinkedListNode llist1: a reference to the head of a list
SinglyLinkedListNode llist2: a reference to the head of a list
Returns

int: return 1 if the lists are equal, or 0 otherwise
Input Format

The first line contains an integer , the number of test cases.

Each of the test cases has the following format:
The first line contains an integer , the number of nodes in the first linked list.
Each of the next  lines contains an integer, each a value for a data attribute.
The next line contains an integer , the number of nodes in the second linked list.
Each of the next  lines contains an integer, each a value for a data attribute.

Constraints

Output Format

Compare the two linked lists and return 1 if the lists are equal. Otherwise, return 0. Do NOT print anything to stdout/console.

The output is handled by the code in the editor and it is as follows:

For each test case, in a new line, print  if the two lists are equal, else print .

Sample Input

2
2
1
2
1
1
2
1
2
2
1
2
Sample Output

0
1
Explanation

There are  test cases, each with a pair of linked lists.

In the first case, linked lists are: 1 -> 2 -> NULL and 1 -> NULL

In the second case, linked lists are: 1 -> 2 -> NULL and 1 -> 2 -> NULL</h3>

```python3
#!/bin/python3

import os
import sys

class SinglyLinkedListNode:
    def __init__(self, node_data):
        self.data = node_data
        self.next = None

class SinglyLinkedList:
    def __init__(self):
        self.head = None
        self.tail = None

    def insert_node(self, node_data):
        node = SinglyLinkedListNode(node_data)

        if not self.head:
            self.head = node
        else:
            self.tail.next = node


        self.tail = node

def print_singly_linked_list(node, sep, fptr):
    while node:
        fptr.write(str(node.data))

        node = node.next

        if node:
            fptr.write(sep)
            
def compare_lists(llist1, llist2):
    if llist1 is None:
        return 1 if llist2 is None else 0
    if llist2 is None:
        return 0
    if llist1.data != llist2.data:
        return 0
    else:
        return compare_lists(llist1.next, llist2.next)
if __name__ == '__main__':
    fptr = open(os.environ['OUTPUT_PATH'], 'w')

    tests = int(input())

    for tests_itr in range(tests):
        llist1_count = int(input())

        llist1 = SinglyLinkedList()

        for _ in range(llist1_count):
            llist1_item = int(input())
            llist1.insert_node(llist1_item)
            
        llist2_count = int(input())

        llist2 = SinglyLinkedList()

        for _ in range(llist2_count):
            llist2_item = int(input())
            llist2.insert_node(llist2_item)

        result = compare_lists(llist1.head, llist2.head)

        fptr.write(str(int(result)) + '\n')

    fptr.close()
        
```

<h2>Tree: Huffman Decoding</h2>

<h3>Huffman coding assigns variable length codewords to fixed length input characters based on their frequencies. More frequent characters are assigned shorter codewords and less frequent characters are assigned longer codewords. All edges along the path to a character contain a code digit. If they are on the left side of the tree, they will be a 0 (zero). If on the right, they'll be a 1 (one). Only the leaves will contain a letter and its frequency count. All other nodes will contain a null instead of a character, and the count of the frequency of all of it and its descendant characters.

For instance, consider the string ABRACADABRA. There are a total of  characters in the string. This number should match the count in the ultimately determined root of the tree. Our frequencies are  and . The two smallest frequencies are for  and , both equal to , so we'll create a tree with them. The root node will contain the sum of the counts of its descendants, in this case . The left node will be the first character encountered, , and the right will contain . Next we have  items with a character count of : the tree we just created, the character  and the character . The tree came first, so it will go on the left of our new root node.  will go on the right. Repeat until the tree is complete, then fill in the 's and 's for the edges. The finished graph looks like:

image

Input characters are only present in the leaves. Internal nodes have a character value of ϕ (NULL). We can determine that our values for characters are:

A - 0
B - 111
C - 1100
D - 1101
R - 10
Our Huffman encoded string is:

A B    R  A C     A D     A B    R  A
0 111 10 0 1100 0 1101 0 111 10 0
or
01111001100011010111100
To avoid ambiguity, Huffman encoding is a prefix free encoding technique. No codeword appears as a prefix of any other codeword.

To decode the encoded string, follow the zeros and ones to a leaf and return the character there.

You are given pointer to the root of the Huffman tree and a binary coded string to decode. You need to print the decoded string.

Function Description

Complete the function decode_huff in the editor below. It must return the decoded string.

decode_huff has the following parameters:

root: a reference to the root node of the Huffman tree
s: a Huffman encoded string
Input Format

There is one line of input containing the plain string, . Background code creates the Huffman tree then passes the head node and the encoded string to the function.

Constraints


Output Format

Output the decoded string on a single line.

Sample Input

image
s="1001011"
Sample Output

ABACA
Explanation

S="1001011"
Processing the string from left to right.
S[0]='1' : we move to the right child of the root. We encounter a leaf node with value 'A'. We add 'A' to the decoded string.
We move back to the root.

S[1]='0' : we move to the left child. 
S[2]='0' : we move to the left child. We encounter a leaf node with value 'B'. We add 'B' to the decoded string.
We move back to the root.

S[3] = '1' : we move to the right child of the root. We encounter a leaf node with value 'A'. We add 'A' to the decoded string.
We move back to the root.

S[4]='0' : we move to the left child. 
S[5]='1' : we move to the right child. We encounter a leaf node with value C'. We add 'C' to the decoded string.
We move back to the root.

 S[6] = '1' : we move to the right child of the root. We encounter a leaf node with value 'A'. We add 'A' to the decoded string.
We move back to the root.

Decoded String = "ABACA"</h3>

```python3

import queue as Queue

cntr = 0

class Node:
    def __init__(self, freq, data):
        self.freq = freq
        self.data = data
        self.left = None
        self.right = None
        global cntr
        self._count = cntr
        cntr = cntr + 1
        
    def __lt__(self, other):
        if self.freq != other.freq:
            return self.freq < other.freq
        return self._count < other._count

def huffman_hidden():#builds the tree and returns root
    q = Queue.PriorityQueue()

    
    for key in freq:
        q.put((freq[key], key, Node(freq[key], key) ))
    
    while q.qsize() != 1:
        a = q.get()
        b = q.get()
        obj = Node(a[0] + b[0], '\0' )
        obj.left = a[2]
        obj.right = b[2]
        q.put((obj.freq, obj.data, obj ))
        
    root = q.get()
    root = root[2]#contains root object
    return root

def dfs_hidden(obj, already):
    if(obj == None):
        return
    elif(obj.data != '\0'):
        code_hidden[obj.data] = already
        
    dfs_hidden(obj.right, already + "1")
    dfs_hidden(obj.left, already + "0")
def decodeHuff(root, s):
    #Enter Your Code Here
    cur = root
    chararray = []
    #For each character, 
    #If at an internal node, move left if 0, right if 1
    #If at a leaf (no children), record data and jump back to root AFTER processing character
    for c in s:
        if c == '0' and cur.left:
            cur = cur.left
        elif cur.right:
            cur = cur.right
        
        if cur.left is None and cur.right is None:
            chararray.append(cur.data)
            cur = root
    
    #Print final array
    print("".join(chararray))

	#Enter Your Code Here
ip = input()
freq = {}#maps each character to its frequency

cntr = 0

for ch in ip:
    if(freq.get(ch) == None):
        freq[ch] = 1
    else:
        freq[ch]+=1

root = huffman_hidden()#contains root of huffman tree

code_hidden = {}#contains code for each object

dfs_hidden(root, "")

if len(code_hidden) == 1:#if there is only one character in the i/p
    for key in code_hidden:
        code_hidden[key] = "0"

toBeDecoded = ""

for ch in ip:
   toBeDecoded += code_hidden[ch]

decodeHuff(root, toBeDecoded)


```

<h2>Cycle Detection</h2>
<h3>A linked list is said to contain a cycle if any node is visited more than once while traversing the list. Given a pointer to the head of a linked list, determine if it contains a cycle. If it does, return . Otherwise, return .

Example

 refers to the list of nodes 

The numbers shown are the node numbers, not their data values. There is no cycle in this list so return .

 refers to the list of nodes 

There is a cycle where node 3 points back to node 1, so return .

Function Description

Complete the has_cycle function in the editor below.

It has the following parameter:

SinglyLinkedListNode pointer head: a reference to the head of the list
Returns

int:  if there is a cycle or  if there is not
Note: If the list is empty,  will be null.

Input Format

The code stub reads from stdin and passes the appropriate argument to your function. The custom test cases format will not be described for this question due to its complexity. Expand the section for the main function and review the code if you would like to figure out how to create a custom case.

Constraints

Sample Input

References to each of the following linked lists are passed as arguments to your function:

Sample Inputs
Sample Output

0
1
Explanation

The first list has no cycle, so return .
The second list has a cycle, so return .</h3>

```python3
#!/bin/python3

import math
import os
import random
import re
import sys

class SinglyLinkedListNode:
    def __init__(self, node_data):
        self.data = node_data
        self.next = None

class SinglyLinkedList:
    def __init__(self):
        self.head = None
        self.tail = None

    def insert_node(self, node_data):
        node = SinglyLinkedListNode(node_data)

        if not self.head:
            self.head = node
        else:
            self.tail.next = node


        self.tail = node

def print_singly_linked_list(node, sep, fptr):
    while node:
        fptr.write(str(node.data))

        node = node.next

        if node:
            fptr.write(sep)
# Complete the has_cycle function below.

#
# For your reference:
#
# SinglyLinkedListNode:
#     int data
#     SinglyLinkedListNode next
#
#
def has_cycle(head):
    visited = set()
    f = head
    while f:
        i = id(f)
        if i in visited:
            return 1
        visited.add(i)
        f = f.next
    return 0
    
if __name__ == '__main__':
    fptr = open(os.environ['OUTPUT_PATH'], 'w')

    tests = int(input())

    for tests_itr in range(tests):
        index = int(input())

        llist_count = int(input())

        llist = SinglyLinkedList()

        for _ in range(llist_count):
            llist_item = int(input())
            llist.insert_node(llist_item)

        extra = SinglyLinkedListNode(-1);
        temp = llist.head;

        for i in range(llist_count):
            if i == index:
                extra = temp

            if i != llist_count-1:
                temp = temp.next

        temp.next = extra

        result = has_cycle(llist.head)

        fptr.write(str(int(result)) + '\n')

    fptr.close()
```


<h2>Strongly Connected Digraphs</h2>
<h3></h3>

```C
include <vector> 
#include <list> 
#include <map> 
#include <set> 
#include <queue>
#include <stack> 
#include <bitset> 
#include <algorithm> 
#include <numeric> 
#include <utility> 
#include <sstream> 
#include <iostream> 
#include <iomanip> 
#include <cstdio> 
#include <cmath> 
#include <cstdlib> 
#include <ctime> 
#include <cstring> 

using namespace std; 

typedef long long ll; 
typedef pair<int, int> pii;

#define INF 1000000000
#define pb push_back 
#define itr iterator 
#define sz size() 
#define mp make_pair

const int mod = 1000000007;

long long pot[1100000];
long long ch[1100][1100];
long long s[1100];
long long nn[1100];

// a*x + b*y = gcd(a,b)
int extGcd(int  a, int b, int &x, int &y){
    if(b == 0){
        x = 1;
        y = 0;
        return a;
    }
    
    int g = extGcd(b,a % b,y,x);
    y -= a / b * x;
    return g;
}

// ASSUME: gcd(a, m) == 1
int modInv(int a){
    int x,y;
    extGcd(a, mod, x, y);
    return (x % mod + mod) % mod;
}

int main() {
    pot[0] = 1;
    for (int i = 1; i <= 1100000; i++) {
        pot[i] = (pot[i-1] * 2) % mod;
    }

    for (int i = 0; i <= 1000; i++) {
        for (int j = 0; j <= i; j++) {
            if (j == 0) ch[i][j] = 1;
            else ch[i][j] = (ch[i-1][j-1] + ch[i-1][j]) % mod;
        }
    }

    nn[0] = 1;
    for (int n = 1; n <= 1000; n++) {
        for (int i = 1; i <= n; i++) {
            long long th = (ch[n][i] * pot[i * (n-1)]) % mod;
            nn[n] -= th * nn[n-i];
            nn[n] = ((nn[n] % mod) + mod) % mod;
        }

        long long nnn = nn[n];
        for (int i = 1; i < n; i++) {
            long long th = (ch[n-1][i-1] * s[i]) % mod; 
            th = (th * nn[n-i]) % mod;
            nnn = (nnn + th) % mod;
        }


        s[n] = mod-nnn;
        //printf("%lld\n", s[n]);
    }

    int t, n;
    for (scanf("%d", &t); t; t--) {
        scanf("%d", &n);
        printf("%lld\n", s[n]);
    }
}

```


<h2>Tree: Inorder Traversal</h2>
<h3></h3>

```py
class Node:
    def _init_(self, info): 
        self.info = info  
        self.left = None  
        self.right = None 
        self.level = None 

    def _str_(self):
        return str(self.info) 

class BinarySearchTree:
    def _init_(self): 
        self.root = None

    def create(self, val):  
        if self.root == None:
            self.root = Node(val)
        else:
            current = self.root
         
            while True:
                if val < current.info:
                    if current.left:
                        current = current.left
                    else:
                        current.left = Node(val)
                        break
                elif val > current.info:
                    if current.right:
                        current = current.right
                    else:
                        current.right = Node(val)
                        break
                else:
                    break                                                                                                                                                           def inOrder(root):
    if root:
        inOrder(root.left)
        print(root.info, end=" ")
        inOrder(root.right)                                                                                                                            tree = BinarySearchTree()
t = int(input())

arr = list(map(int, input().split()))

for i in range(t):
    tree.create(arr[i])

inOrder(tree.root)
```


<h2>Even Tree</h2>
<h3></h3>

```
#!/usr/bin/python3
from collections import deque

tree_length, edges = map(int, input().strip().split())
tree = [list() for i in range(tree_length)]

for i in range(edges):
    parent, child = map(int, input().strip().split())
    parent -= 1
    child -= 1
    tree[parent].append(child)
    tree[child].append(parent)

def reconstruct(tree):
    visited = [False] * len(tree)
    queue = deque([0])
    reconstructed = [list() for i in range(len(tree))]
    while len(queue) > 0:
        current = queue.popleft()
        visited[current] = True
        for i in tree[current]:
            if not visited[i]:
                reconstructed[current].append(i)
                queue.append(i)
    return reconstructed

cuts = 0
def dfs(tree, index):
    global cuts
    subtrees = []
    for i in tree[index]:
        subtrees.append(dfs(tree, i))
    for vertices in subtrees[:]:
        if not vertices % 2:
            cuts += 1
            subtrees.remove(vertices)

    return sum(subtrees) + 1
tree = reconstruct(tree)
dfs(tree, 0)
print(cuts)
```



<h2>Knapsack</h2>
<h3>Given an array of integers and a target sum, determine the sum nearest to but not exceeding the target that can be created. To create the sum, use any element of your array zero or more times.

For example, if  and your target sum is , you might select  or . In this case, you can arrive at exactly the target.

Function Description

Complete the unboundedKnapsack function in the editor below. It must return an integer that represents the sum nearest to without exceeding the target value.

unboundedKnapsack has the following parameter(s):

k: an integer
arr: an array of integers
Input Format

The first line contains an integer , the number of test cases.

Each of the next  pairs of lines are as follows:
- The first line contains two integers  and , the length of  and the target sum.
- The second line contains  space separated integers .

Constraints



Output Format

Print the maximum sum for each test case which is as near as possible, but not exceeding, to the target sum on a separate line.

Sample Input

2
3 12
1 6 9
5 9
3 4 4 4 8
Sample Output

12
9
Explanation

In the first test case, one can pick {6, 6}. In the second, we can pick {3,3,3}.</h3>

```cpp

#include <bits/stdc++.h>
using namespace std;
vector <int> c; int dp[2005]; 
int main()
{
    int tc; cin >> tc;
    for (int g=0;g<tc; g++){c.clear(); memset(dp,0,sizeof(dp)); 
    int a,b; cin >> a >> b;
    for (int g=0;g<a; g++)
    {
    int d; cin >> d; c.push_back(d); 
    }sort(c.begin(), c.end());
    for (int g=1;g<=b; g++)
    {
        for (int y=0;y<c.size(); y++)
        {
            if (c[y]>g) continue;
            dp[g]=max(dp[g], c[y]+dp[g-c[y]]); 
        }
    }
    cout << dp[b] << '\n';} return 0; 
}

```


<h2>Travel in HackerLand</h2>
<h3>HackerLand is a country with  beautiful cities and  undirected roads. Like every other beautiful country, HackerLand has traffic jams.

Each road has a crowd value. The crowd value of a path is defined as the maximum crowd value for all roads in the path. For example, if the crowd values for all roads are , then the crowd value for the path will be .

Each city  has a type value, , denoting the type of buildings in the city.

David just started his vacation in HackerLand. He wants to travel from city  to city . He also wants to see at least  different types of buildings along the path from  to . When choosing a path from city  to city  that has at least  different types of buildings along the path, David always selects the one with the minimum crowd value.

You will be given  queries. Each query takes the form of  space-separated integers, , , and , denoting the respective values for starting city, destination city, and minimum number of unique buildings that David wants to see along the way. For each query, you must print the minimum crowd value for a path between  and  that has at least  different buildings along the route. If there is no such path, print -1.

Note: A path may contain cycles (i.e., the same roads or cities may be traveled more than once).

Input Format

The first line contains  space-separated integers denoting the respective values for  (the number of cities),  (the number of roads), and  (the number of queries).

The second line contains  space-separated integers describing the respective building type for each city in array  (where the -th value is  and ).

Each of the  subsequent lines defines a road in the form of  space-separated integers, , , and , defining an undirected road with crowd value  that connects cities  and .

Each of the  subsequent lines defines a query in the form of  space-separated integers, , , and  (where ), respectively.

Constraints

Each road connect  distinct cities, meaning no road starts and ends in the same city.
Output Format

For each query, print its answer on a new line.

Sample Input

7 6 1
1 1 4 5 1 3 2
1 2 3
2 6 2
2 3 4
3 4 3
2 4 9
5 7 9
1 2 4
Sample Output

4
Explanation

The diagram below depicts the country given as Sample Input. Different values of  are shown in different colors.

davaro.png

The path for the last query (1 2 4) will be . David sees his first type of building in cities  and , his second type of building in city , his third type of building in city , and his fourth type of building in city . The crowd values for each road traveled on this path are ; the maximum of these values is . Thus, we print  on a new line.</h3>

```cpp

#include <set>
#include <cmath>
#include <queue>
#include <cstdio>
#include <vector>
#include <cstring>
#include <iostream>
#include <algorithm>
using namespace std;

#define sz2 200001
#define ii pair<int, int>
#define pb push_back
#define mp make_pair
#define ff first
#define ss second

int qq, N, M, Q, K, C, max_edge = 1000000001;

vector<ii > G[100001];
vector<pair<int, ii > > E;
priority_queue<pair<int, ii > > pq;
pair <int, ii > q[2000001];
int lvl[sz2],T[100001],a[1000001],L[sz2],
    R[sz2],p[sz2],parent[sz2][20],col[100001],
    ll[sz2],rr[sz2],weight[sz2],dis[sz2],
    ans[2000001],st[5000005],used[10000001];
    
bool vis[100001];

int mycmp(pair <int, ii > a, pair <int, ii > b)
{
    if (a.ss.ff != b.ss.ff) return a.ss.ff < b.ss.ff;
    return a.ff < b.ff;
}

// DisjointSet
int find_parent(int i) {
    if (p[i] == i) return i;
    return p[i] = find_parent(p[i]);
}

void set_lvl(int v, int l) {
    lvl[v] = l;
    if (v > N) {
        set_lvl(ll[v], l + 1);
        set_lvl(rr[v], l + 1);
    }
}

// LeastCommonAncestor

void build_lca() {
    for (int i = 1; i < 20; i++)
        for (int v = 1; v <= K; v++) {
            parent[v][i] = parent[parent[v][i - 1]][i - 1];
        }
}

int LCA(int u, int v) {
    if (lvl[u] > lvl[v]) swap(u, v);
    for (int i = 20; i > 0; i--)
        if (lvl[parent[v][i-1]] >= lvl[u]) v = parent[v][i-1];
    
    if (u == v) return u;
    
    for (int i = 20; i > 0; i--)
        if (parent[u][i-1] != parent[v][i-1]) {
            u = parent[u][i-1]; v = parent[v][i-1];
        }
        
    return parent[u][0];
}

class STO {
    public:
        
        int n, m;
        
        STO() { n = m = 0; }
        void add_color(int x) { a[++n] = x; }        
        void add_query(pair<int, ii > query) { q[++m] = query; }
        
        void solve() {
            sort(q + 1, q + m + 1, mycmp);
            for (int i=1,j=1; i<=m; i++)
            {
                while(j <= q[i].ss.ff)
                {
                    if (!used[a[j]]) {
                        Update(1, 1, n, j, 1);
                        used[a[j]] = j;
                    } else {
                        Update(1, 1, n, used[a[j]], 0);
                        Update(1, 1, n, j, 1);
                        used[a[j]] = j;
                    }
                    j++;
                }
                ans[q[i].ss.ss] = Find(1, 1, n, q[i].ff, q[i].ss.ff);
            }
        }        
        int get_ans(int i) {
            return ans[i];
        }
        int Find(int ind, int A, int B, int l, int r)
        {
            if (l > B || r < A) return 0;
            if (A == l && B == r) return st[ind];
            int mid = (A + B) / 2;
            return Find(ind * 2, A, mid, l, min(mid, r)) + Find(ind * 2 + 1, mid + 1, B, max(mid + 1, l), r);
        }        
        void Update(int ind, int l, int r, int x, int d)
        {
            if (l == r) st[ind] = d;
            else {            
                int mid = (l + r) / 2;
                if (x <= mid) Update(ind * 2, l, mid, x, d);
                else Update(ind * 2 + 1, mid + 1, r, x, d);   
                st[ind] = st[ind * 2] + st[ind * 2 + 1];
            }
        }        
};


STO seg_tree;


void dfs(int v) {
    if (v > N) {
        dfs(ll[v]);
        dfs(rr[v]);
        L[v] = L[ll[v]];
        R[v] = R[rr[v]];
        seg_tree.add_query(mp(L[v], mp(R[v], qq))); qq++;
    } else {
        C++;
        seg_tree.add_color(col[v]);
        L[v] = C;
        R[v] = C;
    }
}

void dfs1(int v) {
    if (v == 0) return;
    if (v > N) {
        dfs1(ll[v]);
        dfs1(rr[v]);
        weight[v] = seg_tree.get_ans(qq); qq++;
    } else weight[v] = 1;
    
}

void color_solve() {
    vector<int> v1, v2;
    for (int i = 1; i <= N; i++)
        v1.pb(T[i]);
    sort(v1.begin(), v1.end());
    v2.pb(v1[0]);
    
    for (int i = 1, sz = 0; i<v1.size(); i++)
        if (v2[sz - 1] != v1[i]) {
            v2.pb(v1[i]); sz++;
        }

    for (int i = 1; i <= N; i++)
        col[i] = lower_bound(v2.begin(), v2.end(), T[i]) - v2.begin() + 1;
}

int main() {
    int u, v, e, k, x, y;
    scanf("%d%d%d",&N,&M,&Q);
    for (int i = 1; i <= N; i++) {
        scanf("%d",&T[i]);
        G[0].pb(mp(i, -max_edge));
        G[i].pb(mp(0, -max_edge));
    }
    for (int j = 0; j < M; j++) {
        scanf("%d%d%d",&u,&v,&e);
        G[u].pb(mp(v, -e));
        G[v].pb(mp(u, -e));
    }
    
    pq.push(mp(0, mp(0, -1)));
    while (!pq.empty()) {
        e = pq.top().ff;
        x = pq.top().ss.ff;
        y = pq.top().ss.ss;
        pq.pop();
        
        if (!vis[x]) { 
            vis[x] = true;
            if (y != -1) E.pb(mp(-e, mp(x, y)));            
            for (int i = 0; i < G[x].size(); i++)
              if (!vis[G[x][i].ff]) pq.push(mp(G[x][i].ss, mp(G[x][i].ff, x)));
        }
    }
    
    sort(E.begin(), E.end());
    for (int i = 0; i < 2 * N; i++)
        p[i] = i;
    
    K = N;
    for (int i = 0; i < E.size(); i++) {
        K++;
        int X = find_parent(E[i].ss.ff), Y = find_parent(E[i].ss.ss);        
        p[X] = p[Y] = parent[X][0] = parent[Y][0] = K;        
        dis[K] = E[i].ff == max_edge?-1:E[i].ff;
        ll[K] = X;
        rr[K] = Y;
    }
    
    color_solve();    qq=1; dfs (K);
    seg_tree.solve(); qq=1; dfs1(K);

    set_lvl(K, 1);    
    lvl[0] = parent[0][0] = 0;
    build_lca();
    
    while (Q--) {
        scanf("%d%d%d",&x,&y,&k);
        if (weight[K] < k) {
            printf("-1\n");
            continue;
        }
        
        x = LCA(x, y);        
        if (weight[x] >= k) printf("%d\n",dis[x]);
        else {        
             for (int i = 19; i >= 0; i--) {
             y = parent[x][i];
              if (y && weight[y] < k) x = y;
          }        
          printf("%d\n",dis[parent[x][0]]);
        }
    }
    
    return 0;
}


```

<h2>Kruskal (MST): Really Special Subtree</h2>
<h3>Given an undirected weighted connected graph, find the Really Special SubTree in it. The Really Special SubTree is defined as a subgraph consisting of all the nodes in the graph and:

There is only one exclusive path from a node to every other node.
The subgraph is of minimum overall weight (sum of all edges) among all such subgraphs.
No cycles are formed
To create the Really Special SubTree, always pick the edge with smallest weight. Determine if including it will create a cycle. If so, ignore the edge. If there are edges of equal weight available:

Choose the edge that minimizes the sum  where  and  are vertices and  is the edge weight.
If there is still a collision, choose any of them.
Print the overall weight of the tree formed using the rules.

For example, given the following edges:

u	v	wt
1	2	2
2	3	3
3	1	5
First choose  at weight . Next choose  at weight . All nodes are connected without cycles for a total weight of .

Function Description

Complete the  function in the editor below. It should return an integer that represents the total weight of the subtree formed.

kruskals has the following parameters:

g_nodes: an integer that represents the number of nodes in the tree
g_from: an array of integers that represent beginning edge node numbers
g_to: an array of integers that represent ending edge node numbers
g_weight: an array of integers that represent the weights of each edge
Input Format

The first line has two space-separated integers  and , the number of nodes and edges in the graph.

The next  lines each consist of three space-separated integers ,  and , where  and  denote the two nodes between which the undirected edge exists and  denotes the weight of that edge.

Constraints

**Note: ** If there are edges between the same pair of nodes with different weights, they are to be considered as is, like multiple edges.

Output Format

Print a single integer denoting the total weight of the Really Special SubTree.</h3>

```c

#include <stdio.h>
#include <string.h>
#include <math.h>
#include <stdlib.h>

typedef struct  {
    int u, v, m, w;
} Arco;

int menorArco( Arco * arcos, int M ) {
    int menor, i;
    menor = -1;
    for (i = 0; i < M; i++ ) {
        if ( arcos[i].m == 0 ) {
            if ( menor == -1 )
                menor = i;
            else
                if ( arcos[i].w < arcos[menor].w  )
                    menor = i;
                else
                    if ( arcos[i].w == arcos[menor].w ) 
                        if ( arcos[i].u + arcos[i].w + arcos[i].v < 
                             arcos[menor].u + arcos[menor].w + arcos[menor].v )
                            menor = i;
        }
    }
    return menor;
}

void unirComponentes( int * vertices, int N, int c1, int c2 ) {
    int i;
    for ( i = 0; i < N; i++ )
        if ( vertices[i] == c2 )
            vertices[i] = c1;
}

int main() {

    /* Enter your code here. Read input from STDIN. Print output to STDOUT */    
    int N, M, S, vs, vl, d;
    int **graph;
    Arco *arcos;
    int *vertices;
    
    int i, j, k;
    scanf("%d%d",&N, &M);
    graph = (int **)malloc(N*sizeof(int *));
    for ( i = 0; i < N; i++ )
        graph[i] = (int *)malloc( N*sizeof(int) );    

    for ( i = 0; i < N; i++ )
        for ( j = 0; j < N; j++ )
           graph[i][j] = -1;
    
    for ( i = 0; i < M; i++ ) {
        scanf("%d%d%d", &vs, &vl, &d );
        vs--;vl--;
        if ( vl > vs ) {
            int t = vs; vs = vl; vl = t;
        }
        if ( graph[vs][vl] == -1 || graph[vs][vl] > d )
            graph[vs][vl] = d;
        /*graph[vl][vs] = graph[vs][vl];*/
    }

    M = 0;
    for ( i = 0; i < N; i++ )
        for ( j = 0; j < N; j++ )
           if ( graph[i][j] >= 0 )
               M++;
    
    arcos = (Arco *)malloc( M*sizeof(Arco) );
    for ( k = i = 0; i < N; i++ )
        for ( j = 0; j < N; j++ )
            if ( graph[i][j] >= 0 ) {
                arcos[k].u = i;
                arcos[k].v = j;
                arcos[k].w = graph[i][j];
                arcos[k].m = 0;
                k++;
            }

    for ( i = 0; i < N; i++ )
        free( graph[i] );
    free( graph );
    
    vertices = (int *)malloc( N*sizeof(int) );
    for ( i = 0; i < N; i++ )
        vertices[i] = i;
    
    scanf("%d", &S); //ignored
    S--;

    int menor, u, v;
    while ( (menor = menorArco(arcos,M)) >= 0 ) {
        u = arcos[menor].u;
        v = arcos[menor].v;
        if ( vertices[u] != vertices[v] ) {
            unirComponentes( vertices, N, vertices[u], vertices[v]);
            arcos[menor].m = 1;
        }
        else
            arcos[menor].m = -1;
    }

    long R;
    R = 0;
    for ( i = 0; i < M; i++ )
        if ( arcos[i].m == 1 )
            R = R + arcos[i].w;
    
    printf("%ld",R);

   
    return 0;
}

```

<h2></h2>
<h3></h3>

```

```


<h2></h2>
<h3></h3>

```

```


<h2></h2>
<h3></h3>

```

```
