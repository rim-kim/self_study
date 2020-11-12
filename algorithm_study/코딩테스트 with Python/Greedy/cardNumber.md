* 카드들이 ```N x M``` 형태로 놓여 있을때 가장 높은 숫자를 뽑는 게임
* 게임의 룰 : 뽑고자 하는 카드가 있는 행을 선택하여 그 행에서 가장 작은 수가 적힌 카드를 뽑아야 한다
* 그리디 알고리즘 문제로 각 행마다 가장 작은 수를 찾은 뒤 그 수들 중에서 가장 큰 수를 찾기 

```python
# 첫째줄 입력: N M
n, m = map(int, input().split())

result = 0

# 그 뒤 배열을 차례대로 한 행씩 읽기
for i in range(n):
    data = list(map(int, input().split()))
    min_value = min(data)
    result = max(result, min_value)

print(result)
```

```python
# 2중 반복문
for i in range(n):
    data = list(map(int, input().split()))
    min_value = 10001
    for a in data:
        min_value = (min_value, a)
    result = max(result, min_value)    
```