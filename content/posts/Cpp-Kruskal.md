---
title: C++ Kruskal
date: 2014-04-02
tags:
  - "C++"
  - "Kruskal"
  - "Graf"
categories:
  - "Kodlama"
  - "Algoritmalar"
---

# C++ ile kruskal algoritması parça parça anlatım ve son hali.
<!--more-->

## Kruskal Nedir

İngilizce Anlatım:[Competitive Programmer’s Handbook](https://cses.fi/book/book.pdf#page=152)

Türkçe Anlatım:[Rekabetçi Programcının El Kitabı](/cph_turkce.pdf#page=162)

Kruskal bir MST([Minimum Spanning Tree](https://en.wikipedia.org/wiki/Minimum_spanning_tree)) algoritmasının temsilcisidir.

Kısaca MST bir graf içindeki tüm köşeleri içeren en az maliyetli yoldur.
## İnclude satırları
İnclude ve define satırları.
```cpp
#include <bits/stdc++.h>
#define FOR(i,s,e) for(int i=int(s);i<int(e);i++)
#define pi pair<int,int>
#define pb push_back
#define S second
#define F first
using namespace std;
```
Bu satırlar kodun daha okunabilir olması ve kısaltılması için yazıldı.

## Sınıf Tanımlaması
İleride kullanılacak olan kenar listesi ile graf tutma yöntemi için kenar sınıfı tanımlaması.
```cpp
struct edge{
    int a,b,w;
};
```
## Hafızada Tutulacak Değişkenler
Kullanıcıdan okunacak verilerin tutulması için değişkenlerin tanımlanması.
```cpp
vector<edge> e; //Kenar listesi tutumu
vector<edge> ans; //en kısa yol (cevap)
vector<int> l; //her köşenin atası(ona gelinmesini sağlayan köşe)
vector<int> s; //her köşenin üyesi olduğu guruptaki eleman sayısı
```

## Yardımcı Fonksyon
[Union-find](/cph_turkce.pdf#page=165) yapısı için ata bulan fonksyon.
```cpp
int bul(int a){
    while(l[a]!=a) a=l[a];
    return a;
}
```
Bu fonksyonun çalışma prensibi şöyle:

Her köşe(düğüm) başlangıçta kendisinin atasıdır.

Eğer kendi atası değilse o zaman onun atasını kendisi gibi görüp kendisi kendisinin atası oluncaya kadar atasıyla yer değiştirir. 
## Ana Fonksyon
Kullanıcıdan okuma yapılması ve verilerin kaydedilmesi
```cpp
int main(){
    int n,m;
    cin>>n>>m;
    l.resize(n+1);
    s.resize(n+1);
    e.resize(m);
    FOR(i,0,n+1){
        l[i]=i;
        s[i]=1;
    }
    FOR(i,0,m){
        cin>>e[i].a>>e[i].b>>e[i].w;
    }
    vector<edge> ans=kruskal();
    FOR(i,0,ans.size()){
        cout<<"\t"<<ans[i].w<<"\n"<<ans[i].a<<"\t-->\t"<<ans[i].b<<endl;
    }
    return 0;
}
```
## Kruskal Fonksyonu
Cevabı return eden kruskal fonksyonu
```cpp
vector<edge> kruskal(){
    sort(e.begin(),e.end(),[](const edge& a,const edge& b){
        return a.w<b.w;
    });
    vector<edge> ans;
    FOR(i,0,e.size()){
        int a=bul(e[i].a),b=bul(e[i].b);
        if(a!=b){
            ans.pb(e[i]);
            if(s[a]<s[b]) swap(a,b);
            l[b]=a;
            s[a]+=s[b];
        }
    }
    return ans;
}
```
Burada fonksyon ilk olarak en kısa kenarı alıp iki ucunu birbirine bağlamıştır ve her seferinde öncekinden uzun en kısa kenar için aynı işlemi tekrarlamıştır.

Eğer iki köşenin atası aynı ise bu kenar atlanmıştır.

## Kodun Son Hali

```cpp
#include <bits/stdc++.h>
#define FOR(i,s,e) for(int i=int(s);i<int(e);i++)
#define pi pair<int,int>
#define pb push_back
#define S second
#define F first
using namespace std;

struct edge{
    int a,b,w;
};

vector<edge> e;
vector<edge> ans;
vector<int> l;
vector<int> s;

int bul(int a){
    while(l[a]!=a) a=l[a];
    return a;
}

vector<edge> kruskal(){
    sort(e.begin(),e.end(),[](const edge& a,const edge& b){
        return a.w<b.w;
    });
    vector<edge> ans;
    FOR(i,0,e.size()){
        int a=bul(e[i].a),b=bul(e[i].b);
        if(a!=b){
            ans.pb(e[i]);
            if(s[a]<s[b]) swap(a,b);
            l[b]=a;
            s[a]+=s[b];
        }
    }
    return ans;
}

void f(){
    int n,m;
    cin>>n>>m;
    l.resize(n+1);
    s.resize(n+1);
    e.resize(m);
    FOR(i,0,n+1){
        l[i]=i;
        s[i]=1;
    }
    FOR(i,0,m){
        cin>>e[i].a>>e[i].b>>e[i].w;
    }
    vector<edge> ans=kruskal();
    FOR(i,0,ans.size()){
        cout<<"\t"<<ans[i].w<<"\n"<<ans[i].a<<"\t-->\t"<<ans[i].b<<endl;
    }
    return;
}

int main(){
#ifdef DEVCPP
    freopen("input.txt", "r", stdin);
    cout<<"girdi(input.txt)"<<endl;
#endif
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);
    int t=1;
//  cin>>t;
    while(t--){
        f();
        cout<<endl;
    }
    return 0;
}
```
