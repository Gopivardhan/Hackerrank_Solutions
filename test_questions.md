<h1>DSBS hacker rank</h1>

<h2>1.String Transmission</h2>

<h3>Bob has received a binary string of length N transmitted by Alice. He knows that due to errors in transmission, up to K bits might have been corrupted (and hence flipped). However, he also knows that the string Alice had intended to transmit was not periodic. A string is not periodic if it cannot be represented as a smaller string concatenated some number of times. For example, "0001", "0110" are not periodic while "00000", "010101" are periodic strings.

Now he wonders how many possible strings could Alice have transmitted.

Input Format

The first line contains the number of test cases T. T test cases follow. Each case contains two integers N and K on the first line, and a binary string of length N on the next line.
Constraints

Output Format

Output T lines, one for each test case. Since the answers can be really big, output the numbers modulo 1000000007.</h3>

```c
#include <stdlib.h>
#include <stdio.h>
int N,K;
int F[1000][1000],S[1000];
char s[1001];
int f(int x, int i, int j) {
    if(j>K) return 0;
    if(i==x) return 1;
    if(F[i][j]==-1) F[i][j] = (f(x,i+1,j+S[i])+f(x,i+1,j+N/x-S[i]))%1000000007;;
    return F[i][j];
}
int g(int x, int *p) {
    if((*p)!=0) return (g(x,p+1)-g(x/(*p),p+1))%1000000007;
    int i,j;
    for(i=0; i<x; i++) for(j=0; j<=K; j++) F[i][j] = -1;
    for(i=0; i<x; i++) {
        S[i] = 0;
        for(j=i; j<N; j+=x) S[i]+= (s[j]=='1')?1:0;
    }
    return f(x,0,0);
}
int main() {
    int i,j,k,T;
    int ps[170],l[500],p[5];
    for(i=0;i<500;i++) l[i] = 1;
    ps[0] = 2;
    for(i=3,k=1;i<1000;i+=2) if(l[i/2]) {
        ps[k++] = i;
        for(j=i*i/2;j<500;j+=i) l[j] = 0;
    }
    scanf("%d",&T);
    for(;T>0;T--) {
        scanf("%d %d %[01]",&N,&K,s);
        for(i=0,j=0; i<k; i++) if(N%ps[i]==0) p[j++] = ps[i];
        p[j] = 0;
        printf("%d\n",(g(N,p)+1000000007)%1000000007);
    }
    exit(0);
}


```

<h2>2.String Reduction</h2>

<h3>Given a string consisting of the letters ,  and , we can perform the following operation:

Take any two adjacent distinct characters and replace them with the third character.
Find the shortest string obtainable through applying this operation repeatedly.

For example, given the string  we can reduce it to a  character string by replacing  with  and  with : .

Function Description

Complete the stringReduction function in the editor below. It must return an integer that denotes the length of the shortest string obtainable.

stringReduction has the following parameter:
- s: a string

Input Format

The first line contains the number of test cases .

Each of the next  lines contains a string  to process.

Constraints

Output Format

For each test case, print the length of the resultant minimal string on a new line.</h3>

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>


typedef struct{
  int l;
  char c;
}var;

var arr[100][100];

var compare(var a, var b){
  var ret;

  if(a.c == b.c){
    ret.l = a.l + b.l;
    ret.c = a.c;
    return  ret;
  }
   
  if(a.l % 2 == 0){
    if(b.l % 2 == 0){
      ret.l = 2;
      ret.c = (a.l < b.l) ? a.c : b.c;
    }
    else{
      ret.l = 1;
      ret.c = b.c;
    }
  }
  else{
    if(b.l % 2 == 0){
      ret.l = 1;
      ret.c = a.c;
    }
    else{
      ret.l = 1;
      ret.c = 'a' + 'b' + 'c' - a.c - b.c;
    }
  }

  return ret;
}

int process(char *str){
  int len = strlen(str);

  int i, j;
  for(i=0; i<len; i++){
    arr[i][i].l = 1;
    arr[i][i].c = str[i];
  }

  for(i=1; i<len; i++){
    for(j=0; j<len-i; j++){
      int k;
      var min; min.l = 1000;
      for(k=j; k<j+i; k++){
    var ret = compare(arr[j][k], arr[k+1][i+j]);
    if(ret.l < min.l)
      min = ret;
      }

      arr[j][j+i] = min;
    }
  }

  return arr[0][len-1].l;
}

int main(){
  int T, i;
  scanf("%d", &T);

  char *str = (char *)malloc(101*sizeof(char));
  for(i=0; i<T; i++){
    scanf("%s", str);
    printf("%d\n", process(str));
  }

  return 0;
}

