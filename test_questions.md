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


