---
title: C++ Dijkstra
date: 2014-04-02
tags:
  - "C++"
  - "dijkstra"
  - "Graf"
categories:
  - "Kodlama"
  - "Algoritmalar"
---

## Dijikstra

C++ ile dijikstra algoritması parça parça anlatım ve son hali.

İngilizce Anlatım:[Competitive Programmer’s Handbook](https://cses.fi/book/book.pdf#page=136)

Türkçe Anlatım:[Rekabetçi Programcının El Kitabı](/cph_turkce.pdf#page=146)
<!--more-->

## İnclude satırları
İnclude ve define satırları.
```c++
	#include <bits/stdc++.h>
	#define FOR(i,s,e) for(int i=int(s);i<int(e);i++)
	#define ppi pair<pair<int,int>,int>
	#define pi pair<int,int>
	#define pb push_back
	#define S second
	#define F first
	using namespace std;
```
Bu satırlar kodun daha okunabilir olması ve kısaltılması için yazıldı.
## Hafızada Tutulacak Değişkenler
Kullanıcıdan okunacak verilerin tutulması için değişkenlerin tanımlanması.
```c++
	int n,m; //Edge sayısı(n) ve kenar sayısı(m)
	vector<vector<pi>> adj; //Komşuluk listesi ile Graf tutumu

 ```

## Ana Fonksyon
Kullanıcıdan okuma yapılması ve verilerin kaydedilmesi
```c++
	int main(){
	    cin>>n>>m;
	    adj.resize(n+1);
	    FOR(i,0,m){
	        int a,b,w;
	        cin>>a>>b>>w;
	        adj[a].pb({b,w});
	        adj[b].pb({a,w});
	    }
	    Dijkstra(1);
	    return;
	}
```
## Dijkstra Fonksyonu

```c++
	void Dijkstra(int x){
	    vector<bool> vis(adj.size());
	    vector<int> dis(adj.size(),INT_MAX);
	    priority_queue<pi> q;
	    dis[x]=0;
	    q.push({0,x});
	    while(q.size()){
	        int a=q.top().S;
	        q.pop();
	        if(vis[a]) continue;
	        vis[a]=1;
	        for(pi& i:adj[a]){
	            if(dis[a]+i.S<dis[i.F]){
	                dis[i.F]=dis[a]+i.S;
	                q.push({-dis[i.F],i.F});
	            }
	        }
	    }
	    FOR(i,0,adj.size()){
	        cout<<x<<" --> "<<i<<" = "<<dis[i]<<endl;
	    }
	    return;
	}
```
## Kodun Son hali

```c++
	#include <bits/stdc++.h>
	#define FOR(i,s,e) for(int i=int(s);i<int(e);i++)
	#define ppi pair<pair<int,int>,int>
	#define pi pair<int,int>
	#define pb push_back
	#define S second
	#define F first
	using namespace std;
	
	int n,m;
	vector<vector<pi>> adj;
	
	void Dijkstra(int x){
	    vector<bool> vis(adj.size());
	    vector<int> dis(adj.size(),INT_MAX);
	    priority_queue<pi> q;
	    dis[x]=0;
	    q.push({0,x});
	    while(q.size()){
	        int a=q.top().S;
	        q.pop();
	        if(vis[a]) continue;
	        vis[a]=1;
	        for(pi& i:adj[a]){
	            if(dis[a]+i.S<dis[i.F]){
	                dis[i.F]=dis[a]+i.S;
	                q.push({-dis[i.F],i.F});
	            }
	        }
	    }
	    FOR(i,0,adj.size()){
	        cout<<x<<" --> "<<i<<" = "<<dis[i]<<endl;
	    }
	    return;
	}
	
	int main(){
	    cin>>n>>m;
	    adj.resize(n+1);
	    edge.resize(m);
	    FOR(i,0,m){
	        int a,b,w;
	        cin>>a>>b>>w;
	        adj[a].pb({b,w});
	        adj[b].pb({a,w});
	    }
	    Dijkstra(1);
	    return 0;
	}
```		

