* 거스름돈 ```N```원을 거슬러 줄때의 최소 동전 갯수 구하기  (```N```은 항상 10의 배수)

* 동전 화폐의 종류가 ```K```일떄의 시간 복잡도는 ```O(K)```
* 동전 중 가장 큰 단위가 작은 단위의 배수이므로 그리디 알고리즘으로 최적의 해를 찾을 수 있음

```python
n = 1260
count = 0

# 큰 단위의 동전부터 차례대로 확인
coin_types = [500, 100, 50, 10]

for coin in coin_types:
    count += n // coin
    n %= coin

print(count)
```

```java
public class Main {

    public static void main(String[] args) {
        
        int n = 1260;
        int cnt = 0;
        int[] coinTypes = {00, 100, 50, 10};

        for (int coin : coinTypes) {
            cnt += n / coin;
            n %= coin;
        }

        System.out.println(cnt);
    }
}
```