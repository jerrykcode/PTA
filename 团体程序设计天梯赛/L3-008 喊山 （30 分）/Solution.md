# L3-008 ��ɽ ��30 �֣�

[ԭ���ַ](https://pintia.cn/problem-sets/994805046380707840/problems/994805050709229568)

> ����: ��Խ
��λ: �㽭��ѧ
ʱ������: 150 ms
�ڴ�����: 64 MB
���볤������: 16 KB


��ɽ������˫��Χ����߳�����״������Զ����ɽ������ι��ιι��ιιι�������ĺ�����������ͨ�������Ĵ��ݣ��ص������֮�䣬���͵����Ƕ��У�����Լ���׳ɵġ�Ѷ�š����ﵽ��Ѷ���ݽ�����Ŀ�ġ�ԭ��������������������Ԯ���ȵġ�Ѷ�š�������������������ʵ���з���������ʵ�ü�ֵ���������Ϊһ�ֽ�������������Ϯʹ�á���ͼ��ժ�ԣ�http://news.xrxxw.com/newsshow-8018.html��



һ��ɽͷ�������������Ա��ٽ���ɽͷͬʱ��������Ŀ����ÿ��ɽͷ��������������������ٽ�ɽͷ����������һ������ԭʼ�źŵ�ɽͷ�����������ҳ�����ź���Զ�ܴ��ﵽ�ĵط���

## �����ʽ��

�����һ�и���3��������n��m��k������n����10000�����ܵ�ɽͷ�������Ǽ���ÿ��ɽͷ��1��n��ţ�����������m�У�ÿ�и���2��������n�������������ּ��ÿո�ֿ����ֱ������������˴˵�����ɽͷ�ı�š����ﱣ֤ÿһ��ɽͷֻ������һ�Σ��������ظ��Ĺ�ϵ���롣���һ�и���k����10����������n�������������ּ��ÿո�ֿ���������Ҫ��ѯ��ɽͷ�ı�š�

## �����ʽ��

���ζ��������е�ÿ������ѯ��ɽͷ����һ��������䷢���ĺ����ܹ��������ﵽ����Զ���Ǹ�ɽͷ��ע�⣺����������ȱ����Ǳ���ѯ�ĸ�ɽͷ�����������ġ���������ɽͷ��ֻһ��������������С���Ǹ�������ɽͷ�ĺ����޷������κ�����ɽͷ�������0��

## ����������
7 5 4  
1 2  
2 3  
3 1  
4 5  
5 6  
1 4 5 7  


## ���������

2  
6  
4  
0  

## ˼·��

BFS�����������

ɽͷΪ���㣬���Ա˴�����������ɽͷ֮����һ���ߡ����ڽӱ��ʾͼ���Բ�ѯ��ɽͷΪԴ��BFS�ֲ�����������һ��(��Զ�ܴ�����һ��)����С��ŵ�ɽͷ��

## ����

[L3-008 ��ɽ ��30 �֣�.cpp ](https://github.com/jerrykcode/PTA/blob/master/%E5%9B%A2%E4%BD%93%E7%A8%8B%E5%BA%8F%E8%AE%BE%E8%AE%A1%E5%A4%A9%E6%A2%AF%E8%B5%9B/L3-008%20%E5%96%8A%E5%B1%B1%20%EF%BC%8830%20%E5%88%86%EF%BC%89/L3-008%20%E5%96%8A%E5%B1%B1%20%EF%BC%8830%20%E5%88%86%EF%BC%89.cpp)

```cpp
#include <iostream>
#include <vector>
#include <queue>
using namespace std;

typedef vector<int> *Graph;

int bfs(Graph graph, int src, int n) {
	queue<int>q;
	int last = src, tail = src;
	bool *collected = new bool[n];
	fill(collected, collected + n, false);
	q.push(src);
	collected[src] = true;
	int minV = -1;
	bool newLevel = true;
	while (!q.empty()) {
		int v = q.front();
		q.pop();
		for (int w : graph[v]) {
			if (!collected[w]) {
				collected[w] = true;
				q.push(w);
				if (newLevel || w < minV) {
					if (newLevel) newLevel = false;
					minV = w;
				}
				last = w;
			}
		}
		if (v == tail) {
			tail = last;
			newLevel = true;
		}
	}
	free(collected);
	return minV;
}

int main() {
	int n, m, k;
	cin >> n >> m >> k;
	Graph graph = new vector<int>[n];
	for (int i = 0; i < m; i++) {
		int v1, v2;
		cin >> v1 >> v2;
		v1--; v2--;
		graph[v1].push_back(v2);
		graph[v2].push_back(v1);
	}
	for (int i = 0; i < k; i++) {
		int v;
		cin >> v;
		int minV = bfs(graph, v - 1, n);
		cout << (minV + 1) << endl;
	}
	return 0;
}

```