```

<h2>3.Binary Search Tree : Insertion</h2>

<h3>

You are given a pointer to the root of a binary search tree and values to be inserted into the tree. Insert the values into their appropriate position in the binary search tree and return the root of the updated binary tree. You just have to complete the function.

Input Format

You are given a function,

Node * insert (Node * root ,int data) {

}
Constraints

No. of nodes in the tree  500
Output Format

Return the root of the binary search tree after inserting the value into the tree.

Sample Input

        4
       / \
      2   7
     / \
    1   3
The value to be inserted is 6.

Sample Output

         4
       /   \
      2     7
     / \   /
    1   3 6
</h3>


```c
/* you only have to complete the function given below.  
node is defined as  

struct node {
    
    int data;
    struct node *left;
    struct node *right;
  
};

*/
struct node* insert( struct node* root, int data ) {
    if(root==NULL){
        root = malloc(sizeof(struct node));
            root->data = data;
            root->left = NULL;
            root->right = NULL;
    }
    else if (data > root->data){
        root->right = insert(root->right, data);
    }
    else{
        root->left = insert(root->left, data);
    }
    return root;		
	
}
```

<h2>
	Prefix Compression
</h2>

<h3>
	You are in charge of data transfer between two Data Centers. Each set of data is represented by a pair of strings. Over a period of time you have observed a trend: most of the times both strings share some prefix. You want to utilize this observation to design a data compression algorithm which will be used to reduce amount of data to be transferred.

You are given two strings,  and , representing the data, you need to find the longest common prefix () of the two strings. Then you will send substring ,  and , where  and  are the substring left after stripping  from them.

For example, if  "abcdefpr" and  "abcpqr", then  "abc",  "defpr",  "pqr".

Input Format

The first line contains a single string denoting .
The second line contains a single string denoting .

Constraints

 and  will contain only lowercase Latin characters ('a'-'z').
Output Format

In first line, print the length of substring , followed by prefix . In second line, print the length of substring , followed by substring . Similary in third line, print the length of substring , followed by substring .

Sample Input 0

abcdefpr
abcpqr
Sample Output 0

3 abc
5 defpr
3 pqr
Sample Input 1

kitkat
kit
Sample Output 1

3 kit
3 kat
0
Sample Input 2

puppy
puppy
Sample Output 2

5 puppy
0
0
Explanation

Sample Case 0:
Already explained above in the problem statement.

Sample Case 1:
 "kit", which is also . So  will be "kat" and  will be an empty string.

Sample Case 2:
Because both strings are the same, the prefix will cover both the strings. Thus,  and  will be empty strings.
</h3>

```java
import java.util.Scanner

object Solution {
  def main(args: Array[String]): Unit = {
    val sc = new Scanner(System.in)

    val s0 = sc.nextLine
    val s1 = sc.nextLine

    sc.close()

    val prefixLen = s0.zip(s1).takeWhile { case (c0, c1) => c0 == c1 }.length

    printf(s"$prefixLen ${s0.take(prefixLen)}\n")
    printf(s"${s0.length - prefixLen} ${s0.drop(prefixLen)}\n")
    printf(s"${s1.length - prefixLen} ${s1.drop(prefixLen)}\n")
  }
}

```

<h2>No Prefix Set</h2>
<h3>There is a given list of strings where each string contains only lowercase letters from , inclusive. The set of strings is said to be a GOOD SET if no string is a prefix of another string. In this case, print GOOD SET. Otherwise, print BAD SET on the first line followed by the string being checked.

Note If two strings are identical, they are prefixes of each other.

Example

Here 'abcd' is a prefix of 'abcde' and 'bcd' is a prefix of 'bcde'. Since 'abcde' is tested first, print

BAD SET  
abcde
.

No string is a prefix of another so print

GOOD SET 
Function Description
Complete the noPrefix function in the editor below.

noPrefix has the following parameter(s):
- string words[n]: an array of strings

Prints
- string(s): either GOOD SET or BAD SET on one line followed by the word on the next line. No return value is expected.

Input Format
First line contains , the size of .
Then next  lines each contain a string, .

Constraints

 the length of words[i] 
All letters in  are in the range 'a' through 'j', inclusive.

Sample Input00

STDIN       Function
-----       --------
7            words[] size n = 7
aab          words = ['aab', 'defgab', 'abcde', 'aabcde', 'bbbbbbbbbb', 'jabjjjad']
defgab  
abcde
aabcde
cedaaa
bbbbbbbbbb
jabjjjad
Sample Output00

BAD SET
aabcde
Explanation
'aab' is prefix of 'aabcde' so it is a BAD SET and fails at string 'aabcde'.

Sample Input01

4
aab
aac
aacghgh
aabghgh
Sample Output01

BAD SET
aacghgh
Explanation
'aab' is a prefix of 'aabghgh', and aac' is prefix of 'aacghgh'. The set is a BAD SET. 'aacghgh' is tested before 'aabghgh', so and it fails at 'aacghgh'.</h3>

```cpp
	#include <iostream>
