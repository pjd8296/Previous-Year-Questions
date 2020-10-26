## Dream Internship
Form a rectangular window of size <= a, N rod pairs given and lengths of rod pair given in form of an array. Find possible such combinations.
```c++
int main() {
    ll count = 0;
    ll n, a;
    cin >> n >> a;
    vector<ll> A(n);
    for(ll i = 0; i < n; i++)
        cin >> A[i];
    sort(A.begin(), A.end());
    ll i = 0, j = n-1;
    while(i < j) {
        while(i < j and A[i]*A[j] > a) j--;
        count += j-i; //because all j-i rod pairs will form window <= k
        i++;
    }
    cout << count <<endl;
}
```
