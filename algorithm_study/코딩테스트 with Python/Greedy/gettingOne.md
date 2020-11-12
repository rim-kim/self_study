* ```N``` 과 ```K```(2이상의 자연수) 가 주어졌을때 N을 1로 만들때 까지의 최소 연산 횟수 구하기
* 연산은 1. ```N```에서 1을 빼거나 2. ```N```을 ```K```로 나누기(단 ```N```이 ```K```로 나눠질때만) 중 하나
* 최대한 많이 나누기를 수행해야 하므로 ```N```을 ```K```의 배수가 될때까지 1을 빼기

```python
# 첫째줄 입력 : N K
n, k = map(int, input().split())

result = 0

while True:
    # N이 K의 배수가 될때까지 1 빼기
    multiple = (n // k) * k
    result += (n - multiple)
    n = multiple
    # N이 K 보다 작을때 반복문 탈출
    if n < k:
        break
    # K로 나누기
    result += 1
    n //= k

# 마지막으로 남은 수에서 1 뺴기
result += (n - 1)

print(result)
```

```java
import java.util.Scanner;

public class Main {

    public static void main(String[] args) {

        Scanner sc = new Scanner(Scanner.in);

        int n = sc.nextInt();
        int k = sc.nextInt();

        int result = 0;

        while (True) {
            int multiple = (n / k) * k;
            result += (n - multiple);
            n = multiple;

            if (n < k) break;

            result += 1;
            n /= k;
        }

        result += (n - 1);

        System.out.println(result);
    }
}

```