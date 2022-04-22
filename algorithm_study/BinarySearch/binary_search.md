# Search in Array 배열 검색

배열 검색은 다음의 알고리즘을 활용한다.
1. 선형 검색 (linear search) 또는 순차 탐색 (sequential search) : 무작위로 늘어놓은 데이터 모임에서 검색을 수행한다.
2. 이진 검색 (binary search) : 일정한 규칙으로 늘어놓은 데이터 모임에서 빠른 검색을 수행한다.
3. 해시법 : 추가와 삭제가 자주 일어나는 데이터 모임에서 빠른 검색을 수행한다.
    - 체인법 : 같은 해시 값의 데이터를 선형 리스트로 연결
    - 오픈 주소법 : 데이터를 위한 해시 값이 충돌 시 재해시
<br>

## Linear Search/Sequential Search
- 시간 복잡도 : **_O(N)_**
- 원하는 키 값을 갖는 요소를 만날 때까지 맨 앞부터 순서대로 요소를 검색
```java
Object seek (Integer a, Entry<Integer, Object>[] S) {
    for (int i = 0; i < S.length; i++) {
        if (S[i].getKey() == a) {
            return S[i].getValue();
        }           
    }
    return null;
}
```
## Binary Search
- 시간 복잡도 : **_O(log N)_**
- 배열 내부의 데이터가 정렬되어 있어야만 사용할 수 있는 알고리즘
- 탐색 범위를 절반씩 좁혀가며 데이터를 탐색
```java
Object seek (Integer a, Entry<Integer, Object>[] S) {
    int low = 0;
    int high = S.length - 1;

    while (low <= high) {
        int mid = (high + low) / 2;
        if (a == S[mid]) {
            return mid;
        }
        else if (a < S[mid]) {
            high = mid – 1;
        }
        else { // a > S[mid]
            low = mid + 1;
        }
    }
    return null;
}
```
- 높은 난이도의 문제에서는 이진 탐색 알고리즘이 다른 알고리즘과 함께 사용된다<br> (예를 들어 그리디 알고리즘과 이진 탐색 알고리즘을 모두 사용)
- **탐색 범위가 2,000만**을 넘어가면 이진 탐색으로 문제에 접근해보기
- 처리해야 할 데이터의 개수나 값이 천만 단위 이상으로 넘어가면 이진 탐색과 같이 _O(log N)_ 의 속도를 내야 하는 알고리즘을 떠올려야 문제를 풀 수 있는 경우가 많다
- 단순히 정렬된 배열에서 특정한 데이터를 찾도록 요구하는 문제에서는 이진 탐색을 직접 구현할 필요 없이 단순히 모듈을 사용할 수도 있다 (자바의 binarySearch(), 파이썬의 bisect)

- **suffix array** 예제 : 주어진 String S 안에서 어느 특정한 substring/패턴 P을 찾고 싶을때
    - 선형검색의 시간복잡도는 **_O(|P||S|)_**
    - 각각의 인덱스에 대해 suffix array를 만들고 알파벳 순서로 정렬하여 이진검색을 사용한다. 시간복잡도는 **_O(|P||log S|)_**
