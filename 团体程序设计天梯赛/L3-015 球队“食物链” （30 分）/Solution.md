# L3-015 ��ӡ�ʳ������ ��30 �֣�

[ԭ���ַ](https://pintia.cn/problem-sets/994805046380707840/problems/994805048175869952)


>����: ������
��λ: ������ѧ
ʱ������: 2000 ms
�ڴ�����: 128 MB
���볤������: 16 KB


ĳ����������������N֧������ӣ���Ŵ�1��N�������������ͳ�˫ѭ�����ƣ������������֮����˫����������һ���� 
����ս�գ�����Ѿ������䶨����ʱ��������ϯͻ�����룬ϣ�������ҳ�һ������������ӵġ�ʳ����������˵�������ľ��ʳ̶ȡ���ʳ������Ϊһ��1��N������{T1 T2 T3 �� Tn}�����㣺���T1սʤ�����T2�����T2սʤ�����T3���� �����T(N-1)սʤ�����TN�����TNսʤ�����T1�� 
������ϯ���������������ҳ���ʳ�������������ڶ�����ʳ�����������ҳ��ֵ�����С�ġ� 
ע������{ a1 a2 �� an }���ֵ�����С������{ b1 b2 �� bn }�����ҽ�����������K��1��K��N��������: ak < bk�Ҷ�������С��K��������i, ai = bi�� 
## �����ʽ�� 
�����һ�и���һ������N��2��N��20����Ϊ��������������N�У�ÿ��N���ַ���������N��N��������������е�i�е�j�е��ַ�Ϊ���i�������������j�ı��������W��ʾ���iսʤ���j��L��ʾ���i�������j��D��ʾ���Ӵ�ƽ��- ��ʾ��Ч����i=jʱ�����������޶���ո� 
## �����ʽ�� 
����ĿҪ���ҵ���ʳ������ T1 T2 �� TN ������N�������������һ���ϣ����ּ���1���ո�ָ����е���β�����ж���ո��������ڡ�ʳ�������������No Solution���� 
## ��������1�� 
5   
-LWDW   
W-LDW   
WW-LW   
DWW-W   
DDLW-   
## �������1�� 
1 3 5 4 2   
## ��������2�� 
5   
-WDDW   
D-DWL   
DD-DW   
DDW-D   
DDDD-   
## �������2�� 
No Solution  


## ˼·

DFS + ��֦

DFS�У���"ʳ����"��δѡȡ����ӣ�û��һ��Ӯ��ʳ�����еĵ�1����ӣ����֦��

## ����

[L3-015 ��ӡ�ʳ������ ��30 �֣�.cpp](https://github.com/jerrykcode/PTA/blob/master/%E5%9B%A2%E4%BD%93%E7%A8%8B%E5%BA%8F%E8%AE%BE%E8%AE%A1%E5%A4%A9%E6%A2%AF%E8%B5%9B/L3-015%20%E7%90%83%E9%98%9F%E2%80%9C%E9%A3%9F%E7%89%A9%E9%93%BE%E2%80%9D%20%EF%BC%8830%20%E5%88%86%EF%BC%89/L3-015%20%E7%90%83%E9%98%9F%E2%80%9C%E9%A3%9F%E7%89%A9%E9%93%BE%E2%80%9D%20%EF%BC%8830%20%E5%88%86%EF%BC%89.cpp)


```cpp
#include <iostream>
using namespace std;
#include <vector>

#define WIN(Ti, Tj) (graph[Ti][Tj] == 'W' || graph[Tj][Ti] == 'L')

char **graph;

bool dfs(int start, vector<int>& chain, bool *collected, int n) {
	int size = (int)chain.size();
	int chainLastTeam = chain[size - 1]; //chain is never empty in this function
	if (size == n) {
		if (WIN(chainLastTeam, start)) return true;
	}
	bool flag = true;
	for (int team = 0; team < n; team++)
		if (!collected[team])
			if (WIN(team, start)) {
				flag = false;
				break;
			}
	if (flag) return false;
	for (int team = 0; team < n; team++) {
		if (!collected[team] && WIN(chainLastTeam, team)) {
			chain.push_back(team);
			collected[team] = true;
			if (dfs(start, chain, collected, n)) return true;
			chain.pop_back();
			collected[team] = false;
		}
	}
	return false;
}

int main()
{
	int n;
	cin >> n;
	graph = new char *[n];
	for (int i = 0; i < n; i++) {
		graph[i] = new char[n];
		for (int j = 0; j < n; j++)
			cin >> graph[i][j];
	}
	vector<int> chain;
	bool *collected = new bool[n];
	fill(collected, collected + n, false);
	for (int team = 0; team < n; team++) {
		chain.push_back(team);
		collected[team] = true;
		if (dfs(team, chain, collected, n)) break;
		chain.pop_back();
		collected[team] = false;
	}
	free(collected);
	for (int i = 0; i < n; i++) {
		free(graph[i]);
	}
	free(graph);
	if (chain.empty()) {
		cout << "No Solution" << endl;
	}
	else {
		for (auto it = chain.begin(); it != chain.end(); it++) {
			if (it != chain.begin()) putchar(' ');
			cout << (*it) + 1;
		}
		cout << endl;
	}
	return 0;
}

```