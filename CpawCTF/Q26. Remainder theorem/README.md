## 問題

```text
> x ≡ 32134 (mod 1584891)
> x ≡ 193127 (mod 3438478)
> 
> x = ?
> 
> 
> フラグはcpaw{xの値}です！
```

## 解法

xは1584891をi倍して32134を足した数であり、かつ3438478をj倍して193127を足した数である。
pythonでそれぞれの数のリストを作り、その積集合が答え。

```python
a = [1584891*i+32134 for i in range(100,200000)]
b = [3438478*j+193127 for j in range(100,100000)]

x = set(a) & set(b)
print(x)
```

実行すると、両方の条件を満たす数が、一つ出力された。

```bash
$ python .\q26.py
{35430270439}
```