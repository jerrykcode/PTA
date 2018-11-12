# L3-007 ���ݵ�ͼ ��30 �֣�

[ԭ���ַ](https://pintia.cn/problem-sets/994805046380707840/problems/994805051153825792)

* ��Ŀ����: ��Խ

* ��λ: �㽭��ѧ

* ʱ������: 300 ms

* �ڴ�����: 64 MB

* ���볤������: 16 KB


����Ҫ����ʵ��һ��������ר�����ߵ�ͼ����Ա�����Լ�ѧУ���ڵغ�������

��󣬸õ�ͼӦ���Ƽ�����·�ߣ�һ������쵽��·�ߣ�һ������̾����·

�ߡ���Ŀ��֤������Ĳ�ѯ���󣬵�ͼ�϶����ٴ���һ���ɴ�·�ߡ�

## �����ʽ��

�����ڵ�һ�и�������������N��2 �� N �� 500����M���ֱ�Ϊ��ͼ�����б�

�ǵص�ĸ��������ӵص�ĵ�·���������M�У�ÿ�а����¸�ʽ����һ����

·����Ϣ��

```
V1 V2 one-way length time
```


����V1��V2�ǵ�·�������˵�ı�ţ���0��N-1��������õ�·�Ǵ�V1��V2��

�����ߣ���one-wayΪ1������Ϊ0��length�ǵ�·�ĳ��ȣ�time��ͨ����·��

��Ҫ��ʱ�䡣������һ�������յ�ı�š�

## �����ʽ��

���Ȱ����и�ʽ�����쵽���ʱ��T���ýڵ��ű�ʾ��·�ߣ�

```
Time = T: ��� => �ڵ�1 => ... => �յ�
```


Ȼ������һ�а����и�ʽ�����̾���D���ýڵ��ű�ʾ��·�ߣ�

```
Distance = D: ��� => �ڵ�1 => ... => �յ�
```

�����쵽��·�߲�Ψһ��������������·������̵���������Ŀ��֤����

·����Ψһ�ġ��������̾����·�߲�Ψһ�������;���ڵ������ٵ�����

����Ŀ��֤����·����Ψһ�ġ�

���������·������ȫһ���ģ������и�ʽ�����

```
Time = T; Distance = D: ��� => �ڵ�1 => ... => �յ�
```


## ��������1��

10 15  
0 1 0 1 1  
8 0 0 1 1  
4 8 1 1 1  
5 4 0 2 3  
5 9 1 1 4  
0 6 0 1 1  
7 3 1 1 2  
8 3 1 1 2  
2 5 0 2 2  
2 1 1 1 1  
1 5 0 1 3  
1 4 0 1 1  
9 7 1 1 3  
3 1 0 2 5  
6 3 1 2 1  
5 3  


## �������1��

Time = 6: 5 => 4 => 8 => 3  
Distance = 3: 5 => 1 => 3  


## ��������2��

7 9  
0 4 1 1 1  
1 6 1 3 1  
2 6 1 1 1  
2 5 1 2 2  
3 0 0 1 1  
3 1 1 3 1  
3 2 1 2 1  
4 5 0 2 2  
6 5 1 2 1  
3 5  


## �������2��

Time = 3; Distance = 4: 3 => 2 => 5  

## ˼·��

Dijkstra

��������ά����ֱ��ʾ�����ڽӾ���ͼ���߷ֱ��ʾ������֮���ʱ��;��롣������dijkstra��ʱ����̺;�����̵�·����

����`ʱ�����`ʱ��ÿ��¼һ������minV�󣬱�������������δ��¼����ʱ����ͨ��minV����ö���ʹԴ���ö����ʱ���С����ö������Ϊͨ��minV�����ͨ��minVʱ����ͬ������ʹԴ���ö���ľ����С����Ҳ���¸ö���Ϊͨ��minV����Ķ��㡣

����`�������`ʱ��ÿ��¼һ������minV�󣬱�������������δ��¼����ʱ����ͨ��minV����ö���ʹԴ���ö���ľ����С����ö������Ϊͨ��minV�����ͨ��minV������ͬ������ʹԴ���ö���ľ����Ķ�������С����Ҳ���¸ö���Ϊͨ��minV����Ķ��㡣


## ���룺

[L3-007 ���ݵ�ͼ ��30 �֣�.cpp](https://github.com/jerrykcode/PTA/blob/master/%E5%9B%A2%E4%BD%93%E7%A8%8B%E5%BA%8F%E8%AE%BE%E8%AE%A1%E5%A4%A9%E6%A2%AF%E8%B5%9B/L3-007%20%E5%A4%A9%E6%A2%AF%E5%9C%B0%E5%9B%BE%20%EF%BC%8830%20%E5%88%86%EF%BC%89/L3-007%20%E5%A4%A9%E6%A2%AF%E5%9C%B0%E5%9B%BE%20%EF%BC%8830%20%E5%88%86%EF%BC%89.cpp)

```cpp
#include <iostream>
#include <vector>
#include <stack>
using namespace std;

#define INF 100000

int findMin(int *arr, bool *collected, int n) {
	int min = INF, minV = -1;
	for (int i = 0; i < n; i++) {
		if (!collected[i] && arr[i] < min) {
			min = arr[i];
			minV = i;
		}
	}
	return minV;
}

void getPath(int *path, int src, int des, int n, vector<int>& vpath) 

{
	stack<int> s;
	while (des != src) {
		s.push(des);
		des = path[des];
	}
	vpath.push_back(src);
	while (!s.empty()) {
		vpath.push_back(s.top());
		s.pop();
	}
}

int timeDijkstra(int **timeGraph, int **distGraph, int n, int src, 

int des, vector<int>& vpath) {
	int *time = new int[n];
	int *dist = new int[n];
	int *path = new int[n];
	bool *collected = new bool[n];
	for (int i = 0; i < n; i++) {
		time[i] = timeGraph[src][i];
		dist[i] = distGraph[src][i];
		path[i] = time[i] < INF ? src : -1;
		collected[i] = false;
	}
	time[src] = dist[src] = 0;
	path[src] = -1;
	collected[src] = true;
	while (1) {
		int minV = findMin(time, collected, n);
		if (minV == -1) return -1;
		if (minV == des) break;
		collected[minV] = true;
		for (int v = 0; v < n; v++) {
			if (!collected[v] && timeGraph[minV][v] < 

INF) {
				if (time[minV] + timeGraph[minV][v] 

< time[v]) {
					time[v] = time[minV] + 

timeGraph[minV][v];
					dist[v] = dist[minV] + 

distGraph[minV][v];
					path[v] = minV;
				}
				else if (time[minV] + timeGraph

[minV][v] == time[v] && dist[minV] + distGraph[minV][v] < dist[v]) {
					dist[v] = dist[minV] + 

distGraph[minV][v];
					path[v] = minV;
				}
			}
		}
	} //while
	getPath(path, src, des, n, vpath);
	int result = time[des];
	free(time);
	free(dist);
	free(path);
	free(collected);
	return result;
}

int distDijkstra(int **distGraph, int n, int src, int des, 

vector<int>& vpath) {
	int *dist = new int[n];
	int *num = new int[n];
	int *path = new int[n];
	bool *collected = new bool[n];
	for (int i = 0; i < n; i++) {
		dist[i] = distGraph[src][i];
		num[i] = dist[i] < INF ? 2 : -1;
		path[i] = dist[i] < INF ? src : -1;
		collected[i] = false;
	}
	dist[src] = 0;
	num[src] = 1;
	path[src] = -1;
	collected[src] = true;
	while (1) {
		int minV = findMin(dist, collected, n);
		if (minV == -1) return -1;
		if (minV == des) break;
		collected[minV] = true;
		for (int v = 0; v < n; v++) {
			if (!collected[v] && distGraph[minV][v] < 

INF) {
				if (dist[minV] + distGraph[minV][v] 

< dist[v]) {
					dist[v] = dist[minV] + 

distGraph[minV][v];
					num[v] = num[minV] + 1;
					path[v] = minV;
				}
				else if (dist[minV] + distGraph

[minV][v] == dist[v] && num[minV] + 1 < num[v]) {
					num[v] = num[minV] + 1;
					path[v] = minV;
				}
			}
		}
	} //while
	getPath(path, src, des, n, vpath);
	int result = dist[des];
	free(dist);
	free(num);
	free(path);
	free(collected);
	return result;
}

int main()
{
	int n, m;
	std::cin >> n >> m;
	int **timeGraph = new int*[n];
	int **distGraph = new int*[n];
	for (int i = 0; i < n; i++) {
		timeGraph[i] = new int[n];
		distGraph[i] = new int[n];
		for (int j = 0; j < n; j++)
			timeGraph[i][j] = distGraph[i][j] = INF;
	}
	for (int i = 0; i < m; i++) {
		int v1, v2, oneWay, len, time;
		std::cin >> v1 >> v2 >> oneWay >> len >> time;
		distGraph[v1][v2] = len;
		timeGraph[v1][v2] = time;
		if (oneWay == 0) {
			distGraph[v2][v1] = len;
			timeGraph[v2][v1] = time;
		}
	}
	int src, des;
	std::cin >> src >> des;
	vector<int> timePath;
	int t = timeDijkstra(timeGraph, distGraph, n, src, des, 

timePath);
	for (int i = 0; i < n; i++)
		free(timeGraph[i]);
	free(timeGraph);
	vector<int> distPath;
	int d = distDijkstra(distGraph, n, src, des, distPath);
	for (int i = 0; i < n; i++)
		free(distGraph[i]);
	free(distGraph);
	bool equal = true;
	if (timePath.size() != distPath.size())
		equal = false;
	else {
		for (int i = 0; i < timePath.size(); i++)
			if (timePath[i] != distPath[i]) {
				equal = false;
				break;
			}
	}
	if (equal) {
		printf("Time = %d; Distance = %d: ", t, d);
		for (auto it = timePath.begin(); it != timePath.end

(); it++) {
			if (it != timePath.begin()) cout << " => ";
			cout << *it;
		}
	}
	else {
		printf("Time = %d: ", t);
		for (auto it = timePath.begin(); it != timePath.end

(); it++) {
			if (it != timePath.begin()) cout << " => ";
			cout << *it;
		}
		cout << endl;
		printf("Distance = %d: ", d);
		for (auto it = distPath.begin(); it != distPath.end

(); it++) {
			if (it != distPath.begin()) cout << " => ";
			cout << *it;
		}
	}
	return 0;
}


```




