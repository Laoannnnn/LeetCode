## 28. 实现 strStr()
### 方法一：暴力解法
* 执行用时：0 ms, 在所有 C++ 提交中击败了 100.00% 的用户
内存消耗：6.7 MB, 在所有 C++ 提交中击败了 74.28% 的用户
```C++
#include <string>
#include <iostream>
using namespace std;

int strStr(string haystack, string needle){
	int hlen = haystack.length(), nlen = needle.length(), ans = 0;
	if (nlen == 0) {
		return 0;
	}    
    int i = 0;
    for (int i=0; i<hlen; i++){
    	bool flag = true;
		for (int j=0, k=i; j<nlen; j++, k++) {
			if (i+nlen > hlen){
				flag = false;
				break;
			}
			if (haystack[k] != needle[j]){
				flag = false;
				break;
			}
		} 
		if (flag){
			return i;
		}
	}
	return -1;
}

int main(){
    string haystack = "", needle = "";
    // cin >> haystack >> needle;
    int ans = strStr(haystack, needle);
    cout << ans << endl;
    return 0;
}
```
### 方法二：KMP算法
* 执行用时：0 ms, 在所有 C++ 提交中击败了 100.00% 的用户
内存消耗：6.9 MB, 在所有 C++ 提交中击败了 26.19% 的用户
```C++
int strStr(string haystack, string needle){
	int hlen = haystack.length(), nlen = needle.length();
	if (nlen == 0) {
		return 0;
	}
	// 构建next数组 
	vector<int> next(nlen);
	for (int i=1, j=0; i<nlen; i++){
		while (j>0 && needle[i] != needle[j]){
			j = next[j-1];
		}
		if (needle[i]==needle[j]){
			j++;
		}
		next[i] = j;
	}
	// 进行检索
	for (int i=0, j=0; i<hlen; i++) {
		while (j>0 && haystack[i] != needle[j]){
			j = next[j-1];
		}
		if (haystack[i] == needle[j]){
			j++;
		}
		if (j == nlen){
			return i-nlen+1;
		}
	}
	return -1;
}
```