* 배열의 크기 ```N```, 숫자가 더해지는 횟수 ```M```, 연속으로 같은 숫자를 더할 수 있는 횟수 K가 주어질 때 가장 큰 수를 구하기
* 그리디 알고리즘 문제로 가장 큰 수를 K번 더하고 두번째로 큰 수를 한번 더하는 연산을 반복하기
* 반복되는 (연산) 수열의 크기 = ```K + 1```
* 가장 큰 수가 더해지는 횟수 = ```int(M / (K + 1)) * K + M % (K + 1) ```

```python
# 첫째줄 입력 : N M K
n, m, k = map(int, input().split())
# 둘째줄 입력 : 배열 N
data = list(map(int, input().split()))

data.sort()
first = data[n-1]
second = data[n-2]

# 가장 큰 수가 더해지는 횟수
count = int(m / (k+1)) * k
count += m % (k+1)

result = 0
result += count * first
result += (m - count) * second
print(result)
```

```java
import java.util.Arrays;
import java.util.Scanner;

public class Main {

    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);

        int n = sc.nextInt();
        int m = sc.nextInt();
        int k = sc.nextInt();

        int[] arr = new int[n];
        for (int i = 0; i < n; i++) {
            arr[i] = sc.nextInt();
        }

        Arrays.sort(arr);
        int first = arr[n - 1];
        int second = arr[n - 2];

        int cnt = (m / (k+1)) * k;
        cnt += m % (k+1);

        int result = 0;
        result += cnt * first;
        result += (m - cnt) * second;
        System.out.println(result);
    }
}
```