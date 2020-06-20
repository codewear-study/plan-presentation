개미는 뚠뚠~ 오늘도 뚠뚠~ 열심히 일을 하네
==================================

## BOJ 3048 개미(실버 4)
[본 문제](https://www.acmicpc.net/problem/3048)

첫번째 그룹의 선두를 A, 중간을 B, 마지막은 C  
두번째 그룹의 선두를 D, 중간을 E, 마지막은 F  

첫번째 그룹은 오른쪽으로 가다가, 두번째 그룹은 왼쪽으로 가다가 좁은 길에서 만났다!  
그때 개미들의 위치는 C B A D E F 순으로 될 것이다.   
이때 개미는 좁은 길을 통과하기 위해 점프를 한다.   
하지만 모든 개미가 점프를 하는 것이 아니라,  자신의 앞에 반대 방향으로 움직이던 개미를 마주쳤을 때만 점프를한다!  

0초 C B A D E F  
1초 C B D A E F  
2초 C D B E A F  

T초가 지난 뒤 개미의 순서를 구하시오!

<details>
<summary>해설</summary>

</details>
<details>
<summary>정답 코드</summary>
<div markdown="1">
<pre>
<code>
#include <bits/stdc++.h>

using namespace std;

int main(){
	cin.tie(0);
	ios_base :: sync_with_stdio(0);

	int a, b;
	cin >> a >> b;
	string s1, s2;
	cin >> s1 >> s2;
	reverse(s1.begin(), s1.end());
	int T;
	cin >> T;
	vector<int> v;
	for(int i = 0; i < s1.size(); i++){
		v.push_back(s1[i]);
	}
	for(int i = 0; i < s2.size(); i++){
		v.push_back(-s2[i]);
	}
	while(T--){
		for(int i = 0; i < v.size()-1; i++){
			if(v[i] > 0 && v[i+1] < 0){swap(v[i], v[i+1]); i++;}
		}
	}
	
	for(int i = 0; i < v.size(); i++){
		cout << (char)(v[i] > 0 ? v[i] : -v[i]);
	}
}
</code>
</pre>
</div>
</details>


## BOJ 3163 떨어지는 개미(골드 1)
[본 문제](https://www.acmicpc.net/problem/3163)  
<img src="https://github.com/SeonghoJin/plan-presentation/blob/moretall/cycle-10/reflection/presentation/1..PNG"></img><br/>  
개미가 행진을 시작하기 전의 상태 (ID와 막대 상의 위치)가 주어진다. 두 개미가 동시에 막대의 양 끝에서 떨어지는 경우에는, ID가 작은 개미가 조금   더 먼저 떨어진다고 한다. 위 그림은 이와 같은 경우를 나타낸 그림이다. 두 개미 {-1, +2}는 끝에 동시에 도착하게 된다. -1 < +2 이기   때문에, ID가 -1인 개미가 +2인 개미보다 조금 더 먼저 떨어지게 된다. 따라서, 위 그림의 네 개미가 떨어지는 순서는 {-1, 2, 4, 3}이 된다.  
<details>
<summary>해설</summary>
이 문제는 시뮬레이션 해서는 절대 풀 수 없습니다.  

이 문제에서 포인트는  
* 개미들이 떨어질 경우 무조건 맨 왼쪽과 맨 오른쪽 개미 둘 중 하나가 떨어진다는 점!
* 어떤 개미가 떨어질지는 몰라도 어느 방향에서 개미가 떨어지는 시간은 알 수 있다는 점!
	* 개미들이 부딪힐때 통과한다고 생각하면 된다.

오른쪽에서 개미가 떨어지면 맨 오른쪽 개미가 떨어진 것이다.
왼쪽에서 개미가 떨어지면 맨 왼쪽 개미가 떨어진 것이다.

이 2가지 특징을 이용하면 이 문제를 풀 수 있다.


</details>
<details>
<summary>정답 코드</summary>
<div markdown="1">
<pre>
<code>
#include <bits/stdc++.h>

using namespace std;

int main(){
	cin.tie(0);
	ios_base :: sync_with_stdio(0);
	
	int T;
	cin >> T;
	while(T--){
		vector<int> minus;
		vector<int> plus;
		list<int> li;
		int N, L, k;
		cin >> N >> L >> k;
		for(int i = 0; i < N; i++){
			int a, b;
			cin >> a >> b;
			li.push_back(b);
			if(b > 0)plus.push_back(L-a);
			else if(b < 0)minus.push_back(a);
		}

	    reverse(plus.begin(), plus.end());
		int pcur = 0;
		int mcur = 0;
		int answer = 0;

		while(k-- && (pcur < plus.size() || mcur < minus.size())){
			if((mcur == minus.size()) || (pcur < plus.size() && plus[pcur] < minus[mcur])){
				answer = li.back();
				li.pop_back();
				pcur++;
			}
			else if((pcur == plus.size()) || plus[pcur] > minus[mcur]){
				answer = li.front();
				li.pop_front();
				mcur++;
			}
			else{
				if(li.back() < li.front()){
					answer = li.back();
					li.pop_back();
					pcur++;
				}
				else{
					answer = li.front();
					li.pop_front();
					mcur++;
				}
			}
		}
		cout << answer << '\n';
	}
}
</code>
</pre>
</div>
</details>