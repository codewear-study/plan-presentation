배경지식이 필요없고, 신기한 문제
==================================

## Codefroces Round #634(Div. 3) D번
[본 문제](https://codeforces.com/problemset/problem/1335/D)

스도쿠퍼즐의 정답인 81개의 숫자중 최대 9개까지의 숫자를 바꿔서   
각 열과 행은 같은 숫자가 2개  
그리고 3X3블록 또한 같은 숫자가 2개가 되게하라.  
Ex)  
154873296     
386592714  
729641835  
863725149  
975314628  
412968357  
631457982  
598236471  
247189563  

154873396  
336592714  
729645835  
863725145  
979314628  
412958357  
631457992  
998236471  
247789563  

<details>
<summary>해설</summary>
간단히 생각하면 풀리는 문제입니다. 
일단 스도쿠 퍼즐의 정답이기 때문에 각 열과 행 그리고 3X3블록에는 각 한가지 숫자만 존재합니다. 
따라서 스도쿠에 존재하는 모든 숫자 1을 숫자 2로 바꾸게 되면 안티스도쿠가 됩니다.
</details>
<details>
<summary>정답 코드</summary>
<div markdown="1">
<pre>
<code>
#include <iostream>
#include <vector>
#include <algorithm>
#include <cmath>
 
using namespace std;
 
int main(){
 
    cin.tie(0);
    ios_base :: sync_with_stdio(0);
 
    int T;
    cin >> T;
    
    while(T--){
        string s[9];
        for(int i = 0; i < 9; i++)cin >> s[i];
        s[1][1] = s[1][0];
        s[0][6] = s[0][5];
        s[2][5] = s[3][5];
        s[3][8] = s[2][8];
        s[4][2] = s[4][0];
        s[5][4] = s[6][4];
        s[6][7] = s[6][6];
        s[7][0] = s[7][1];
        s[8][3] = s[8][2];
       for(int i = 0; i < 9; i++){
            cout << s[i] << '\n';
        }
    }
}
</code>
</pre>
</div>
</details>
<details>
<summary>정해</summary>
<div markdown="1">
<pre>
<code>
#include <bits/stdc++.h>

using namespace std;

int main() {
	
	int t;
	cin >> t;
	while (t--) {
		for (int i = 0; i < 9; ++i) {
			string s;
			cin >> s;
			for (auto &c : s) if (c == '2') c = '1';
			cout << s << endl;
		}
	}
	
	return 0;
}
</code>
</pre>
</div>
</details>