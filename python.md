<h1 align='center'>Python with questions</h1>

<div align='justify'>

An extra day is added to the calendar almost every four years as February 29, and the day is called a leap day. It corrects the calendar for the fact that our planet takes approximately 365.25 days to orbit the sun. A leap year contains a leap day.
	
</div>

```python
def is_leap(year):
    if year==2100:
        return False
    elif year%4==0 or (year%400==0 and year%100==0):
        return True
    else:
        return False 

```
<div>
Task
Given an integer, , perform the following conditional actions:

If  is odd, print Weird
If  is even and in the inclusive range of  to , print Not Weird
If  is even and in the inclusive range of  to , print Weird
If  is even and greater than , print Not Weird

</div>

```python
#!/bin/python3

import math
import os
import random
import re
import sys
n = int(input(""))
if (n%2)!=0 or (n%2)==0 and n in range(6,20) or n==20:
    print("Weird")
elif (n%2)==0 and n > 20 or (n%2)==0 and n in range(2,5):
    print("Not Weird")    
else:
    print("Enter a valid number")        

```
<h2> Python CCC traning

Hello world:</h2>
```python

if __name__ == '__main__':
    print("Hello, World!")
    
```
<h2>Print function:</h2>

```python

if __name__ == '__main__':
    n = int(input())
    for i in range(1,n+1):
        print(i,end='')
	
```

<h2>Arithmetic Operators:</h2>

```python

if __name__ == '__main__':
    a = int(input())
    b = int(input())
    print(a+b)
    print(a-b)
    print(a*b)
    
```

<h2>Division:</h2>

```python

from __future__ import division

if __name__ == '__main__':
    a = int(raw_input())
    b = int(raw_input())
    print(a//b);
    print(a/b);
    
```

<h2>If-Else:</h2>

```python
#!/bin/python3

import math
import os
import random
import re
import sys



if __name__ == '__main__':
    n = int(input().strip())

    if n%2 != 0:
        print("Weird")
    else:
        if n>=2 and n<=5:
            print("Not Weird")
        elif n>=6 and n<=20:
            print("Weird")
        else:
            print("Not Weird")
```

<h2>Come in all sizes:</h2>

```python
a=int(input())
b=int(input())
c=int(input())
d=int(input())
print(pow(a,b)+pow(c,d))
```
<h2>Grading Students:</h2>

```python
#!/bin/python3

import math
import os
import random
import re
import sys

#
# Complete the 'gradingStudents' function below.
#
# The function is expected to return an INTEGER_ARRAY.
# The function accepts INTEGER_ARRAY grades as parameter.
#

def gradingStudents(grades):
    
    for i in range(0,len(grades)):
        
        if grades[i] < 38:
            continue
        else:
            temp = grades[i]
            te = temp % 5
            if te == 3:
                temp = temp + 2
                grades[i] = temp
            elif te == 4:
                temp = temp + 1
                grades[i] = temp
            else:
                continue
    return grades



if __name__ == '__main__':
    fptr = open(os.environ['OUTPUT_PATH'], 'w')

    grades_count = int(input().strip())

    grades = []

    for _ in range(grades_count):
        grades_item = int(input().strip())
        grades.append(grades_item)

    result = gradingStudents(grades)

    fptr.write('\n'.join(map(str, result)))
    fptr.write('\n')

    fptr.close()

```

<h2>Apple&Orange:</h2>

```python

import math
import os
import random
import re
import sys
# Complete the countApplesAndOranges function below.
def countApplesAndOranges(s, t, a, b, apples, oranges):
    count_Apples = 0
    count_Oranges= 0
    for i in range(len(apples)):
        if a+apples[i] >= s and a+apples[i] <= t:
            count_Apples +=1
    for i in range(len(oranges)):
        if b+oranges[i] >= s and b+oranges[i] <=t:
            count_Oranges +=1
    print(count_Apples)
    print(count_Oranges)
if __name__ == '__main__':
    st = input().split()
    s = int(st[0])
    t = int(st[1])
    ab = input().split()
    a = int(ab[0])
    b = int(ab[1])
    mn = input().split()
    m = int(mn[0])
    n = int(mn[1])
    apples = list(map(int, input().rstrip().split()))
    oranges = list(map(int, input().rstrip().split()))
    countApplesAndOranges(s, t, a, b, apples, oranges)

```
TIme in words:

```python
#include <cmath>
#include <cstdio>
#include <vector>
#include <iostream>
#include <algorithm>
using namespace std;

string words[30] = {string("one"),string("two"),string("three"),string("four"),string("five"),string("six"),string("seven"),string("eight"),string("nine"),string("ten"),string("eleven"),string("twelve"),string("thirteen"),string("fourteen"),string("fifteen"),string("sixteen"),string("seventeen"),string("eighteen"),string("nineteen"),string("twenty"),string("twenty one"),string("twenty two"),string("twenty three"),string("twenty four"),string("twenty five"),string("twenty six"),string("twenty seven"),string("twenty eight"),string("twenty nine")};


int main() {
    int H,M;
    cin >> H >> M;
    if (M==0) {
        printf("%s o' clock\n",words[H-1].c_str());
    } else if (M==1) {
        printf("one minute past %s\n",words[H-1].c_str());
    } else if (M==15) {
        printf("quarter past %s\n",words[H-1].c_str());
    } else if (M<30) {
        printf("%s minutes past %s\n",words[M-1].c_str(),words[H-1].c_str());
    } else if (M==30) {
        printf("half past %s\n",words[H-1].c_str());
    } else if (M==45) {
        printf("quarter to %s\n",words[H%12].c_str());
    } else if (M==59) {
        printf("one minute to %s\n",words[H%12].c_str());
    } else {
        printf("%s minutes to %s\n",words[60-M-1].c_str(),words[H%12].c_str());
    }
    
    return 0;
}
```

Save the prisoner! :

```python
t = int(input())
for _ in range(t):
    parts = list(map(int, input().split(' ')))
    # print('parts', parts)
    print((parts[1] + parts[2] - 2) % parts[0] + 1)
```

Electronics Shop:

```python
#!/bin/python3

import sys


s,n,m = [int(x) for x in input().strip().split(' ')]
keyboards = [int(keyboards_temp) for keyboards_temp in input().strip().split(' ')]
pendrives = [int(pendrives_temp) for pendrives_temp in input().strip().split(' ')]

total = -1

for x in keyboards:
    for y in pendrives:
        z = x + y
        if z > total and z <= s:
            total = z
         
print(total)
```
Taum and B’Day:

```python
tcs = int(input())
for i in range(tcs):
    b, w = map(int, input().split(' '))
    x, y, z = map(int, input().split(' '))
    if x + z < y:
        print(b*x+w*(x+z))
    elif y + z < x:
        print(w*y+b*(y+z))
    else:
        print(b*x+w*y)
```
<h2>A E01 - Square Area</h2>

```python
#!/bin/python3

import math
import os
import random
import re
import sys



if __name__ == '__main__':
    side = int(input())
    print(side*side)
```
<h2>A E02 - Rectangle Area </h2>

```python
#!/bin/python3

import sys

if __name__ == "__main__":
    side1 = int(input().strip())
    side2 = int(input().strip())
    print(side1*side2)
```
<h2>A E03 Circle Area </h2>

```python
#!/bin/python3

import sys

if __name__ == "__main__":
    radius = int(input().strip())
    print(3.14*radius*radius)
 ```
<h2>A E04 Rhombus Area </h2>

```python
#!/bin/python3

import sys

if __name__ == "__main__":
    diag1 = int(input().strip())
    diag2 = int(input().strip())
    print((diag1*diag2)/2)
```
<h2>A E05 Digit Count</h2>

 ```python
#!/bin/python3

import sys

if __name__ == "__main__":
    num = int(input().strip())
    print(len(str(num)))
```
<h2>A E06 Cylinder Volume</h2> 