#include <cstring>
#include <algorithm>
using namespace std;
class Trie
{
public:
    bool is_element;
    Trie *p[10];
    Trie()
    {
        is_element = false;
        memset(p,0,sizeof(p));
    }
    ~Trie();
    
    bool add(string s);
};
bool Trie::add(string s)
{
    Trie *ch = this;
    for (int i = 0; i < s.length(); ++i)
    {
        int cur = s[i] - 'a';
        if (ch->p[cur] == NULL)
            ch->p[cur] = new Trie;
        else
            if (ch->p[cur]->is_element)
                return false;
        ch = ch->p[cur];
    }
    ch -> is_element = true;
    for (int i = 0; i < 10; ++i)
        if (ch->p[i] != NULL)
            return false;
    return true;
}
int main()
{
    int n;
    Trie *trie = new Trie;
    cin>>n;
    for (int i = 0; i < n; ++i)
    {
        string s;
        cin>>s;
        if (!trie->add(s))
        {
            cout<<"BAD SET"<<endl<<s<<endl;
            return 0;
        }
    }
    cout<<"GOOD SET"<<endl;
    return 0;
}

```

<h2>Equal Stacks</h2>
<h3>You have three stacks of cylinders where each cylinder has the same diameter, but they may vary in height. You can change the height of a stack by removing and discarding its topmost cylinder any number of times.

Find the maximum possible height of the stacks such that all of the stacks are exactly the same height. This means you must remove zero or more cylinders from the top of zero or more of the three stacks until they are all the same height, then return the height.

Example




There are  and  cylinders in the three stacks, with their heights in the three arrays. Remove the top 2 cylinders from  (heights = [1, 2]) and from  (heights = [1, 1]) so that the three stacks all are 2 units tall. Return  as the answer.

Note: An empty stack is still a stack.

Function Description

Complete the equalStacks function in the editor below.

equalStacks has the following parameters:

int h1[n1]: the first array of heights
int h2[n2]: the second array of heights
int h3[n3]: the third array of heights
Returns

int: the height of the stacks when they are equalized
Input Format

The first line contains three space-separated integers, , , and , the numbers of cylinders in stacks , , and . The subsequent lines describe the respective heights of each cylinder in a stack from top to bottom:

The second line contains  space-separated integers, the cylinder heights in stack . The first element is the top cylinder of the stack.
The third line contains  space-separated integers, the cylinder heights in stack . The first element is the top cylinder of the stack.
The fourth line contains  space-separated integers, the cylinder heights in stack . The first element is the top cylinder of the stack.
Constraints

Sample Input

STDIN       Function
-----       --------
5 3 4       h1[] size n1 = 5, h2[] size n2 = 3, h3[] size n3 = 4  
3 2 1 1 1   h1 = [3, 2, 1, 1, 1]
4 3 2       h2 = [4, 3, 2]
1 1 4 1     h3 = [1, 1, 4, 1]
Sample Output

5
Explanation

Initially, the stacks look like this:

initial stacks

To equalize thier heights, remove the first cylinder from stacks  and , and then remove the top two cylinders from stack  (shown below).

modified stacks

The stack heights are reduced as follows:

All three stacks now have , the value to return.</h3>

```py
def check_equal_heights(heights):
    h_0 = heights[0]
    for h_i in heights[1:]:
        if h_i != h_0:
            return False
    return True


num_blocks = [int(num) for num in input().strip().split()]
num_stacks = len(num_blocks)
stacks = []
for __ in range(num_stacks):
    stack = [int(h) for h in input().strip().split()]
    stacks.append(stack[::-1])

goal = 1
best_height = 0
heights = [0] * num_stacks
positions = [0] * num_stacks
total_blocks = sum(num_blocks)
while sum(positions) < total_blocks:
    for i, stack in enumerate(stacks):
        if positions[i] == num_blocks[i]:
            continue
            
        if heights[i] == goal:
            heights[i] += stack[positions[i]]
            positions[i] += 1
        
        at_end = False
        while heights[i] < goal:
            if positions[i] == num_blocks[i]:
                at_end = True
                break
            heights[i] += stack[positions[i]]
            positions[i] += 1
            
        goal = heights[i]
            
        if at_end:
            continue
            
        if check_equal_heights(heights):
            best_height = heights[i]
            
print(best_height)

```
