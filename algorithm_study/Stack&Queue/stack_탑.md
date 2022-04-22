# 프로그래머스 스택/큐 문제 탑

### 문제 이해하기
수평 직선에 탑 N대를 세웠습니다. 모든 탑의 꼭대기에는 신호를 송/수신하는 장치를 설치했습니다. 발사한 신호는 신호를 보낸 탑보다 높은 탑에서만 수신합니다. 또한, 한 번 수신된 신호는 다른 탑으로 송신되지 않습니다.

예를 들어 높이가 6, 9, 5, 7, 4인 다섯 탑이 왼쪽으로 동시에 레이저 신호를 발사합니다. 그러면, 탑은 다음과 같이 신호를 주고받습니다. <br>
높이가 4인 다섯 번째 탑에서 발사한 신호는 높이가 7인 네 번째 탑이 수신하고, 높이가 7인 네 번째 탑의 신호는 높이가 9인 두 번째 탑이, 높이가 5인 세 번째 탑의 신호도 높이가 9인 두 번째 탑이 수신합니다. 높이가 9인 두 번째 탑과 높이가 6인 첫 번째 탑이 보낸 레이저 신호는 어떤 탑에서도 수신할 수 없습니다.
송신 탑(높이)  | 수신 탑(높이)
--- | ---
5(4) | 4(7)
4(7) | 2(9)
3(5) | 2(9)
2(9) | -
1(6) | -

맨 왼쪽부터 순서대로 탑의 높이를 담은 배열 heights가 매개변수로 주어질 때 각 탑이 쏜 신호를 어느 탑에서 받았는지 기록한 배열을 return 하도록 solution 함수를 작성하세요.

- 입력조건 
    - heights는 길이 2 이상 100 이하인 정수 배열입니다.
    - 모든 탑의 높이는 1 이상 100 이하입니다.
    - 신호를 수신하는 탑이 없으면 0으로 표시합니다.
- 입출력 예시
    heights  | return
    --- | ---
    [6,9,5,7,4] | [0,0,2,2,4]
    [3,9,9,3,5,7,2] | [0,0,0,3,3,3,6]
    [1,5,3,6,7,6,5] | [0,0,2,0,0,5,6] 
    - 입출력 예 #2
    - [1,2,3] 번째 탑이 쏜 신호는 아무도 수신하지 않습니다.
    - [4,5,6] 번째 탑이 쏜 신호는 3번째 탑이 수신합니다.
    - [7] 번째 탑이 쏜 신호는 6번째 탑이 수신합니다.

### 문제 접근 방법

- 수신하는 탑은 언제나 송신하는 탑의 왼쪽에 위치하며 수신된 신호는 다시 송신되지 않는다.
	- 배열에 두개의 포인터(두개의 for문) 를 이용해 구현이 가능 하나 LIFO의 Stack 구조를 활용하여 문제를 풀 수 있다.
- 스택에 들어가는 Tower 클래스를 만들어 탑의 index와 height를 저장한다.

### 접근 방법을 적용한 코드

```java
import java.util.Stack;

class Solution {
    
    class Tower {
        int index;
        int height;

        public Tower(int index, int height) {
            this.index = index;
            this.height = height;
        }
    }

    public int[] solution(int[] heights) {

        Stack<Tower> st = new Stack<>();
        int[] answer = new int[heights.length];

        for (int i = 0; i < heights.length; i++) {

            Tower tower = new Tower(i + 1, heights[i]);
            int receiverIndex = 0;

            while (!st.isEmpty()) {
                Tower left = st.peek();
                // 왼쪽의 탑이 더 길때
                if (left.height > tower.height) {
                    receiverIndex = left.index;
                    break;
                }
                st.pop();
            }

            st.push(tower);
            answer[i] = receiverIndex;
        }

        return answer;
    }
}
```