```python
#!/bin/python3

import math
import os
import random
import re
import sys



if __name__ == '__main__':
    radius = int(input())

    height = int(input())
    print(3.14*radius*radius*height)

```
<h2>Strong password:</h2>

```python
#!/bin/python3

import sys

def minimumNumber(n, password):
    numbers = "0123456789"
    lower_case = "abcdefghijklmnopqrstuvwxyz"
    upper_case = "ABCDEFGHIJKLMNOPQRSTUVWXYZ"
    special_characters = "!@#$%^&*()-+"
    
    n_bool = 1
    l_bool = 1
    u_bool = 1
    s_bool = 1
    for c in password:
        if c in numbers: n_bool = 0
        elif c in lower_case: l_bool = 0
        elif c in upper_case: u_bool = 0
        elif c in special_characters: s_bool = 0
    return max(6-n, n_bool + l_bool + u_bool + s_bool)

if __name__ == "__main__":
    n = int(input().strip())
    password = input().strip()
    answer = minimumNumber(n, password)
    print(answer)
```
<h2>Shakespeare’s play:</h2>

```python
import string

alphabet = set(string.ascii_lowercase)

def ispangram(input_string):
    return set(input_string.lower()) >= alphabet

inp = input()
print("France" if ispangram(inp) else "Italy")

```
<h2>Super Reduced string:</h2>

```python
s = input()

changed = True
while changed and s != "":
    changed = False
    for i in range(len(s) - 1):
        if s[i] == s[i+1]:
            changed = True
            s = s[:(i)] + s[(i+2):]
            break

if s == "":
    print('Empty String')
else:
    print(s)
```

<h2>Diagonal DIfference:</h2>

```python
#!/bin/python3

import math
import os
import random
import re
import sys

#
# Complete the 'diagonalDifference' function below.
#
# The function is expected to return an INTEGER.
# The function accepts 2D_INTEGER_ARRAY arr as parameter.
#

def diagonalDifference(arr):
    # Write your code here
    d1 = sum([arr[x][x] for x in range(len(arr))])
    d2 = sum([arr[x][n - 1 - x] for x in range(len(arr))])
    return(abs(d1 - d2))

if __name__ == '__main__':
    fptr = open(os.environ['OUTPUT_PATH'], 'w')

    n = int(input().strip())

    arr = []

    for _ in range(n):
        arr.append(list(map(int, input().rstrip().split())))

    result = diagonalDifference(arr)

    fptr.write(str(result) + '\n')

    fptr.close()
```
<h2>Making ANAgrams:</h2>

```python
import math

def number_needed(a, b):
    aString = [0]*26
    for ch in a:
        aString[ord(ch)-97] += 1
    
    bString = [0]*26
    for ch in b:
        bString[ord(ch)-97] += 1
        
    deletions = 0
    for i in range(len(aString)):
        deletions += math.fabs(aString[i]-bString[i])
    
    return int(deletions)

a = input().strip()
b = input().strip()

print(number_needed(a, b))
```
<h2>Sherlock and the valid string:</h2>

```python
#!/bin/python3

import math
import os
import random
import re
import sys
from collections import Counter
# Complete the isValid function below.
def isValid(s):
    d = Counter(s)
    counts = Counter(d.values())
    if len(counts) == 1:
        return "YES"
    elif len(counts) > 2:
        return "NO"
    else:
        max_v = max(counts.values())
        k1, k2 = counts.keys()
        if (max_v == len(d) - 1):
            if (abs(k1 - k2) == 1):
                return "YES"
            elif (min(k1, k2) == 1):
                if counts[1] == 1:
                    return "YES"
                else:
                    return "NO"
            else:
                return "NO"
        else:
            return "NO"

if __name__ == '__main__':
    fptr = open(os.environ['OUTPUT_PATH'], 'w')

    s = input()

    result = isValid(s)

    fptr.write(result + '\n')

    fptr.close()
```







