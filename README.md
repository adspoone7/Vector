# Vector


#include "stdafx.h"
#include "math.h"
#include <iostream>
#include <list> 
#include <Windows.h>
#include <string.h>

using namespace std;

class Graph
{
	int V;    // No. of vertices
	list<int> *adj;    // Pointer to an array containing adjacency lists
	void DFSUtil(int v, bool visited[]); //A function used by DFS
public:
	Graph(int V);   // Constructor
	void addEdge(int v, int w);   // function to add an edge to graph
	void DFS(int v);    // DFS traversal of the vertices reachable from v
};


Graph::Graph(int V)
{
	this->V = V;
	adj = new list<int>[V];
}

void Graph::addEdge(int v, int w)
{
	adj[v].push_back(w); // Add w to v’s list.
}

void Graph::DFSUtil(int v, bool visited[])
{
	// Mark the current node as visited and print it
	visited[v] = true;
	cout << v << " ";

	// Recur for all the vertices adjacent to this vertex
	list<int>::iterator i;
	for (i = adj[v].begin(); i != adj[v].end(); ++i)
		if (!visited[*i])
			DFSUtil(*i, visited);
		
}

// DFS traversal of the vertices reachable from v. It uses recursive DFSUtil()
void Graph::DFS(int v)
{
	// Mark all the vertices as not visited
	bool *visited = new bool[V];
	for (int i = 0; i < V; i++)
		visited[i] = false;

	// Call the recursive helper function to print DFS traversal
	DFSUtil(v, visited);
	cout << " || "<< visited << endl;
}



int _tmain(int argc, _TCHAR* argv[])
{
	
	Graph g(5);

	g.addEdge(0, 1);
	g.addEdge(0, 2);
	g.addEdge(1, 2);
	g.addEdge(2, 0);
	g.addEdge(2, 3);
	g.addEdge(3, 4);
	g.addEdge(4, 4);

	int k;
	cin >> k;
	
	if (k < 5)
	{
		cout << "Following is Depth First Traversal (starting from vertex " << k << ") \n" << endl;

		g.DFS(k);

		cout << endl;
	}
	else cout << "integer value must be less than 5...";

	return 0;
}





