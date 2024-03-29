# 탐색 알고리즘

> 데이터에서 목적에 맞는 데이터를 찾아내기 위한 알고리즘 

<br>

- [선형탐색](##-1.-선형-탐색-알고리즘-(Linear-Search-Algorithm))
- [이진탐색](##-2.-이진-탐색-알고리즘-(Binary-Search-Algorithm))
- [해시탐색](##-3.-해시-탐색-알고리즘-(Hash-Search-Algorithm))
- [이진탐색트리](##-4.-이진-탐색-트리-(BST-/-Binary-Search-Tree))

<br>

## 1. 선형 탐색 알고리즘 (Linear Search Algorithm)

<br>

맨 앞이나, 맨 뒤부터 순서대로 하나하나 찾아보는 알고리즘

가장 단순하고 간단한 탐색 알고리즘   

### Process

1. 맨 끝부터 하나하나 원하는 값을 찾아본다.   

2. 원하는 값을 찾으면, 탐색을 종료한다.

<br>

### 예시   

5를 찾을 때, 맨 왼쪽에 있는 1부터 시작해서 하나씩 탐색한다.

![img](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FFKc2x%2FbtqHEE9vGvH%2FGMbnkVkRZNzBF3tbPHEhR0%2Fimg.png)

![img](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcuQicy%2FbtqHMwvIWGK%2F7rPy5JIYmOuI7vb78dWHF0%2Fimg.png)   

<br>

### 시간 복잡도   

길이 n짜리의 리스트를 탐색할 때,   

최선의 경우   
- 리스트의 첫 번째 원소가 정답인 경우 : 1번  

최악의 경우   
- 리스트의 맨 마지막 원소가 정답이거나, 리스트에 정답이 없을 때 : n번   

따라서 O(n)의 시간복잡도를 가진다.   

<br>
<br>


## 2. 이진 탐색 알고리즘 (Binary Search Algorithm)  

<br>

중간지점을 기준으로 데이터를 반씩 나눠서 탐색하는 알고리즘

<br>

### Process

1. 중간지점을 선택한 뒤, 중간지점을 기준으로 왼쪽 혹은 오른쪽 부분만 남긴다.   

2. 남긴 부분 중에서 다시 중간지점을 선택한 뒤, 왼쪽 혹은 오른쪽만 남긴다.   

3. 위 과정을 원하는 값을 찾을 때 까지 반복한다

<br>

### 예시
5를 찾을 때,  

![img](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FA19rE%2FbtqHxc0yaka%2FPOTMTtkKYZSzudXVyDUOUK%2Fimg.png)

<br>

### 시간 복잡도   

최선의 경우

- 리스트의 중간부분이 정답일 때 : 1번   

최악의 경우

- 리스트에 정답이 없는 경우 : logn 번   

따라서 O(logn)의 시간 복잡도를 가진다

<br>

선형탐색은 n이 증가함에 따라 시간복잡도가 선형적으로 증가하지만, 이진탐색은 n이 증가해도 시간복잡도가 아주 천천히 증가한다.

보통 정렬된 리스트에는 이진탐색을 사용하고,

정렬되지 않은 리스트에는 선형탐색을 사용한다.   

<br>
<br>

## 3. 해시 탐색 알고리즘 (Hash Search Algorithm)   
<br>

선형탐색이나 이진탐색은, 어떤 값이 어떤 index에 들어있는지에 대한 정보가 없는 상태에서 탐색할 때 사용하는 방식

반면에 해시 탐색은 값과 index를 미리 연결해 둠으로써 짧은 시간에 탐색할 수 있는 알고리즘

> 함수를 사용하여 데이터를 보관한 후에,    
> 보관하는데 사용된 함수를 사용하여 한 번에 데이터를 탐색한다.

<br>

### 아이디어

- 1차 아이디어

   처음에는 데이터와 같은 index에 저장   

  ex) 데이터 24는 24번 index에 저장, 데이터 30은 30번 index에 저장

  -> 최소한 데이터의 종류 만큼의 index 필요(메모리 낭비)   

- 2차 아이디어

  데이터에 함수(일정 계산)을 적용하여 나온 값을 index로 하여 보관하는 방법

  ex) data MOD 10 에 저장하는 방식을 이용하면, 0~9 까지의 10개의 index를 사용하여 값을 저장할 수 있다.

<br>

### 해시 함수

어떤 값이 주어졌을 때, 그 값을 대표하는 값을 계산하는 함수  

<br>

### 해시 값

해시 함수의 계산으로 나온 값

<br>

### 시간 복잡도   

평균적으로 O(1), 해시 충돌이 일어날 경우 O(n)

<br>
<br>

## 4. 이진 탐색 트리 (BST / Binary Search Tree)

<br>

트리 자료구조를 이용한 탐색 트리

### 정의
- 왼쪽 서브트리의 키값들은 root의 키값보다 작다  

- 오른쪽 서브트리의 키값들은 root의 키값보다 크다  

- 왼쪽, 오른쪽 서브트리들은 각각 모두 BST정의를 만족한다   

- BST의 모든 node들의 키값은 unique하다.   

 위의 4가지를 모두 만족해야 한다.

<br>


### 탐색 알고리즘   

어떠한 BST에서 원하는 값을 찾고자할 때,

root값을 기준으로

- 원하는 값 > root 키 값 : 오른쪽 서브트리로 이동   

- 원하는 값 < root 키 값 : 왼쪽 서브트리로 이동   

- 원하는 값 = root 키 값 : 탐색 종료
이 것을 계속 반복해나가면 된다.

<br>

### 삽입 알고리즘

어떠한 값을 삽입하고자 할 때,

1. 위의 탐색알고리즘을 먼저 수행한다.

2. 탐색 실패시에 , 탐색이 종료된 위치에 해당 노드를 삽입한다.

3. 탐색 성공시에, 이미 저장되있는 키값이므로 삽입에 실패한다.

<br>

### 삭제 알고리즘

어떠한 값을 삭제하고자 할 때,

1. 위의 탐색 알고리즘을 먼저 수행한다.

2. 삭제하려는 노드의 차수에 따라

- 차수 : 0 (leaf node)  

  그냥 삭제한다  


- 차수 : 1 (한 개의 자식 존재)

  삭제하고 자식을 삭제한 자리에 붙인다

- 차수 : 2

  자신을 대체할 노드를 찾아야 한다.

  삭제할 노드의 (왼쪽 서브트리에서 가장 큰 값 or 오른쪽 서브트리에서 가장 작은 값)을 자신을 대체할 노드로 정한다.

<br>

### 시간복잡도

평균 O(logn), 트리가 한쪽으로 치우친 최악의 경우에는 O(n)

<br>

### 이진 탐색 트리와 이진 탐색의 차이점

- 이진 탐색 트리는 정렬된 Binary Tree를 이용한다. 또한, Tree의 구조로 인하여 데이터 원소의 추가와 삭제가 용이하다는 장점이 있다.

- 이진 탐색은 정렬된 배열을 이용한다. 반면, 데이터 원소의 추가와 삭제가 비효율적이다는 단점이 있다.