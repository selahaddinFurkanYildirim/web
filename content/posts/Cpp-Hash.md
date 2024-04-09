---
title: "C++ Hash"
date: 2024-04-09T10:40:00+03:00
draft: true
---

## Hash

C++ ile Hash algoritması parça parça anlatım ve son hali.

İngilizce Anlatım:[Competitive Programmer’s Handbook](https://cses.fi/book/book.pdf#page=255)

Türkçe Anlatım:[Rekabetçi Programcının El Kitabı](/cph_turkce.pdf#page=269)

<!--more-->

## İnclude satırları
İnclude ve define satırları.

```cpp
#include <bits/stdc++.h>
#define FOR(i,s,e) for(int i=int(s);i<int(e);i++)
#define ppi pair<pair<int,int>,int>
#define pi pair<int,int>
#define pb push_back
#define S second
#define F first
typedef long long ll;
using namespace std;
```
Bu satırlar kodun daha okunabilir olması ve kısaltılması için yazıldı.

## Hafızada Tutulacak Değişkenler

Kullanıcıdan okunacak verilerin tutulması için değişkenlerin tanımlanması.

```cpp
string x;
```

## Ana Fonksyon
Kullanıcıdan okuma yapılması ve verilerin Hash fonksyonuna gönderilmesi
```cpp
int main(){
    cin>>x;
	cout<<x<<endl<<Hash(x)<<endl<<UnHash(Hash(x))<<endl;
	return 0;
}
```

## Hash Fonksyonu

Hash ve UnHash fonksyonlarının implementasyonu.

```cpp
ll Hash(string x){
	ll ans=0;
	for(auto& i:x){
		ans*=31;
		ans+=i-'a'+1;
	}
	return ans;
}
string UnHash(ll x){
	string ans;
	while(x){
		ans.pb(x%31+'a'-1);
		x/=31;
	}
	reverse(ans.begin(),ans.end());
	return ans;
}
```


## Kodun Son hali

```cpp
#include <bits/stdc++.h>
#define FOR(i,s,e) for(int i=int(s);i<int(e);i++)
#define ppi pair<pair<int,int>,int>
#define pi pair<int,int>
#define pb push_back
#define S second
#define F first
typedef long long ll;
using namespace std;

ll Hash(string x){
	ll ans=0;
	for(auto& i:x){
		ans*=31;
		ans+=i-'a'+1;
	}
	return ans;
}
string UnHash(ll x){
	string ans;
	while(x){
		ans.pb(x%31+'a'-1);
		x/=31;
	}
	reverse(ans.begin(),ans.end());
	return ans;
}

int main(){
	string x="metin";
	cout<<x<<endl<<Hash(x)<<endl<<UnHash(Hash(x))<<endl;
	return 0;
}

```