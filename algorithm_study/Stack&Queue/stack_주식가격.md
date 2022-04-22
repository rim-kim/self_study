# 프로그래머스 스택/큐 문제 주식가격

[주식가격](https://programmers.co.kr/learn/courses/30/lessons/42584)

### 문제 이해하기
초 단위로 기록된 주식가격이 담긴 배열 prices가 매개변수로 주어질 때, 가격이 떨어지지 않은 기간은 몇 초인지를 return 하도록 solution 함수를 완성하라.
- 입력조건 
    - prices의 각 가격은 1 이상 10,000 이하인 자연수입니다.
    - prices의 길이는 2 이상 100,000 이하입니다.
- 입출력 예시
    prices  | return
    --- | ---
    [1, 2, 3, 2, 3] | [4, 3, 1, 1, 0]
    - 1초 시점의 ₩1은 끝까지 가격이 떨어지지 않았습니다.
    - 2초 시점의 ₩2은 끝까지 가격이 떨어지지 않았습니다.
    - 3초 시점의 ₩3은 1초뒤에 가격이 떨어집니다. 따라서 1초간 가격이 떨어지지 않은 것으로 봅니다.
    - 4초 시점의 ₩2은 1초간 가격이 떨어지지 않았습니다.
    - 5초 시점의 ₩3은 0초간 가격이 떨어지지 않았습니다.    

### 문제 접근 방법

- 탑 스택 문제와 마찬가지로 두개의 for 문 만으로도 구현 가능하나 Stack 구조를 활용해 구현
- 주식 가격 배열의 index를 차례로 스택에 쌓으며 다음 index에 가격이 하락 되는지 확인한다.
	- 하락 시 다음 index - 하락 전 index
	- 유지 또는 상승됬을 시 배열 끝까지의 유지/상승 되는 시간 그대로

### 접근 방법을 적용한 코드

```java
import java.util.Stack;

class Solution {
    public int[] solution(int[] prices) {

        Stack<Integer> st = new Stack<>();
        int[] answer = new int[prices.length];

        for (int i = 0; i < prices.length; i++) {
            // 가격이 하락 했을때
            while (!st.empty() && prices[i] < prices[st.peek()]) {
                int index = st.pop();
                answer[index] = i - index;
                }

            st.push(i);
        }

        while (!st.empty()) {
            int index = st.pop();
            answer[index] = (prices.length - 1) - index;
        }

    return answer;
    }
}
```
