#include <bits/stdc++.h>
#define ll long long
using namespace std;
ll T,n,tot;
ll p[70] = {0}; 
void in(ll x){//向线性基中添加数x 
	for(int i=62;i>=0;i--){
		if(!(x>>(ll)i)) continue;
		if(!p[i]){
			p[i] = x;
			break;
		}
		x ^= p[i];
	}
}
ll query_max(){//求最大异或和 
	ll ans = 0;
	for(int i=62;i>=0;i--){
		if((ans^p[i]) > ans) ans ^= p[i];
	}
	return ans; 
}
ll query_min(){//求最小异或和 
	for(int i=0;i<=62;i++){
		if(p[i]) return p[i];
	}
	return 0;
} 
void work(){
	for(int i=1;i<=62;i++){
		for(int j=1;j<=i;j++){
			if(p[i] & (1ll<<(j-1)))
				p[i] ^= p[j-1];
		}
	}
}
ll k_th(ll k){//求第K小异或和 
	if(k==1 && tot<n) return 0;
	if(tot<n) k--;
	work();
	ll ans = 0;
	for(int i=0;i<=62;i++){
		if(p[i]!=0){
			if(k%2==1) ans ^= p[i];
			k /= 2;
		}
	}
	return ans;
}
int main(void){
	ios::sync_with_stdio(false);
	cin.tie(0), cout.tie(0);
	cin >> T;
	while(T--){
		memset(p,0,sizeof(p));
		tot = 0;
		cin >> n;
		for(int i=1;i<=n;i++){
			ll x;
			cin >> x;
			in(x);
		}
		for(int i=0;i<=62;i++)
			if(p[i]) tot++;
		//cout << query_max() << endl;
		//cout << query_min() << endl;
		//cout << k_th(2) << endl; 
	}
	return 0;
}
