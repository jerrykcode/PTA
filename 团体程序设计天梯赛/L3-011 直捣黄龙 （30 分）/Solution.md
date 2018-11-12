# L3-011 ֱ������ ��30 �֣�

[ԭ���ַ](https://pintia.cn/problem-sets/994805046380707840/problems/994805049455132672)

>����: ��Խ
��λ: �㽭��ѧ
ʱ������: 150 ms
�ڴ�����: 64 MB
���볤������: 16 KB


������һ��ս����Ƭ ���� ����Ҫ�Ӽ�����Ӫ������һ·�����Ե�ɱ���з���Ӫ������ʱ��������������������ѡ����ʵ�·�����������ٶ�ռ��з���Ӫ����������·����Ψһʱ��Ҫ��ѡ�������;����������·������������·��Ҳ��Ψһ����ѡ�������Чɱ�����о���·����

## �����ʽ��

�����һ�и��� 2 �������� N��2 �� N �� 200�������������� K��������·���������Լ�������Ӫ�͵з���Ӫ�Ĵ��š���� N-1 �У�ÿ�и������˼�����Ӫ���һ������Ĵ��ź�פ�صĵо�����������Կո�ָ����ٺ����� K �У�ÿ�а���ʽ����1 ����2 ���������������֮���·�ĳ��ȡ�������ÿ�����򣨰���˫����Ӫ���Ĵ������� 3 ����дӢ����ĸ��ɵ��ַ�����

## �����ʽ��

������ĿҪ���ҵ�����ʵĽ���·������Ŀ��֤�ٶ���졢�����ࡢɱ����ǿ��·����Ψһ�ģ������ڵ�һ�а��ո�ʽ������Ӫ->����1->...->�з���Ӫ������ڶ���˳�����������·������������̽������롢�ߵ������������ 1 ���ո�ָ�������β�����ж���ո�

## ����������
10 12 PAT DBY  
DBY 100  
PTA 20  
PDS 90  
PMS 40  
TAP 50  
ATP 200  
LNN 80  
LAO 30  
LON 70  
PAT PTA 10  
PAT PMS 10  
PAT ATP 20  
PAT LNN 10  
LNN LAO 10  
LAO LON 10  
LON DBY 10  
PMS TAP 10  
TAP DBY 10  
DBY PDS 10  
PDS PTA 10  
DBY ATP 10  


## ���������
PAT->PTA->PDS->DBY  
3 30 210  


## ˼·

Dijkstra + DFS

Dijkstra������·������¼��Դ��������Ķ���minV�������������ڲ�δ����¼�Ķ��㣬��ͨ��minV����ʹԴ��һ����ľ����С������¸ö����·��ͨ��minV��������벻�䵫ʹ·���Ͼ����Ķ�����������Ҳ���£���·���Ͼ����Ķ�����Ҳ���䣬��·���Ͼ����Ķ����Ȩ�غ����ӣ���Ҳ���¡���vector����paths�洢���о�����ͬ��·������paths[i]��ʾ���д�Դ��i�ľ�����ͬ��·����i��ǰһ������ļ��ϡ�dijkstra��ͨ��minV�����Сʱ��```paths[v].clear(); paths[v].push_back(minV)```(����v��·��)�����벻��ʱ```paths[v].push_back(minV)```(minVΪһ��������ͬ��·��)��dijkstra��������DFS����paths��������о�����ͬ��·������

## ����

[L3-011 ֱ������ ��30 �֣�.cpp](https://github.com/jerrykcode/PTA/blob/master/%E5%9B%A2%E4%BD%93%E7%A8%8B%E5%BA%8F%E8%AE%BE%E8%AE%A1%E5%A4%A9%E6%A2%AF%E8%B5%9B/L3-011%20%E7%9B%B4%E6%8D%A3%E9%BB%84%E9%BE%99%20%EF%BC%8830%20%E5%88%86%EF%BC%89/L3-011%20%E7%9B%B4%E6%8D%A3%E9%BB%84%E9%BE%99%20%EF%BC%8830%20%E5%88%86%EF%BC%89.cpp)


```cpp
#include <iostream>
using namespace std;
#include <map>
#include <string>
#include <vector>
#include <stack>

#define INF 1000000

map<string, int> nameToIndex;
map<int, string> indexToName;
string srcName, desName;
int n, src, des;
int indexCount = 1;

int **graph;
int *weight;

int getIndex(string name) {
	if (name == srcName) return 0;
	if (nameToIndex[name] == 0) {
		nameToIndex[name] = indexCount;
		indexToName[indexCount] = name;
		indexCount++;
	}
	return nameToIndex[name];
}

int findMin(int *dist, bool *collected, int n) {
	int minV = -1, min = INF;
	for (int v = 0; v < n; v++)
		if (!collected[v] && dist[v] < min) {
			minV = v;
			min = dist[v];
		}
	return minV;
}

void dijkstra(int *bestPath, vector<int> *paths, int *minDist, int *maxW) {
	int *dist = new int[n];
	int *num = new int[n];
	int *w = new int[n];
	bool *collected = new bool[n];
	for (int v = 0; v < n; v++) {
		dist[v] = graph[src][v];
		num[v] = dist[v] < INF ? 2 : 0;
		w[v] = dist[v] < INF ? weight[src] + weight[v] : 0;
		collected[v] = false;
		bestPath[v] = dist[v] < INF ? src : -1;
		if (bestPath[v] == src) paths[v].push_back(src);
	}
	dist[src] = 0;
	num[src] = 1;
	w[src] = weight[src];
	collected[src] = true;
	while (true) {
		int minV = findMin(dist, collected, n);
		if (minV == des) break;
		collected[minV] = true;
		for (int v = 0; v < n; v++) {
			if (!collected[v] && graph[minV][v] < INF) {
				if (dist[minV] + graph[minV][v] < dist[v]) {
					dist[v] = dist[minV] + graph[minV][v];
					num[v] = num[minV] + 1;
					w[v] = w[minV] + weight[v];
					bestPath[v] = minV;
					paths[v].clear();
					paths[v].push_back(minV);
				}
				else if (dist[minV] + graph[minV][v] == dist[v]) {
					paths[v].push_back(minV);
					if (num[minV] + 1 > num[v]) {
						num[v] = num[minV] + 1;
						w[v] = w[minV] + weight[v];
						bestPath[v] = minV;
					}
					else if (num[minV] + 1 == num[v] && w[minV] + weight[v] > w[v]) {
						w[v] = w[minV] + weight[v];
						bestPath[v] = minV;
					}
				}
			}
		} //for
	} //while
	*minDist = dist[des];
	*maxW = w[des];
	free(dist);
	free(num);
	free(w);
	free(collected);
}

void printPath(int *path) {
	stack<int> s;
	int v = des;
	while (v != src) {
		s.push(v);
		v = path[v];
	}
	cout << indexToName[src];
	while (!s.empty()) {
		cout << "->";
		cout << (indexToName[s.top()]);
		s.pop();
	}
}

int nPaths = 0;
void dfs(vector<int> *paths, int v) {
	if (v == src)
		nPaths++;
	else {
		for (int w : paths[v]) {
			dfs(paths, w);
		}
	}
}

int main() {
	int k;
	cin >> n >> k;
	graph = new int *[n];
	for (int i = 0; i < n; i++) {
		graph[i] = new int[n];
		fill(graph[i], graph[i] + n, INF);
	}
	weight = new int[n];
	fill(weight, weight + n, 0);
	cin >> srcName >> desName;
	src = 0;
	nameToIndex[srcName] = src;
	indexToName[src] = srcName;
	src = getIndex(srcName);
	des = getIndex(desName);
	for (int i = 0; i < n - 1; i++) {
		string cityName;
		int nEnemies;
		cin >> cityName >> nEnemies;
		int cityIndex = getIndex(cityName);
		weight[cityIndex] = nEnemies;
	}
	for (int i = 0; i < k; i++) {
		string cityName1, cityName2;
		int dist;
		cin >> cityName1 >> cityName2 >> dist;
		int cityIndex1 = getIndex(cityName1), cityIndex2 = getIndex(cityName2);
		graph[cityIndex1][cityIndex2] = graph[cityIndex2][cityIndex1] = dist;
	}
	int *bestPath = new int[n];
	vector<int> *paths = new vector<int>[n];
	int minDist, maxW;
	dijkstra(bestPath, paths, &minDist, &maxW);
	printPath(bestPath);
	cout << endl;
	dfs(paths, des);
	cout << nPaths << " " << minDist << " " << maxW;
	free(bestPath);
	for (int i = 0; i < n; i++)
		free(graph[i]);
	free(graph);
	free(weight);
	return 0;
}

```
